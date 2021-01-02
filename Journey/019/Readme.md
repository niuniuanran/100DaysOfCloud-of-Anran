# Architect Professional Prep - Day 6

## AWS Application Discovery Service
AWS Application Discovery Service helps enterprise customers plan migration projects by gathering information about their on-premises data centers.

- Planning data center migrations can involve thousands of workloads that are often deeply interdependent. 
- Server utilization data and dependency mapping are important early first steps in the migration process. 
- AWS Application Discovery Service collects and presents configuration, usage, and behavior data from your servers to help you better understand your workloads.

### Agent-based discovery
- The agent captures system configuration, system performance, running processes, and details of the network connections between systems.
- Just like on local VM, you can install the AWS Discovery Agents on your EC2 instances to perform discovery and report upon performance information, network connections, and running processes, just as for any other server.

### Agentless discovery
- ‘Agentless’ means no software needs to be installed on each host to use Application Discovery. Simply install the AWS Application Discovery Agentless Connector as an OVA on VMware vCenter.
- Data collection can be enabled or disabled from the AWS console or via the AWS Discovery SDK or AWS Command Line Interface (CLI). Newly installed Connectors have data collection initially disabled when installed.
- You cannot run agentless discovery on EC2 instances. The AWS Agentless Discovery Connector installs on VMware and collects information only from VMware vCenter.

### What data can be collected
- AWS Application Discovery Service is designed to capture a variety of data including **static configuration** such as server hostnames, IP addresses, MAC addresses, CPU allocation, **network throughput**, **memory allocation**, **disk resource allocations**, DNS servers. 
- It also captures **resource utilization** metrics such as **CPU usage and memory usage**. 
- In addition, the AWS Application Discovery **Agent** can help determine **server workloads** and **network relationships** by identifying network connections between systems.

## Organisation SCP
- SCP **does not grant anything**. You still need to add IAM permission.

## Kinesis Data Firehose
### Destination
It supports:
- Amazon S3, 
- Amazon Redshift, 
- Amazon Elasticsearch Service
- Splunk

### Kinesis Agent
Kinesis Agent is a stand-alone Java software application that offers an easy way to collect and send data to Kinesis Data Streams. The agent continuously **monitors a set of files** and sends new data to your stream. 

## Near Real-Time and Real-time
### Real-time
- Kinesis Data Stream
- CloudWatch
- Trusted Advisor

### Near Real-time
- Kinesis Data Firehose
- AWS AppSync
    1. With managed GraphQL subscriptions, AWS AppSync can push real-time data updates over Websockets to millions of clients. 
    2. For mobile and web applications, AppSync also provides local data access when devices go offline, and data synchronization with customizable conflict resolution, when they are back online.

## DMS and SMS
### DMS
#### Migrating to ES
- AWS DMS can do a one-time data migration, or it can do a continuous replication of the data from any of our supported sources to an Amazon ES target. 
- These sources include:
    1. Relational databases (such as Oracle and Amazon Aurora), 
    2. NoSQL database (MongoDB/Cassandra), or 
    3. Amazon S3 bucket.

### Server Migration Service
- Currently, you can migrate virtual machines from VMware vSphere, Windows Hyper-V, or Microsoft Azure to AWS using AWS Server Migration Service.
- AWS Server Migration Service is a significant enhancement of EC2 VM Import. The AWS Server Migration Service provides automated, live incremental server replication and AWS Console support. For customers using EC2 VM Import for migration, we recommend using AWS Server Migration Service.

## SWF and StepFunction
- Amazon Simple Workflow Service (SWF) is a web service that makes it easy to coordinate work across distributed application components. 
- In Amazon SWF, tasks represent invocations of logical steps in applications.
- Tasks are processed by workers which are programs that interact with Amazon SWF to get tasks, process them, and return their results.
- You should consider using StepFunctions, **unless** you require **external signals** to intervene in your processes, or you would like to launch **child processes** that return a result to a parent.

## IAM roles for ECS tasks
- With IAM roles for Amazon ECS tasks, you can specify an IAM role that can be used by the containers in a task. 

## IPv6 Support
- NAT gateways are not supported for IPv6 traffic.
- Use an **outbound-only (egress-only) internet gateway** instead.

## AD Trust Relationship
- You can configure one and two-way external and forest trust relationships between your AWS Directory Service for Microsoft Active Directory and on-premises directories, as well as between multiple AWS Managed Microsoft AD directories in the AWS cloud. 
- AWS Managed Microsoft AD supports all three trust relationship directions: Incoming, Outgoing and Two-way (Bi-directional).







  
