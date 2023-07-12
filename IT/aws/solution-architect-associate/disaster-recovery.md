# Disaster recovery
- 3 types:
  - On premises -> on premises: expensive
  - On premises -> cloud: hybrid
  - Cloud region A -> cloud region B
- Recovery Point Objective (RPO) & Recovery Time Objective (RTO): RPO -> disaster (data loss) -> RTO (downtime)
- Strats:
  - Backup & restore:
    - High RPO & high RTO (in hours)
    - Cheap, easy to implement
  - Pilot light:
    - Small version of app always run in the cloud
    - Useful for critical part of system
    - RPO: in minutes
  - Warm standby:
    - Full system up & running but at minimum size
    - Upon disaster, can scale to production load
  - Hot site/multi-site approach: full production scale running on AWS & on premises
- -> Later strats are better (lower RPO & RTO) but costlier
## Database Migration Service (DMS)
- Migrate data between on premises DB & AWS
- Source DB can be available during migration
- Supports:
  - Same tech: Oracle -> Oracle
  - Dif tech: Microsoft SQL -> Aurora
- Support continuous data replication using change data capture (CDC)
- Must create EC2 to perform replication tasks
- Sources: most SQL DBs & AWS SQL DBs, S3, DocumentDB
- Targets: most SQL DBs & AWS SQL DBs, Kafka, Redis, Babelfish, Redshift, DynamoDB, S3, OpenSearch, Kinesis Data Streams, DocumentDB, Neptune
- Schema Conversion Tool (SCT): convert schema from one engine to another
- Multi AZ deployment: DMS provisions & maintains sync standby replica in a dif AZ
## Migration cases
- RDS -> Aurora MySQL migration options:
  - Restore DB snapshot: need to stop DB
  - Create Aurora Read Replica from RDS. Promote when replication lag is 0.
  - -> Take time & network cost
  - DMS for continuous migration
- External MySQL to Aurora MySQL migration options:
  - Use Percona XtraBackup to create backup file in S3 -> create Aurora DB from S3
  - Create Aurora DB, use mysqldump utility to migrate (slower than first option)
  - DMS for continuous migration
## On premise strategy
- Can download Amazon Linux 2 AMI as a VM (.iso) to run on premises
- VM import/export
- AWS Application Discovery Service
- (eg server utilization data, dependency mapping)
- DMS: replicate on-premise <-> AWS
- Server Migration Service: incremental replication of on-premise live servers to AWS
## AWS Backup
- Managed service, to manage & automate backups centrally across AWS
- Supported services: EC2/EBS, S3, RDS, DocumentDB, Neptune, EFS, FSx (Lustre & Windows FS), Storage Gateway (Volume)
- Features:
  - Cross region/acc backups
  - PITR
  - On-demand & scheduled backup
  - Tag-based backup policies
- Backup Plans: user created backup policies
- Vault Lock: enforce WORM state for the backups to prevent accidental deletes (including root user)
## Application Discovery Service
- Function: gather info about on-premise servers to plan for migration
- 2 types:
  - Agentless discovery (Agentless Discovery Connector)
  - Agent-based Discovery (Application Discovery Agent): more info
- Resulting data can be viewed within Migration Hub
- Application Migration Service: lift and shift solution simplifying migration to AWS
- -> Minimal downtime, reduce costs
## Transferring large dataset
- Over the Internet/Site to site VPN: quick setup, high transfer period
- Over Direct Connect: slow setup, quick transfer
- Over Snowball: might need several Snowballs, faster, can be combined with DMS
- Ongoing replication/transfers:
  - Site to site VPN
  - DX with DMS/DataSync
## VMware Cloud on AWS
- VMware Cloud: app to manage on-premise data center
- -> VMware Cloud on AWS: extend capacity to data center managing to AWS