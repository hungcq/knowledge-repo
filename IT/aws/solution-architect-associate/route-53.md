# Route 53
## DNS
- Hostname -> IP address
- Hierarchical structure (right to left)
- Domain registrar (vs DNS service provider). Usually also provide DNS service.
- DNS record
- Zone file: contain DNS records
- Name server: resolve DNS queries
- Top level domain (eg com, org), second level domain. Local DNS server get addresses from each domain level DNS server.
- -> Cache IP in local web browser & local DNS server
## Route 53
- Functions:
  - Highly available, scalable, fully managed authoritative DNS (customer can update DNS records)
  - Domain registrar
- Features:
  - Resource health check
  - 100% availability SLA
- Record: how to route traffic for a domain. Attributes:
  - Domain, subdomain name
  - Record types:
    - A: hostname -> IPv4
    - AAAA: hostname -> IPv6
    - CNAME: hostname -> A/AAAA hostname. Can't create for top node of DNS space (eg example.com. www.example.com can)
    - NS: IPs of name servers for hosted zone -> control how traffic is routed for a domain
    - Others
  - Value: IP
  - Routing policy
  - TTL: cache time at DNS resolvers
- Hosted zone:
  - Def: container for records defining how to route traffic to a domain & its subdomains
  - Types:
    - Public: Internet record
    - Private: how to route traffic within/cross VPCs (private domain name)
- Alias:
  - Point hostname to AWS resource
  - Work for root domain (vs CNAME record)
  - Free
  - Native health check
  - Always of type A/AAAA for AWS resources
  - Auto recognize change in IP
  - Targets: eg ALB, Cloud Front distributions, API gateway, Beanstalk, S3. Not work for EC2 DNS name.
- Routing policy: how to respond to DNS queries. Types:
  - Simple: one AWS resource (alias)/IP/multi IPs (client chooses a random one), no health check
  - Weighted: control % of request go to each specific resource, have health check
  - -> Allow LB, traffic routing (eg failover, new version testing)
  - Failover: based on health check. Define primary & secondary records.
  - Latency based: based on traffic between users & AWS regions
  - Geolocation:
    - Based on user location
    - Use cases: web localization, content restriction, LB
    - Should have default record when there is no matching location
    - Can associate with health check
  - Multi-value answer:
    - Route to multiple resources
    - Associate with health check -> only return healthy resources (vs simple routing - might include unhealthy resources)
  - -> Not a substitute for ALB
  - Geo proximity (using Route 53 traffic flow feature):
    - Bias def: ability to move traffic to resources. Positive/negative: increase/decrease size of the geographic region.
    - Resource types:
      - AWS resource
      - Non AWS resource (latitude & longitude)
    - Usage: shift more traffic to a specific region
  - IP based:
    - Based on client IP
    - Define list of CIDRs for client (eg 1.2.3.0 cover all 1.2.3.x). Mapping IP to endpoint.
    - Use case: route users from an ISP to specific endpoint
- Health check:
  - HTTP health check only works for public resources
  - Automated DNS failover. Monitor:
    - Endpoint (eg AWS resource):
      - ~15 global health checkers in dif regions will check the endpoint health
      - Healthy if >18% health checkers report healthy
      - Status code: 2xx/3xx
      - Can customize to check first 5120 bytes of response
      - Need to config router/firewall to allow health checkers
    - Other health checks (calculated health check):
      - Combine using AND/OR/NOT
      - Max 256 child health checkers
      - Can specify num of child health checks to pass
    - Cloud Watch alarms:
      - Useful for private resource because route 53 health checkers are outside VPC
      - Create CW metric & CW alarm -> associate health check with the alarm
  - Integrated with Cloud Watch metric
- Use as DNS service provider:
  - Create hosted zone in Route 53
  - Update NS record on 3rd party domain registrar to use Route 53 name servers