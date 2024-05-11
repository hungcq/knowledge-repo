## 5. A model expressed in software

### Object association
- Difficulty: many-to-many & bidirectional associations:
  - Complex
  - Communicate little about the nature of the relationship
- 3 ways of making associations more tractable:
  - Impose a traversal direction following app's requirement
  - -> Use one that is more imp & meaningful
  - Add a qualifier, effectively reducing multiplicity (eg 1 investment per stock)
  - Eliminate nonessential associations

### 3 model elements

#### Entity
- Def -> not identity (object reference) in OOP language
- -> Has continuity through a life cycle and distinctions independent of attributes that are imp to the app's user
- Ways to define key:
  - Combination of attributes into a unique key
  - Randomly generated
  - -> Need to deal with concurrency/distributed system
- Design:
  - Define ID operation
  - Keep the class definition simple & focused on life cycle continuity & identity
  - -> Extract behavior/attributes into other associated objects
  - Entities coordinate the operations of objects they own

#### Value object
- Problem: adding ID to non-entity objects has performance & complexity cost
- Def
- Chars:
  - Can have complicated rules
  - Can be combined into another value object
  - Can reference entities
- Usage:
  - Passed as parameters in messages between objects
  - Used as attributes of entities and other value objects
- Design:
  - Treat as immutable except when frequently changed
  - Encapsulate related attributes into a conceptual whole
  - When there are many similar ones, optimize performance by sharing using patterns like Flyweight
  - Association: can't be bidirectional (only make sense to entity)
- Optimize DB performance: denormalize: store value object data inside entity table to avoid costly joins

#### Service
- Problems when forcing inapt operations into an object:
  - Obscure its role
  - Create complex dependencies between objects
- Def
- Naming:
  - Name after an activity (a verb)
  - Operation names should be part of ubi lang
- Design:
  - Should be used judiciously & not allowed to strip the entities and value objects of all their behavior
  - Operation:
    - Related to a domain concept that is not a natural part of an entity or value object
    - Is stateless
  - Interface is part of the domain model, defined in terms of other elements of the domain model
  - Have defined responsibility
- Types:
  - Infra service (eg sending email): no business meaning
  - App service:
    - Handle input
    - Call infra service
    - Call domain service/objects
  - Domain service:
    - Have business rules for operations
    - Coordinate domain objects (eg entity, value objects)

### Module (ie package)
- Design:
  - Divide not only code but also concepts into module
  - -> Its name should be part of ubi lang
  - Low coupling & high cohesion
  - -> Advs:
    - Avoid cognitive overload by having dif level of abstraction
    - Allow modeling & design work to concentrate within a single module
    - -> Improve the model if needed
  - Should be resilient to change of elements within a module
  - -> Avoid costly refactor
  - Only impose convention of separating domain layer into dif module
  - -> Leave it to devs to determine the choice of module
- Best practices:
  - Deal with early mistake in module design: need to consider tradeoff between costly refactor & high coupling
  - -> Need to look for ways of minimizing the work of refactoring modules
  - Import package instead of individual file/class
  - Avoid breaking conceptual object into separate tiers placed in dif modules

### Modeling paradigms
- Model driven design depends on having an expressive impl of the model constructs, be they objects, rules, or workflows
- Why OOP is suitable as an impl tech:
  - Maturity of tech & community
  - Object modeling can capture domain knowledge effectively
  - -> Some exceptions (eg mathematical domain)
- When other paradigms better express the domain model or part of it, can mix paradigms & integrate dif systems
- -> Tradeoffs:
  - The coherence of the model
  - Complicated integration of dif tools
- -> Need to enforce coherence of the heterogeneous model & design, most effectively by using ubi lang