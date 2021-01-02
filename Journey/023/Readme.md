# Architect Professional Prep - Day 10

## Ephemeral Port
- An ephemeral port is a short-lived port number used by an Internet Protocol (IP) transport protocol. Ephemeral ports are allocated automatically from a predefined range by the IP stack software.
- In practice, to cover the different types of clients that might initiate traffic to public-facing instances in your VPC, you can open ephemeral ports 1024-65535. However, you can also add rules to the ACL to deny traffic on any malicious ports within that range. Ensure that you place the deny rules earlier in the table than the allow rules that open the wide range of ephemeral ports.
- For the private subnets, if 