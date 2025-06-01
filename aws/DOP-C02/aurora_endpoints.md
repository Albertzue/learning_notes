![image](https://github.com/user-attachments/assets/1c36652e-8177-4dfc-847f-e98b6ac22b2f)




### Cluster endpoint
Connect to the primary instance of your cluster to develop and test applications, and perform transformations like INSERT statements and DDL, DML, and ETL operations. Find the cluster endpoint location by using the AWS Management Console, AWS CLI, or Amazon RDS API, as described in Viewing the endpoints for an Aurora cluster.
![image](https://github.com/user-attachments/assets/88f8fd2c-992d-4405-953b-7d60abca8c91)


### Reader endpoint
Perform queries. Aurora automatically performs connection-balancing among all the Aurora Replicas. Find the reader endpoint location by using the AWS Management Console, AWS CLI, or Amazon RDS API, as described in Viewing the endpoints for an Aurora cluster.
![image](https://github.com/user-attachments/assets/9c3c2741-9096-4904-9011-e85a375fae18)


### Instance endpoint
Examine details about a specific DB instance for diagnosis or tuning. You can find the instance endpoint location for each of your instances in the AWS Management Console only, on the instance detail page for your instance.


### Custom endpoint
Connect to different subsets of DB instances on the DB cluster. This is useful when you have different instance capacities and configurations within your DB cluster. Find the custom endpoint locations by using the AWS Management Console, AWS CLI, or Amazon RDS API, as described in Viewing the endpoints for an Aurora cluster.

![image](https://github.com/user-attachments/assets/a5128219-0649-4774-8423-a08972149a17)
