# Other services
## CloudFormation
- Def: declarative way of outlining AWS infra, showing resources & relations
- -> Deploy & manage infra at scale
- -> CloudFormation create resources with the right order & configuration
- Advs:
  - Infra as code: easy to control & review
  - Cost: review & auto deletion for saving
  - Productivity
  - Work with any resource
- Stack Designer: visualization of resources & relations
## Simple Email Service (SES)
- Def: managed service to send emails securely & globally at scale
- Features:
  - Allow inbound/outbound email
  - Dashboard, insight, feedback, stats
  - Flexible IP deployment
## Pinpoint
- Def: scalable 2 way (outbound/inbound) marketing communication service
- -> Higher level than SNS/SES
- Features:
  - Support email, SMS, push, voice, in-app messaging
  - Segmentation & personalization
  - Events (eg TEXT_SUCCESS, TEXT_DELIVERED) sent to SNS/Firehose/CW Logs
## Systems Manager (SSM)
### Session Manager
- Def: allow creating secure shell on EC2 & on premises servers
- -> No SSH, Bastion hosts, SSH keys, port 22 needed
- Work with most OSs
- Can send logs to S3/CW Logs
### Run Command
- Execute script/command across instances (using resource groups)
- Features:
  - No SSH needed
  - Command output can be shown in Console, sent to S3/CW Logs
  - Send command status noti to SNS
  - Integrated with IAM & CloudTrail
  - Can be invoked via EventBridge
- Need to install SSM Agent
### Patch Manager
- Automate patching managed instances (EC2 & on premises)
- Features:
  - Patch on demand or scheduled
  - Scan instances & generate patch compliance report
- Need to install SSM Agent
### Maintenance Windows
- Define schedule to perform action on instances
### Automation
- Simplify common maintenance & deployment tasks of EC2s & other AWS resources (eg restart, create AMI, EBS snapshot)
- Automation Runbook: SSM Docs to define Automation
- Can be triggered via many services/CLI/SDK
## Cost Explorer
- Def: visualize, understand & manage AWS costs & usage over time
- Features:
  - Create custom reports
  - Analyze total costs & usage across accs
  - Choose optimal Savings Plan (alternative to Reserved Instances)
  - Forecast usage up to 12 months based on previous usage
## Elastic Transcoder
- Convert media files stored in S3 into media files in formats required by consumer playback devices (eg phone)
- Flow: S3 input bucket -> Transcoding Pipeline -> S3 output bucket
## AWS Batch
- Allow run multi-node parallel job (dynamically launch EC2s or Spot Instances)
- Batch jobs defined as Docker images & run on ECS
- Example use case: generate image thumbnails using S3 events
- (Vs Lambda): not serverless, no time limit, rely on EBS/instance storage for disk space
## AppFlow
- Def: managed integration service to securely transfer data between SaaS apps & AWS
- Sources: eg Salesforce
- Destination: eg S3, Redshift
- Features:
  - Can define when to transfer: schedule, events, on demand
  - Data transformation (eg filtering, validation)
  - Encryption
## Resource Access Manager
- Def: share AWS resources with any AWS account or within AWS Org
- Resources:
  - Transit Gateways
  - Subnets (via VPC sharing feature)
  - License Manager configurations
  - Route 53 Resolver rules