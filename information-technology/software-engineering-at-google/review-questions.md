# Review questions

## Software engineering
- 3 main differences between SE & programming

## Culture
- What are the main sections of a postmortem?
- What is the philosophy of knowledge sharing?
- How to setup a psychologically safe env for knowledge sharing?
- What is the leadership philosophy?

## Process
- Code review:
  - Requirements
  - What shouldn't be done
  - Review criteria (see 3 types of approvals)
  - Point of focus when reviewing dif types of changes:
    - New feature
    - Behavior changes (API), improvements & optimizations
    - Bug fixes & rollbacks
- Documentation:
  - Main best practices
  - Criteria to categorize audience
  - Review criteria (see 3 types of reviews)
  - Questions to be answered in any doc
  - Doc structure
  - Doc types: reference, design, tutorial, conceptual, landing page
- Automated testing:
  - Advs over manual testing: see Notes
  - Test sizes: constraint, adv & disadv: see Notes
  - 3 testing activities
- Unit testing:
  - Chars of bad tests: see Notes
  - How to prevent brittle tests & unclear tests: see Notes
  - Code reuse in test
  - 4 types of code changes & what to do with tests
- Test doubles:
  - Real implementation: advs over test doubles, when to use
  - Test double techniques: def, advs, disadvs, use cases:
    - Faking
    - Stubbing
    - Interaction testing (mocking)
- Larger testing: chars, adv over unit tests
- Deprecation:
  - Goal
  - When to deprecate
  - Process, how to scale

## Tools
- Distributed VCS: def, disadvs
- WIP dev branch: disadvs
- Trunk-based development: process
- Task-based vs artifact-based build system: overall mechanism
- Limitations of semantic versioning
- Large scale change:
  - 4 types
  - Process
- CI:
  - Functions, from a testing perspective
  - Types of tests to run at:
    - Pre-submit
    - Post-submit
    - Release candidate (RC) testing
- CD:
  - Short-term operational fixes to mitigate risks & problems
  - Advs of early, frequent release
- CaaS:
  - Serverless mechanism
  - Public (vs private) cloud: advs, disadv & mitigations