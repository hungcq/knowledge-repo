# Monitoring & metrics

## CloudWatch
- Provide metrics for all services in AWS
- Metric:
  - Def: variable to monitor
  - Belong to namespaces
  - Have timestamps
- Dimension: attribute of a metric. Max 30 dimensions/metric.
- Features:
  - Can create dashboards of metrics
  - Can create custom metrics
- Metric Stream:
  - Continually stream CloudWatch metrics to a destination of choice (Firehose, third party service)
  - Near realtime delivery & low latency

### Logs
- Store app logs
- Log groups: usually representing an app
- Log stream: instances within app or log files or containers
- Can define log expiration policies
- CloudWatch Logs can send logs to:
  - S3 (export):
    - Up to 12 hours delay -> use Logs Subscription for realtime
    - API: CreateExportTask
  - Kinesis Data Streams (KDS)
  - Firehose
  - Lambda
  - OpenSearch
- Encrypted by default (can setup KMS based encryption)
- Send via: SDK, CW Logs Agent, CW Unified Agent
- Sources:
  - Beanstalk: collect from apps
  - ECS: collect from containers
  - Lambda: function logs
  - API Gateway
  - VPC Flow Logs: VPC specific logs
  - Route53: DNS queries
  - CloudTrail based on filter
- Logs Insights: search & analyze CW logs
- Logs Subscriptions:
  - Provide realtime log events from CW Logs for processing & analysis
  - Destinations: KDS, Firehose, Lambda
  - Subscription Filter: filter logs to deliver to destination
  - Logs Aggregation: from dif accounts & regions into KDS
  - Cross-acc Subscription: send log events to resources in a dif AWS account (need proper permissions)

## Agent & Logs Agent
- Need to run agent (with proper permission) on EC2 to push log files
- Can be setup on premises
- Logs Agent: old version, can only send to CW Logs
- Unified Agent:
  - Collect additional system level metrics
  - Collect logs & send to CW logs
  - Centralized config using SSM param store
  - Metrics:
    - CPU
    - Disk
    - RAM
    - Netstat (eg TCP, UDP connections)
    - Processes
    - Swap space

## Alarms
- Can trigger notis for any metric
- States:
  - OK
  - INSUFFICIENT_DATA
  - ALARM
- Targets:
  - EC2: stop/terminate/reboot/recover EC2 instance
  - ASG: trigger autoscaling action
  - SNS: send noti
- Composite Alarms: monitor states of multiple other alarms (AND/OR conditions)
- -> Reduce noise
- EC2 instance recovery: triggered by StatusCheckFailed_System alarm. Can alert SNS topic. Can't recover terminated instance.
- -> Recovery: same instance ID, private/public/elastic IP, metadata, placement group
- Can be created based on CW Logs Metrics Filter

## EventBridge (ex CW Events)
- Functions:
  - Schedule cron jobs
  - React to events
  - Trigger Lambda/send SNS
- Features:
  - Allow advanced filtering options with JSON rules
  - Allow multiple destinations
  - Other features: archive, event relay, reliable delivery
- Flow: source -> event filter -> EventBridge: create JSON event -> destination
- Event Bus:
  - Can send to Default/Partner/Custom Event Bus
  - Can be accessed by other AWS accounts via policies
  - Can archive & replay events
- Schema Registry:
  - Event Bridge analyze events in the bus & infer the schema
  - Schema Registry can gen code for app, knowing in advance how data is structured in event bus
  - Schema can be versioned
- Resource-based policy:
  - Manage permissions for a specific Event Bus (eg allow/deny events from other AWS accounts/regions)
  - Use case: aggregate all Org events in a single AWS account/region
- Can be used in event-based app. Use case: the only service integrated with SaaS partners.

## Insights & Operational Visibility
- Container Insights:
  - Collect, aggregate, summarize metrics & logs from containers
  - Supported containers:
    - ECS
    - EKS
    - Kubernetes on EC2
    - Fargate (both ECS & EKS)
  - -> Use containerized version of CW Agent to discover containers in EKS & Kubernetes
- Lambda Insights (provided as Lambda Layer): collect, aggregate & summarize system level metrics
- -> Monitor & troubleshoot serverless app on Lambda
- Contributor Insights:
  - Analyze log data & create time series displaying contributor data (eg VPC, DNS)
  - Create metrics about top N contributors (eg top heaviest network users, URLs generating most errors)
  - Can build or use example rules using CW Logs
- App Insights: provide automatic dashboards showing potential problems with monitored apps/related AWS services
- -> Isolate ongoing issues

## CloudTrail
- Provide governance, compliance & audit for user's AWS account: history of events/API calls made within AWS account
- -> Who do what
- Sources: console, CLI, SDK, IAM users/roles
- Enabled by default
- Targets: can export to CW Logs/S3
- A trail can be applied to all regions (default) or 1 region
- Event types:
  - Management:
    - Def: operations performed on resources in AWS account (eg config security, routing rules, logging)
    - Enabled by default
    - 2 types: read & write events
  - Data:
    - Disabled by default
    - Eg: S3 object level activity, Lambda execution activity
  - Insights:
    - Detect unusual activity
    - Analyze normal events to create baseline, then continuously analyze write events to detect unusual patterns
    - Flow: management events -> CloudTrail Insights -> Insight Events -> Cloud Trail console/S3 bucket/EventBridge
- Event retention: 90 days
- -> Need to log to S3 for longer retention, analyze using Athena
- Organizational Trail:
  - Created in management account
  - Logs to S3 bucket by member account ID

## Config
- Audit & record compliance of AWS resources
- Record configs & changes over time (eg public access to S3, unrestricted SSH access to EC2)
- -> Can trigger SNS noti alert for changes
- Per region service, can agg across regions/accounts
- Can store config data in S3 & analyze using Athena
- Rules:
  - Rule types:
    - AWS managed config rules
    - Custom config rules
  - Can be evaluated/triggered for each config change or at intervals
  - Does not prevent actions from happening
  - Remediation: auto remediate non-compliant resources using SSM Automation Documents
  - -> Can set Retries if resource is still non-compliant after remediation
  - Noti: trigger EventBridge/SNS when resources are non-compliant
- Config Resource: view config/compliance/CloudTrail API calls of a resource over time