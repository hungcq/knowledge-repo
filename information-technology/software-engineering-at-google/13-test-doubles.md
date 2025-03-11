## 13. Test doubles
### Overview
- Def: an object or function that can stand in for a real implementation in a test
- Impact of test doubles on software development:
  - Codebase needs to be designed to be testable (eg use dep injection)
  - -> Can swap out real implementation with test doubles
  - Double should be used carefully to avoid brittle, complex tests
  - Behavior of test double should closely resemble behavior of real implementation
  - -> No perfect fidelity -> need to supplement unit tests with larger scope tests that exercise real implementation
- Real implementations (vs test doubles):
  - Advs:
    - Give more confidence that the system under test is working properly
    - -> Don't need to rely on integration/manual tests
    - Tests don't depend on implementation details (test state vs using doubles to test detailed interaction)
  - Use when real implementation is fast (build time & execution time),
  deterministic, has simple dependencies (eg value object)
  - Can structure real implementation to make construction simpler (eg factory pattern)
### Techniques for using test doubles
- Faking:
  - Def: a lightweight implementation of an API that behaves similar to the real implementation
    but isn't suitable for production (eg in-memory DB)
  - Ideal technique when using test doubles
  - Require maintenance effort to follow real impl:
    - Should be maintained by the team that owns the real impl
    - Worth dev effort if there are lots of users (more user benefit)
  - Should be created at the root of dependency (eg DB, not classes depended on DB)
  - *Fidelity*:
    - To the API contracts of the real impl, from the perspective of the test
    - Can fail fast for unnecessary behaviors
    - Must have its own tests to ensure fidelity
    - -> How: test the public API against both the real impl & the fake
  - If fake is not provided by API owner: create your own fake by:
    - Wrap all calls to the API in a single class, then
    - Create a fake version of that class that doesn't talk to the API
- Stubbing:
  - Def: the process of giving behavior to a function that otherwise has no behavior by specifying what values to return
  - Usually done through mocking frameworks to reduce boilerplate (same with interaction testing)
  - Disadvs:
    - Unclear tests: need extra code to define behaviors of functions being stubbed
    - -> Difficult to understand if unfamiliar with impl of SUT
    - Brittle tests: leak impl details into tests
    - -> Tests need to change following impl change, not change in API beha
    - Less effective tests:
      - Can't ensure the stubbed function behaves like the real impl
      - Can't store state -> hard to test certain aspects of SUT
  - Use case: need a function to return a specific value to get the SUT into a certain state
  - Best practice:
    - Each stubbed function should have a direct relationship to the test's assertions
    - Num of stubs should be small to avoid complexity
- Interaction testing:
  - Def: a way to validate how & whether a function is called
  without actually calling the implementation of the function
  - Disadvs:
    - Can't ensure that the SUT is working properly: can only validate that certain functions are called as expected
    - -> Need to make assumption about the beha of the code
    - Leak impl details: reveal that the SUT calls a function
  - Use cases:
    - Can't use real impl & no fake exists
    - -> Use mock as a compromise
    - Differences in the number/order of calls to a function would cause undesired behavior
    (eg when using cache, need to verify that the DB object is not accessed more times than expected)
  - Best practice:
    - Not a complete replacement for state testing
    - -> When using mock in unit tests, need to supplement the test suite with larger scoped tests that perform state testing
    - Should be used for state-changing functions (with side effects, eg send email, save to DB)
    - -> For non-state-changing function (eg query function), stubbing is enough:
    the SUT will return the value of the function to do other work that can be asserted
    - Avoid over-specifying which functions/arguments are validated
    - -> Resilient to changes made to behavior that are outside the scope of the test
