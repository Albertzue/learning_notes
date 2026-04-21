4 NLB does not support round robin and least outstanding algorithm
7  lambda can only use ecr url for docker image 
9 The unlimited mode is a credit configuration option for burstable performance instances. 
10 you can add custom error page in the cloudfront distribution error pages
13 AWS OpsWorks is a managed configuration management service that helps customers configure, deploy, and operate applications using Chef or Puppet   Note: AWS OpsWorks is scheduled to reach End of Life (EOL) on May 26, 2024
14 This option might not work: Preventing ASG termination could create further trouble and there is no guarantee the script will run if the instance happens to be unhealthy
15 <img width="1090" height="509" alt="image" src="https://github.com/user-attachments/assets/9a39ccf0-1603-47f8-8c66-596241596d33" />
20 the S3 Glacier Deep Archive storage class cannot be used directly for web hosting
21 'Use active directory to sign in Aws accounts' = AWS IAM Identity Center (AWS Single Sign-On) , SAML 2.0, 'conditional access to the accounts based on user groups and roles' = AWS IAM (ABAC)
26 Secrets Manager has RotationSchedule resource
29 Only a management account in an organization and single accounts that aren't members of an organization have access to the cost allocation tags manager in the Billing and Cost Management console
32 SCP evaluation follows a deny-by-default model, meaning that any permissions not explicitly allowed in the SCPs are denied. If an allow statement is not present in the SCPs at any of the levels such as Root, Production OU or Account B, the access is denied.

39 AWS Migration Hub provides automated Amazon EC2 instance recommendations to help you estimate the cost of running existing on-premises servers in the AWS Cloud

43 UltraWarm provides a cost-effective way to store large amounts of read-only data on Amazon OpenSearch Service. Standard data nodes use "hot" storage, which takes the form of instance stores or Amazon EBS volumes attached to each node. Hot storage provides the fastest possible performance for indexing and searching new data. Rather than attached storage, UltraWarm nodes use Amazon S3 and a sophisticated caching solution to improve performance. For indexes that you are not actively writing to, query less frequently, and don't need the same performance from, UltraWarm offers significantly lower costs per GiB of data. Because warm indexes are read-only unless you return them to hot storage, UltraWarm is best-suited to immutable data, such as logs. [https://docs.aws.amazon.com/opensearch-service/latest/developerguide/ultrawarm.html]()

46  AWS Agentless Discovery Connector does not provide processes visibility
53  Since there is a Transit Gateway involved it is unlikely to have VPC peering and the resources in a VPC attached to a transit gateway cannot access the security groups of a different VPC that is also attached to the same transit gateway

54 AWS Compute Optimizer enhanced infrastructure metrics is for ec2 instance, asg instance and Amazon RDS DB instances.

55 AWS Cost Categories, found in the AWS Billing and Cost Management console, enable rule-based grouping of costs by dimensions like accounts, tags, or services. It facilitates detailed cost allocation for internal business structures. Users can define up to 50 categories with 500 rules each to analyze data in tools like Cost Explorer and Budgets

60 <img width="996" height="744" alt="image" src="https://github.com/user-attachments/assets/5b1ddf6a-f7b0-43ec-81bd-b4d428c7713f" />

62 AWS VM Import/Export allows migrating on-premises VMs to EC2 instances or AMIs, and vice versa, while maintaining configurations

66  EC2 Instance Connect is also providing audit but it requires the sg for ssh port 22

67 aws aurora db can be shared by RAM

70 AWS Organizations is recommended, but not required, for use with IAM Identity Center. If you haven't set up an organization, you don't have to. If you've already set up AWS Organizations and are going to add IAM Identity Center to your organization, make sure that all AWS Organizations features are enabled

77 AWS Transit Gateway supports five primary attachment types to centralize network connectivity: VPC (Virtual Private Cloud), VPN (Site-to-Site VPN), Direct Connect Gateway, Transit Gateway Peering (intra/inter-region), and TGW Connect (for SD-WAN appliances)

78 STARTTLS supports ports 25, 587, and 2587  TLSWRAPPER supports ports 465 and 2465

83 . s3 storage lens Free metrics are available for queries for a 14-day period, and advanced metrics are available for queries for a 15-month period

92 Using S3 Select is good for filtering data in S3, but it may not be a suitable solution for querying and analyzing large amounts of data

96 you encrypt data with KMS Data Key and not KMS Key directly, unless data is < 4K

104 In AWS Elastic Beanstalk, you can create a load-balanced, scalable environment or a single-instance environment. 

113 <img width="986" height="231" alt="image" src="https://github.com/user-attachments/assets/16e47482-f331-4f2f-9f30-f7c57d7c5cbd" />

114 Amazon Data Firehose (formerly Kinesis Data Firehose) automatically scales to handle varying data throughput without manual intervention or pre-provisioning
