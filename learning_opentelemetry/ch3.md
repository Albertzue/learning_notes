![image](https://github.com/user-attachments/assets/cb8b5868-6473-4eb9-92cf-b941efedf923)

# Primary Observability Signals
instrumentation is the process of adding observability code to a service or system.
Broadly, there are two ways to perform this. 
- `white-box` approach that involves directly adding telemetry code to a service or library
- `black-box` approach that utilizes external agents or libraries to generate telemetry without requiring direct code changes.

OpenTelemetry concerns itself with three primary signals: traces, metrics, and logs.2 These signals are ordered roughly by importance. Their importance comes from the following goals:
- Capturing the relationships between services in your system using actual production data and service-to-service communication
- Annotating service telemetry with consistent and descriptive metadata about what the service is doing and where it’s running
- Definitively identifying the relationships between arbitrary groups of measurements—basically, “this thing happened at the same time as this other thing”
- Efficiently creating accurate counts and measurements of events occurring in a system, such as the number of requests that occur, or how many requests took between 100 and 150 milliseconds to complete

# Traces
Tracing is the fundamental signal of observability for a distributed system. Each trace is a collection of related logs, called spans, for a given transaction. Each span in turn contains a variety of fields.
If you’re familiar with structured logging, you can think of a trace as a set of logs that are correlated through a shared identifier.
![image](https://github.com/user-attachments/assets/5a0c29b4-f349-48a4-b8e8-ddac1ea4ec56)

The difference between structured logs and tracing, though, 
is that tracing is an incredibly powerful observability signal for request/response transactions,
which are prevalent throughout cloud native distributed systems. 
Traces offer several semantic benefits that make them a valuable observability signal—for example:
- A single trace represents a single transaction, or journey, through a distributed system. This makes traces the best way to model end-user experience, since one trace corresponds to one user’s path through a system.

- A group of traces can be aggregated across multiple dimensions in order to discover performance characteristics that would be difficult to spot otherwise.

- Traces can be transformed into other signals, such as metrics, allowing for downsampling of the raw data without losing key performance information. In other words, a single trace contains all the information needed to compute the “golden signals” (latency, traffic, errors, and saturation) for a single request.


# Metrics
Metrics are numeric measurements and recordings of system state, 
such as the number of users concurrently logged into a system, the amount of disk space used on a device, 
or the amount of RAM available on a virtual machine (VM). 
They’re useful for accurately measuring the “big picture” of a system because they’re cheap to create and store.

Metrics are often the first port of call for developers trying to understand overall system health.
They’re ubiquitous, fast, and inexpensive for what they do.

In OpenTelemetry, metrics have been designed to support three main goals:
- Developers should be able to define important, semantically meaningful events in their code and specify how those events translate into metric signals.
- Operators should be able to control costs, data volume, and resolution by aggregating or reaggregating the time or attributes of those metrics.
- Conversions should not change the intrinsic meaning of a measurement.

# Logs
Fundamentally, the OpenTelemetry model seeks to unify this signal by enriching log statements with trace context and links to metrics and traces recorded concomitantly. 
In plainer terms, OpenTelemetry can take existing log statements in your application code, 
see if there’s an existing context, and, if so, ensure that the log statements are associated with that context.

# Observability Context
There are three basic types of context in OpenTelemetry: time, attributes, and the context object itself

#### The Context Layer
The goal of the context layer is to provide a clean interface either to existing context managers (such as Golang’s context.Context, Java ThreadLocals, or Python’s context manager) 
or to some other suitable carrier. 
What’s important is that the context is required and that it holds one or more propagators.

**Propagators** are how you actually send values from one process to the next. When a request begins, OpenTelemetry creates a unique identifier for that request based on registered propagators. 
This identifier can then be added to the context, serialized, and sent to the next service, which will deserialize it and add it to the local context.

```
Baggage
Propagators carry the hard context of a request (such as W3C Trace Context),
but they can also carry what’s known as baggage, or soft-context values.
Baggage is meant to transmit certain values that you may wish to put on other signals (for example, customer or session IDs) from where they were created to other parts of your system.
Once baggage is added, it cannot be removed and will be transmitted to external systems as well—so be careful about what you put in there!
```

![image](https://github.com/user-attachments/assets/2c6b03c5-f16c-436b-9b16-c5bbe8178a76)

f the traces, metrics, and logs are the verbs that describe how your system functions, the semantic conventions provide the nouns that describe what it’s doing.

#### Attributes and Resources
These attributes are a form of metadata that tell you what a piece of telemetry represents.
Simply put, an attribute is a key-value pair that describes an interesting, or useful, dimension of a piece of telemetry.
Attributes are things you’d want to filter on or group by if you were trying to understand what’s happening in your system.

Attributes are not infinite, and you should be careful when using them on different types of telemetry.
By default, any single piece of telemetry can have no more than 128 unique attributes in OpenTelemetry; 
there’s no limit on how long those values can be.

There are two reasons for these requirements.
First, it’s not free to create or assign an attribute. 
The OpenTelemetry SDK needs to allocate memory for each attribute, and it can be very easy to accidentally run out of memory in the event of unexpected behavior or code errors.
(Incidentally, these are extremely challenging crashes to diagnose, because you’re also losing your telemetry about what’s happening.) 
Second, when adding attributes to metric instruments, you can quickly trigger what’s known as a cardinality explosion when sending them to a time-series database.

OpenTelemetry also defines a special type of attribute called a resource. 
The difference between an attribute and a resource is straightforward: attributes can change from one request to the next, 
but resources remain the same for the entire life of a process.
For example, a server’s hostname would be a resource attribute, while a customer ID would not be. 

#### Semantic Conventions
System operators are forced to contend with a significant amount of toil simply to ensure that attribute keys, values, and what they represent are the same across multiple clouds, application runtimes, hardware architectures, and versions of frameworks and libraries.
The OpenTelemetry Semantic Conventions are designed to remove this consistent point of friction and offer developers a single well-known and well-defined set of attribute keys and values.
#### OpenTelemetry Protocol
One of the most exciting features of OpenTelemetry is that it provides a standard data format and protocol for observability data. [OpenTelemetry Protocol (OTLP)](https://oreil.ly/Ad6TE) offers a single well-supported wire format (how data is stored in memory or sent across the network) for telemetry to be transmitted between agents, services, and backends. It can be sent or received in both binary and text-based encoding and aims to use low amounts of CPU and memory. 
In practice, OTLP offers significant benefits to an array of telemetry producers and consumers
#### Compatibility and Future-Proofing
The foundation of OpenTelemetry is built on two points: standards-based context and conventions, alongside a universal data format. 

OpenTelemetry has a concept of telemetry schemas to help consumers and producers of telemetry address changes in semantic conventions over time. 
By building schema-aware analysis tools and storage backends or relying on the OpenTelemetry Collector to perform schema transformations, you can benefit from changes in semantic conventions (and their associated support in analysis tools) without having to reinstrument or redefine output from existing services
![image](https://github.com/user-attachments/assets/990aec82-b868-4885-a186-4dc9a5077117)
