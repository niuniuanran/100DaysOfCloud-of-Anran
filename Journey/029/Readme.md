# Architect Professional Prep - Day 15

## AWS Elemental MediaConvert
- Process video files and clips to prepare on-demand content for distribution or archiving
- video-on-demand (VOD) content

## Dead Letter Queue
The dead-letter queue of a FIFO queue must also be a FIFO queue. Similarly, the dead-letter queue of a standard queue must also be a standard queue.

## AWS Budgets - RI Coverage and RI Utilization
- You can use the AWS Billing and Cost Management console to create a reservation budget for RI Coverage and RI Utilization.
- You can either directly enter the emails to be alerted or use an SNS topic.
- You can filter resources by Region, Instance Type/Family, Tag, AZ.

## EC2 Auto Scaling service-linked role
- `AWSServiceRoleForAutoScaling`
- `AWSServiceRoleForAutoScaling_mysuffix`

In both cases, **you CANNOT edit the roles**. 

### Update key policy to allow service-linked role to use CMK to encrypt instance volumes
- You can specify either role when you edit your **AWS Key Management Service key policies** to allow instances that are launched by Amazon EC2 Auto Scaling to be encrypted with your customer managed CMK. 
- However, if you plan to give granular access to a specific customer managed CMK, you should use a custom suffix service-linked role. 

## What type of Virtual Interface should I choose for DX
### Public virtual gateway
To connect to AWS resources that are reachable by a public IP address (such as an S3 bucket) or AWS public endpoints, use a public virtual interface. 

### Private virtual interface
To connect to your resources hosted in an Amazon Virtual Private Cloud (Amazon VPC) using their private IP addresses, use a private virtual interface.

### Transit virtual interface
To connect to your resources hosted in an Amazon VPC (using their private IP addresses) through a transit gateway, use a transit virtual interface.


