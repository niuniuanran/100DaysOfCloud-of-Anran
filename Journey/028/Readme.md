# Service Limitations I did not know before
1. An interface endpoint supports TCP traffic only.
2. OpsWorks does not support canary deployment.
3. Aurora Serverless can only reside in a private subnet of a VPC and cannot have public IP.
4. DynamoDb strongly consistent read cannot be cross region.
5. Snowball devices can only be used to import or export data within the AWS Region where the devices were ordered.
6. Endpoint connections cannot be extended out of a VPC. Resources on the other side of a VPN connection, VPC peering connection, transit gateway, **DX** CANNOT use the endpoint to communicate with resources in the endpoint service.
7. You cannot copy ACM-managed certificates between regions.
8. Volume Gateway takes a volume snapshot, and you cannot restore a single file through S3.
9. CloudTrail logs -> SNS notification has no filtering, you will receive all updates.
10. Amazon Redshift only supports Single-AZ deployments.
11. CloudWatch Events cannot detect events from S3. 
12. AWS Config cannot monitor OS state.
