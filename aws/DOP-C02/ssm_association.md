[Link](https://docs.aws.amazon.com/systems-manager/latest/userguide/state-manager-about.html)
A State Manager association is a configuration that you assign to your AWS resources. The configuration defines the state that you want to maintain on your resources.
For example, an association can specify that antivirus software must be installed and running on a managed node, or that certain ports must be closed.

An association specifies a schedule for when to apply the configuration and the targets for the association. For example, an association for antivirus software might run once a day on all managed nodes in an AWS account. 
If the software isn't installed on a node, then the association could instruct State Manager to install it.
If the software is installed, but the service isn't running, then the association could instruct State Manager to start the service.
