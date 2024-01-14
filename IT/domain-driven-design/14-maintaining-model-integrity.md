# IV - Strategic design
- Problem: manipulate and comprehend large models
- -> Principles to scale the modeling process to large domain, at org level
- -> Involve both design & politics
- Goal: decompose while remain consistent & integrated
- Requirements:
  - Model must capture the conceptual core (vision) of the system
  - Design must be connected to impl

## 14. Maintaining model integrity

### Model unification
- Def
- -> A model is meaningless unless it is logically consistent
- -> Too costly to maintain across the entire org
- -> Need to allow multiple models to develop in dif parts of the system
- -> Need to consider which parts of the system will be allowed to diverge and what their rela to each other will be
- Risks of large-scale unification:
  - Wide-spread changes
  - Coordination overhead
  - Divergences outside of the model due to dif processes/politics/priorities/special requirements
  - Complex models when trying to satisfy every requirements
- Process:
  - Decide on what should be/not be unified
  - Maintain the unified parts & prevent confusion/corruption of the not unified parts
- Goal: reorganize, comm, choose the limits of a model & its relationship to the others
- Context components:
  - Bounded context: define the range of applicability of each model
  - Context map: give a global overview of the project's contexts and the relas between them
  - Continuous integration process to keep the model unified within a context
- img 14.1

### Bounded context
- Example situations of unclear but hard to recognize model boundary:
  - 2 teams working on dif functionality for the same new system
  - Conflicting interpretation or legacy code within a single team
- Process problems:
  - No demarcation criteria
  - No process to hold a shared model together
  - No process to detect divergences
- Consequences of unclear context:
  - Complex, buggy code that combines model
  - Confusing comm
- Root cause: the way teams are organized & the way people interact
- Process:
  - Define the context of a model explicitly
  - Explicitly set boundaries in terms of team org, usage within specific parts of the app
  & physical manifestations (eg code bases & DB schemas)
  - -> Keep the model strictly consistent within these bounds, but don't be distracted or confused by issues outside
- Translation mechanism:
  - Is not in the bounded context
  - Is part of the boundary itself
- When 2 teams working on a single unified system but are not working in the same bounded context
- -> Define the shared context & the rela between 2 related models of dif contexts before sharing code/data
- Symptoms of unrecognized model difs within a context:
  - Coded interfaces don't match up
  - Unexpected behavior
  - Confusion of language
  - Duplicated concepts
  - -> Duplicated changes, divergences
  - False cognates: the case when 2 people who are using the same term (or implemented object)
  think they are talking about the same thing, but really are not
  - -> Dev teams stepping on each other's code, DBs having weird contradictions & confusion in comm within the team

### Patterns to relate 2 models (model context strategies)
- 