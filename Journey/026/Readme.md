# Architect Professional Prep - Day 13

## Alias Record
Alias records let you route traffic to selected AWS resources, such as **CloudFront distributions** and Amazon S3 buckets.

## Secure RDP access to Windows EC2 instance
One solution to this problem is to protect your Windows instances at the network layer using **Microsoft Remote Desktop (RD) Gateway** server set up as a bastion. 

## Simple Active Directory
- Simple AD provides a subset of the features offered by AWS Managed Microsoft AD, including the ability to manage user accounts and group memberships, create and apply group policies, securely connect to Amazon EC2 instances, and provide Kerberos-based single sign-on (SSO). 
- However, note that Simple AD does not support features such as multi-factor authentication (MFA), trust relationships with other domains, Active Directory Administrative Center, PowerShell support, Active Directory recycle bin, group managed service accounts, and schema extensions for POSIX and Microsoft applications.

##  What is the difference between EC2 VM Import and AWS Server Migration Service?
- AWS Server Migration Service is a **significant enhancement** of EC2 VM Import. 
- The AWS Server Migration Service provides automated, **live** incremental server replication and AWS Console support. 
- For customers using EC2 VM Import for migration, we recommend using AWS Server Migration Service.

## IAM Role permissions for working with S3 SSE-KMS
- All IAM roles which need to read data encrypted with SSE-KMS must have the permissions to decrypt using the specific key the data was encrypted with: kms:Decrypt
- All IAM roles which need to both read and write data need the encrypt and decrypt permissions (encrypt-only permission is not supported).
- When a user sends a GET request, Amazon S3 checks if the AWS Identity and Access Management (IAM) user or role that sent the request is authorized to decrypt the key associated with the object. If the IAM user or role belongs to the same AWS account as the key, then the permission to decrypt must be granted on the AWS KMS key’s policy.

Example IAM policy:
``` 
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": [
        "kms:Decrypt",
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:kms:example-region-1:123456789012:key/example-key-id",
        "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
      ]
    }
  ]
}
```

Example Key policy:
``` 
{
  "Sid": "Allow decryption of the key",
  "Effect": "Allow",
  "Principal": {
    "AWS": [
      "arn:aws:iam::123456789012:user/Bob"
    ]
  },
  "Action": [
    "kms:Decrypt"
  ],
  "Resource": "*"
}
```

## Bucket owner granting cross-account permission to objects it does not own
- By default, an S3 object is owned by the AWS account that uploaded it. This is true even when the bucket is owned by another account. To get access to the object, the object owner must explicitly grant you (the bucket owner) access. 
- The object owner can grant the bucket owner full control of the object by updating the **access control list (ACL)** of the object to be `bucket-owner-full-control`. The object owner can update the ACL either during a put or copy operation, or after the object is added to the bucket.

### References
- [Why can't I access an object that was uploaded to my Amazon S3 bucket by another AWS account?](https://aws.amazon.com/premiumsupport/knowledge-center/s3-bucket-owner-access/)
- [When other AWS accounts upload objects to my Amazon S3 bucket, how can I require that they grant me ownership of the objects?](https://aws.amazon.com/premiumsupport/knowledge-center/s3-require-object-ownership/)


```
{
    "Id": "Policy1541018284691",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1541018283275",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::awsexamplebucket/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            },
            "Principal": {
                "AWS": [
                    "arn:aws:iam::111122223333:user/ExampleUser"
                ]
            }
        }
    ]
}
```
After you add this bucket policy, users must set the object's ACL to bucket-owner-full-control as part of the upload request, similar to the following:
```
aws s3 cp example.jpg s3://awsexamplebucket --acl bucket-owner-full-control
```

## RDS I/O baseline and credit 

### Baseline
- Baseline I/O performance for General Purpose SSD storage is 3 IOPS for each GiB, with a minimum of 100 IOPS. 
- Provisioned IOPS storage is designed to meet the needs of I/O-intensive workloads, particularly database workloads, that require low I/O latency and consistent I/O throughput.

### I/O credits and burst performance
- Volumes below 1 TiB in size also have ability to burst to 3,000 IOPS for extended periods of time. 
- Burst is not relevant for volumes above 1 TiB. Instance I/O credit balance determines burst performance.
- When using General Purpose SSD storage, your DB instance receives an initial I/O credit balance of 5.4 million I/O credits. This initial credit balance is enough to sustain a burst performance of 3,000 IOPS for 30 minutes. 
- This balance is designed to provide a fast initial boot cycle for boot volumes and to provide a good bootstrapping experience for other applications. 
- Volumes earn I/O credits at the baseline performance rate of 3 IOPS for each GiB of volume size.

## SAML 2.0-based federation

### Using SAML-based federation for API access to AWS
<img src="https://docs.aws.amazon.com/IAM/latest/UserGuide/images/saml-based-federation.diagram.png" width="600px" alt=""/>

Process:
1. Client app requests authentication from organization's IdP.
2. The IdP authenticates user against the organization's identity store.
3. IdP constructs a **SAML assertion** with information about the user, and sends the assertion to the client app.
4. The client app calls the **AWS STS `AssumeRoleWithSAML` API**, passing the ARN of the SAML provider, the ARN of the role to assume, and the SAML assertion from IdP.
5. The `AssumeRoleWithSAML` API response to the client app includes **temporary security credentials**.
6. The client app uses the temporary security credentials to call Amazon API.

### Key steps in configuring SAML 2.0-based federation

1. Register AWS with your IdP as a service provider (SP).
2. Using your organization's IdP, you generate an equivalent metadata XML file that can describe your IdP as an IAM identity provider in AWS. 
3. In the IAM console, you create a **SAML identity provider** entity. Upload the SAML metadata document that was produced by the IdP in your organization in Step 2.
4. In IAM, you create one or more IAM roles. In the role's **trust policy**, you set the **SAML identity provider** as the principal, which establishes a trust relationship between your organization and AWS. The role's permission policy establishes what users from your organization are allowed to do in AWS.
5. In your organization's IdP, you define **assertions** that **map users or groups in your organization to the IAM roles**.
6. In the application that you're creating, you call the **AWS Security Token Service** `AssumeRoleWithSAML` API, passing it:
    1. the ARN of the SAML provider you created in Step 3, 
    2. the ARN of the role to assume that you created in Step 4, 
    3. the SAML assertion about the current user that you get from your IdP.  
7. If the request is successful, the API returns a set of **temporary security credentials**, which your application can use to make signed requests to AWS. 





