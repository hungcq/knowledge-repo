# Networking - VPC
## Classless inter-domain routing (CIDR)
- Def: method for allocating IP addresses
- Used in security group rules & AWS networking in general
- 2 components:
  - Base IP: represent IP contained in range xx.xx.xx.xx
  - Subnet mask: define how many bits can't change in the IP (eg /32 allows 1 IP, /24 allows 256 IPs, /0 allows all IPs)
## Private vs public IP
- Private IP: possible values:
  - 10.0.0.0 -> 10.255.255.255 (10.0.0.0/8): big network
  - 172.16.0.0 -> 172.31.255.255 (172.16.0.0/12): AWS default VPC
  - 192.168.0.0 -> 192.168.255.255 (192.168.0.0/16): eg home networks
- -> Others are public IPs
## Default VPC
- Virtual private cloud (VPC) def: a secure, isolated private cloud hosted within a public cloud
- All new AWS accs have a default VPC
- New EC2 instances are launched into the default VPC if no subnet is specified
- Has Internet connectivity & all EC2 instances inside have public IPv4 addresses, public & private IPv4 DNS names
- Limit in AWS:
  - Max 5 per region
  - Max 5 CIDR per VPC
  - CIDR:
    - Max size /16, min size /28
    - Only private IPs allowed
    - Should not overlap with user's other VPC/networks (eg corporate)
## Subnet
- Def: sub range in IPv4 within VPC
- AWS reserves 5 IPs (first 4 & last 1) in each subnet:
  - First: network addr
  - Second: VPC router
  - Third: mapping to Amazon provided DNS
  - Fourth: future use
  - Last: network broadcast addr (reserved since broadcast not supported)
## Internet Gateway (IGW)
- Allow resources (eg EC2) in a VPC to connect to the Internet
- VPC-IGW mapping: 1-1
- Must also edit routes table to allow Internet access
- Egress-only IGW:
  - ~NAT Gateway, used only for IPv6
  - Must update Route Tables
