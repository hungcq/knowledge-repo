# Category: software engineering

# Structure
## Simple outline
- Culture:
  - Collective nature of software development enterprise
  - -> Dev is team effort
  - Proper culture principles
  - -> Org to grow & stay healthy
- Processes: familiar engineering process
- -> Best practices, tested at Google
- Tools:
  - How to use tools to benefit the codebase
  - Describe Google tools & provide 3rd party alternative
## Outline
- Preface:
  - Basic concepts
  - Problems & solutions
  - Scope
  - 3 SE principles
  - Structure
- Part 1:
  - Chap 1: basic concepts in SE with examples:
    - Time & change
    - Scale & efficiency
    - Tradeoffs & cost
    - SE vs programming
- Part 2: culture:
  - Chap 2: team work: how
  - Chap 3: growing knowledge: individual & organization
  - Chap 4: equity & diversity: in product & culture
  - Chap 5, 6: leading: concepts, principles, scale
  - Chap 7: productivity measurement: why, when and how
- Part 3: processes:
  - Chap 8: style guides & rules: why, how to create, maintain & apply
  - Chap 9: code review: why, how, types
  - Chap 10: documentation:
    - Overview: def, advs
    - Best practices: audience, workflow, audience, structure, deprecation, technical writers
    - Types & content of each type
  - Chap 11, 12, 13, 14: testing:
    - Why, how, history at Google, limitation
    - Unit test, test double, larger tests: why, how, concepts, types
  - Chap 15: deprecation: why, difficulty, types, how
- Part 4: tools:
  - Chap 16: version control & branch management: concepts, how
  - Chap 17: code search: how, why, scale, tradeoffs
  - Chap 18: build system: why, how
  - Chap 19: code review tool: how
  - Chap 20: static analysis: why, how
  - Chap 21: dependency management: difficulty, how
  - Chap 22: Large scale change: concepts, difficulties, how
  - Chap 23: CI: concepts, how
  - Chap 24: CD: how
  - Chap 25: compute as a service: how, types, scale
- Part 5: conclusion

## Detailed structure
- Chap 16: version control and branch management:
  - Overview: def, comparison with other approaches, functions, centralized vs distributed VCS
  - Branch management practice: analysis & recommendations
  - Google practice: dependency management, branch management, monorepo
- Chap 17: code search:
  - Functionalities
  - Goals of code search & corresponding functions
  - Advs of separate web tool
  - Challenges
  - Google implementation details
  - Tradeoffs in code search implementation
- Chap 18: build systems & build philosophy
  - Overview: function & goal of a build system
  - Types of build systems: mechanism, advs & disadvs
  - Considerations when choosing build system
  - Best practice for managing modules & dependencies
- Chap 19: code review tool:
  - Code review tool principles
  - Google code review process & corresponding features of the review tool
- Chap 20: static analysis:
  - Overview: def, advs, chars of effective static analysis tool
  - Recommended static analysis process
  - Review of Google's static analysis tool

# Author problems & solutions
- Current SE theory & practice are not very rigorous
- -> Share Google collective exp (why: scale & many years of exp)
- -> Path toward more reliable software practices
- Provide 3 principles to consider when designing, architecting & writing code
- -> Able to react to necessary change
- Describe lessons that a typical SE should learn on the jobs: culture, process & tools
- -> Can be applied directly or adjusted to specific problems
- Not cover: software design & development
- -> Focus on engineering, not programming
- (Also in outline)

# Presentation & styles
- Author claim:
  - Link 3 principles throughout the chapters
  - -> How they affect engineering practice
  - Not everything described is perfect
- Written by many authors: collected & organized into a book
- Not very condense: lots of example, can be read fast

# Terms
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
- Psychological safety: dare to take risk/make mistake in front of others

# Criticism
- Chap 1 discuss at quite a high level: need familiarity with many concepts to understand the examples
- 2 chaps about leadership are high level and self-help style
- -> Need real life experiments to see whether the strategies work & how to apply them in specific situations
- Chap 16: branch management: dev branch merge overhead should not be a problem with small microservices
- Chap 17: code search:
  - Too much boring technical details
  - Is the idea even remotely feasible for normal orgs?

# Take away
- How to write clear, resilient to change tests