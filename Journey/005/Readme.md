# EBS Volume

- A network drive
- EBS is locked in one AZ.
- You get billed for all provisioned capacity
- To move across AZ, use snapshot.
- GP2: 1GiB - 16Tib. 3 IOPS per GiB, with minimum of 100; burstable to 3000 if you're below 1000Gib. Maximum 16000IOPS (stops increasing when you have 16000/3 GiB)
- IO1: 4GiB - 16TiB. 
    1. IOPS is provisioned
    2. IOPS 100 -> max 64, 000 on Nitro instances; 32,000 on other instances.
    3. Max ratio of provisioned IOPS : GiB = 50:1
    4. Suitable for:
        - Critical business application needing sustained IOPS
        - More than 16,000 IOPS
        - Large DB workload
- ST1 (throughput-optimised HDD)
    1. Streaming workload; low price
    2. Apache Kafka, Big data, data warehouse, log processing
    3. Max IOPS: 500
    4. Max throughput: 500MiB/s
- SCI
    1. infrequent access
    2. max IOPS: 250
    3. max throughput: 250MiB/2
    
## EFS
- You can have SG in front of it to control access
- Only Linux
- Works with EC2 instances in multi-AZ
- User case: Content management, web servng, data sharing, wordpress
- EBS backups use IO and shouldn't be run when handling large production traffic.

### EFS scale
- 1000s of concurrent NFS clients
- 10GB/s throughput
- Grow to PB scale automatically

- Performance mode (set at EFC **creation** time)
    1. General purpose (default): low latency, for web servers, CMS
    2. Max I/O: **higher latency**, good throughput, highly parallel: for big data, media processing.
- Storage tier (with lifecycle management to move files after N days)
    1. Standard: frequently accessed files
    2. IA: cost to retrieve files, lower price to store
    
### EFS is locked within one VPC & EFC mount target
- Specify the VPC where EC2 instances will connect to the file system
- Mount targets provide **NFSv4** endpoints to mount your EFS file system.
- AWS recommends creating one mount target per AZ.
- Each mount point has an AZ, a subnet, a security group.
- Each Mount Target has ONE ENI, with one SG in front of it.

### EFS pricing
- 3* GP2
- Pay for what you use (compared with EBS: pay for what you provision.)


# VPC

- Site-to-site VPN and DX cannot access VPC endpoints (gateway/interface). Endpoints are just for WITHIN the VPC.


