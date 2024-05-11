## 22. Large-scale changes
### Overview
- Author problems:
  - Discuss techniques, both social and technical, that enable Googlers to keep the large codebase
  flexible & responsive to changes in underlying infra
  - Provide real life examples of how and where they have used those approaches
- Types of changes:
  - Clean up
  - Deprecation
  - Low level infra improvement
  - Migration
- Infra teams perform most parts of LSCs, but tools & resources are available across the company
- LCS can be reused for small/non-functional changes
### Reasons why many kinds of changes can't be committed atomically
- Technical limitation of VCS
- Increased risk of merge conflict
- Haunted graveyard
- -> Need thorough testing -> can change with confidence
- Heterogeneity in system, process & tech
- Large amount of tests that need to be run & high amount of potential failure
- -> Hard to fix & debug
- Review large, single commit is tedious & error-prone
### LSC infra
- Policy & culture:
  - Approval process by language expert & domain expert
  - -> Make sure there is oversight & thoughtfulness in the change
  - Cultural norms: product teams to trust domain expertise of infra teams
- Change generation: large scale analysis & generation via tools
- Change management platform/tooling:
  - Shard a master change into smaller pieces
  - Manage process of testing, mailing, reviewing & committing the shards independently
- Testing: shard the change & run tests against each shard
- Language support:
  - Type aliasing & forwarding functions
  - Statically typed, compiler-based
  - Automatic language formatters
### LSC process: 4 phases
- Authorization:
  - Proposal: design decision & consideration
  - Approval
  - Submission
- Change creation: edit code
- Sharding & submitting:
  - Based on project boundaries & ownership rules, shard into changes that can be submitted atomically
  - Put each individually sharded change through an independent test-mail-submit pipeline:
    - Review: send to local owners only when domain knowledge is required, otherwise send to global approver
    - Submit: do pre-commit check first
- Clean up:
  - Depend on change
  - Deprecation tools can be used to prevent back-sliding to old usage