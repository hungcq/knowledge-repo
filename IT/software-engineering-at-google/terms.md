# Software engineering
- SE vs programming:
  - SE:
    - Encompasses:
      - Act of writing code
      - All the tools and processes an organization uses to build and maintain that code over time
    - Imply application of some theoretical knowledge to build something real and precise
  - 3 principles:
    - Time & change
    - Scale & growth
    - Tradeoffs & costs
- Sustainable codes: able to react to necessary change

# Documentation
- Documentation: every supplemental text that an engineer needs to write to do their job,
including standalone docs & code comments

# Testing
- Test size: resources needed to run the test
- Test scope: how much code is being validated (not executed) by a given test
- Hermetic: contain all the info necessary to set up, execute & tear down
- Flaky test: test that fails non-deterministically
- Code coverage: % feature code executed by tests
- Exploratory testing:
  - A form of manual testing
  - Interact with a product via a public API, try new paths/user scenarios in the system
  - Looking for:
    - Behavior deviating from expected/intuitive behavior
    - Security vulnerability
- Test infrastructure: code shared across multiple test suites
- Test double: an object or function that can stand in for a real implementation in a test
- Fidelity: how closely the behavior of a test double resembles the behavior of the real implementation
- Mocking framework: a software library that makes it easier to create test doubles within tests
by allowing replacing an object with a mock
- -> Don't need to define a test double class -> reduce boilerplate 
- Mock: a test double whose behavior is specified inline in a test
- Fake: a lightweight implementation of an API that behaves similar to the real implementation
but isn't suitable for production (eg in-memory DB)
- Stubbing: the process of giving behavior to a function that otherwise has no behavior by specifying what values to return
- Interaction testing (mocking): a way to validate how & whether a function is called
without actually calling the implementation of the function
- UAT: automated test that exercise the product through public APIs to ensure the overall beha for specific user journeys
- Prober: function test that run encoded assertions against the production env
- Deprecation: the process of orderly migration away from and eventual removal of obsolete systems
- Version control system: system that tracks version of file over time,
by maintaining metadata about the set of file being managed
- Repository: a collective copy of files and metadata in VCS
- Static analysis: programs analyzing source code to find potential issues that can be diagnosed
without executing the program
- Semantic versioning:
  - Def: the practice of representing a version number for some dependency (esp libs) using 3 decimal-separated integers
  - Types of versions:
    - Major: breaking change to an existing API
    - Minor: purely added functionality, backward compatible
    - Patch: low risk non-API-impacting implementation details & bug fixes
- Large-scale change (LSC): any set of changes that are logically related
but cannot practically be submitted as a single atomic unit
- Haunted graveyard: a system that is so ancient, obtuse or complex that no one dares enter it
- TAP: Google CI framework
- Continuous integration (CI): the continuous assembling and testing of our entire complex and rapidly evolving system
- Continuous build (CB): integrate the latest code changes at head & runs an automated build & test
- Release candidate (RC): a cohesive, deployable unit created by an automated process, assembled of code, configuration,
and other dependencies that have passed the continuous build
- Continuous delivery (CD): a continuous assembling of release candidates, followed by the promotion and testing
of those candidates throughout a series of environments - sometimes reaching production and sometimes not
- Cattle versus pets