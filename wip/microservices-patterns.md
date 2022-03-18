# Category
IT, backend, microservices, architecture, development

# Summary
The author start by introducing the situations and the need to use microservice architecture.
Then he covers the problems you will face when developing microservices and the patterns to solve it.
Last part of the book handles the difficulty when transitioning from monolithic to microservice architecture.

# Structure
- Preface:
  - History of microservice architecture
  - The problems & how they will be addressed in the book
  - Reason to organize the book around patterns
- Chap 1 & 2:
  - Basic concepts
  - Problem of monolithic, when and why to use microservice architecture
  - Advs & disadvs of microservice architecture
  - Microservice patterns as a solution
  - Defining application architecture:
    - Decompose & define services
    - Define APIs
- Chap 3-12: problems & patterns:
  - Interprocess communication
  - Managing transactions
  - Designing business logic
  - Implementing queries
  - Designing external APIs for various types of client
  - Automated testing for microservices
  - Developing production-ready services:
    - Security
    - Configuration
    - Observability
  - Deployment
- Chap 13: refactoring from monolithic to microservice architecture: difficulty & strategies

# Author's problems & solutions
- Discuss benefits & drawbacks of microservices, when to use microservices and when to use monolithic architecture
- Show how to adopt microservice architecture & develop microservices successfully
- Offer solutions to numerous design challenges, including managing distributed data
- Explain microservice architecture patterns & other concepts
- Make the material accessible regardless technology stack of the reader

# Presentation & style
- Organize around a collection of patterns

# Terms
- List of microservice patterns:
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
    - Circuit breaker (78)
  - Service discovery patterns:
    - 3rd party registration (85)
    - Client-side discovery (83)
    - Self-registration (82)
    - Server-side discovery (85)
  - Transactional messaging patterns:
    - Polling publisher (98)
    - Transaction log tailing (99)
    - Transactional outbox (98)
  - Data consistency patterns:
    - Saga (114)
  - Business logic design patterns:
    - Aggregate (150)
    - Domain event (160)
    - Domain model (150)
    - Event sourcing (184)
    - Transaction script (149)
  - Querying patterns:
    - API composition (223)
    - Command query responsibility segregation (228)
  - External API patterns:
    - API gateway (259)
    - Backends for frontends (265)
  - Testing patterns:
    - Consumer-driven contract test (302)
    - Consumer-side contract test (303)
    - Service component test (335)
  - Security patterns:
    - Access token (354)
  - Cross-cutting concerns patterns:
    - Externalized configuration (361)
    - Microservice chassis (379)
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
    - Service mesh (380)
    - Serverless deployment (416)
    - Sidecar (410)
  - Refactoring to microservices patterns:
    - Anti-corruption layer (447)
    - Strangler application (432)
- Pattern

# Arguments
## Preface
- Enterprise applications are typically large monoliths (is it?)
- Pattern:
  - Def: reusable solution to a problem that occur in a particular context
  - Describe:
    - Benefits
    - Drawbacks
    - Issues to address to successfully implement a solution
  - -> Objectivity -> better decision making

## 1. Escaping monolithic hell
- 

# Criticism

# Take away
