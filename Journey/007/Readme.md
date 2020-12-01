# RDS 

## RDS Security

### RDS Encryption at rest
- If master is not encrypted, the read replicas CANNOT be encrypted.
- Encryption has to be defined at launch time
- TDS available for Oracle and SQL Server - Transparent Data Encryption

### RDS in-flight SSL Encryption
To enforce SSL:
- PostgreSQL: `rds.force_ssl=l` in the RDS Console (Parameter Groups)
- MySQL: Run this SQL on DB: `GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL;`

### RDS Access management
- IAM Policies help control who can **manage** RDS
- Traditional username and password used to login into the db
- IAM-based authentication can be used to login into RDS MySQL & PostgreSQL.

### RDS - IAM Authentication
- Available for **MySQL** & **PostgreSQL**
- Don't need a password, just an **authentication token** obtained through IAM & RDS API calls.
- Auth token lifetime: 15 mins

EC2 instances with the right IAM role can make an API call to RDS Service to get Auth Token; Pass Auth Token to the database will make it log in.

## DB engine features
### MySQL and PostgreSQL
- Ways to reinforce SSL connection 
    - MySQL: run SQL command on DB
    - PostgreSQL: set parameter group `rds.force_ssl` in RDS console
- IAM authentication DB login
- Aurora supported. The two features above applies to Aurora!

### Oracle and SQL Server
- Transparent Data Encryption, another option for encryption at rest.

# Aurora
- Aurora storage automatically grows in increment of 10 GB, up to 64 TB.
- Up to 15 Replicas
- Failover in Aurora is instantaneous
- Natively HA
- Cost 20% more than RDS

## Highly Available

6 copies of your data across 3AZ:
- 4 of 6 copies needed for writes
- 3 of 6 copies needed for reads
- self healing with peer-to-peer replication
- storage is striped across 100s of volumes.

- One Aurora instance takes writes (master)
- Automated failover for master in less than 30 seconds
- Master + up to 15 Aurora Read Replicas serves reads
- Support cross-region replication.

## Endpoints

### One Writer Endpoint
Connected to master instance.

### One Reader Endpoint
- Connection Load Balancing
- Automatically connected to all read replicas
- Load balancing happens at the connection level, not statement level.
- Expose one connection
- Balanced to all the read replicas.

### Good Practice: Use the endpoints to connect to DB
- You can get access to the endpoints of your instances, but you should not use that.
- The good practice is to use the Writer and Reader endpoints.

## Aurora Security
- You cannot SSH
- You are responsible for Security Group


# Aurora Serverless
- Pay per-second
- Good for infrequent, intermittent or unpredictable workloads.

## How it works
- In the backend, there are Aurora instances instantiated by AWS
- There will be a **Proxy Fleet**, managed by Aurora, which the clients can connect to.
- If the request increases, the Proxy Fleet gets connected with more Aurora instances.

# Global Aurora
## Cross-Region Read Replicas
- Up to 15 read replicas
- Can be used for disaster recovery

## Global Database
- 1 Primary region (read/write)
- Up to 5 secondary regions (read-only), read replication lag is < 1 second
- Up to 16 read replicas per secondary region
- Promoting another region (DR) has an RTO of < 1 minute

# ElastiCache
- Managed cache service
- Caches are in-memory databases with high performance
- Reduce load off database for read intensive workloads
- Offers multi-AZ with failover capacity.
- AWS takes care of OS patching, setup, config, monitoring, failure rrecovery, backups

## ElastiCache scalling
- Write scaling using **sharding**
- Read scaling using **read replica**

## Two common use cases

### Load read workload off database
- Application queries ElastiCache, if not available (cache miss), get from RDS and then cache in RDS.
- Cache must have an invalidation strategy to make sure only the most current data is cached.

### Store User session data
- User logs into any of the application instances
- Application writes the session data into ElastiCache
- User hits another instance
- The other instance retrieves the data, and the user is logged in.

## Redis v.s. Memcached
### Redis
- Multi-AZ, Auto-failover
- Read Replica
- Data durability using AOF persistence
- Backup and restore.
- Similar to RDS
- Pub/Sub
- Snapshot
- Redis-AUTH (if you enable encryption in transit)

### Memcached
- Sharding: multi-node for partitioning of data
- Non persistent
- Multi-threaded
- distributed
- no backup and restore
- Pure cache living in memory

## Caching considerations
- Eventually Consistent
- Anti-patterns: data changing rapidly, large key space frequently needed
- Pattern: data changing slowly, few keys are frequently needed.

# Caching patterns
 
## Cache-Aside/Lazy Population/Lazy Loading 
- Pros:
    - Not populating cache with unused data
    - Node failures are not fatal
- Cons:
    - Stale data: data can be updated in DB and outdated in cache
    - Cache miss penalty: 3 round trips, noticeable delay.
    
## Write Through
- Update/Add cache when database is updated

- Pros:
    - Data never stale
    - Reads are quick
    - Write penalty: each write requires 2 calls (call on db + call on cache)
- Cons:
    - Missing data until add/update the DB, might need to combine with lazy loading to handle cache miss.
    - Cache churn: a lot of data might never be read.

## Cache Evictions and Time-to-live (TTL)

- Cache eviction can occur in three ways:
    1. You delete item from cache explicitly
    2. Item is evicted because memory is full and it's not recently used (LRU, least recently used)
    3. You set an item Time-To-Live(TTL)
- TTL are helpful for any kinds of data 
    1. Leaderboards
    2. Comments
    3. Activity stream
- TTL can range from few seconds to hours or days
- Nice option to keep a balance between using cache space wisely and enhancing performance
- If too many evictions happen due to the second reason (memory), you should scale up or out.


