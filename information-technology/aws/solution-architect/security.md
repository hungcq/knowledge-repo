# Security

## Encryption overview
- In flight (SSL):
  - Def: data encrypted before sending & decrypted after receiving
  - Prevent man in the middle attack
- Server side encryption at rest:
  - Data stored encrypted by server, decrypted before being sent
  - Encryption keys must be managed & server must have access to keys
- Client side:
  - Data encrypted by client, decrypted by receiving client. Server can't decrypt data.
  - Could leverage Envelop Encryption

## KMS
- Manage encryption keys
- SDK/CLI available to access key, encrypt/decrypt
- Fully integrated with IAM for authorization, integrated with most AWS services
- Secret best practice:
  - Never store in plaintext, esp in code
  - Encrypted secret can be stored in code/env vars
- Cryptographic keys types:
  - Symmetric (AES-256 keys):
    - Used for both encryption/decryption
    - For AWS services
    - Can't access key, must call KMS for encryption/decryption
  - Asymmetric (RSA & ECC key pairs):
    - Public (publicly downloadable) & private key pair
    - Used for encrypt/decrypt or sign/verify operations
    - Use case: encryption outside AWS by users without KMS API access
- Keys types:
  - AWS owned keys:
    - Free, shared with other accs: eg SSE-S3, SSE-SQS, SSE-DDB (default key)
    - Key rotation: handle by AWS
  - KMS Keys (ex KMS Customer Master Key) types:
    - AWS managed key:
      - Created only for user's account. User can view metadata.
      - Pricing: no monthly fee, only usage fee (depending on service)
      - Key rotation: default, every 1 year
      - Eg aws/rds, aws/ebs
    - Customer managed keys (CMK):
      - Created in KMS
      - Pricing: 1$/month + usage fee (API calls)
      - Key rotation: must be enabled, every 1 year
- Key material origin:
  - AWS_KMS: managed by AWS, default
  - EXTERNAL:
    - Imported key
    - Managed by users: security, availability, durability, rotation
    - Support both symmetric & asymmetric keys
  - AWS_CLOUDHSM:
    - KMS creates the key in a custom key store (CloudHSM cluster)
    - Encrypt/decrypt done in the cluster
- API call cost: 0.03$/10000 calls
- Key scope: per region
- Key policies:
  - Control access to KMS keys
  - Required to access keys
  - 2 types:
    - Default key policy: root user has complete access to the key
    - Custom: define users, roles that can access/administer the key
    - -> Useful for cross account access
- Multi-region Keys:
  - Same key replicated across regions (not global). Each key managed independently.
  - -> Can encrypt in 1 region & decrypt in another
  - Use cases:
    - Global client side encryption
    - Global DynamoDB/Aurora encryption:
      - DynamoDB: can encrypt specific attributes at client-side using DynamoDB Encryption Client (calling KMS to encrypt/decrypt)
      - Aurora: encrypt specific attributes at client side using Encryption SDK
    - -> Protect fields from DB admins

## S3 replication encryption considerations
- Unencrypted objects & objects encrypted with SSE-S3 are replicated by default
- Object encrypted with SSE-C (customer-provided key) are not replicated
- Objects encrypted with SSE-KMS, need to enable replication
- Can use multi region keys: treated independently - objects still decrypted & encrypted using the same key

## Encrypted AMI sharing process
- Modify image attribute: add Launch Permission for target account
- Share KMS key with target account
- IAM user/role in target account must have proper permissions
- Launch EC2 instance from target account (can encrypt with dif key)

## SSM Parameter Store
- Def: secure storage for config & secrets
- Features:
  - Optional seamless encryption using KMS
  - Config/secret versioning
  - IAM security
  - EventBridge noti
  - CloudFormation integration
- Hierarchy structure
- Param Policies (for advance parameters option):
  - Allow assigning TTL to a param to force update/delete of sensitive data. Can noti via EventBridge.
  - Can assign multiple policies at a time

## Secret Manager
- Def: new service to store secrets
- Features:
  - Force rotation of secrets every x days
  - Integration with RDS
- Multi region secrets: replicate secrets across multiple regions
- -> Availability, allow multi region app/DB

## Certificate Manager (ACM)
- Provision, manage, deploy TLS certs
- Integrations (load TLS certs on):
  - ELB: HTTP -> HTTPS redirection
  - CloudFront Distributions
  - API Gateway APIs. Process:
    - Create Custom Domain Name in API Gateway
    - For:
      - Edge-optimized Gateway (in 1 region): TLS cert must be in same region as CloudFront (us-east-1)
      - Regional Gateway: TLS cert must be in same region as API Stage
- -> Not work on EC2
- Request public certs process:
  - List domain names
  - Select validation method: DNS/email
  - Cert registered for auto-renewal
- Import outside public certs:
  - No auto renewal
  - Noti of expiration via:
    - ACM -> EventBridge: daily expiration event (daily, starting 45 days prior to expiration)
    - AWS Config: check with ACM -> EventBridge

## Web App Firewall (WAF)
- Protect web apps from common web exploits (layer 7 - HTTP)
- Deploy on:
  - ALB
  - API Gateway
  - CloudFront
  - AppSync GraphQL API
  - Cognito User Pool
- Usage: define Web ACL rules:
  - IP Set: up to 10k IP addresses
  - HTTP headers, body, URI strings Protects from common attack (eg SQL injection & XXS)
  - Req size constraints
  - Geo-match (block countries)
  - Rate-based rules: DDoS protection
- Regional except for CloudFront
- Rule Group: reusable set of rules that can be added to a web ACL
- Architecture: fixed IP: WAF not support NLB so must use GA for fixed IP:
client -> Global Accelerator -> ALB + WAF -> EC2 instances

## Shield
- Def: DDoS protection service
- 2 types:
  - Shield Standard: free, activate for all AWS customers
  - Shield Advanced: optional DDoS mitigation service, protect against more sophisticated attack on EC2, ELB, CloudFront, GA, Route53

## Firewall Manager
- Def: service managing rules in all accounts of Org (eg WAF rules, security groups, network firewall)
- Rules applied to new resources as they are created across all & future accs in Org

## GuardDuty
- Def: intelligent thread discovery to protect AWS account
- Use ML, anomaly detection, third party data
- Input data:
  - CloudTrail Event Logs:
    - Management Events
    - S3 Data Events
  - VPC Flow Logs
  - DNS Logs
  - Optional Features: eg EKS Audit Logs, RDS & Aurora
- Can setup EventBridge rules for noti
- Can protect against CryptoCurrency attacks (has dedicated finding for it)

## Inspector
- Def: automated security assessment
- Target:
  - EC2 instances: use System Manager agent to analyze:
    - Unintended network accessibility
    - Known vulnerabilities of running OS
  - Container images pushed to ECR
  - Lambda
- Reporting & integration with Security Hub/EventBridge

## Macie
- Def: managed data security & privacy service using ML & pattern matching to discover & protect sensitive data in AWS
- -> Identify & alert to sensitive data (eg personally identifiable info)
- Noti via EventBridge