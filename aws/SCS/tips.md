13 AWS Network Load Balancers (NLBs) support direct native delivery to Amazon CloudWatch Logs, while Application Load Balancers (ALBs) and Classic Load Balancers (CLBs) require an intermediary AWS Lambda function to forward access logs from Amazon S3 to CloudWatch Logs

41 When you create a permission set with a customer managed policy, you must create an IAM policy with the same name and path in each AWS account where IAM Identity Center assigns your permission set. If you are specifying a custom path, make sure to specify the same path in each AWS account. 

44 https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-state.html   Systems Manager State Manager can not detect RDS database encryption configuration drift.

45 AWS Backup cannot directly copy an encrypted (or unencrypted) EBS volume or its recovery points into a customer-managed Amazon S3 bucket.
