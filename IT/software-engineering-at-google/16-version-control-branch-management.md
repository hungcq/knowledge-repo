# IV - Tools
## 16. Version control and branch management
### Overview
- Functions:
  - Allow separate storage & reference to versions over time
  - -> Allow reversion to mitigate failure
  - Allow coordination between multiple dev and/or multiple points in time
  - Support auditing for legal & regulatory practices
  - Trigger non-technical changes in behavior (eg check code before committing)
- Distributed VCS: 
  - Built around the idea of downloading the entire codebase & having access to it locally
  - Disadvs:
    - Hard to scale to large repo/codebase
    - Require more explicit policy & norms to specify the source of truth
- Dif between VCS & dependency management: manage your own code vs manage projects owned by other orgs
### Branch management
- Work in progress ~ branch
- Dev branch as a way to control risk of regression. Problems:
  - Big change accumulates risk
  - Hard to trace bug
  - Scale: increased number of dev branches -> expensive & risky merge conflict
  - -> More effort needed to coordinate branch merge strategy
- Alternative paradigm to reduce merge overhead:
  - Trunk-based development
  - Extensive use of tests, CI (eg keep the build green) & quality enforcement practices (eg code review)
  - Disable incomplete/untested features at runtime
- Release branch:
  - Function: represent the exact code that went into the release build for the product
  - Fix bug: small merge from master to release
  - Use cases:
    - Irregular release
    - Control which version is released
  - Best practice:
    - Should not re-merge with trunk
    - Can be removed after CD adoption
  - Might be needed for outsource project
### Google practice
- One version rule: for every dependency in the (mono) repository,
there must be only one version of that dependency to choose from
- -> Forking needs repackaging or renaming
- No long-lived branches: work should be done in small increments against trunk, committed regularly:
  - Goal: reduce work in progress
  - 2 approaches to design new feature:
    - Coexist with old feature
    - Use feature toggle, visibility control
  - Exception: mainly for compatibility, should be rare & discouraged
- Monorepo:
  - Depend on use cases. Imp point: maintain one-version rule for consistency & reduced complexity.
  - Can leverage VCS & build systems to have sth similar to monorepo
### Additional info
- Google devops research and assessment (DORA):
suggest strong positive correlation between trunk-based dev, no long-lived dev branches & good technical outcomes