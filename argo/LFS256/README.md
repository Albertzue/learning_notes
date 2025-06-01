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

## ArgoRollout

#### Progressive Delivery
Progressive delivery is often described as an evolution of continuous delivery. It focuses on releasing updates of a product in a controlled and gradual manner, thereby reducing the risk of the release, typically coupling automation and metric analysis to drive the automated promotion or rollback of the update.

##### Canary releases
Gradually roll out the change to a small subset of users before rolling it out to the entire user base.

##### Feature flags
Control who gets to see what feature in the application, allowing for selective and targeted deployment.

##### Experiments & A/B testing
Test different versions of a feature with different segments of the user base.

##### Phased rollouts
Slowly roll out features to incrementally larger segments of the user base, monitoring and adjusting based on feedback.

The primary goal of Progressive Delivery is to reduce the risk associated with releasing new features and to enable faster iteration by getting early feedback from users.


![image](https://github.com/user-attachments/assets/cf602195-85b9-4b12-b8b2-f11f12ee79b2)
#### Argo Rollouts Components

##### Argo Rollouts Controller
An operator that manages Argo Rollout Resources. It reads all the details of a rollout (and other resources) and ensures the desired cluster state.

##### Argo Rollout Resource
A custom Kubernetes resource managed by the Argo Rollouts Controller. It is largely compatible with the native Kubernetes Deployment resource, adding additional fields that manage the stages, thresholds, and techniques of sophisticated deployment strategies, including canary and blue-green deployments.

##### Ingress
The Kubernetes Ingress resource is used to enable traffic management for various traffic providers such as service meshes (e.g., Istio or Linkerd) or Ingress Controllers (e.g., Nginx Ingress Controller).

##### AnalysisTemplate and AnalysisRun
Analysis is an optional feature of Argo Rollouts and enables the connection of Rollouts to a monitoring system. This allows automation of promotions and rollbacks. To perform an analysis an AnalysisTemplate defines a metric query and their expected result. If the query matches the expectation, a Rollout will progress or rollback automatically, if it doesn’t. An AnalysisRuns is an instantiation of an AnalysisTemplate (similar to Kubernetes Jobs).



|Templates|	DescriptionUse Case|
|---------|--------------------|
|AnalysisTemplate|	This template defines the metrics to be queried and the conditions for success or failure. The AnalysisTemplate specifies what metrics should be monitored and the thresholds for determining the success or failure of a deployment. It can be parameterized with input values to make it more dynamic and adaptable to different situations.|
|AnalysisRun|	An AnalysisRun is an instantiation of an AnalysisTemplate. It is a Kubernetes resource that behaves similarly to a job in that it runs to completion. The outcome of an AnalysisRun can be successful, failed, or inconclusive, and this result directly impacts the progression of the Rollout's update. If the AnalysisRun is successful, the update continues; if it fails, the update is aborted; and if it's inconclusive, the update is paused.|
