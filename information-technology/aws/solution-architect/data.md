# Data
## RDS (relational database service)
- Managed SQL DB (maintained infra, backup, read replica, vertical & horizontal scalability, availability, monitoring)
- -> Can't SSH into underlying EC2 instances
- Offered DB: Postgres, MySQL, MariaDB, Oracle, Microsoft SQL Server, Aurora
- Storage autoscaling:
  - Need to set maximum storage threshold
  - Auto modify storage when:
    - Free storage < 10%
    - Low storage lasted > 5 min
    - 6 hours passed since last modification
- Read replica:
  - Same AZ, cross AZs or cross regions
  - Eventual consistency
  - Need to add replica address to apps
  - Network cost of data replication: only for cross regions
  - Should be created with the same amount of compute and storage resources as the source DB instance
- RDS multi AZs (disaster recovery):
  - Sync replication to standby replica: use one DNS -> automatic failover -> increase availability
  - Can set up read replica as standby replica
  - 0 downtime operation: just need to modify RDS DB attribute
- RDS custom:
  - Def: managed Oracle/Microsoft SQL Server DB with OS & DB customization
  - Can access underlying DB & OS to config, patch, enable native features, access underlying EC2 instances using SSH
  - Need to deactivate automation mode to perform customization, should take snapshot before, for recovery
- Aurora:
  - MySQL/Postgres compatible
  - Cloud optimized: 5x/3x performance over MySQL/Postgres on RDS
  - Up to 15 read replicas, auto-scaled, fast replication compared to MySQL. Also serve as standby for failover.
  - Instantaneous failover
  - Cost ~20% more than RDS
  - High availability & scalability: 6 copies of data across 3 AZs. Self-healing with peer to peer replication.
  - Support cross region replication
  - Clustering:
    - Write endpoint: auto point to the master, even when failover
    - Read endpoint: load balancing to the read replicas
  - Backtrack: restore data at any point in time without backups
  - Advanced features:
    - Custom endpoint: define subset of replica instances as a custom endpoint
    - -> Allow query subset of read replicas (eg to run analytical query)
    - Serverless:
      - Def: automated DB instantiation & autoscaling based on actual usage
      - Use case: infrequent, unpredictable workload
      - Pay per second, can be more cost-effective
      - Mechanism: client connect to proxy fleet (managed Aurora autoscaling instances)
    - Multi-master: allow continuous write availability. Every replica is a writer node.
    - Global Aurora: 2 types:
      - Cross region read replicas
      - Global DB: 1 primary region, up to 5 secondary (read only) regions, less than 1 sec for cross region replication
    - Machine learning:
      - Def: allow adding ML based predictions to app via SQL
      - Mechanism: SQL query -> Aurora connect to ML services -> return result
      - Optimized & secured integration with AWS ML (SakeMaker - any ML model, Comprehend - sentiment analysis)
- Backup:
  - Automated:
    - Daily full backup
    - Transaction log backup every 5 mins
    - 1-35 day of retention. Disabled by setting to 0 day (can't for Aurora).
  - Manual snapshot: can store for any time period
  - -> Can snapshot & restore to save cost, compared to stopped DB (still cost money)
  - Restoration:
    - Create new DB
    - For MySQL RDS/Aurora, can restore from S3 backup into new DB instance
  - Cloning:
    - Created from existing cluster
    - Faster than snapshot & restore: use copy on write mechanism
    - Use case: create staging DB from production DB
- Security:
  - At rest encryption: set at launch time
  - -> To encrypt unencrypted DB, need to: create snapshot -> copy snapshot as encrypted -> restore from snapshot
  - In flight encryption: use AWS TLS cert on client side
  - IAM auth: use IAM roles to connect to DB instead of username & password (supported for MySQL & PostGreSQL)
  - -> Also allow SSL in flight encryption
  - Security group: control network access
  - Audit logs: can be enabled & sent to Cloud Watch for longer retention
- RDS proxy:
  - Def: managed DB proxy for RDS
  - Mechanism: client -> proxy -> RDS instances
  - No code change required
  - Advs:
    - Pool connections to DB
    - -> Reduce load & open connections to actual RDS instances
    - Reduce failover time by 66%
    - Enforce IAM auth to connect to DB. Credentials stored in Secrets Manager.
  - Not publicly accessible
  - Use case: lambda functions
## ElasticCache
- Def: managed Redis/Memcached: maintenance, patching, optimization, setup, configuration, monitoring, backup & recovery
- Require code change
- Use cases:
  - DB cache: need to handle cache hit, cache miss (read DB & write to cache) in code
  - Store user session
- -> Read heavy or compute intensive workload
- Features:
  - Redis:
    - Multi AZ with auto failover
    - Read replicas for scalability & availability
    - Durability using AOS persistence
    - Backup & restore
    - Support set & sorted set
  - Memcached:
    - Multi nodes for sharding
    - No replication -> no high availability
    - Non persistent
    - No backup & restore
    - Multi-thread architecture
- Security:
  - Support IAM auth: use for AWS API level security
  - Redis auth:
    - Set password/token when creating Redis cluster
    - Extra level of security on top of security group
    - Support SSL inflight encryption
  - Memcached: support SASL based auth
- Patterns:
  - Lazy loading: all read data is cached, cache data can be stale
  - Write through: update cache when write
  - Session store
- Use case: Redis sorted set for gaming leaderboards
- Important ports (FTP 21, SSH SFTP 22, HTTP 80 HTTPS 443) vs DB ports (>1k)