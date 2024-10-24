At the highest level, a distributed system consists of resources and transactions:
- **Resources**
  These are all the physical and logical components that make up a system. Physical components, such as servers, containers, processes, RAM, CPU, and network cards, are all resources. Logical components, such as clients, applications, API endpoints, databases, and load balancers, are also resources. In short, resources are everything from which the system is actually constructed.

- **Transactions**
  These are requests that orchestrate and utilize the resources the system needs to do work on behalf of the user. Usually, a transaction is kicked off by a real human, who is waiting for the task to be completed. Booking a flight, hailing a rideshare, and loading a web page are examples of transactions.


Telemetry is data that describes what your system is doing. Without telemetry, your system is just a big black box filled with mystery.

Many developers find the word telemetry confusing. It’s an overloaded term. The distinction we draw in this book, and in systems monitoring in general, is between user telemetry and performance telemetry:

- **User telemetry**
  Refers to data about how a user is interacting with a system through a client: button clicks, session duration, information about the client’s host machine, and so forth. You can use this data to understand how users are interacting with an ecommerce site, or the distribution of browser versions accessing a web-based application.

- **Performance telemetry**
  This is not primarily used to analyze user behavior; instead, it provides operators with statistical information about the behavior and performance of system components. Performance data can come from different sources in a distributed system and offers developers a “breadcrumb trail” to follow, connecting cause with effect.

  A signal is a particular form of telemetry.
  Event logs are one kind of signal. System metrics are another kind of signal.
  Continuous profiling is another. These signal types each serve a different purpose,
  and they are not really interchangeable. You can’t derive all the events that make up a user interaction just by looking at system metrics,
  and you can’t derive system load just by looking at transaction logs. You need multiple kinds of signals to get a deep understanding of your system as a whole.

  Each signal consists of two parts: instrumentation—code that emits telemetry data—within the programs themselves,
   and a transmission system for sending the data over the network to an analysis tool, where the actual observing occurs.
  
  Finally, telemetry plus an analysis equals observability. Understanding the best way to combine these two pieces into a useful observability system is what this book is all about.
