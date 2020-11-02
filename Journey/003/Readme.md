# NLB & ALB

## Cloud Research
- One public IPv4 address per AZ
    - Network Load Balancers expose a public **static** IP per AZ and allows assigning Elastic IP per AZ. Good for network whitelisting.
    - ALB and CLB is assigned a public IPv4 IP address per AZ, but it is not static. You should use the domain name to access the ALB/CLB.
- Security Groups 
    - NLB does NOT have a security group. You just need to allow traffic from NLB to your targets by allowing its IPv4 addresses.
    - ALB and CLB have security groups. You put them in a security group, and allow traffic from ELB security group to targets' security group.
- Supported protocols
    - ALB supports: HTTP, HTTPS, WebSocket
    - NLB supports: TCP, TLS(secure TCP), UDP.
    - CLB supports: HTTP, HTTPS, TCP
- ALB/NLB Health Checks are done at the Target Group level.
    - You go into the "Target Group" -> Targets, and see which instances are healthy there.
- ALB action rules:
    1. authenticate-cognito
    2. authenticate-oidc
    3. fixed-response
    4. forward
    5. redirect
- SNI (Server Name Indication) is a feature allowing you to expose multiple SSL certs for different hostnames in one ALB.
- Stickiness:
    1. ALB 
    2. enabled at target group level
    3. has an expiration time
- Cross-Zone Load Balancing
    1. CLB: disabled by default, no charge if enable
    2. ALB: always on, cannot disable, no charge
    3. NLB: disabled by default, get charged if enable

    
