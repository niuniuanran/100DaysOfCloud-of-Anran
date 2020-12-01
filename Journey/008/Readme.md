# Day 8: Route53

## Common Types of Records
- A record: hostname -> IPv4
- AAAA record: hostname -> IPv6
- CNAME record: hostname -> hostname
- Alias: hostname -> AWS Resource

## Route53 can use:
- public domain names you own (or buy)
- private domain names that can be resolved by instances in your VPCs.

## Route53 has advanced features like:
- Load balancing through DNS - client load balancing
- Health checks (though limited)
- Routing policies: simple, geolocation, geoproximity, failover, multivalue, weighted, latency

## Pricing
Not free: $0.50 per month per hosted zone

# DNS Records TTL
- The DNS record will be cached on the client side for the TTL period. 
- TTL is sent together with the response to DNS queries, therefore decided on the DNS server side
- Therefore, an update on the DNS record might not reach the clients immediately. Have to wait for the client's cached records to expire.
- High TTL: e.g. 24 hrs
    1. Less traffic on DNS
    2. Possibly outdated records
- Low TTL: e.g. 60s
    1. More traffic on DNS
    2. Records are outdated for less time
    3. Easy to change records

**TTL is mandatory to each DNS record.**

# CNAME v.s. Alias
Scenario: AWS Resources expose an AWS hostname looking like `lb1-1234-us-west-2.elb.amazonaws.com` and you want `myapp.mydomain.com`.

## CNAME
- points a hostname to another hostmane
- only works for NON-ROOT Domain (works for `myapp.mydomain.com` but not `mydomain.come`)

## Alias
- Points a hostname to an AWS Resource hostname (a hostname looking like `blabla.amazonaws.com`)
- Works for ROOT domain and NON-ROOT domain.
- Free of charge
- Native health check.

## When you are asked whether to use CNAME ane Alias
Generally if you want to point to an AWS resource, Alias is the better choice: free, native health check, more flexible

# Route53 routing policies
- You cannot attach health check to a simple routing policy.
- With simple routing policy, you can return multiple values within one simple routing record, and the client will automatically choose among them - client load balancing.
- You can associate health check to weighted health check.
- Multi-value needs health check, and returns up to 8 healthy records.
# Route 53 Health checks
- Health checks can be routed to Route53 DNS records.

