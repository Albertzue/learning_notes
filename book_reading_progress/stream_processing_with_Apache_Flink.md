### info:
[code example](https://github.com/streaming-with-flink)

### schedule (plan/finish)
2025/10/28 52/66
### keynotes

#### chapter 1&2
1. The process of copying data to the data warehouse is called **extract–transform–load(ETL)**
2. Event-driven applications are an evolution of microservices. They communicate via event logs instead of REST calls and hold application data as local state instead of writing it to and reading it from an external datastore, such as a relational database or key-value store.
3. Operators without input ports are called **data sources** and operators without output ports are called **data sinks**
   <img width="1012" height="224" alt="image" src="https://github.com/user-attachments/assets/8f19dc20-73e8-4c50-b9c4-9800c8507dee" />
4. Data ingestion is the operation of fetching raw data from external sources and converting it into a format suitable for processing
5. **A rolling aggregation** is an aggregation, such as sum, minimum, and maximum, that is continuously updated for each input event. Aggregation operations are stateful and combine the current state with the incoming event to produce an updated aggregate value. Note that to be able to efficiently combine the current state with an event and produce a single value, the aggregation function must be associative and commutative.

6. <img width="825" height="229" alt="image" src="https://github.com/user-attachments/assets/cbe51385-69b5-48fa-9217-2299b8704ad2" />
<img width="820" height="186" alt="image" src="https://github.com/user-attachments/assets/4fd9ce07-3785-4b88-bda1-1b382fc31539" />
<img width="833" height="272" alt="image" src="https://github.com/user-attachments/assets/80db1d06-2dc4-4abb-9ceb-b5fcd2e7f295" />
<img width="839" height="222" alt="image" src="https://github.com/user-attachments/assets/58535117-b828-464d-9fcf-1a8faa0b15c1" />
#### chapter 3
1. A Flink setup consists of four different components that work together to execute streaming applications. These components are a JobManager, a ResourceManager, a TaskManager, and a Dispatcher
2. The ResourceManager is responsible for managing TaskManager slots, Flink’s unit of processing resources.
3. <img width="932" height="283" alt="image" src="https://github.com/user-attachments/assets/8afab445-6cc5-4735-b3e6-df21ac5d9bfb" />
4. <img width="943" height="425" alt="image" src="https://github.com/user-attachments/assets/6861731d-f5df-4149-a12b-9bf5b48caeaf" />
5. <img width="971" height="594" alt="image" src="https://github.com/user-attachments/assets/7071ed45-3929-4f0a-ba80-1f33edd19d8e" />

### new words
1. omnipresent
2. barista
