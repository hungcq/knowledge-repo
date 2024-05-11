# II - The building blocks of a model-driven design
- Advs of using standard patterns:
  - Good design
  - Understandability
  - Contribute to ubi lang to discuss model & design decisions
- Part 2 focus: patterns to design individual model elements
- -> Basis for combination into a good design/domain model

## 4. Isolating the domain
- Problem: isolate the part of software that solves domain problems (~business logic) from other parts
- -> Can see the domain model in the system

### Layered architecture
- Goal: separation of concerns while maintaining interaction
- Principles:
  - Dependency: same layer/layers beneath
  - Upward comm must be indirect, except when responding to direct query (eg via callbacks/observers)
- 4 main layers:
  - Presentation: UI/API interface
  - Application (~service):
    - Can be combined with presentation
    - Function: coordinate tasks & delegate works to domain layer
  - Domain: represent business concepts, states & rules
  - Infra: provide generic technical capabilities (eg sending messages, persist data, draw UI widgets, archi frameworks)
  - -> Accessed by app & domain layer
- -> The separation of domain layer is the most imp
- Architectural framework in the form of technical components designed to directly support the basic functions of other layers
  (eg providing an abstract base class for all domain objects) and provide the mechanisms for them to relate (eg  impl of MVC)
has much more impact on the design of other parts of the program
- -> Need to choose & use carefully to:
  - Avoid constraining domain design choices on making impl heavy weight
  - Able to support impl that express a DM well
  - Avoid tight coupling to the framework
  - Maintain understanding of the business objects

### Domain layer
- DDD requires only domain layer to exist
- Functions:
  - Reflect the model
  - Consist of the design & impl of business logic

### Smart UI pattern
- Def: all business logic in the UI
- Use case: small, simple projects
- Disadvs:
  - Hard to integrate
  - Hard to extend business functionalities
  - Lock-in: need to rewrite everything to take a dif approach
- DDD use case: ambitious projects with experienced, competent team members
- DDD needs commitment from the outset to isolate the domain layer