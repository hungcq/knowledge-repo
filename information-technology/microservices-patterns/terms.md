# List of microservice patterns
- Application architecture patterns:
  - Monolithic architecture (40)
  - Microservice architecture (40)
- Decomposition patterns:
  - Decompose by business capability (51)
  - Decompose by subdomain (54)
- Messaging style patterns:
  - Messaging (85)
  - Remote procedure invocation (72)
- Reliable communications patterns:
  - Circuit breaker: RPC proxy. Functions:
    - Track num of successful/failed requests
    - If error rate exceeds some threshold, trip the circuit breaker -> further attempts fail immediately
    - After a period, client can try again. Close the circuit if successful.
    - 3 states: closed, half-open, open
- Service discovery patterns:
  - 3rd party registration (85)
  - Client-side discovery (83)
  - Self-registration (82)
  - Server-side discovery (85)
- Transactional messaging patterns:
  - Transactional outbox: publish an event or message as part of a DB trans by saving it in an outbox table in the DB
  - Transaction log tailing: publish changes made to the DB by reading transaction logs of the outbox table
  - Polling publisher: publish messages by pulling the outbox table
- Data consistency patterns:
  - Saga: maintain data consistency across services using a sequence of local trans coordinated using async messaging
- Business logic design patterns:
  - Aggregate: organize a domain model as a collection of aggregates,
  each of which is a graph of objects that can be treated as a unit
  - Domain event: an aggregate publishes a domain event when it's created or undergoes some other significant change
  - Domain model: organize business logic as an object model consisting of classes that have state and behavior
  - Event sourcing: persist an agg as a sequence of domain events that represent state changes.
  - Transaction script: organize business logic as a collection of procedural transaction scripts,
  one for each type of request
- Querying patterns:
  - API composition: implement a query that retrieves data from several services
  by querying each service via its API & combine the results
  - Command query responsibility segregation (CQRS): implement a query that needs data from several services
  by using events to maintain a read-only view that replicates data from the services
- External API patterns:
  - API gateway: implement a service that's the entry point for external API client into the microservices-based app
  - Backends for frontends: implement a separate API gateway for each type of client
- Testing patterns:
  - Consumer-driven contract test (302)
  - Consumer-side contract test (303)
  - Service component test (335)
- Security patterns:
  - Access token: API gateway passes a token containing information about the user (eg identity & roles)
  to the services that it invokes
- Cross-cutting concerns patterns:
  - Externalized configuration
  - Microservice chassis
- Observability patterns:
  - Application metrics (373)
  - Audit logging (377)
  - Distributed tracing (370)
  - Exception tracking (376)
  - Health check API (366)
  - Log aggregation (368)
- Deployment patterns:
  - Deploy a service as a container (393)
  - Deploy a service as a VM (390)
  - Language-specific packaging format (387)
  - Service mesh
  - Serverless deployment (416)
  - Sidecar (410)
- Refactoring to microservices patterns:
  - Anti-corruption layer (447)
  - Strangler application (432)
# Terms
- Pattern: reusable solution to a problem that occur in a particular context
- Microservice pattern language: collection of interrelated software architecture and design patterns for microservices
- Software architecture: high level structure of a software,
which consists of constituent parts & the dependencies between those parts
- Monolithic architecture: architectural style that structures a system (implementation *view*) 
as a single executable or deployable component
- Microservice architecture: architectural style that structures a system (implementation *view*)
as a set of multiple loosely coupled, independently deployable services
- Service: standalone, independently deployable software component that implements some useful functionality
- Business capability: something that a business does in order to generate value
(eg order management, item management, shipping...)
- IDL: interface definition language
- Service registry: database of network locations of an app's service instances
- Message broker: an intermediary through which all messages flow (sender -> broker -> receiver)
- Transactional messaging: publish messages as part of a transaction that updates the DB
- State machine:
  - Consist of a set of states and transitions between states that are triggered by events
  - Each transition can have an action
- Anomaly: when a trans reads of writes data in a way that wouldn't if trans were executed once at a time
- Countermeasure: saga design strategy that deal with the lack of isolation
- Domain driven design (DDD): a refinement of object oriented design to develop complex business logic
- Aggregate (in DDD):
  - A cluster of domain objects within a boundary that can be treated as a unit
  - Consist of a root entity and possibly one or more other entities and value objects
- Domain event (in DDD): sth happened to an agg (eg state change)
- Optimistic locking: typically use a version column to detect whether the agg has changed since it was read
- Authentication: verify the identity of the principal (app or human) that is attempting to access the app
- Authorization: verify that the principal is allowed to perform the requested operation on the specified data:
  - Role-based security: assign each user one or more roles that grant them permission to invoke particular operations
  - Access control list (ACL): grant users or roles permission to perform an operation
  on a particular business object or aggregate
- Audit: track the operations that a principal performs in order to detect security issues, help CS & enforce compliance
- Trace (in distributed tracing): represent an external request, consist of one or more spans
- Span (in distributed tracing): represent an operation. Key attributes: operation name, start & end time.
- Aspect oriented programming (AOP) (~middleware in Node):
automatically intercept each service method call & perform an action
- Deployment: combination of process & architecture:
  - Deployment process: steps that must be performed by people (devs & operations) to get software into production
  - Deployment architecture: structure of the env in which that software runs
- Container image: a filesystem image consisting of the app & any software required to run the service
- Release: make a service in production available to handle production traffic
- Sidecar: a process or container that runs alongside the service instance and implements cross-cutting concerns
- Test case (test): a set of test inputs, execution conditions & expected results
to verify the behavior of the system under test (SUT)
- Test suite: a collection of related tests
- Test double: an object that simulates the behavior of the dependency
- Consumer driven contract test: an integration test for a provider
that verifies that the shape of its API matches the expectations of a consumer
- Deployment pipeline: the automated process of getting code from dev's computer into production
- User journey test: corresponds to a user's journey through the system
- Strangler app: new app consisting of microservices, developed by implementing new functionality as services
  and extracting services from the monolith