# Architect Professional Prep - Day 7

## Direct Connect facilities
### Direct Connect Gateway
- A Direct Connect gateway is a globally available resource. You can create the Direct Connect gateway in any Region and access it from all other Regions. 
- Use AWS Direct Connect gateway to connect your VPCs. You associate an AWS Direct Connect gateway with either of the following gateways:
    1. A transit gateway when you have multiple VPCs in the same Region
    2. A virtual private gateway

### VIF(AWS Direct Connect virtual interfaces)
You must create one of the following virtual interfaces to begin using your AWS Direct Connect connection.
1. **Private virtual interface**: Access an Amazon VPC using private IP addresses.
2. **Public virtual interface**: Access AWS services from your on-premises data center. Allow AWS services, or AWS customers access your public networks over the interface instead of traversing the internet.
3. **Transit virtual interface**: Access one or more *Amazon VPC Transit Gateways* associated with Direct Connect gateways. 

<img src="https://docs.aws.amazon.com/directconnect/latest/UserGuide/images/dx-gateway.png" alt="VIF is connected with VGW attached to the VPC" width="700px"/>

## Route53 Health Check
You can choose which locations you want Route 53 to use, and you can specify the interval between checks: every 10 seconds or every 30 seconds. 

### Health check types
#### HTTP and HTTPS health checks
- Route 53 must be able to establish a TCP connection with the endpoint within **4 seconds**. 
- In addition, the endpoint must respond with an HTTP status code of 2xx or 3xx within **2 seconds after connecting**.

#### TCP health checks
Route 53 must be able to establish a TCP connection with the endpoint within **ten seconds**.

#### HTTP and HTTPS health checks with string matching
1. As with HTTP and HTTPS health checks, Route 53 must be able to establish a TCP connection with the endpoint within **four seconds**
2. The endpoint must respond with an HTTP status code of 2xx or 3xx within **two seconds after connecting**.
- After a Route 53 health checker receives the HTTP status code, it must receive the response body from the endpoint within the **next two seconds**. 
- Route 53 searches the response body for a string that you specify. The string must appear entirely in the **first 5,120 bytes** of the response body or the endpoint fails the health check. 

## RDS read replica for data recovery
 You can promote a read replica to a standalone instance as a disaster recovery solution if the primary DB instance fails. Almost no data loss.

## Building a Cloud Call Centre
### Amazon Connect
- Amazon Connect is an easy to use omnichannel cloud contact center that helps you provide superior customer service at a lower cost.
- Amazon Connect has queuing built in it.

### Amazon Lex
- Amazon Lex is a service for building conversational interfaces into any application using voice and text. 
- Amazon Lex provides the advanced deep learning functionalities of automatic speech recognition (ASR) for converting speech to text, and natural language understanding (NLU) to recognize the intent of the text, to enable you to build applications with highly engaging user experiences and lifelike conversational interactions. 

## AWS Systems Manager
### Patch baseline
- A patch baseline defines which patches are approved for installation on your instances. 
- You can specify approved or rejected patches one by one. 
- You can also create auto-approval rules to specify that certain types of updates (for example, critical updates) should be automatically approved. 
- The rejected list overrides both the rules and the approve list.

#### Predefined baselines
- `AWS-DefaultPatchBaseline`, `AWS-WindowsPredefinedPatchBaseline-OS`, `AWS-WindowsPredefinedPatchBaseline-OS-Applications` for Windows server
- `AWS-[OS name]DefaultPatchBaseline` for other systems, for example, `AWS-AmazonLinuxDefaultPatchBaseline`, `AWS-MacOSDefaultPatchBaseline`.

## Elastic Network Adapter
Used **within** a placement group to get network throughput of 20 GiB/s

## RDS event notifactions
Amazon RDS uses the Amazon Simple Notification Service (Amazon SNS) to provide notification when an Amazon RDS event occurs. These notifications can be in any notification form supported by Amazon SNS for an AWS Region, such as an email, a text message, or a call to an HTTP endpoint.

## AWS WorkSpaces
- Amazon WorkSpaces is a managed, secure Desktop-as-a-Service (DaaS) solution. 
- You can use Amazon WorkSpaces to provision either Windows or Linux desktops in just a few minutes and quickly scale to provide thousands of desktops to workers across the globe.

### Amazon WorkSpaces Application Manager
- Amazon WorkSpaces Application Manager (Amazon WAM) offers a fast, flexible, and secure way for you to deploy and manage applications for Amazon WorkSpaces. 
- Amazon WAM allows you to build and curate a selection of desktop applications for your users and control access to those applications. 

## Apache Cassandra
- Distributed, wide column store, NoSQL database management system
- Designed to handle large amounts of data across many commodity servers, providing high availability with no single point of failure.


