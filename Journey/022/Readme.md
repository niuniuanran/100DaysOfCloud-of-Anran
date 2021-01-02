# Architect Professional Prep - Day 9

## Amazon Mechanical Turk
- Amazon Mechanical Turk (MTurk) is a **crowdsourcing marketplace** that makes it easier for individuals and businesses to outsource their processes and jobs to a distributed workforce who can perform these tasks virtually. 
- MTurk enables companies to harness the collective intelligence, skills, and insights from a global workforce to streamline business processes, augment data collection and analysis, and accelerate machine learning development.

## Amazon Transcribe
Automatically convert speech to text.

## Service Control Policies (SCPs)
- Service control policies (SCPs) are a type of organization policy that you can use to manage permissions in your organization. 
- SCPs offer central control over the maximum available permissions for all accounts in your organization. 
- SCPs help you to ensure your accounts stay within your organization’s access control guidelines. 
- SCPs are available only in an organization that has all features enabled.
- SCPs don't affect users or roles in the management account. 
- They affect only the member accounts in your organization.
- No permissions are granted by an SCP. 
- An SCP defines a guardrail, or sets limits, on the actions that the account's administrator can delegate to the IAM users and roles in the affected accounts. 
- The effective permissions are the **logical intersection** between what is allowed by the SCP and what is allowed by the IAM and resource-based policies.

### SCP Inheritance
- To allow an AWS service API at the member account level, you must allow that API at **every level** between the member account and the root of your organization. 
    - A `deny list strategy` makes use of the `AWSFullAccess` SCP that is attached by default to every OU and account. This SCP overrides the default implicit deny, and explicitly allows all permissions to flow down from the root to every account, unless you explicitly deny a permission with an additional SCP that you create and attach to the appropriate OU or account.
    - An `allow list strategy` has you remove the `AWSFullAccess` SCP that is attached by default to every OU and account. This means that no APIs are permitted anywhere unless you explicitly allow them. 




