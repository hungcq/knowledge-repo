## 11. Developing production-ready services
- Problem: ensure quality attributes before deploying in production: security, configurability, observability

### Security: authentication & authorization
- 4 aspects of security:
  - Authentication
  - Authorization: apps often use role based security with access control lists (ACLs)
  - Auditing
  - Secure IPC (eg services communicate over TLS with authentication)
#### Monolith security approaches:
- Session-based:
  - Session: store principal ID & role in:
    - Memory: require requests to be routed to the same instance
    - DB
  - Session token: used to identify the session. Usually opaque token. Can be:
    - Cryptographically strong random number
    - Store of session state
  - Steps: login -> server returns session token -> client includes token in each subsequent request -> server
- API client: use API key & secret in every request
#### Microservice security:
- Authentication:
  - Approach: centralize authentication in the API gateway before forwarding to the services
  - <img src="./resources/11.3.png" width="500"/>
  - Advs:
    - One place to implement -> safe effort
    - Hide complexity of dif auth mechanisms from the services
- Authorization:
  - Where to implement:
    - Authorize in the API gateway:
      - Advs:
        - One place to implement
        - Can reject requests before forwarding to services
      - Disadvs:
        - Coupling API gateway to the services
        - Can only implement role-based authorization, not ACLs
    - Authorize in the services (standard way) -> can do both role-based & ACLs
  - Types of tokens:
    - Opaque token (eg UUID):
      - Adv: can be revoked
      - Disadv: reduce performance, availability & increase latency:
        token recipient must validate token via a sync RPC call to security service
    - Transparent token (eg JWT) (standard way):
      - Approach: API gateway & services use the token to pass around info about the principal
      - Adv & disadv: reverse of opaque token
      - Solution to irrevocable problem: issue token with short expiration times
      - -> New problem: app must continually reissue JWTs to keep the session active
      - -> Use long-lived refresh tokens (OAuth 2.0 security standard)

### Configuration
- Problem: dif config properties for dif envs
- Externalized configuration def: provide the configuration property values to a service instance at runtime
- 2 approaches for externalized config:
  - Push model:
    - Deployment infra passes the config properties to the service instance using OS env var or configuration file
    - Adv: simple to implement
    - Disadvs:
      - Reconfig a running service is difficult
      - Can't reuse a config that is common to many services
    - -> Pull model
  - Pull model:
    - Service instance reads its config properties from a configuration server (eg on start up)
    - Types of config server:
      - Version control system (eg Git)
      - DB
      - Specialized config server
    - Advs:
      - Centralized config:
        - Easy to manage
        - Can have override-able global defaults to avoid duplicate common properties
      - Transparent decryption of sensitive data:
      encrypt/decrypt can be handled by config server before returning to service
      - Dynamic reconfig (eg via polling)
    - Disadv: increased complexity: another highly available component that needs to be set up & maintain
    - -> Use open source frameworks

### Observability
- Goal: make the service easier to manage & trouble shoot
- <img src="./resources/11.9.png" width="500"/>
- Aspects: health check, log aggregation, distributed tracing, application metrics, exception tracking, audit logging
#### Health check
- Service exposes health check API endpoint which returns the health of the service
- Goal: service instance can tell the deployment infra whether it can handle requests
- -> Deployment infra can take appropriate actions:
  - Route requests to dif instances
  - Terminate/restart the instance
- Design issues:
  - Implement health check endpoint: request handler checks service instance's connections to external service
  (eg DB, message broker)
  - Invoke health check endpoint: depend on details of deployment infra
#### Log aggregation
- Aggregate logs of all services in a centralized database that supports searching & alerting
- Logging infra functions:
  - Aggregate logs
  - Store logs
  - Enable users to search
- Design issues:
  - Choose log lib
  - Decide where to log: stdout
  - -> Let deployment infra handle
#### Distributed tracing
- Goal: see how the services interact during the handling of external requests,
including a breakdown of where the time is spent
- Mechanism: assign each external request a unique ID and record how it flows through the system
(eg timestamps, tree of service calls)
- -> Unique req ID also help with searching logs related to an external request
  in a centralized server that provides visualization and analysis
- Components:
  - Distributed tracing lib:
    - Function: build the tree of spans & send to distributed tracing server
    - Used by each service by:
      - Call directly in code
      - AOP
  - Distributed tracing server: combine the spans to form a complete trace & store in DB
#### Application metrics
- Service reports metrics to a central server that provides aggregation, visualization & alerting
- Goal: monitor service health & alert when there are problems
- Types:
  - Infra-level metrics: eg CPU, memory, disk utilization
  - App-level metrics: eg request latency, QPS, num of requests
- Architecture:
  - <img src="./resources/11.14.png" width="500"/>
- Properties of a metric sample:
  - Name
  - Value
  - Timestamp
  - Other dimensions (name-value pairs)
- Dev responsibility:
  - Add metric collection code
  - Send metric to metric service. 2 approaches:
    - Push model: service instances invoke Metrics service API
    - Pull model: Metrics service (or its agent running locally) invokes a service API
    to retrieve metrics from the service instance
    - -> Central place to config aggregation
#### Exception tracking
- Disadvs of logging exception to log file:
  - Can't handle multiple line exceptions
  - Don't have a mechanism to track the resolution of exceptions
  - No automatic mechanism to deduplicate exceptions
- -> Need a centralized Exception service
- Service report exceptions to a central service
that de-duplicates exceptions, generates alerts & manages their resolution
- Approaches for service to report exception:
  - Call Exception service's API directly
  - Use client lib provided by Exception service
#### Audit logging
- Record each user actions in a DB
- Goal: help CS, ensure compliance, detect suspicious behavior
- Record information:
  - User identity
  - Action performed
  - Business objects
- Ways to implement:
  - Add audit logging code to business logic. Disadvs:
    - Reduce maintainability: intertwine audit logging code with business logic
    - Error prone: dev writing audit logging code
  - AOP:
    - Adv: automatic -> more reliable
    - Disadv: lack of details
  - Event sourcing:
    - Adv: automatically provide an audit log for create & update operation
    - Disadv: doesn't record queries
### Microservice chassis & service mesh
- Microservice chassis:
  - Dev: a framework/set of frameworks that handle cross-cutting concerns (eg observability, config)
  - Adv: reduce dev effort
  - Disadv: need one for every language/platform used to write services
- Service mesh:
  - Def:
    - Networking infra that handles all communication between services and external apps
    - Implement cross-cutting concerns related to inter-service communication
    - -> Help simplify the chassis: only implement concerns tightly integrated with app code
      (eg externalized config, health checks)
  - <img src="./resources/11.17.png" width="500"/>