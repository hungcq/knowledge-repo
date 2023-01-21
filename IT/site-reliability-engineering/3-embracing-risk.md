## 3. Embracing risk
- Tradeoff: reliability vs product release velocity
### Overview
- 2 types of costs to increase reliability:
  - Cost of redundant machine/compute resources
  - Opportunity cost: dev features to reduce risk instead of dev product feature
- Use a non-linear risk continuum
- -> Do cost-benefit analysis to determine the risk level

### Metrics to measure service risk
- Standardize impact by using unplanned downtime
- Time-based availability = uptime/total time
- Aggregate availability (request success rate) = successful requests/total requests
- -> Work better for global services that are usually not down in all regions
- Can be applied to other non-serving systems using notion of successful & unsuccessful units of work
- Process:
  - Set quarterly availability targets for a service & track performance against those targets on daily/weekly basis
  - Looking for, tracking down & fixing meaningful deviations when they arise

### Considerations when defining risk tolerance of services
- Consumer services:
  - Target level of availability. Considerations:
    - What level of service will the users expect?
    - Does this service tie directly to revenue (ours or customer's)
    - Is this a paid service?
    - If there are competitors in the marketplace, what level of service do those competitors provide?
    - Is this service targeted at consumers, or at enterprise?
  - Types of failures: full vs partial
  - -> Choose one with the least impact on the business
  - Cost (key factor): monetary cost of increasing availability vs increase in revenue
  (eg convert 1% availability into revenue: 1% * total revenue, then compared with cost of improving availability)
  - Other service metrics: determine which metrics are imp to take thoughtful risk
- Infra services:
  - Dif vs consumer service: infra services have multiple clients, often with varying needs
  - Considerations:
    - Target level of availability
    - Types of failures
    - Cost:
      - Provide at dif levels of service. Externalize the dif in the cost at a given level to clients.
      - -> Motivate the clients to choose the level of service with the lowest cost that still meets their needs
      - How to provide dif levels of service:
        - Adjusting a variety of service characteristics (eg quantity of resources, degree of redundancy...)
        - Use dif hardware & software

### Error budget
- Problems:
  - Tension due to conflicting incentive between product team & SRE team
  - Info asymmetry
- Goal: define an objective metric, agreed upon by both sides, that can be used to guide the negotiations in a reproducible way
- Process:
  - Product management defines an SLO: how much uptime the service should have per quarter
  - The actual uptime is measured by a neutral third party: the monitoring system
  - The dif between these 2 numbers is the budget of how much unreliability is remaining for the quarter
  - As long as there is error budget remaining, new releases can be pushed
  - Can negotiate to change the SLO if more reliability/innovation is needed
- Advs:
  - Provide a common incentive
  - Product teams control release velocity & reliability themselves, depending on how much error budget is left