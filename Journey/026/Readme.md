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






