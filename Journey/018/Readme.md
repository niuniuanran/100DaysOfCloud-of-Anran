# Professional Question Prep - Day 5

## AWS Config
- Config **continuously** monitors and records your **AWS resource** configurations and allows you to automate the evaluation of recorded configurations against desired configurations. 
- AWS Config cannot monitor OS states.

## AWS OpsWork
- AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet. 
- Chef and Puppet are **automation platforms** that allow you to use code to automate the configurations of your servers. 

### Managing Linux Security Updates
- Linux operating system providers supply regular updates, most of which are operating system security patches but can also include updates to installed packages. 
- By default, AWS OpsWorks Stacks automatically installs the latest updates during **setup**, after an instance finishes booting. 
- AWS OpsWorks Stacks does not automatically install updates after an instance is online, to avoid interruptions such as restarting application servers. 
- Instead, you **manage updates to your online instances yourself**, so you can minimize any disruptions.

## ElastiCache
- It is not persistent storage.
- To provide high availability, Amazon ElastiCache for **Redis** supports Redis Cluster configuration, which delivers superior scalability and availability.

## IAM
### Developer power user
- AWS managed policy name: PowerUserAccess
- Use case: This user performs application development tasks and can create and configure resources and services that support AWS aware application development.

## Central logging
- Create Amazon Kinesis Data Strems in the logging account
- Subscribe the stream to CloudWatch Logs stream in each application AWS account.
- Configure an Amazon Kinesis Data Firehose delivery stream with the Data Stream as its source, and persist the log data in a S3 bucket inside the logging AWS account.

### Kibana
- Kibana is an open-source data visualization and exploration tool used for log and time-series analytics, application monitoring, and operational intelligence use cases. 



