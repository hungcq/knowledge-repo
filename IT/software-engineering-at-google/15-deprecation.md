## 15. Deprecation
### Overview
- Goal: remove redundancy & complexity that builds up in a system over time
- -> Reduce resource costs & improve velocity
- Deprecation scope: range from individual function calls to entire software stacks
- Scope of chap:
  - Code-level deprecation
  - Technical systems, not end-user products
  - System owner has visibility into its use

### When to deprecate
- When: better alternatives exist
- -> In the long run, extra cost of old system become significant (operation & maintenance)
- Amount of deprecation work should be limited to:
  - Focused effort
  - Reduce impact on users

### Difficulties
- Affect users
- Dif between old & new system -> lots of tradeoffs
- Human tendency: emotional attachment, change aversion
- Visible deprecation cost & unclear benefit
- -> Need to research & measure
- -> Focus on incremental, small changes that deliver benefit

### Deprecation during design
- Affect design decisions. Considerations:
  - Users' migration effort
  - Incremental replacement plan
- -> Many are related to how a system provides & consumes dependencies

### Types of deprecation
- Advisory deprecation:
  - Def:
    - Don't have a deadline
    - Aren't high priority for the org
  - Goal: advertising the existence of a new system
  - When: new system offers compelling benefits
- Compulsory deprecation:
  - Def: usually comes with a deadline for the removal of obsolete system
  - How to scale: done by 1 team of expert. Advs:
    - Reuse expertise
    - Reduce burden to users
  - Need enforcement mechanism
  - -> Allow deprecating team to break non-compliant users

### Tools
- Types:
  - Discovery: find users & how they use the system, before & during migration:
    - Static analysis
    - Logging & runtime sampling
    - Tests on dependency behavior
    - Planned outage
  - Migration:
    - Code generation
    - Review tooling
  - Preventing backsliding:
    - Static analysis
    - Alerting/deprecation warnings: should be:
      - Actionable: specify how to migrate
      - Relevant: show at the right time
      - -> Avoid creating alert fatigue & being ignored
    - -> Can help to prevent new users but rarely lead to migration of existing systems

### Process
- Similar to other SE projects
- Need explicit project owners
- Need concrete, incremental, beneficial milestones