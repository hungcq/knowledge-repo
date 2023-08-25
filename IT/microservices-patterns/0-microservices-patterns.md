# Category
IT, backend, microservices, architecture, development

# Summary
The author start by introducing the situations and the need to use microservice architecture.
Then he covers the problems you will face when developing microservices and the patterns to solve it.
Last part of the book handles the difficulty when transitioning from monolithic to microservice architecture.

# Author's problems & solutions
- Discuss benefits & drawbacks of microservices, when to use microservices and when to use monolithic architecture: OK
- Show how to adopt microservice architecture & develop microservices successfully: OK
  - Effective microservice testing
  - Microservice deployment
  - Refactoring strategies from monolith to microservice
  - How to design a microservice app: solutions to design challenges, including managing distributed data
  - How to develop business logic for a service
- Explain microservice architecture patterns & other concepts: OK
- Make the material accessible regardless technology stack of the reader: OK except the example parts

# Presentation & style
- Organize around a collection of patterns
- Some repetition in content of some chap: when summary/introduce next part

# Criticism
- Implementation examples in each chapter is too elaborated, make it difficult to read, esp without familiarity with Java & Spring
- -> Maybe can organize the book differently? Architecture part vs Technologies/examples part.
- Preface: are enterprise applications are typically large monoliths?
- Chap 2: decompose by subdomain pattern part has too vague a description to apply. Result is the same as using decompose by business capability?
- Chap 3:
  - Polling publisher pattern faces the same initial problem:
  what happen if the Message relay deletes from the outbox table then crashes before able to publish message?
  - Discussion of async design didn't take into account FE flow design, which dictates whether sync/async option is possible
- Chap 4: advs & disadvs of choreography saga seem a bit forced, with contradictions
- Chap 5:
  - Rule 3 of aggregate: one trans creates or updates one agg: how about aggs of the same type?
  - How to load other aggs for business logic? CQRS? Req/res?
- Chap 6: deleting techniques only work when deleting a user data completely, not deleting a particular field
- Chap 7: when discuss ways to build CQRS view, haven't dealt with: how to choose the starting event correspond to the snapshot
- Chap 9: all the examples are solitary unit test. Can't see why entity tests and saga tests are sociable tests.
- Chap 10: where to run the tests? Need to read full code examples.
- Chap 13:
  - Why place anti-corruption layer in service? Should keep the service adapter clean for new usages.

# Takeaways
- Lots of architectural concepts, problems & solutions
- -> Deeper understanding of system design, microservice concepts, design issues & dif solutions
- -> Bring out all relevant exp to reflect
- Modern technologies & frameworks to consider/experiment with

# S's problems when migrate from the monolith to microservices
- Split the services horizontally instead of vertically
- -> Compromise transaction isolation. Services depend on each other.
- Keep the account database schema instead of refactoring it