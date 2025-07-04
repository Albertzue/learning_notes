OpenTelemetry consists of three kinds of components: 
instrumentation installed within applications, exporters for infrastructure such as Kubernetes, 
and pipeline components for sending all of this telemetry to a storage system
![image](https://github.com/user-attachments/assets/a3bf6461-a320-4dfa-a705-e387755b8b8c)

# Application Telemetry
The most important source of telemetry is applications. 
This means that OpenTelemetry must be installed in every application for it to work properly.
![image](https://github.com/user-attachments/assets/6457c637-2407-43ec-8b6c-06041f496ac7)

# Library Instrumentation
The most critical telemetry comes from OSS libraries such as frameworks, HTTP and RPC clients, and database clients. These libraries perform the heavy lifting in most applications, and often the telemetry from these libraries is sufficient to cover almost all the work that an application performs.

# What’s Not Included in OpenTelemetry
What OpenTelemetry does not include is almost as critical as what it does include. Long-term storage, analysis, GUIs, and other frontend components are not included and never will be.
