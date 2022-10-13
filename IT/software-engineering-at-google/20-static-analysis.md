## 20. Static analysis
### Overview
- Advs:
  - Find bugs early
  - Codify best practice
  - Enforce migration (eg API)
  - Prevent/reduce technical debt
- Chars of effective static analysis:
  - Performance: can run on large codebase
  - Usability:
    - Understandable
    - Actionable & easy to fix
    - Process: 
      - Avoid bottleneck, show only to relevant people
      - Easy to submit feedback
  - Flexibility: num of analyses available, optional analyzer
- Tradeoffs: cost:
  - Code quality: fix dead code -> buggy, low benefit
  - -> Should focus on new code/edited code exception security/clean up
  - Dev time: auto fix -> ease the integration/upgrade

### Process
- Focus on dev happiness:
  - Measure effectiveness
  - Gather & act on feedback
  - Reduce false positive rate
- Make it a part of the core dev workflow: at pre-commit step, compiler,
IDE (higher performance requirement, higher complexity), code review
- Encourage contribution from domain expert, use plugin mechanism

### Google tool
- New features:
  - Focus on analyzing only affected files/lines
  - Tools that allow generating analyzer using sample code
- Other lesson: per-project customization, not per-user -> for consistency