# Day 10: Programmatically access AWS

## AWS CLI
- Never put your personal credentials on an EC2. EC2 does not belong to you.
- AWS CLI on EC2 - the right way: IAM roles.

### AWS Dry Run
Some commands have `--dry-run` parameter for you to simulate the command but do not really do it.

### (popular question) AWS CLI STS Decode Errors
Error message you get from failed API calls can be decoded using the **STS Command Line**.

#### AWS STS
AWS Security Token Service (AWS STS) is a web service that enables you to request temporary, limited-privilege credentials for AWS Identity and Access Management (IAM) users or for users that you authenticate (federated users).

### AWS STS decode-authorization-message

[decode-authorization-message](https://docs.aws.amazon.com/cli/latest/reference/sts/decode-authorization-message.html) decodes additional information about the authorization status of a request from an encoded message returned in response to an AWS request.

Syntax:
`aws sts decode-authorization-message --encoded-message <value of the encoded message>`


