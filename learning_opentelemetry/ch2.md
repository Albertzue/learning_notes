# Hard and Soft Context
Broadly speaking, there are two types of context that you care about, and those contexts appear in two places. 
The types of context are what we’ll refer to as “hard” and “soft” contexts, 
and they appear in an application or in infrastructure. 
An observability frontend can identify and support varying mixtures of these contexts, 
but without them, the value of telemetry data is significantly reduced—or vanishes altogether.

**A hard context** is a unique, per-request identifier that services in a distributed application can propagate to other services that are part of the same request. A basic model of this would be a single request from a web client through a load balancer into an API server, which calls a function in another service to read a database and returns some computed value to the client (see Figure 2-1). This can also be referred to as the logical context of the request (as it maps to a single desired end-user interaction with the system).

**A soft context** would be various pieces of metadata that each telemetry instrument attaches to measurements from the various services and infrastructure that handle that same request—for example, a customer identifier, the hostname of the load balancer that served the request, or the timestamp of a piece of telemetry data (also pictured in Figure 2-1). The key distinction between hard and soft contexts is that a hard context directly and explicitly links measurements that have a causal relationship, whereas soft contexts may do so but are not guaranteed to.

![image](https://github.com/user-attachments/assets/fb5ce495-a899-43d7-b6e5-8e4112f8f058)

To summarize: Hard context defines the overall shape of a system by defining relationships between services and signals. Soft context allows you to create unique dimensions across telemetry signals that help explain what a particular signal represents.
