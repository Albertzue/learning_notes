[link](https://aws.amazon.com/cn/blogs/compute/cost-optimization-and-resilience-eks-with-spot-instances/)
When EC2 needs the capacity back, the Spot Instance service arbitrarily sends Spot interruption notifications to instances within the associated Spot capacity pool. 
This Spot interruption notification lands in both the EC2 instance metadata and Eventbridge. Two minutes after the Spot interruption notification, the instance is reclaimed. 
You can set up your infrastructure to automate a response to this two-minute notification. Examples include draining containers, draining ELB connections, or post-processing.

```
Spot capacity pools = (Availability Zones) * (Instance Types)
```
If your application is deployed across two AZs and uses only an c5.4xlarge then you are only using (2 * 1 = 2) two Spot capacity pools. 
To follow Spot Instance best practices, consider using six AZs and allowing your application to use c5.4xlarge, c5d.4xlarge, c5n.4xlarge, and c4.4xlarge. 
This gives us (6 * 4 = 24) 24 Spot capacity pools, greatly increasing the stability and resilience of your application.

The architecture deploys the EKS worker nodes over three AZs, and leverages three Auto Scaling groups – two for Spot Instances, 
and one for On-Demand. The Kubernetes Cluster Autoscaler is deployed on On-Demand worker nodes, and the AWS Node Termination Handler is deployed on all worker nodes.


![image](https://github.com/user-attachments/assets/21f71c79-53a8-4085-887a-6cd01de3e6be)



Spot Instance Interruption Handling
To mitigate the impact of potential Spot Instance interruptions, leverage the [node termination handler](https://github.com/aws/aws-node-termination-handler). The DaemonSet deploys a pod on each Spot Instance to detect the Spot Instance interruption notification, so that it can both terminate gracefully any pod that was running on that node, drain from load balancers and allow the Kubernetes scheduler to reschedule the evicted pods elsewhere on the cluster.

The workflow can be summarized as:

1. Identify that a Spot Instance is about to be interrupted in two minutes.
2. Use the two-minute notification window to gracefully prepare the node for termination.
3. Taint the node and cordon it off to prevent new pods from being placed on it.
4. Drain connections on the running pods.

You can run the termination handler on any Kubernetes cluster running on AWS, including self-managed clusters and those created with Amazon Elastic Kubernetes Service. If you're using EKS managed node groups, you don't need the aws-node-termination-handler.
