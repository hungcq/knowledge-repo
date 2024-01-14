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
- Process when project is ongoing:
  - Define bounded context & context map as-is
  - Tighten up the team's practices around that current organization:
    - Naming context as part of the ubi lang
    - Improve CI within context
    - Refactor stray translation code
  - Consider change to boundaries & relas in small, incremental changes

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

### Continuous integration
- Observation: when a number of people are working in the same bounded context,
there is a strong tendency for the model to fragment
- Causes of divergence:
  - Lack of understanding of the original intent of the model
  - Not aware a concept has been used somewhere else
  - Duplicate to avoid affecting existing functionality
- -> Need to increase comm and reduce complexity & create safety nets that prevent overcautious behavior
- Process:
  - XP
  - Continuous integration
  - -> Caught & correct divergence early
- CI practice:
  - 2 levels of operation:
    - Integration of model concepts: cultivate a shared understanding of the ever-changing model
    - Integration of impl: systematic merge/build/test process that exposes model splinters early
  - Set some reasonably small upper limit on the lifetime of unintegrated changes
  - Only applied within a single bounded context

### Context map
- Problem: people on other teams won't be aware of the context bounds
- -> Unknowingly make changes that blue the edges or complicate the interconnections
- -> Blend dif contexts into each other
- Goal: reduce confusion by defining the rela between dif contexts
& creating a global view of all the model contexts on the project
- Context map involves team org & software design
- -> Still need a clear view into the ongoing conceptual subdivision of the software model and design
- Process:
  - Identify each model in play on the project and define its context
  - Name each context & make the names part of ubi lang
- Map documentation:
  - Can be in any form (including informed discussion)
  - Requirements:
    - Shared & understood by everyone on the project
    - Provide a clear name for each context
    - Make the points of context & their natures clear
    - Represent the current situation, not the ideal
  - Name all the contexts
  - Document & comm the boundaries:
    - Code: organize into services/modules
    - Discussion: informal diagrams
- Main goal: map the rela
- -> Can refactor the divergence/rela but not required
- -> Update the map only after the change is done
- Example: Img 14.3
- Best practices:
  - Some translations are impossible due to ambiguous mapping
  - For simple case, create a Translator object/function to translate between 2 models
  - Need to choose which service to have respon to coordinate interactions
  - Should have automated tests at the boundary

### Patterns to relate 2 models (model context strategies)
- Include description & organization
- Cover imp cases
- -> Suggestions for other cases
- Dif stages of model integration:
  - Separate parts
  - Crude integration: recognize & integrate parts of a larger whole
  - Integrate into a deeper model: based on new insights to create new concepts & clear relas
  - -> Depending on the requirements, might not need to reach later stages
- Recognizing the incompleteness of the model in each context is imp for integration
- Guideline to choose model context strategy after having the context map:
  - Team decision or higher:
    - Regarding:
      - Scope of bounded contexts
      - Their rela
    - Should be made by teams or at least understood by everyone
    - Should be based on cost-benefit analysis
    - -> Often involve team politics in reality
    - -> Should still try to assess & comm the tradeoff
  - Should be aware of the primary contexts (to be dev/changed) & supporting & external contexts
  - Considerations when choosing context size:
    - Small context advs:
      - Reduce cmm & continuous integration overhead
      - Easy to model
      - Specialized model & system
    - Large context advs:
      - Straight forward user flow
      - Easier to understand model of the whole system
      - No need for translation
      - Shared ubi lang
  - Identify & segregate from the design systems not in any bounded context. Examples:
    - Legacy system that is big and can't be changed immediately
    - External service systems
  - Number of bounded contexts within a project:
    - 1: suitable for team with < 10 people
    - Many contexts with customer/supplier or shared kernels: larger team
    - Separate ways: when can't resolve model conflict
    - -> Integrate via a translation layer. General guide: 1 team per context.
  - Cater to special needs with distinct models & contexts & dialects of ubi lang
  - -> Should balance between cost & benefit of integration
  - Deployment:
    - Difficulties:
      - Dependencies
      - Compatibility: between systems (deps) & inside system (gradual release)
    - -> Use contexts & rela to identify difficult spots
    - Use deployment feasibility as a feedback signal to refactor the context boundary
    - -> Translation is easier to deploy than shared kernel
