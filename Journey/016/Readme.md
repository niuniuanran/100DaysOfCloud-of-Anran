# Professional Question Prep - Day 3

##  Does ACM copy certificates across AWS Regions?
No. 
- The private key of each ACM certificate is stored in the **Region** in which you request the certificate. 
- For example, when you obtain a new certificate in the US East (N. Virginia) Region, ACM stores the private key in the N. Virginia Region. 
- ACM certificates are only copied across Regions if the certificate is associated with a CloudFront distribution. In that case, **CloudFront distributes the ACM certificate to the geographic locations configured for your distribution**.

## Server Migration Service
- Server Migration Service works with VM.
- SMS only support Linux and Windows.

## CloudTrail -> SNS has no filtering
You can be notified when CloudTrail publishes new log files to your Amazon S3 bucket. You manage notifications using Amazon Simple Notification Service (Amazon SNS).

Notifications are optional. If you want notifications, you configure CloudTrail to send update information to an Amazon SNS topic whenever a new log file has been sent. To receive these notifications, you can use Amazon SNS to subscribe to the topic. As a subscriber you can get updates sent to a Amazon Simple Queue Service (Amazon SQS) queue, which enables you to handle these notifications programmatically.

> Monitor recorded CloudTrail activities using CloudWatch logs.

## Redshift
- Amazon Redshift only supports Single-AZ deployments
- For a four-hour RTO, ensure Redshift is templated with CloudFront and can be easily launched in another AZ; data restored from Redshift automated back-ups from S3.

## Detect public object in S3 and automatically remediate
- S3 event notifications will not work: potential loss, delay
- Turn on object logging on S3, Configure a CloudWatch Event to notify by using an SNS topic when PutObject request with public-read permission.
- Configure CloudWatch Events rule to trigger Lambda to remediate.

<img src="https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2017/01/25/Diagram1-012417-MT.png" width="600px" alt="AWS answer"/>

See [this link](https://aws.amazon.com/blogs/security/how-to-detect-and-automatically-remediate-unintended-permissions-in-amazon-s3-object-acls-with-cloudwatch-events/) for more details.


