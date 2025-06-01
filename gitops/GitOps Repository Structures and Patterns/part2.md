This part is about patterns in the area of operator deployments. 
These describe how many GitOps operators you deploy relative to Kubernetes clusters or namespaces


![image](https://github.com/user-attachments/assets/1c18eb71-ed9b-4976-a0ad-f95baa8c5b9f)
"Instance per cluster" (synonym: "standalone") refers to the use of a GitOps operator with a Kubernetes cluster,
see Figure 1. This pattern provides strong isolation. On the one hand, this has advantages in terms of security, 
since in the event of a breach, only the applications of the one instance are at risk. On the other hand,
this approach scales better in terms of load and downtime. The disadvantage is the maintenance effort,
since several instances have to be operated instead of one central instance.
In addition, the resource requirements increase.

![image](https://github.com/user-attachments/assets/73f9a3db-77cf-49a0-8994-d5bda08f70e5)
This contrasts with the "hub and spoke" pattern, see Figure 2, where a central GitOps operator is used for multiple Kubernetes clusters. Accordingly, 
the advantages and disadvantages are exactly inverted to the instance per cluster pattern: The maintenance effort is lower,
but there is a single point of failure, which scales worse and is less secure.

![image](https://github.com/user-attachments/assets/3b5d2e7e-6b0d-47f6-bede-88c3173a6ffb)
The "instance per namespace" pattern (synonym "namespaced") is similar to "instance per cluster",
but here one operator is operated per namespace instead of per cluster, 
see Figure 3. Using this pattern can be beneficial if a high level of isolation is desired,
but the operation of separate Kubernetes clusters is out of the question. This may occur, for example, 
due to high on-premises costs or organizational constraints. In principle, 
this pattern has the same advantages as "instance per cluster". 
It should be noted that the isolation of Kubernetes namespaces is generally lower than for separate clusters.
Also, it should be noted whether operators support subdivision into namespaces at all.

![image](https://github.com/user-attachments/assets/4b826159-37f1-44b2-9ec3-149a8f120b36)
#### Split-Instance
Definition: A single management instance of Argo CD connects and manages many clusters. 
Unlike hub and spoke, the components of Argo CD are split,
with some components living on target clusters and networking generally provided via tunnel.


![image](https://github.com/user-attachments/assets/1a3d1064-9f06-4b27-9820-426b24142b20)
#### Control Plane
Definition: Argo instances can be deployed in a mix of standalone and hub and spoke but a control-plane is added for managing and rolling information into a centralized place.
