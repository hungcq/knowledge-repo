## 21. Handling overload
- BE: serve degraded res or return error
### Capacity measurement
- Modeling capacity as QPS or using static features of the requests
believed to be a proxy for the resource they consume make a poor metric. Reasons:
  - - Dif query cost: queries can have vastly dif resource requirements
  - -> A query's cost can vary based on arbitrary factors. Eg:
    - Code in the client that issues them
    - Time of the day
  - Change in the service (eg new version)
- Better solution: measure capacity directly in available resources
(cost of a request usually refer to a normalized measure of how much CPU time it has consumed (over dif CPU architectures)):
  - In most cases, simply using CPU consumption as the signal for provision works well. Reasons:
    - In platforms with GC, memory pressure naturally translates into increased CPU consumption
    - In other platforms, it is possible to provision the remaining resources
    in such a way that they are very unlikely to run out before CPU runs out
  - In cases where over-provisioning the non-CPU resources is prohibitively expensive,
  take each system resource into account separately
### Load limit mechanisms
- Per-client limits:
  - Goal: service delivers error responses to misbehaving customers, while other customers remain unaffected
  - Process: service owners provision their capacity based on the negotiated usage with their customers
  and define per-customer quotas according to these agreements
  - It is unlikely for all of their customers to hit their resource limits simultaneously
  - -> Total quotas may add up to more than the total CPU allocated to the backend service
  - How to measure & limit usage:
    - Aggregate global usage info in real time from all backend tasks
    - Compute in real time the amount of resources (CPU) consumed by each individual request
- Client-side throttling:
  - When a client is out of quota, backend task should reject requests quickly and returns an "out of quota" error
  - Limitations:
    - Cheap normal responses consume the same resource as returning an error
    - Very high number of rejections will still consume lots of resource & overload service
  - -> Client-side throttling as a solution: adaptive throttling (~circuit breaker)
  - Criticality:
    - A request made to a backend is associated with 1 of 4 possible criticality values:
      - Critical-plus: result in serious user-visible impact if fail
      - Critical:
        - Default value for requests sent from production jobs
        - Result in user-visible impact, but less severe than those of critical-plus
        - Services are expected to provision enough capacity for all expected critical and critical-plus traffic
      - Sheddable-plus:
        - Partially unavailability is expected
        - Default for batch jobs: can be retried
      - Sheddable: frequent partial unavailability and occasional full unavailability is expected
    - Integrated into many control mechanisms to deal with overload. Egs:
      - Reject lower criticality first
      - -> Per-customer limits can be set per criticality
      - Integrate with adaptive throttling 
    - The criticality of a request is orthogonal to its latency requirements
    - Propagation & override:
      - RPS system propagate criticality automatically
      - Set as close to FE criticality as possible, only override in specific cases
### Utilization measurement (skipped)
### Handling overload error at client side
- 2 possible situations:
  - A large subset of backend tasks in the datacenter are overloaded: not retry request, return error to callers
  - A small subset of backend tasks in the datacenter are overloaded:
    - Typically caused by imperfections in the load balancing inside the datacenter
    - Retry request immediately (eg redirect traffic to nearest datacenter)
- Decide whether to retry:
  - Per-request retry budget of up to 3 attempts
  - Per-client retry budget: max 10% retry rate
  - Clients include a counter of how many times the request has already been tried in the request metadata
  - -> BE aggregate & keep track to determine
- Avoid explosion of retry: requests should only be retried at the layer immediately above the layer that is rejecting them
- -> Return "overloaded, don't retry" response -> upper layer should not retry
### Handling connection overload
- Handling bursts of new connection (eg very large batch jobs):
  - Cross datacenter load balancing
  - Use batch proxy tasks to shield the real BE