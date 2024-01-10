# Domain-Driven Design

## Info
- Type: book
- Author: Eric Evans

## Category
- SE
- Design
- Best practices

## Structure

### Outline
- Part 1:
  - Basic goals of domain-driven development
  - Terms
  - Overview of the implications of using the domain model to drive communication & design
- Part 2: basic building blocks: condensed from a core of best practices in object-oriented domain modeling:
  - Bridge the gap between models & practicals, running software
  - Keep the model & implementation aligned with each other, each reinforcing the other's effectiveness
- Part 3: modeling principles & techniques to be used in:
  - Model discovery process
  - Assembling building blocks into practical models
- Part 4: system principles to deal with situations that arise in:
  - Complex systems
  - Larger orgs
  - Interactions with external/legacy systems

### Detailed structure
- Foreword: Fowler's thoughts about the book:
  - Problem
  - Goals
- Preface:
  - Problem
  - Goal
  - Style
  - Relation between design & dev process
  - Structure
  - Audience
- Part 1: putting the domain model to work:
  - Chap 1: knowledge crunching: model distills business knowledge:
    - Example modeling work & discussion
    - Modeling principles
    - Evolution of model
  - Chap 2: communication and the use of language:
    - Ubi lang: adv, vocab, difficulty, example
    - Document, diagram, code: relation to ubi lang, best practices
    - Explanatory models: def, use case
  - Chap 3: binding model and implementation:
    - Imp of tight association between model and impl
    - Suitable programming paradigm & tools
    - Implication for team's division of responsibility
  - Chap 4: isolating the domain:
    - Layered architecture: def, layers, adv
    - Domain layer
    - Smart UI pattern (vs DDD) discussion: use case & disadvs
  - Chap 5: a model expressed in software:
    - Object associations: difficulty, mitigation
    - 3 model elements: def, chars, design:
      - Entity
      - Value object
      - Service
    - Module (package) best practices
    - Modeling paradigms: suitability, use cases: OOP vs others
  - Chap 6: the life cycle of a domain object:
    - Managing complex objects life cycle: challenges & design patterns
    - Aggregate: problem, invariants, impl
    - Factory: goal, design
    - Repository:
      - 3 ways of getting ref to an obj
      - Problem
      - Advs
      - Design

## Goals
- Problem: sources of complexity:
  - Technological (eg network, DB)
  - Business domain (most imp)
- -> Advs of a good design: control & exploit complexity
- Premises:
  - For most software projects, the primary focus should be on the domain & domain logic
  - Complex domain designs should be based on a model
- Goals:
  - Provide a framework for making design decisions
  - Provide a technical vocab for discussing domain design, including design practices, techniques & principles

## Style
- Expositional
- Code example: Java, old version
- Author's claim:
  - Contain:
    - Best practices
    - Author's own insights & experiences
  - Design & process are inextricable (how things are done)
  - -> Talk about process when necessary. Oriented towards Agile.
  - -> Use XP as the basis for discussion of the interaction of design & process
  - Discussions are illustrated with realistic examples adapted from actual projects
  - Written as a set of patterns (format see Appendix)
  - Require some knowledge of OO modeling

## Terms
- Model: a simplification. An interpretation of reality
that abstracts the aspects relevant to solving the problem at hand and ignores extraneous detail.
- Domain: a subject area to which the user applies the program
- -> Usually have little to do with computers
- Domain model: a rigorously organized and selective abstraction of domain knowledge
- Domain modeling: loosely representing reality to a particular purpose
- Entity: an object defined primarily by its identity (not attributes)
- Value object: an object that represents a descriptive aspect of the domain with no conceptual identity
- Service: an operation offered as an interface that stands alone in the model, without encapsulating state
- Aggregate: a cluster of associated objects treated as a unit for the purpose of data changes
- Factory: a program element whose responsibility is the creation of other objects
- Reconstitution: the creation of an instance from stored data
- Repository: a mechanism for encapsulating storage, retrieval & search behavior which emulates a collection of objects

## Criticism
- Some parts are too abstract. Hard to understand/apply given only 1 example.

## Takeaway
- Best practices & patterns to organize the codebase for extensibility & maintainability
- Motivations & suggestions for applying model driven design & related patterns
- Opportunities for reflection upon past work & points of improvement
- Intro to fundamental books

## Content

### Graphs
- <img src="./resources/building-block-supple-design.png" width="800">
- <img src="./resources/strategic-design.png" width="800">

### Foreword
- Problem: main source of complexity in SE is the intricacy of the problem domain
- -> Need a good model with an underlying structure
- Goals:
  - Describe & build a vocab about the art of domain modeling
  - Provide a frame of reference to explain domain modeling activity
  - Teach domain modeling skill
  - Share lessons about domain modeling:
    - Shouldn't separate concepts from implementation
    - Domain models need refinement after a system is released

### Preface
- Rela between design & development process:
  - Process necessary to apply DDD:
    - Iterative development
    - Close rela between devs & domain experts throughout the project's life
  - On XP:
    - Resist upfront design
    - Emphasize communication & ability to change project's course rapidly
  - Design affect Agile process in:
    - Ease of refactoring
    - Easy of communication
- Audiences:
  - Developers of OO software
  - Analysts & relatively technical project managers
- Reading recommendation:
  - Core: intro to part 1, chap 1, 2, 3, 9, 14
  - Advanced topic: part 3, 4
- Imp of adopting DDD for the whole team: better comm, better design & impl, better collaboration with other teams