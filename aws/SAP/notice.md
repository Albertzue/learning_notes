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

83 s3 storage lens Free metrics are available for queries for a 14-day period, and advanced metrics are available for queries for a 15-month period

92 Using S3 Select is good for filtering data in S3, but it may not be a suitable solution for querying and analyzing large amounts of data

96 you encrypt data with KMS Data Key and not KMS Key directly, unless data is < 4K

104 In AWS Elastic Beanstalk, you can create a load-balanced, scalable environment or a single-instance environment. 

113 <img width="986" height="231" alt="image" src="https://github.com/user-attachments/assets/16e47482-f331-4f2f-9f30-f7c57d7c5cbd" />

114 Amazon Data Firehose (formerly Kinesis Data Firehose) automatically scales to handle varying data throughput without manual intervention or pre-provisioning

117 cloud trail can use sns  event bridge( real time) and CloudWatch Logs to monitor and alert on log data

135 Enabling Amazon DynamoDB Streams is a fundamental prerequisite for configuring DynamoDB Global Tables. The stream acts as the mechanism that captures and propagates item-level changes across all replica regions

136 DocumentDB has no on-demand capacity "mode".

141 To protect EC2 instances managed by an Auto Scaling Group (ASG) from termination, you must use Instance Scale-In Protection rather than standard EC2 termination protection. This prevents the ASG from terminating specific instances during scale-in events while allowing them to be replaced if they fail health checks.

146 Amazon DLM can be used for scheduling snapshots, but it does not provide real-time replication and may not meet the requirement of no data loss in case of a failure.

147 Using Fargate may not be the most cost-effective solution and also it may not handle large amount of data.
155 an apex domain cannot use CNAME records in AWS
157  AWS IoT Greengrass supports offline operation by enabling devices to continue processing data even when they are disconnected from the internet.

163 Amazon ElastiCache for Redis now supports updates to encryption in transit on existing cluster resources. You can change the TLS configuration of your Redis clusters without re‑building or re‑provisioning them or impacting application availability. ... Upgrade your Redis cluster to version 7 or above. You can then modify the encryption‑in‑transit property for your cluster using the ElastiCache Console, API or CLI.

164 launch template cannot be updated
165 FSx for Luster doesn't support NFS protocol It actually support only POSIX protocol
171 CodeCommit is not supported by AWS Backup and has no snapshot feature

173  can use IAM Access Analyzer-> resource access analyzer for S3
174 Migration Evaluator builds the business case and server inventory, Migration Hub provides a single view of the portfolio, and Application Discovery Service reveals application/database dependencies. The other options focus on migration execution (SMS, DMS, MGN) 
175 AWS EBS Multi-Attach  All instances must reside in the same AZ.

190 Route 53 failover will not be as immediate as cloudfront failover

199 
```
AWS Firewall Manager has the following prerequisites:
AWS Organizations: Your organization must be using AWS Organizations to manage your accounts, and All Features must be enabled. For more
information, see Creating an Organization and Enabling All Features in Your Organization.
A firewall administrator AWS Account: You must designate one of the AWS accounts in your organization as the administrator for AWS Firewall
Manager. This gives the account permission to deploy AWS WAF rules across the organization.
AWS Config: You must enable AWS Config for all of the accounts in your organization so that AWS Firewall Manager can detect newly created
resources. To enable AWS Config for all of the accounts in your organization, you can use the Enable AWS Config template on the StackSets
Sample Templates page. For more information, see Getting Started with AWS Config.
``


204 DLM itself does not directly support restore operations
205 cloudfront can redirect http to https  at Behaviors tab
210 kms can rotate key but can not use lambda
211 the Application Migration Service needs to install agent on thousands of VMs, so it is not suitable for initial inventory collection and is high Operational overhead

218 AWS Global Accelerator cannot directly target an Amazon API Gateway endpoint as its backend
231 AWS Storage Gateway's FSx File Gateway is no longer available to new customers
251 Amazon API Gateway doesn't support request limiting through resource policies
254 only dynamodb Provisioned r/w mode can autoscaling
268 You can detach/attach instances from your Auto Scaling group
289 You cannot natively convert the RDS for MySQL DB instance to an Amazon Aurora MySQL DB cluster. Instead, you can create an Amazon Aurora MySQL replica of the RDS MySQL RDS DB instance:
301 REST APIs and HTTP APIs are both RESTful API products. REST APIs support more features than HTTP APIs, while HTTP APIs are designed with minimal features so that they can be offered at a lower price. Choose REST APIs if you need features such as API keys, per-client throttling, request validation, AWS WAF integration, or private API endpoints. Choose HTTP APIs if you don't need the features included with REST APIs.
303 field-level encryption in CloudFront uses asymmetric encryption with RSA key

306 <img width="616" height="432" alt="image" src="https://github.com/user-attachments/assets/adf61f60-b0be-4070-95c9-4235d0c0fdaa" />

308 aws backup can daily weekly  monthly and coustom define as following<img width="843" height="391" alt="image" src="https://github.com/user-attachments/assets/ed80bde2-89d1-4f22-8751-76c389c3d7a5" />
311 Compute Savings Plans (up to 66% off) offer maximum flexibility across EC2, Fargate, and Lambda, automatically applying to different families and regions. EC2 Instance Savings Plans (up to 72% off) offer higher discounts but restrict you to specific instance families within a single region

319 cannot join an EC2 to On-prem AD just over the VPN. You should be having an AD connector for the same

321 When you connect to an instance using EC2 Instance Connect through the console or AWS CLI, the EC2 Instance Connect API automatically pushes an SSH public key to the instance metadata where it remains for 60 seconds

326 AWS Directory Service Simple AD does not support (MFA)

332 security group can have only 60 rules, so you can't add ALL CloudFront IPs into it, so prefix list

335 Global Database is recommended for low-latency global reads and high-resilience, whereas cross-region replicas are more suitable for specific, limited migration or read-only use cases

338 cloudwatch log subscription filters can be intergrated with  kinesis  data firehose open search and lambda as following
<img width="448" height="205" alt="image" src="https://github.com/user-attachments/assets/4786fa93-68e1-4c7a-a739-2fb0b828f6b0" />

339  the AWS VM Import/Export process generally requires the source Virtual Machine (VM) to be shut down to ensure data consistency during the export and import phases
346 Amazon Aurora PostgreSQL serverless v2 is not existing
350 <img width="678" height="256" alt="image" src="https://github.com/user-attachments/assets/fa19c873-d391-47ce-aa76-a9db7116cb9d" />
356 agentless discovery which is only used for on-prem VMs
361 Network Load Balancers now support connections from clients to IP-based targets in peered VPCs across different AWS Regions
