# Architect Professional Prep - Day 11

## AWS Service Catalog
- AWS Service Catalog allows organizations to centrally manage **commonly deployed IT services**, and helps organizations achieve consistent governance and meet compliance requirements. 
- End users can quickly deploy only the **approved IT services** they need, following the constraints set by your organization.

### AWS Service Catalog Launch Constraints
A **launch constraint** specifies the AWS Identity and Access Management (IAM) role that AWS Service Catalog assumes when an end user launches a product. An IAM role is a collection of permissions that an IAM user or AWS service can assume temporarily to use AWS services. 

## Ad hoc Query
- An Ad-Hoc Query is a query that cannot be determined prior to the moment the query is issued. 
- It is created in order to get information when need arises and it consists of dynamically constructed SQL which is usually constructed by desktop-resident query tools.

### Amazon Athena
Amazon Athena is an interactive query service that makes it easy to analyze data directly in Amazon S3 using standard SQL. With a few clicks in the AWS Management Console, customers can point Athena at their data stored in S3 and begin using **standard SQL** to run **ad-hoc queries** and get results in seconds. 

## AWS Glue
### AWS Glue Crawler
- You can use a crawler to populate the AWS Glue Data Catalog with tables. This is the primary method used by most AWS Glue users. 
- A crawler can crawl multiple data stores in a single run. Upon completion, the crawler creates or updates one or more tables in your **Data Catalog**.

## AWS CDK
- The AWS Cloud Development Kit (AWS CDK) is an open source software development framework to **define your cloud application resources** using familiar programming languages and provision them with CloudFormation.
- You get all the benefits of CloudFormation, including repeatable deployment, easy rollback and drift detection.
- It also enables you to compose and share your own custom constructs that incorporate your organization's requirements, helping you start new projects faster.

## AWS CodeBuild
- AWS CodeBuild is a fully managed **continuous integration** service that *compiles source code, runs tests, and produces software packages* that are ready to deploy. 
- Use AWS CodeBuild to run unit tests.

## ECS Task Role v.s. Task Execution Role
- ECS task execution role is capabilities of ECS agent (and container instance), e.g:
    - Pulling a container image from Amazon ECR
    - Using the awslogs log driver
- ECS task role is specific capabilities within the task itself, e.g:
    - When your actual code runs
    
### Example
> A fleet of Amazon ECS instances is used to poll an Amazon SQS queue and update items in an Amazon DynamoDB database. Items in the table are not being updated, and the SQS queue is filling up. Amazon CloudWatch Logs are showing consistent 400 errors when attempting to update the table. The provisioned write capacity units are appropriately configured, and no throttling is occurring.
  What is the LIKELY cause of the failure?

- "400 errors when attempting to update table" means the API calls to update the DynamoDB table is not properly authenticated.
- The ECS task is attempting to update the DynamoDB table without the proper **Task Role**, the role to actually conduct the task.

## Improving Athena Performance
### Use Compression
For Athena, we recommend using either **Apache Parquet or Apache ORC**, which compress data by default and are splittable. 

### Partition your data
- Partitioning divides your table into parts and keeps the related data together based on column values such as date, country, region, etc. 
- Partitions act as **virtual columns**.
- Athena supports Hive partitioning


 







