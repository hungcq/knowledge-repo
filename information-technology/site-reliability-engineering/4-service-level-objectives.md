## 4. Service level objectives
- Goal of having SLO: to understand:
  - Which behaviors really matter for that service
  - How to measure & evaluate those behaviors
### Service level indicator (SLI)
- Def: a carefully defined quantitative measurement of some aspect of the level of service provided
- Examples:
  - Request latency
  - Error rate
  - System throughput (eg QPS)
  - Availability
  - Durability
- Might need proxy SLI if can't obtain the desired measure
- Considerations when choosing SLI:
  - Usually a handful are enough to evaluate & reason about a system's health
  - Relevant SLIs by service categories:
    - User-facing systems: availability, latency, throughput
    - Storage systems: latency, availability, durability
    - Big data systems: throughput & end to end latency
  - Correctness:
    - Imp for all types of systems
    - Often a property of the data in the system rather than the infra per se
    - -> Usually not an SRE responsibility to meet
- Collection:
  - Usually on server side:
    - Monitoring system (eg Prometheus)
    - Periodic log analysis
  - On client side for some problems hard to measure on server side
- Aggregation:
  - Average
  - Distribution: better to identify anomaly
- Standardization: to save effort, build a set of reusable SLI templates for each common metric
### Service level objective (SLO)
- Def: a target value or range of values for a service level that is measured by an SLI
- Types:
  - SLI `<=` target
  - Lower bound `<=` SLI `<=` upper bound
- Focus on what users care about, not what you can measure
- Should work from desired objectives backward to specific indicators
- Definition:
  - Should specify:
    - How to measure
    - The condition under which it is valid
  - Example: 99% (average over 1 minute) of Get RPC calls will complete in less than 100 ms (measured across all BE servers)
  - Process: track SLOs & SLO violations on a daily or weekly basis
  - -> See trend & get early warning of potential problems before they happen
- Choose targets:
  - Require product & business involvement
  - SRE should advise on the risks & viability of dif options
  - Best practices:
    - Keep it simple: avoid complicated aggregations in SLIs
    - Avoid absolutes (eg infinite scalability & always available)
    - -> Choose realistic goal that meet users' need
    - Have as few SLOs as possible
    - Perfection can wait: can refine SLO defs & targets after learning about system's behaviors
- Control loops used to manage systems:
  - Monitor & measure the system's SLIs
  - Compare the SLIs to the SLOs, and decide whether or not action is needed
  - If action is needed, figure out what needs to happen in order to meet the target
  - Take that action
- Publishing SLOs:
  - Set expectations for system behavior
  - How to set realistic expectations for users:
    - Keep a safety margin. Advs:
      - Have time to respond to issues before users are impacted
      - Flexibility for internal adjustment
    - Don't overachieve: using planned outage/request throttling/other strats to force users not to depend on not promised beha
### Service level agreement (SLA)
- Def: an explicit or implicit contract with your users that includes consequences of meeting or missing the SLOs they contain
- Characteristic: have consequence for not meeting it
- Process of defining SLAs:
  - Business & legal teams pick appropriate consequences and penalties for a breach
  - SRE help them understand the likelihood and difficulty of meeting the SLOs contained in the SLA
- Advice on SLO construction is also applicable for SLAs