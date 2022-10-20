## 25. Compute as a service
### Evolution of CaaS, with challenges & solutions
- New idea: automate the setting of resource requirement & number of replicas
### Effect on software development
- Architect for failure: treat service instance/task as cattle, not pet
- -> Producer-consumer approach for batch job
- Serving service code needs handler to react to automated management
- Treat state as cattle by:
  - Replicating it
  - Plan for cache failure
  - Save local storage periodically to persistent storage
- Connecting to a service:
  - Service discovery & load balancing
  - Retry request when instance down:
    - Idempotency
    - Deduplication: client-assigned unique ID
  - Check for mis-identified failed node using address resolution system
- Run once job: run on compute service to save engineer time, esp for heavy job
- -> Need a limit to avoid accidental overuse
### Compute architecture lessons learned at Google, over time and scale
- Containers as an abstraction of the compute env
- Compute service manage resource for both batch job & serving job
- Submitted configuration using standardized language for consistency
### Considerations when choosing a compute service
- Why the choice of a compute architecture is imp & involves tradeoffs:
  - Most org will choose a compute service
  - Compute infra has a high lock-in factor:
    - Code will be written in a way that takes adv of all the properties of the system (Hyrum's Law)
    - Any compute service choice will eventually become surrounded by a large ecosystem of helper services
    - -> Costly migration
- Considerations:
  - Centralization vs customization:
    - Customization: expanded & splitted API surface & compute env
    - Centralization: single CaaS solution to manage its entire fleet of machines
    - -> Should be goal: to make the cost of managing the fleet remains manageable
  - VM advs:
    - Bring our own operating system
    - In most orgs, can take adv of preexisting exp in managing VMs & preexisting configurations & workloads based on VM
  - Serverless:
    - Idea: instead of making the machines multi-tenant, make the framework servers multi-tenant
    - Mechanism:
      - Run a large number of framework servers
      - Dynamically load/unload the action code on dif servers as needed
      - Dynamically direct requests to those servers that have the relevant action code loaded
    - Consideration: should be compared with persistent-container architecture like Kubernetes
    - Tradeoffs:
      - True stateless: everything must be set up in request scope
      - Suitable for adaptable scaling of resource cost, esp at the low-traffic end
      - Mid-level of traffic: the scaling will be more reactive & granular than that of the persistent container one
      - Loss of control over the env but less management overhead
    - -> Simpler & cheaper solution for small org or 1 team
    - -> Cost in resource & management of a shared cluster amortizes well only if the cluster is truly shared between multiple teams
  - Public (vs private) cloud:
    - Advs:
      - Less management overhead but increased cost
      - Easy to scale
    - Disadv: lock-in
    - -> Suitable for young orgs or products when predicting resource requirement is challenging
    - Mitigation of lock-in problem:
      - Use public cloud solutions that run using an open source architecture (eg Kubernetes)
      - -> Difficult to guarantee that no parts specific to a provider is used
      - Use a lower level public cloud solution (eg Amazon EC2)
      & run a higher level open source solution (eg OpenWhisk, KNative) on top of it
      - Run multi-cloud: use managed services based on the same open source solutions
      from two or more dif cloud providers (eg GKE & AKS for Kubernetes)
      - Run in a hybrid cloud: part of workload on private infra, part on public cloud provider
        (eg use public cloud as a way to deal with overflow) -> can also manage migration
      - -> Requirement for multi-cloud & hybrid cloud solution: require multiple envs to be connected well, through
        - Direct network connectivity between machines in dif envs
        - Common APIs that are available in both