- -> Tradeoffs sum:
  - Benefits of seamless integration of functionality against additional effort of coordination & comm
  - Independent action against smoother comm
- Img 14.13

#### Shared kernel
- Def
- -> Usually the core domain, some set of generic subdomains, or any part of the model that is needed by both teams
- Goals:
  - Reduce but not eliminate duplication
  - Ease the integration between 2 subsystems
- Best practices:
  - Any change needs to be coordinated
  - Create automated tests on the shared part
  - Can't be used when dif impl techs are used

#### Customer/supplier development teams
- Upstream & downstream subsystems separate naturally into 2 bounded contexts
- Problem: dif incentives & conflict of interest between 2 teams:
  - Upstream can but reluctant to change
  - Downstream needs change but can't change
- Process:
  - Establish customer/supplier rela between downstream/upstream team
  - Negotiate budget tasks during upstream team's planning sessions
  - Jointly develop automated integration tests to be run by upstream team during CI
  - -> Need explicit comm when changing or breaking tests
  - Need to share upper management to have shared goals
- Examples:
  - BI team vs product team
  - Product team vs infra team

#### Conformist
- Situation: can't establish customer/supplier rela between downstream/upstream team
- Solutions:
  - When the value of the dep not worth the cost of maintaining: abandon the upstream
  - -> Separate ways pattern
  - When the value of the dep is high or rela is required:
    - Bad upstream design: downstream devs its own model & handles translation
    - -> Anticorruption layer
    - Ok upstream design: use the upstream model
    - -> Conformist pattern
- Advs:
  - Shared ubi lang
  - Simplify integration
- Disadvs:
  - The model might not be ideal for downstream team
  - At the mercy of upstream team
- Similar to shared kernel except the lack of collaboration
- Design:
  - Place yourself in the bounded context of the other system
  - Only extend, not change the existing model

#### Anticorruption layer
- Problem: when systems based on dif models are combined,
the need for the system to adapt to the semantics of the other system can lead to a corruption of the new system's own model
- -> Create an isolating translation layer to provide clients with functionality in terms of their own domain model
- Should consider benefit of isolation against the cost of maintaining it
- -> Should make periodic revision to the model to fit more with foreign ones
- Design:
  - Public interface: usually appears as a set of services, although occasionally as an entity
  - Can break down an external system into multiple services, each with a coherent respon in terms of our model
  - Can be bidirectional: to handle the case of serving reqs or receiving events from other system
  - If integration is extensive, might need to change the model to be closer to the model of the other system
  to make translation easier
  - -> Should not compromise the integrity of the model
  - -> Can also consider conformist
  - Functionality can be added to the anticorruption layer if it is specific to the rela of the 2 systems (eg audit, trace/logging)
- Impl:
  - Patterns: facade, adapters, translators:
    - Client -> service -> adapter -> facade of the other system
    - Adapter call translator to do object/data conversion
    - Facade is optional if the other system have simple/clean interface
  - Include comm and transport mechanisms to talk between systems
  - If have access to the other system, can refactor its interface or add automated tests to ease the integration
- Img 14.8

#### Separate ways
- Integration is expensive. When benefit is small, strive for isolated bounded contexts without any integration
- -> Later reintegration might be costly

#### Open host service
- ~ define & maintain a simple API
- -> Use a one-off translator for special cases

#### Published language
- ~ standardized comm protocol
- -> Can change model internally without affecting the interface

### Transformations
- Imp changes in bounded contexts & their relas
- -> Transformation plans: as a manageable steps
- -> Need adaptation to specific circumstances
- Process (refer to book):
  - Merging contexts:
    - Separate ways -> shared kernel
    - Shared kernel -> CI
  - Phasing out a legacy system
  - Open host service -> published language