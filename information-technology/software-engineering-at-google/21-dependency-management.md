## 21. Dependency management
### Problems
- Direct vs transitive dependency
- Conflicting upgrades: diamond dependency: lib a & lib b use dif version of lib base
- -> Problem: can't include both version of lib base into one build (depending on language)
### Importing dependency
- Tradeoff: maintenance cost vs dev cost
- Considerations:
  - Have runnable tests?
  - Tests passed?
  - Who is the provider? Any reputation?
  - Compatibility promise
  - Supported usage?
  - Popularity
  - How long to depend on the project?
  - Frequency of breaking changes
  - Internal questions:
    - How complicated to self-implement it?
    - Any incentive to keep the dep up to date?
    - Who will upgrade?
    - Difficulty of upgrade
- Should aim for source control over dep management: dev it yourself
### 4 common solutions
- Change nothing: unrealistic assumption of indefinite stability: there are security issues, bugs
- -> Suitable for startup: not sure about the lifespan of the project yet
- Semantic versioning:
  - Current standard
  - Mechanism of package management system: given a set of constraints (version requirements on dep edges),
  find a set of versions for the nodes in questions that satisfies all constraints
- Bundled distribution: distributors find, patch & test a mutually compatible set of versions, then bundle together
- Live at head:
  - Def: always depend on the current version of everything & never change anything
  in a way which makes it difficult for dependents to adapt
  - Practice: dep providers test changes against the entire ecosystem before committing
  - Make a break only if either:
    - Dependents are updated
    - Automated tool is provided to perform the update in place
  - Incentive structures & technological assumptions:
    - There exist unit tests & CI
    - API providers are bound by whether dependents are broken
    - API consumers keep their tests passing & relying on their dep in supported ways
### Limitations of semantic versioning
- Version value is provided by the maintainer as an estimate of how compatible the new version is,
given the code that used the previous version
- -> Lossy estimate:
  - Over-constrain: major version change even though clients don't depend on the breaking API
  - Over-promise:
    - Version estimate of the providers might not be correct
    - Users might depend on part of the API that is not in the contract
  - -> Breaking or non-breaking is not well-defined: depend on how the API is used
  - No incentive for providers to create stable code
- -> Hard to scale: suitable when there are only a few carefully chosen & well-maintained dep in the dep graph
### Practical proposal: make use of info about dependent
- -> Run test against all dependents or a selected subset (eg big/reliable dependents or dependents affected by the change)
- -> Need compute resource & usable unit tests
### Additional info
- Risks of exporting deps:
  - Reputation risk when not maintaining it properly
  - Engineering efficiency: delay internal project
  - -> Might need internally forked version -> abandon external version
- Minimum version selection: upgrade/use the lowest version that satisfies the requirement
- -> Closest to the version used for development/testing