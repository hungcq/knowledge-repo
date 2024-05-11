## 10. Supple design
- Problems of bad design:
  - Hard to refactor/reuse/recombine elements
  - -> Duplication
  - Haunted graveyard
  - -> Hard to build rich features
  - -> Need supple design for better maintainability
- Iterative refinement process: insight -> concepts -> model -> design -> impl -> more insights
- Advs of supple design:
  - When building new features: easy to understand & recombine elements
  - When making changes:
    - Easy to change at flexible points
    - Effects of change are obvious
- Early versions of a design are usually stiff
- -> Need to make the most crucial, intricate parts supple, not every parts

### Patterns that contribute to a supple design

#### Intention-revealing interfaces
- Problems of obscure interfaces: lose the value of encapsulation: need to read impl details to understand & use
- -> Misuse, cognitive overload
- All public elements are parts of interface:
  - Type name
  - Method name
  - Argument name
- -> Names should focus on effect & purpose, not mechanism
- -> Write a test for each behavior before development
- Making a method predictable via:
  - Side-effect-free functions
  - Assertions to simplify side effects
- Side-effect-free functions:
  - Commands (have side effect) vs queries
  - Side effect problem: difficult to understand all the effects of an operation in a complex system
  - Function def: operation that returns results without producing side effects
  - -> Idempotent, easy to test, understand, combine
  - Ways to reduce/simplify commands:
    - Separate commands & queries. Keep command thin by delegate most sub operations to queries
    - Immutability with value objects: eg create new value object class that handle the operation (example in p.253),
    or derive value object instead of changing state
- Assertions:
  - Problem: side effects hidden in impl
  - -> Lost encapsulation, difficult to understand
  - Assertion def: state post-conditions of operations & invariants of classes and aggregates
  - Write assertions in:
    - Code if supported by language
    - Unit tests: as setup & verify steps
    - Docs/diagrams
  - Should be intuitively understandable & logically consistent
  - -> Need to look for a good model that corresponds to real world concept while satisfying the needs of the app

#### Effective decomposition
- Conceptual contours:
  - Difficulty: choose the level of granularity of elements/functionalities
  - Def: decompose design elements (operations, interfaces, classes & aggs) into cohesive units,
  taking into consideration your intuition of the imp divisions in the domain
  - Indicator of a model that needs refactoring: changes are not localized, affecting multiple broad concepts of the model
- Standalone classes:
  - Problem: interdependencies -> have to reason about many things at once
  - -> Cognitive overload
  - Reduce dep by:
    - Remove superfluous concepts
    - Remove non essential dep, esp inter-module
  - Refactor intricate computations/operations into standalone classes (eg value object)
- Closure of operations:
  - Def: define an operation without involving other concepts
  - -> Application to design: operation with return type the same as the type of its arguments
  (including the class owning the method if its state is used)
  - Advs:
    - Simplify the interpretation of an operation
    - Easy to chain together or combining closed operations
    - Provide a high level interface without introducing any dependency on other concepts
  - Use case: mostly operations of value object
  - Design: halfway is OK: eg not match entirely or using an extra primitive/library type
  - -> Still get some advs of the pattern
  - Require high level of skill to apply to a detailed design & to implement

### Declarative design
- Potential impl issues that can obscure the model driven design:
  - Assertions can't cover everything
  - Need to write procedure for conceptual interactions
  - Lots of boilerplate code
- -> The need for declarative design
- Def: a way to write a program, or some part of a program, as a kind of executable specification
  (ie a very precise description of properties actually controls the software)
- Difficulties:
  - Hard to extend the software beyond the automated portion when the language/framework can't do everything needed
  - Hard to regenerate code when it is merged with hand-written code
  - Unpredictability: when system is difficult to use (too restrictive)
  - -> Devs bypass the rules
  - Technical difficulty & high learning curve when trying to improve/extend the code generation tool
- Working, common case: ORM, persistence

### Approaches to fit the patterns together to make a big system supple
- Separate specialized subdomains as separate models
- -> What is left is smaller and clearer and can be written in a declarative style (ie composing the specialized models)
- Use formal conceptual framework of the domain (eg math)
- -> Adapt to a deep model and a supple design

### Additional info
- Write tests to reflect the way the clients prefer to use the class
- -> Tests as example usage
- Changing an argument is a bad practice