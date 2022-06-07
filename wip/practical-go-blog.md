## 3. Style
- Don't mix unrelated ideas in 1 function
- -> Reduce usage of blank lines
- -> Shorter functions
- Make use of zero value or prevent its construction
- Receiver:
  - Use pointer receiver when caller will change the receiver or to avoid copying data
  - Return values with method by reference
  - Name receiver as normal argument (method is just shorthand for function with receiver as first argument)
- Use method when state is retain/mutated, function when it is not
- -> Function is pure and easier to test
- Avoid named return values & naked return: separate declaration & use, hard to follow
- Avoid incomplete initialization, specifically public Init function
- -> No invalid immediate state
- Avoid finalization: not guaranteed to be run timely
- -> Associate lifetime of resource to lifetime of a goroutine

## 4. Understanding nil
- Always return an explicit nil, rather than a typed value containing nil: will lead to unexpected error in case of Interface return type
- Never use nil to indicate a failure, only to indicate the absence of an error
- Don’t check for a nil receiver. Employ high test coverage and vet/lint tools to spot unhandled error conditions resulting in nil receivers.

## 6. API design
- API consists of exported:
  - Function
  - Method
  - Constant
  - Symbol
  - Formal param
  - Return values
  - Interface method
  - Fields in struct, including their order
  - Errors, contents & types
- API should be easy to use & hard to misuse
- Design API for default use case:
  - Avoid unused param in default case
  - Use functional options to configure complex types
  - Discourage the use of nil as param
  - Avoid public APIs with test only param
- Strive for minimal API surface: less params
- Avoid using several params of the same type:
  - Exception: commutative case
  - Fix: create helper type for first param
- Prefer var args to slice param. To ensure at least 1 param is pass, use: first int, args ...int
- Prefer single method interface: simpler implementation, better abstraction
- Prefer streaming interfaces: use io.Reader, io.Writer for untyped sequences of bytes. Use channels for typed sequences of values.
- Functions should be named for what they return, methods should be named after the action they perform
- Let callers define the interface they require
- Prefer types rather than names for interface methods: variable name is not needed. Types of params should display what the function does.

## 7. Package design
- Unit of software in Go is package
- -> Design question: what does this package provide
- Name:
  - Use 1 word, describe what the package does
  - Utility package names should be plural, they provide helpers to work with things of a specific type
  - Unique
  - Avoid package names like base, common, or util
- Avoid package level state (global state)
- Avoid leaking internal state: getter method, esp one returning pointer/slice

## 8. Project structure
- Avoid elaborate package hierarchy
- -> Use fewer, larger packages
- A Java package is equivalent to a single .go source file
- Arrange files by import statements:
  - Same imports -> merge
  - Separate by imports
- Use internal packages to reduce your public API surface: a package .../a/b/c/internal/d/e/f:
  - Can be imported only by code in the directory tree rooted at .../a/b/c
  - Cannot be imported by code in .../a/b/g or in any other repository