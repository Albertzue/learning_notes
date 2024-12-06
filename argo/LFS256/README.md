# Essential Concepts for Argo

### What Is GitOps?
GitOps embodies a set of principles that form the backbone of modern software delivery practices. 
At its core, GitOps hinges on five key aspects, 
each contributing to a streamlined and efficient development and deployment process.
#### Core Elements
1. **Declarative configuration**
First and foremost is the principle of declarative configuration. This implies a departure from the traditional imperative style of issuing specific commands. Instead, GitOps centers around expressing the desired end state of a system, allowing developers to declare intentions rather than prescribe exact actions. 
For instance, specifying the desire for three containers for a given application prompts automated agents to adjust the current state accordingly, potentially terminating existing containers to align with the declared configuration.

2. **Immutable storage**
Git, in the context of GitOps, serves as more than just a version-controlled storage solution; 
it represents immutable storage. While Git is the predominant source control system, the principles of GitOps are adaptable to other version control systems as well. 
The immutability aspect underscores the idea that once a configuration is committed to Git, 
it becomes a static reference point, aiding in reproducibility and traceability. It is also often referred to as the source of truth.

3. **Automation**
Automation is a cornerstone of GitOps, emphasizing the importance of eliminating manual interventions post-commit to the version control system.
 The moment changes are integrated into the VCS, the baton is passed to software agents.

4. **Software agents**
These agents play a pivotal role in executing the necessary actions to realize the newly declared configuration.
The process involves assessing the disparity between the existing system state and the desired state specified in the version control,
encapsulating the essence of GitOps' closed-loop nature.

5. **Closed loop**
Closed loop, in the GitOps paradigm, encapsulates the continuous feedback loop between the actual and desired states of a system.
It signifies that the automated actions taken by software agents are not arbitrary but are a direct response to the evolving configuration stored in the version control.
The closed loop mechanism ensures that the system perpetually converges towards the declared state, fostering consistency and predictability.


### Vocabulary
#### Configuration
1. Application: A collection of Kubernetes resources defined by manifests, specified in Argo CD as Custom Resource Definitions (CRDs).
2. Application source type: The tool utilized for building applications, such as Helm or Kustomize.

#### States
1. Target state: The desired state of an application, represented in a Git repository, serving as the source of truth.
2. Live state: The current state of the application, indicating the deployed Kubernetes resources.

#### Statuses
1. Sync status: The status indicating whether the live state aligns with the target state. Essentially, it confirms if the application deployed in Kubernetes matches the desired states outlined in the Git repository.
2. Sync operation status: The status during the sync phase, specifying whether it has failed or succeeded.
3. Health status: The well-being of the application, assessing its running condition and ability to handle requests.

#### Actions
1. Refresh: The act of comparing the latest code in Git with the live state to identify any differences.
2. Sync: The process of transitioning an application to the target state by applying changes in the Kubernetes cluster.

### Overview diagram of Argo CD and its components:
![image](https://github.com/user-attachments/assets/5d254ee1-03af-4b36-b74f-4ecd21394ab6)

### Argo CD reconciliation loop
![image](https://github.com/user-attachments/assets/5b1fc80b-b2d6-4270-b5dd-f48fed883bd1)

## Synchronization Principles
The sync phase is a very important operation and its behavior can be customized by using resource hooks and sync waves. In this section, we explore both ways of customization and learn how to use them.

#### Resource hooks
A sync, as described in the "Vocabulary" section, is the transition of an application into the target state. There are five possible definitions of when a resource hook can be run:

1. PreSync, execute before the Sync phase (e.g., create a backup before syncing)
2. Sync, execute after all PreSync hooks completed successfully and do actions during application of the manifests (e.g., for more complex rollout strategies like blue-green or canary instead of Kubernetes rolling update)
3. PostSync, execute after all successful Sync hooks and application, and all resources are in Healthy state (e.g., run additional health checks after deployment or run integration checks)
4. Skip, indicates Argo CD to skip the application of the manifest
5. SyncFail, executes when Sync fails (e.g., clean up operations)
6. 
To keep things simple, resource hooks use the Kubernetes kind Job and are identified by an annotation. Using the annotation Argo CD identifies Jobs and when they should be executed.

The following is an example for a database schema migration resource hook:
```
apiVersion: batch/v1
kind: Job
metadata:
  generateName: schema-migrate-
  annotations:
    argocd.argoproj.io/hook: PreSync
```

#### Sync waves
Essentially sync waves are a convenient way to split and order to-be-synced manifests. Waves can range from negative to positive values. If not defined, the default value is wave zero. Using sync waves is achieved in the same way as resource hooks; by using annotations.
```
metadata:
  annotations:
    argocd.argoproj.io/sync-wave: "5"
```


## ArgoEvent

The main components of Argo Events are:
1. Event Source: This is where events are generated. Event sources in Argo Events can be anything from a simple webhook or a message from a message queue, to a scheduled event. Understanding event sources is key to knowing how your system will interact with various external and internal stimuli.
2. Sensor: Sensors are the event listeners in Argo Events. They wait for specific events from the event sources and, upon detecting these events, trigger predefined actions. Understanding sensors involves knowing how to respond to different types of events.
3. EventBus: The EventBus acts as a backbone for event distribution within Argo Events. It's responsible for managing the delivery of events from sources to sensors. Understanding the EventBus is crucial for managing the flow of events within your system.
4. Trigger: Triggers in Argo Events are the mechanisms that respond to events detected by sensors. They can perform a wide range of actions, from starting a workflow to updating a resource. Understanding triggers is essential for automating responses to events.

![image](https://github.com/user-attachments/assets/037ce29d-2323-482f-bdfb-59b88c80c8a5)
