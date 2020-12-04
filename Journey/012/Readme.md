# Day 12: S3 Security

## S3 MFA Delete
- To use MFA-Delete, you need to enable versioning.
    - (By the way, To enable DynamoDB Global table, you need to enable streaming.)
- You need MFA to:
    1. Permanently delete an object version
    2. Suspend versioning on the bucket
- You won't need MFA for
    1. Enabling versioning
    2. Listing deleted versions
- Only the bucket owner (root account) can enable/disable MFA-delete.
- Only CLI can enable MFA-delete. Therefore you have to use the root Access Key. Use it to enable MFA delete and disable it!
- After MFA delete is enabled, you cannot delete a version permanently or suspend versioning from the console. You have to do it on CLI and provide the MFA device + code.

## S3 Default Encryption
- Old way: set bucket policy to refuse any HTTP command without proper encryption headers.

``` 
{
     "Version": "2012-10-17",
     "Id": "PutObjPolicy",
     "Statement": [
           {
                "Sid": "DenyIncorrectEncryptionHeader",
                "Effect": "Deny",
                "Principal": "*",
                "Action": "s3:PutObject",
                "Resource": "arn:aws:s3:::<bucket_name>/*",
                "Condition": {
                        "StringNotEquals": {
                               "s3:x-amz-server-side-encryption": "AES256"
                         }
                }
           },
           {
                "Sid": "DenyUnEncryptedObjectUploads",
                "Effect": "Deny",
                "Principal": "*",
                "Action": "s3:PutObject",
                "Resource": "arn:aws:s3:::<bucket_name>/*",
                "Condition": {
                        "Null": {
                               "s3:x-amz-server-side-encryption": true
                        }
               }
           }
     ]
 }
```

- New way: use the "default encryption" option in S3.

## S3 Access Logs
- For audit purpose, you might want to log all access to S3 buckets.
- Any request made to S3, from any account, authorized or denied, will be logged into another S3 bucket.
- The access logs can be analysed with Amazon Athena.
- Do not put your logging to your monitored bucket: logging loop!

## S3 Replication (CRR, SRR)
- After activating repliication, only new objects are async replicated.
- S3 Replication requirements
    1. Must enable versioning in source and destination
    2. Buckets can be in different accounts
    3. Copying is async
    4. Must give proper IAM permissions to S3
- User cases
    1. CRR: compliance, lower latency, replication across accounts
    2. SRR: log aggregation, live replication between production and test accounts.
- Pricing:
    1. For S3 Replication (Cross-Region Replication and Same Region Replication), you pay the S3 charges for 
        - storage in the selected destination S3 storage classes, 
        - the storage charges for the primary copy, 
        - replication PUT requests, and 
        - applicable infrequent access storage retrieval fees. 
    2. For CRR, you also pay for
        - inter-region Data Transfer OUT from S3 to each destination region. 
- Handling DELETE operations:
    1. If you delete without a version ID, it adds a delete marker, the marker not replicated.
    2. If you delete with a version ID, it deletes the version on the origin, but deleting action is not replicated either.
- You cannot "chain" replication. If bucket 1 has replication into bucket 2 and 2 into 3, bucket 3 does not replicate bucket 1.

## S3 pre-signed URLs
You use CLI or SDK to generate pre-signed URL for download; you can only use SDK to generate for upload. You can specify the expiration time of the URL.

## S3 storage class
- S3 Storage Classes can be configured at the object level, and a single bucket can contain objects stored across S3 Standard, S3 Intelligent-Tiering, S3 Standard-IA, and S3 One Zone-IA. 

