# Architect Professional Prep - Day 12

## Access control VPC gateway endpoint -> S3 bucket
### Restricting Access to a Specific VPC Endpoint
The `aws:SourceVpce` condition is used to specify the endpoint. The `aws:SourceVpce` condition does not require an Amazon Resource Name (ARN) for the VPC endpoint resource, only the **VPC endpoint ID**. 

``` 
{
   "Version": "2012-10-17",
   "Id": "Policy1415115909152",
   "Statement": [
     {
       "Sid": "Access-to-specific-VPCE-only",
       "Principal": "*",
       "Action": "s3:*",
       "Effect": "Deny",
       "Resource": ["arn:aws:s3:::DOC-EXAMPLE-BUCKET",
                    "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"],
       "Condition": {
         "StringNotEquals": {
           "aws:SourceVpce": "vpce-1a2b3c4d"
         }
       }
     }
   ]
}
```

### VPC endpoint policy
- A VPC endpoint policy is an IAM resource policy that you attach to an endpoint when you create or modify the endpoint. 
- If you do not attach a policy when you create an endpoint, we attach a **default policy for you that allows full access to the service**.

## DynamoDB Consistency
If your application requires strongly consistent reads, it must perform all of its strongly consistent reads and writes in the same region. DynamoDB does not support strongly consistent reads across Regions.

## CodePipeline v.s. CodeDeploy
- CodeDeploy suits application deployment but doesn't do CloudFormation infrastructure deployment.

## CloudFormation Stack Policy
- You can prevent stack resources from being unintentionally updated or deleted during a stack update by using a stack policy. A stack policy is a JSON document that defines the update actions that can be performed on designated resources.
- A stack policy applies only during stack updates. It **doesn't provide access controls** like an AWS Identity and Access Management (IAM) policy. Use a stack policy only as a fail-safe mechanism to prevent accidental updates to specific stack resources. To control access to AWS resources or actions, use IAM.

## AWS Macie
- Targets S3 buckets. 
- With Amazon Macie, you are charged based on two dimensions, the number of Amazon S3 buckets in your account per month and the amount of data processed for sensitive data discovery in a given month.

## Static IP address for NLB in each AZ
- By default, AWS assigns an IPv4 address to **each load balancer node** from the subnet for its **Availability Zone**. 
- Alternatively, if you create an internet-facing load balancer, you can select an Elastic IP address for each Availability Zone. 
- This provides your load balancer with static IP addresses. If you create an internal load balancer, you can assign a private IP address from the IPv4 range of each subnet instead of letting AWS assign one.

## Quorum Authentication (M of N Access Control)
- The HSMs in your AWS CloudHSM cluster support quorum authentication, which is also known as M of N access control. 
- With quorum authentication, no single user on the HSM can do quorum-controlled operations on the HSM. Instead, a minimum number of HSM users (at least 2) must cooperate to do these operations. 
- With quorum authentication, you can add an extra layer of protection by requiring approvals from more than one HSM user. 

## AWS IoT Greengrass
You can program your devices to act locally on the data they generate, execute predictions based on machine learning models, filter and aggregate device data, and only transmit necessary information to the cloud.

## Debugging 403 errors with S3 bucket as a CloudFront origin
- Objects in the bucket must be publicly accessible.
- Objects in the bucket can't be encrypted by AWS Key Management Service (AWS KMS).
- The bucket policy must allow access to s3:GetObject.
- If the bucket policy grants public read access, then the AWS account that owns the bucket must also own the object.
- The requested objects must exist in the bucket.
- Amazon S3 Block Public Access must be disabled on the bucket.
- If Requester Pays is enabled, then the request must include the request-payer parameter.
- If you're using a Referer header to restrict access from CloudFront to your S3 origin, then review the custom header.

