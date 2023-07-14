# Notes
- Services involved dev effort: Lambda, Glue
- Services not involved dev effort: DMS
- Request throttling: API gateway
- Request buffering: SQS, Kinesis
- CloudFront can't have a custom origin pointing to the DNS record of the website on Route 53
- Route 53 geolocation routing can be used to restrict distribution of content to specific locations
- Global Accelerator works for both non HTTP (TCP/UDP) & HTTP use cases
- Lustre (vs EMR): suitable for high performance computing, also integrated with S3 for cold storage
- Rollout new software version gradually:
  - Globally: can use GA
  - Regional: can use ELB
- Scale out ECS services: use service metric, not CW alarm
- Use AWS CloudFormation StackSets to deploy the same template across accs/regions
- NLB routing: when specifying targets using an instance ID,
traffic is routed to instances using the primary private IP address specified in the primary network interface for the instance
- CloudFront field level encryption (secured during transfer): encryption using public key at CloudFront -> decrypt at app
## S3
- S3 versioning: after enabled, can only be suspended, not disabled
- To transition objects from Standard to IA, min storage duration is 30 days
- S3 unsupported lifecycle transitions:
  - Any -> Standard
  - Any -> Reduced Redundancy
  - Intelligent Tiering -> Standard IA
  - One-zone IA -> Standard IA/Intelligent Tiering
- S3 Transfer Acceleration cost: only for the transfers accelerated
- S3 objects are owned by the AWS account that uploaded it
- -> Even S3 bucket owner (dif acc) will not implicitly have access to the objects
- Improve performance:
  - For object > 1GB: use Transfer Acceleration
  - For object < 1GB: use CloudFront
- Strong consistency model for read-after-write when the write is successful
## ASG
- Putting instance in Standby state for maintenance prevents ASG from creating another replacing instance
- Launch configuration (deprecated):
  - Can't specify multiple instance types (eg on-demand & spot)
  - Can't be modified: need to create new launch config & point ASG to that
- -> Use launch template instead
- Potential causes of unhealthy instance not terminated:
  - Instance in Impaired status
  - Health check grace period not expired
  - Instance failed ELB health check where ASG use EC2 type of health check
- Termination precedence: oldest launch configuration -> oldest launch template -> closest to billing hour
- Rebalancing when AZ is unbalanced. Steps:
  - Launch new instances
  - Terminate the old instances
- -> App's performance/availability not affected
- Terminating unhealthy instance steps:
  - Create a new scaling activity for terminating the unhealthy instance
  - Create another scaling activity to launch a new instance to replace the terminated instance
## Data
- Aurora failover: select replica with the highest priority (lowest tier) with the largest size
- Multi AZ option is only available for RDS. Aurora has use read replica as standby instance (async replication).
- Snapshot in S3: managed by RDS -> can't access directly
- To recover DynamoDB to previous state, should use PITR instead of DynamoDB Stream (no code required)
- DocumentDB (vs DynamoDB): no in-memory caching layer
- Global Aurora failover (vs Global DynamoDB tables): cheaper
- -> DynamoDB Global tables have no concept of failover (active-active replication)
- DynamoDB is not in-memory DB (only have in-memory caching layer with DAX)
- RDS standby: can't serve read/write requests -> can't be used as read replica
- RDS OS update steps:
  - Perform maintenance on the standby
  - Promote the standby to primary
  - Perform maintenance on the old primary, which becomes the new standby
- Database engine level upgrade for an RDS DB instance with Multi-AZ deployment:
triggers both the primary and standby DB instances to be upgraded at the same time
- -> Cause downtime until the upgrade is complete
## Messaging
- Kinesis Data Analytics: realtime
- DynamoDB is not a target of Firehose (only S3)
- Firehose: producers can be any. Also allow processing (via Lambda).
- Kinesis Agent cannot write to a Firehose for which the delivery stream source is already set as Kinesis Data Streams
## Security
- Shield handles DDoS, not traffic spike
- GuardDuty: disable service to delete all findings & configs
- Delete KMS keys: change to Pending deletion state (configurable, 7-30 days). Can cancel to restore the keys.
- Cognito authentication: only via User Pools. Identity Pools is only a mechanism to obtain credential.
- Single region KMS keys can't be changed into multi-region keys
- -> Must create new keys
## Networking
- Shared services VPC: use with Transit Gateway to reduce administrative overhead & cost
- Transit virtual interface (transit VIF): used to access one or more Transit Gateways associated with DX gateways
- DNS hostnames and DNS resolution are required settings for private hosted zones
- Use AZ ID to uniquely identify the AZ across accs