## 15. Distillation
- Problem: in a large system, even the isolated domain may be unmanageably complex
- Advs:
  - Aid all team members in grasping the overall design of the system & how it fits together
  - Facilitate comm by identifying a core model of manageable size to enter the ubi lang
  - Guide refactoring
  - Focus work on areas of the model with the most value
  - Guide outsourcing, use of off-the-shelf components & decisions about assignments
- Chapter goal:
  - Layout systematic approach to strategic distillation of the core domain
  - Explain how to effectively share a view of it within the team & provide a language to walk about what we are doing
- Img 15.1

### Core domain
- Problems of big, complicated model:
  - Specialization
  - -> Reduced knowledge transfer & integration, lack of flexibility in assigning work, duplication
  - Skilled devs gravitate towards technical infra & other specialized domain problem
  - -> Without a good core model, app lose the core value
- Core domain def:
- Goals:
  - Make the core small & distinguishable from supporting model
  - Focus talent & product resources to features & development & refactoring of the core model
- Choosing the core:
  - Can be identified throughout one project, and usually throughout one company
  - Should evolve through iterations
- Who should model core domain:
  - Skilled, long-term committed devs + domain experts
  - Temporary expert: hire as mentor, not designer
  - -> Avoid losing knowledge
  - Avoid pre-designed framework: lack of control
- Distillation techniques & increasing level of redesign, refactoring & commitment:
  - Domain vision statement, highlighted core
  - Generic subdomains, cohesive mechanisms
  - Segregated core
  - Abstract core
- Continuously refactor core & subdomains, not only separating them
- Choose refactoring target:
  - XP refactoring starting point:
    - Anywhere
    - Paint points encountered while working on a task
  - -> Impractical, lack of focus on root cause
  - Suggestions:
    - Pain driven refactoring: find & fix the root cause
    - Free refactoring: focus on core domain & its distillation

### Distillation techniques

#### Generic subdomains
- Def
- Chars:
  - You would like to take for granted
  - Abstract concepts probably needed for a many business
- Examples:
  - Corporate org chart
  - Dates & times with time zones
  - Money & multi currency
  - Is infra functionalities also counted as subdomain?
- Process:
  - Identify cohesive subdomains
  - Factor out generic models of these subdomains & place them in separate modules
  - Can give their continuing development lower priority than the core domain & avoid assigning core devs to the tasks
- Impl:
  - Try to apply outside expertise. Rationale:
    - No deep understanding & learning required
    - Less confidentiality concern
    - Reduce effort
  - Options when developing these packages:
    - Option 1: use off the shelf solution:
      - Advs: reduced effort, mature & stable solution
      - Concerns: quality, integration, dependency
    - -> Worth investigating, but usually not worth the trouble
    - Option 2: use published design/model (eg accounting, physics, those in analysis patterns):
      - Advs: more mature, available docs
      - Concerns: might not fit the needs
      - -> Need to extract relevant parts or customize
    - Option 3: use outsourced impl:
      - Can be well-combined with option 2
      - Advs: reduced effort & personnel cost, force separation via API
      - Concerns: integration effort, overhead of transferring ownership, code quality
      - -> Should require/leverage unit & integration tests
    - Option 4: in-house impl:
      - Can be well-combined with option 2
      - Advs: easy integration, meet the needs
      - Disadvs: increased effort, risk of underestimation of effort
- Should not concern too much with the reusability of that code, which cost more effort
- -> Can reuse model instead of code
- Agile process:
  - Talking the riskiest tasks early via prototype
  - Technical risks vs domain modeling risks: depending on project
  - Domain modeling risk is usually higher
  - -> Avoid the temptation to build prototype for generic subdomain/technical concerns

#### Domain vision statement
- Focus on the nature of the domain model & how it is valuable to the enterprise
- -> Dif from requirements
- Usage: by management & technical staff during all phases of development to:
  - Guide resource allocation
  - Guide modeling choices
  - Educate team members
  - Show how dif functionalities are balanced
- Format: short description (about one page)
- Process: write early & revise after gaining new insight

#### Highlighted core
- Problems:
  - Mental cost of constantly identifying the core from the model
  - Redesigning & separating the generic subdomains take time & effort
- Goal: mark off the core & related impl
- Advs:
  - Lightweight solution to identifying the core
  - Serve as documents
- 2 techniques:
  - Distillation doc:
    - Def: a separate doc to describe & explain the core domain
    - -> Not a complete design doc
    - Forms:
      - A list of the most essential conceptual objects
      - UML diagrams of crucial objects & relas
      - Sequence diagrams of fundamental interactions
      - Any combinations/other informal diagrams
    - -> Should be understandable to non-technical members
    - Content (3-7 pages);
      - Description of core domain
      - Primary interactions among core elements
    - Disadvs:
      - Extra maintenance cost
      - Duplication
      - Negligence
    - -> Keep the doc minimal to avoid getting outdated
  - Flagged core:
    - Forms:
      - Page tabs
      - Highlight
      - Code comments
    - Usage: for big documents or when lacking docs
- Code change process & distillation doc:
  - Change on domain layer might have a big impact
  - -> Can use distillation doc to evaluate impact of a change: big impact when changing the core
  - Should consult when changes also affect the distillation doc
  - Should notify all team members of the change & the change to distillation doc
  - -> Not necessary when making other changes because they are not critical

#### Cohesive mechanism
- Separate specialized or formalized algos/computations into a separate framework/lib (eg graph)
- -> Separation of concerns: keep the model simple & flexible
- Refactor to/from generic subdomain, depending on whether the computation is pure or is mixed with model elements
- A mechanism can be part of the core domain when it is proprietary and a key part of the value of the software
  (eg highly specialized software)
- Design: encapsulate mechanisms via an intention-revealing interface
with conceptual coherent assertions & side-effect-free functions

#### Segregated core
- Difficulties of separating core:
  - No clear division of core/supporting role
  - Coupling
  - Low payoff from refactoring
- Def: separate core into its own package. Place other objects into the packages. Refactor the rela to be simpler/more communicative.
- -> No need to figure out what to do with those. Insight might appear later.
- Cost:
  - Breaking cohesive module
  - -> Complicate the rela
  - Lots of refactoring
- Usage: when the model is too big
- Process:
  - Team agreement
  - Synchronize between team members via comm: insights & decision

#### Abstract core
- img under title
- Problem: even the core domain model usually has so much detail that comm the big picture can be difficult
- Def: refactor interaction between subdomains in separate modules into a special core module (~ a manager)
- -> Must be based on domain insight