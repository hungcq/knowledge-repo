## 9. Code review
### Overview
- Require:
  - Process
  - Supporting tools
- Shouldn't: debate previous design decisions
- 3 types of approval needed from 3 roles (goal: flexibility -> scalable):
  - Another engineer: functional correctness & understandability
  - Code owner: suitable for the repo
  - Engineer with the language's readability: consistency of style
- -> Usually done by 1 person, or the author performs both role 2 & 3
### Advs
- Code correctness
- Comprehensibility: optimized for readers
- Consistency
- Psychological & cultural benefits:
  - Responsibility
  - Openness to criticism
  - Validation/recognition of one's work
  - Being more careful
- Knowledge sharing
### Best practices
- Be polite & professional:
  - Ask for the reason before assuming sth is wrong
  - If not agree with reviewer: offer an alternative & ask reviewer to take another look
- Write small changes: ~200 lines
- -> Easy to review & rollback
- Write good change descriptions: list the changes briefly
- Keep num of reviewers to a minimum -> easy to scale
- Automate where possible
- Types of code reviews for dif types of changes:
  - New feature: focus on sustainability
  - Behavior changes (API), improvements & optimizations: focus on:
    - Benefit
    - Update/ensure tests work correctly
  - Bug fixes & rollbacks: focus on:
    - Fix the bug only
    - Update test to catch the error
  - Refactoring & large-scale changes:
    - Low-risk: reviewed by owners of the entire codebase
    - High-risk/local expertise needed: reviewed by individual engineers:
      limit comments to concerns specific to local code, not the tool -> scalable