## Bastion host
- Def: EC2 instance in public subnet which is connected to all other private subnets
- -> Used to SSH to private EC2 instances
- Network config:
  - Bastion host security group must allow inbound from the Internet on port 22 from restricted CIDR (eg public CIDR of user's corp)
  - Private EC2 instances security group must allow security group/private IP of Bastion Host
## NAT instance (outdated)
- EC2 in public subnet that allows EC2s in private subnets to connect to the Internet
- Must disable EC2 setting: source/destination check
- Must have Elastic IP attached & route table of private EC2 configured
- Traffic flow: private EC2 -> NAT instance -> Internet
- Lots of manual config/setup needed
- Adv: can be used as Bastion Host
## NAT Gateway
- Function: allow EC2s in private subnets to connect to the Internet
- Managed NAT, no security group required, better than NAT instance
- Pay per hour for usage & bandwidth
- Created in a specific AZ, use Elastic IP
- Can only be used by EC2s in dif subnet
- Require IGW
- Data flow: private subnet -> NAT gateway -> IGW
- Availability:
  - Resilient within single AZ
  - Must create a NAT gateways in each AZ for fault tolerance
## Network ACL (NACL)
- Define inbound/outbound rules for subnet
- 1 per subnet. New subnets are assigned the default NACL.
- Rules:
  - Numbered from 1 -> 32766, lower number higher precedence
  - First rule match drive decisions
  - No rule match = not allowed
  - Inbound/outbound rules are stateless
  (vs stateful inbound/outbound rules of security groups - response of accepted reqs are auto accepted)
  - Allow Deny rules
- -> Used to block IPs at subnet level
- Default NACL: accept everything
- Ephemeral port: client connects to defined port, expect a res from an ephemeral port (sent in req - Source Port)
- -> Must config outbound rules of BE & inbound rules of subnet to allow ephemeral ports
## VPC Peering
- Privately connect 2 VPCs (no overlapping CIDR) using AWS network
- -> 2 VPCs behave as if in the same network
- Not transitive: VPC A -> VPC B -> VPC C, no A -> C
- Must update route tables in each VPC subnets to allow EC2s to communicate with each other
- Can work cross-acc/regions
- Can reference a security group in a peered VPC (work cross accs, same region)
## VPC Endpoints
- All AWS services are publicly exposed
- VPC Endpoints (using AWS PrivateLink) allow connecting VPC to AWS services using private network instead of public Internet
- -> Don't have to use IGW, NATGW to access AWS services
- 2 types:
  - Interface (using PrivateLink):
    - Provision an ENI (private IP) as an entry point (must attach a security group)
    - Supports most AWS services
    - Pay per hour + per GB data processed
  - Gateway:
    - Provision a gateway & must be used as a target in a route table (not using security groups)
    - Support S3 & DynamoDB
    - Free
  - -> Preferred way to access S3 most of the time
## VPC Flow Logs
- Functions:
  - Capture info about IP traffic going to interfaces:
    - VPC Flow Logs
    - Subnet Flow Logs
    - ENI Flow Logs
  - Capture network info from AWS managed interfaces: eg ELB, RDS, ElastiCache, NATGW
- -> Help monitor & troubleshoot connectivity issues
- Flow logs data can go to S3, CW Logs, Firehose
- Log info:
  - srcaddr & dstaddr
  - srcport & dstport
  - Action: ACCEPT/REJECT
- Can query flow logs using Athena on S3 or CW Log Insights
- Troubleshoot security group (SG) & NACL issues:
  - Internet -> VPC req:
    - Inbound REJECT: NACL/SG issue
    - Inbound ACCEPT, outbound REJECT -> NACL (stateless)
  - VPC -> Internet req:
    - Outbound REJECT: NACL/SG issue
    - Outbound ACCEPT, inbound REJECT -> NACL
## Site to site VPN
- Goal: connect VPC to corp data center using private connection
- Flow: EC2s in VPC -> VPN Gateway -> Site to site VPN connection -> Customer Gateway -> Corp data center
- Components:
  - Virtual private gateway (VPN gateway - VGW): on AWS side, attached to VPC
  - Customer gateway (CGW): software/physical device on customer side
- -> Connect using Site to site VPN
- Customer gateway device (on premises): use IP of:
  - Public Internet routable IP address for customer gateway device
  - If behind a NAT device enabled for NAT traversal, use public IP of the NAT device
- Must enable Route Propagation for VGW in the route table associated with subnets
- To ping EC2 instances from on-premises, add ICMP protocol on inbound rules of security groups
- VPN CloudHub:
  - Provide secure communication between multiple sites when user have multiple VPN connections
  - VPN connection -> traffic go over public internet
  - Setup: connect multiple VPN connections on the same VGW, setup dynamic routing & config route tables
## Direct Connect (DX)
- Provide dedicated private connection from a remote network to VPC
- Dedicated connection must be setup between user's DC & Direct Connect locations
- Need to setup VGW on VPC
- Can access both public & private resource
- Use cases:
  - Increase bandwidth, lower cost
  - Stable network (eg realtime app)
  - Hybrid env (on premises + cloud)
- To setup Direct Connect to 1+ VPC in dif regions (same acc), must use a Direct Connect Gateway
- Connection types:
  - Dedicated: physical ethernet port dedicated to a customer
  - Hosted:
    - Connection requests made via Direct Connect Partners
    - Capacity can be added/removed on demand
- Setup time usually longer than 1 month
- Data in transit is not encrypted
- -> Must use with VPN to provide IPsec-encrypted private connection
- Resiliency:
  - High resiliency: 1 connection/location
  - Maximum resiliency: 2+ connections/location
- Can use Site to site VPN as backup connection for lower cost
## Transit Gateway
- Function: transitive peering between thousands of VPC & on premises, star connection schema
- The only service supporting IP Multicast
- Equal cost multi path routing (ECMP): routing strat to forward a packet over multiple best path
- -> Use case: create multiple Site to site VPN connections to increase bandwidth of connection to AWS
- Can use Resource Access Manager to share Transit Gateway with other accs
## VPC Traffic Mirroring
- Allow capturing & inspecting network traffic in VPC by routing traffic to customer's managed security appliances
- Info captured:
  - From (Source) - ENIs
  - To (Targets): ENI/NLB
- -> Source & Target can be in the same or in dif VPCs (VPC Peering)
- Can select packets to capture
## IPv6 for VPC
- Cannot disable IPv4 for VPC/subnet
- Can enable IPv6
- EC2 instances get at least a private internal IPv4 & a public IPv6
- -> Can communicate with the Internet using either IPv4/IPv6 through Internet Gateway
- Troubleshooting: when can't launch EC2 in subnet -> out of IPv4 -> need to create new IPv4 CIDR
## ClassicLink
- Connect EC2-Classic EC2 privately into VPC
## Networking Costs
- Traffic in EC2: free
- EC2 in same AZ, communicate using private IP: free
- EC2 in dif AZs same region, communicate using
  - Private IP: 0.01/GB
  - Public IP/elastic IP: 0.02/GB
- Inter region: 0.02/GB
- Egress traffic: outbound traffic (AWS -> outside)
- Ingress traffic: inbound traffic: typically free
- Direct Connect location co-located in the same AWS region result in lower egress network cost
- Best practice:
  - Use private IP for cost saving & better network performance
  - Use same AZ for max saving at cost of high availability
  - Keep traffic within AWS: minimize egress
- S3:
  - Egress cost
  - Transfer Acceleration: faster transfer, additional cost
  - To CloudFront: free. CloudFront to Internet: cheaper than S3
  - Cross Region Replication: cost
- VPC Endpoint (vs NAT Gateway) to access S3: much cheaper since traffic go in private network
## Network Firewall
- Network protection summary:
  - NACL
  - Security groups
  - WAF
  - Shield
  - Firewall Manager (cross acc)
- Network Firewall: protect the entire VPC:
  - Layer 3 -> 7, all types of traffic
  - Traffic filtering: allow, drop, alert for traffic that matches the rules
  - Active flow inspection: protect against network threats with intrusion prevention capabilities
  - Send logs to S3, CW Logs, Firehose