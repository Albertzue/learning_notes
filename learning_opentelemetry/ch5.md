# Registering Providers
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
