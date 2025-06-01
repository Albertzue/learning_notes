![image](https://github.com/user-attachments/assets/89f1c867-5e95-42f6-9a3c-e934f2606869)# Registering Providers
What happens if you make an OpenTelemetry API call? By default, nothing. That API call is a no-op, meaning that the API is safe to call, but nothing happens and there is no overhead.

For something to happen, you need to register providers with the API.
A provider is an implementation of the OpenTelemetry instrumentation API. 
These providers handle all of the API calls. The `TracerProvider` creates tracers and spans.
The `MeterProvider` creates meters and instruments. 
The `LoggerProvider` creates loggers.
As OpenTelemetry expands in scope, more providers may be added in the future.

You should register providers as early as possible in the application boot cycle. 
Any API calls made before registering a provider will be no-ops and will not be recorded.

### Providers
When we talk about the SDK, we’re talking about a set of provider implementations.
Each provider is a framework that can be extended and configured through various types of plug-ins

#### TracerProvider
A TracerProvider implements the OpenTelemetry tracing API. 
It consists of samplers, SpanProcessors, and exporters. 
![image](https://github.com/user-attachments/assets/5a6ada4c-be53-4f11-b3df-c57b43846337)

##### Samplers
Samplers choose whether the span is recorded or dropped.
A variety of sampling algorithms are available, and choosing which sampler to use and how to configure it is one of the most confusing parts of setting up a tracing system.
```
Dropped or Recorded?
Calling a span “sampled” can mean it was “sampled out” (dropped) or “sampled in” (recorded), so it’s good to be specific.
```


It’s difficult to choose a sampler without understanding how you plan to use the telemetry. 
Sampling means losing data. What data is safe to lose?
If you’re trying to measure only average latency, a random sampler that records only one out of 1,024 traces will work fine and could save quite a bit of money.
But if you want to investigate edge cases and outliers—extreme latency, rare but dangerous errors—a random sampler will lose too much data and could miss recording these events.

When in doubt, do not sample at all.
It’s better to start out without any sampling and then add it later in response to specific costs or overhead you are looking to reduce. 
Don’t reflexively add a sampler until you understand the costs you are trying to reduce and the kinds of sampling your tracing product is compatible with. 


##### SpanProcessors
SpanProcessors allow you to collect and modify spans. 
They intercept the span twice: once when it starts and once when it ends.

The default processor is called a BatchProcessor. 
This processor buffers span data and manages the exporter plug-ins described in the following subsection.
Generally, you should install the BatchProcessor as the last SpanProcessor in your processing pipeline.

##### Exporters
How do you get all these spans out of a process and into something you can read? 
Exporters!
These plug-ins define the format and destination of your telemetry data.

The default is to use the OpenTelemetry Protocol (OTLP) exporter, which we recommend. 
The only situation in which you should not use OTLP is when you are not running a Collector and are sending data directly to an analysis tool that does not support OTLP

Here are the OTLP configuration options that you should be aware of:

`protocol`\
OTLP supports three transport protocols: gRPC, http/protobuf, and http/json. We recommend http/protobuf, which is also the default.

`endpoint`\
The URL to which the exporter is going to send spans or metrics. The default values are http://localhost:4318 for HTTP and http://localhost:4317 for gRPC.

`headers`\
Additional HTTP headers added to every export request. Some analysis tools may require an account or security token header to route data correctly.

`compression`\
Used to turn on GZip compression. This is recommended for larger batch sizes.

`timeout`\
The maximum time the OTLP exporter will wait for each batch export. It defaults to 10 seconds.

`certificate file, client key file, and client certificate file`\
Used for verifying a server’s TLS credentials when a secure connection is required.

#### MeterProvider
A MeterProvider implements the OpenTelemetry metrics API.
![image](https://github.com/user-attachments/assets/abf19eab-b620-4deb-b198-27dbd1e54642)
MetricReaders are the metric equivalent of SpanProcessors. They collect and buffer metric data until it can be exported. The default MetricReader is a PeriodicExportingMetricReader. This reader collects metric data and then pushes it to an exporter in batches. Use it when exporting OTLP. Periodic readers have two configuration options you should be aware of:

`exportIntervalMillis`\
The time interval in milliseconds between two consecutive exports. The default value is 60,000.

`exportTimeoutMillis`\
How long the export can run before it is canceled. The default value is 30,000.

##### MetricProducers

It is common for existing applications to already have metric instrumentation of some kind. You need MetricProducers to connect some types of third-party instrumentation to an OpenTelemetry SDK, so that you can start mixing your existing instrumentation with new OpenTelemetry instrumentation. For example, Prometheus instrumentation may require a MetricProducer.

Every MetricProducer is registered with a MetricReader. 

##### MetricExporters
MetricExporters send batches of metrics over the network. As with traces, we recommend using the OTLP exporter to send telemetry to a Collector.

If you are a Prometheus user and are not using a Collector, then you’ll want to use Prometheus’s pull-based collection system instead of the push-based system used by OTLP. Installing the Prometheus exporter will set this up.

If you are first sending data to a Collector, then use the OTLP exporter in your application and install the Prometheus exporter in the Collector. We recommend this approach.

##### Views
Views are a powerful tool for customizing the metrics the SDK outputs. You can choose which instruments are ignored, how an instrument aggregates data, and which attributes are reported.

#### LoggerProvider
A LoggerProvider implements the OpenTelemetry logging API. It consists of LogRecordProcessors and LogRecordExporters. 

![image](https://github.com/user-attachments/assets/f688521e-c89c-456d-9f1f-63d6596e8235)

##### LogRecordProcessors
LogRecordProcessors work just like SpanProcessors. The default processor is a batch processor, which you use to register your exporters. As with the span batch processor, we recommend lowering the `scheduledDelayMillis` config parameter when sending data to a local Collector.

##### LogRecordExporters
LogRecordExporters emit logging data in a variety of common formats. As with the other signals, we recommend using the OTLP exporter.

#### Shutting Down Providers
When shutting down an application, it’s critical to flush any remaining telemetry before the application terminates. Flushing is the process of immediately exporting any remaining telemetry data already buffered in the SDK while blocking shutdown. If your application terminates before flushing the SDK, you could lose critical observability data.

To perform a final flush, every SDK provider includes a Shutdown method. Make sure to integrate this method into your application shutdown procedure as one of the final steps.

# Configuration Best Practices
You can configure the SDK in three ways:
- In code, when constructing exporters, samplers, and processors
- Using environment variables
- Using a YAML config file

#### Remote Configuration
As we write this, OpenTelemetry is developing Open Agent Management Protocol (OpAMP), a remote configuration protocol for Collectors and SDKs. OpAmp will allow Collectors and SDKs to open a port, through which they transmit their current status and receive configuration updates. Using OpAMP, a control plane can manage the entire OpenTelemetry deployment without the need to restart or redeploy.
