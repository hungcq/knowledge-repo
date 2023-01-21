# I - Introduction
## 1. Introduction
### Sysadmin approach to service management:
- Sysadmin role: run the service & respond to events & updates as they occur
- Distinction with devs: development team vs operations (ops) team
- Adv: easy to implement: available processes, candidates & tools
- Disadvs:
  - Direct cost: expensive manual effort
  - Indirect cost: the division into 2 teams with dif incentives (change vs not change) causes conflict
### Google's approach to service management: SRE:
- Hire software engineers to:
  - Run products
  - Create systems to accomplish the work that would otherwise be performed, often manually, by sysadmins
- Composition in each SRE team:
  - Normal SEs (50-60%)
  - Nearly-qualified SE (40-50%), with technical skills useful to SRE:
  2 most common skills: UNIX system internals & networking
- Chars of the team:
  - Common background with dev team
  - Predisposed to & have the ability to design & implement automation with software to replace human labor
  - Policy to reduce manual work & keep the focus on development: place a 50% cap on the aggregate ops work for all SREs
  - -> Approach:
    - Measure time spent
    - Redirect excess ops work to dev team
- Advs:
  - Involve coding -> rapid innovation & a large acceptance of change
  - Scalable: in terms of human resources
  - Reduce conflict, shared expertise
- Challenges:
  - Small pool of candidates, competing with product teams
  - New discipline -> no industry standard
  - Unorthodox approaches to service management require strong management support
- Relation to DevOps: devops as a generalization of several core SRE principles
to a wider range of orgs, management structures & personnel
### SRE tenets
- Tenet: codified rule of engagement & principles for how SRE teams interact with their env. Env includes:
  - Production env
  - Product development teams, testing teams, users...
- -> Goal: maintain focus on engineering work, as opposed to operations work
- Tenets:
  - Ensure durable focus on engineering
  - -> Guide devs to build systems that don't need manual intervention
  - Pursue maximum change velocity without violating a service's SLO:
    - Resolve innovation & reliability conflict by introducing error budget (see chap 3)
    - Observation: 100% is the wrong reliability target for almost everything:
    users can't tell the dif due to many other sources of external issues
  - Monitoring:
    - Should never require a human to interpret any part of the alerting domain
    - Software should do the interpreting, humans should be notified only when they need to take action
    - 3 kinds of monitoring outputs:
      - Alerts: a human needs to take action immediately in response to sth that is either happening
      or about to happen, in order to improve the situation
      - Tickets: a human needs to take action, but not immediately
      - Logging: recorded for diagnostic or forensic purposes
  - Emergency response:
    - Avoid emergencies that require human intervention
    - When humans are necessary:
      - Think through & record the best practices ahead of time in a playbook
      - -> Reduce reaction time
      - Disaster role playing
  - Change management: use automation to:
    - Implement progressive rollouts
    - Quickly & accurately detect problems
    - Roll back changes safely when problems arise
  - -> Advs: increase release velocity & safety
    - Minimize aggregate number of users & operations exposed to bad changes
    - Remove humans from the loop
    - -> Avoid the problems of fatigue, familiarity/contempt & inattention to highly repetitive tasks
  - Demand forecasting & capacity planning:
    - Def: ensure that there is sufficient capacity & redundancy to serve projected future demand with the required availability
    - Types of growths to be considered when plan for capacity:
      - Organic growth: increased users
      - Inorganic growth: due to product decision
    - Mandatory steps:
      - Accurate demand forecast, extending beyond the lead tine required for acquiring capacity
      - Accurate incorporation of inorganic demand sources
      - Regular load testing of the system to correlate raw capacity (eg servers, disks) to service capacity
  - Provisioning:
    - Combine both change management & capacity planning
    - Approaches:
      - Conduct quickly & only when necessary: capacity is expensive
      - Do correctly or capacity doesn't work when needed
    - Steps:
      - Spin up a new instance or location
      - Make significant modification to existing systems (config files, load balancers, networking)
      - Validate that the new capacity performs and delivers correct results
  - Efficiency & performance: work with devs to predict demand, provision capacity & modify software