# Category: software engineering

# Outline
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

# Structure
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
  - Chap 10: documentation: concept, why, how
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

# Arguments
## I - Thesis
### 1. What is software engineering
- SE vs programming: 2 dif problem domains with dif constraints, values & best practices -> dif tools
- 3 difs between SE vs programming: time, scale & tradeoffs:
  - Time & change (most imp):
    - Time add a new dimension to programming: code needs to be sustainable
    - <img src="../resources/software-engineering-at-google/1.png" alt="drawing" width="500"/>
    - Require planning & manage impact of required change
    - -> Need practice & expertise
    - Hyrum's law: given enough time & users, all observable behaviors of a system will be depended by sb, no matter what you promise in the contract
    - -> Changes always introduce breakage & have to consider tradeoffs of such breakages
    - Why change is needed:
      - Issue: underlying tech change (eg fix security issue)
      - Opportunity: efficiency improvement
      - Product requirement
  - Scale & efficiency:
    - Everything your org relies upon to produce & maintain code (do repeatedly) should be scalable in terms of overall cost & resources consumption
      (eg human, compute resources of dev, codebase)
    - SE is team effort: need to be able to scale both projects & org
    - Examples of policies that don't scale:
      - Dev branch: merge overhead
      - Forcing users to do deprecation
      - -> Should update in-place or migrate the users -> make use of expertise
    - Take adv of scale:
      - Automation
      - Consolidation/consistency -> low level changes have limited problem scope
      - Expertise
      - Find problems earlier in the dev workflow to reduce cost
  - Tradeoffs & costs:
    - Complex decisions: need to consider cost when deciding between 2 engineering options
    - Stay rational: adjust decision when new data is available
    - Types of cost:
      - Financial
      - Resources
      - Personnel
      - Transaction (cost to act this way)
      - Opportunity
      - Societal
      - Psychological (employees' happiness)
    - Types of decision:
      - Quantifiable cost & benefit
      - -> Straightforward: consult table of cost of dif types of resources
      - Not quantifiable:
        - Should treat with same priority & greater care
        - Rely on exp, leadership & precedents

## II - Culture
### 2. How to work well on teams
- Tendency to hide WIP so people won't judge
- -> Part of bigger problem: want to be seen as genius
- -> Only a myth: great works are result of collaboration
- Why shouldn't hide:
  - Early detection of mistake -> reduced cost
  - Have backup -> reduced risk
  - Advice to problems, shared knowledge -> efficiency
- SE is a team endeavor
- 3 pillars of social interaction:
  - Humility
  - Respect
  - Trust
- -> Good rela will help get the work done
- Creative nature of SE requires risk being taken & mistake being learned
- -> How to learn from mistakes: document failures by performing root-cause analysis & writing a postmortem describing:
  - Summary of the event
  - Timeline
  - Primary cause
  - Impact & damage
  - Immediate actions to fix
  - Preventive actions
  - Lessons learned

### 3. Knowledge sharing
- Summary: mechanism & culture to share knowledge effectively
- Challenge to learning:
  - Lack of psychological safety
  - Info islands. Consequences:
    - Info fragmentation
    - Info duplication
    - Info skew: dif, conflicting way of doing the same thing
  - Single point of failure
  - All or nothing expertise: 2 groups:
    - Know everything: accumulate knowledge & responsibility
    - Novice: lag behind
  - Parroting: copy without understanding
  - Haunted graveyards: code people avoid touching because they afraid sth might go wrong
- Philosophy: combine personalized help with documentation (scale better but has maintenance code)
- Set up psychologically safe env via:
  - Mentorship: safe to ask
  - Groups: via rules for interation
- Grow personal knowledge:
  - Ask questions
  - Understand context
- Dif approaches to ask the community:
  - Group chats: less structured, hard to document
  - Mailing lists: clumsy, suited for complicated questions
  - Q&A platform: same advs as mailing list, but more usable & editable
- Why ask the community:
  - Can get help from broader community
  - Answers are broadly available to others in the community
- Other stuffs about Google knowledge sharing culture:
  - Tech talks & classes
  - Documentation
  - Newsletter
  - Communities
  - Code style review

### 4. Engineering for equity
- Responsibilities of engineers when designing products for a broad base of users
- -> How: org embraces diversity
- How to ensure equity:
  - Build multicultural capacity:
    - Make data set comprehensive, cover all groups
    - Increase diversity in the workforce
    - Educate to increase awareness
  - Focus on actionable & comprehensive approaches
  - Challenge established processes
  - Consider tradeoff between product velocity and inclusivity

### 5. How to lead a team
- Goal:
  - For leaders: people management & technical leadership
  - For others: understand leaders better
- 3 types of role:
  - Engineering manager: people & product aspect
  - Tech lead: technical & project management aspect
  - Tech lead manager (combine both roles): for new, small teams
- Difficulties:
  - Hard to measure impact
  - Less time coding
  - Afraid not able to
- Why lead: increase impact: scalable job
- How:
  - Serve the team: remove obstacles, create good technical & social env
  - Focus on what things should be done, trust the team to figure out how to do it
- Anti-patterns:
  - Hire pushover -> need to tell them what to do everytime
  - Ignore low performers:
    - Team spirit down: having to carry
    - Solutions: work with them early, set small incremental goals
    - -> Meet expectation: OK. Not: out.
  - Ignore human issues: need to show understanding & sympathy
  - Be everyone's friend: to soft. Don't have to.
  - Compromise the hiring bar -> low performers
  - Treat your team like children
- Positive patterns:
  - Lose the ego:
    - Trust
    - Appreciate rational discussion & constructive criticism
    - Sincerely apologize when making mistakes
  - Remain calm: always observed & have emotional impact on others
  - When people ask for advice:
    - Don't try to solve the problem
    - Help them solve by asking questions to refine & explore the problem
  - Be a catalyst: build consensus
  - Remove roadblocks (eg technical/org): solve or find the right person to solve
  - Be a teacher & a mentor: give people time to learn on their own
  - -> Must balance with product priority
  - Set clear goals: create concise mission statement for the team
  - Be honest: situations:
    - Can't tell sth/don't know sth -> admit it
    - Give criticism:
      - Don't use compliment sandwich to soften the blow
      - -> Listener will miss the critical message
      - Be kind, honest & to the point
  - Track & ensure happiness
  - Give complements & ack
  - Insulate team from unrelated, org problems

#### Additional info:
- Attributes of a mentor:
  - Experienced with your team's processes & system
  - Explanation ability
  - Ability to gauge how much help the mentee needs
- Common career goals:
  - Be promoted
  - Learn sth new
  - Launch sth imp
  - Work with smart people

### 6. Leading at scale
- Problem: how to lead a set of related teams
- Decision-making process when solving ambiguous, high-level problems:
  - Identify the blinder: bigger picture view, new perspective
  - -> Ask questions about previous assumptions
  - Identify the key tradeoffs
  - Decide, then iterate/re-evaluate the tradeoffs & re-decide
- Build self-driving team
  - Aim: you are no longer single point of failure
  - How:
    - Divide the problem space, delegate to team leaders
    - Spend most time observing & listening, then make critical judgement/decision
- Success generates more responsibilities & work over time
- -> Scale your own time & attention & protect your energy:
  - Divide imp & urgent tasks: focus on imp tasks:
    - Delegate
    - Schedule dedicated time
    - Use a tracking system
  - Divide & drop 80% unimp work: will be handled by others or will make itself noticeable
  - Take break & occasion to recharge

### 7. Measuring engineering productivity
- Goal:
  - Improve SE productivity -> can scale
  - Measure efficiently
- Hard to measure
- -> Create productivity specialist team: multi-discipline -> understand both tech & human aspects
- How to decide whether it is worth measuring:
the data help stakeholders make a decision, not to prove/disprove a hypothesis
- Goals/signals/metrics framework to guide metric creation:
  - Goal
  - Signal:
    - How you might know that you have achieved the end result
    - Might not be measurable
  - Metric:
    - Proxy to a signal
    - Measurable
- -> Benefits:
  - Avoid bias
  - Decide & ack in advance what is measurable
  - Maintain traceability (ie what this metric is for)
- Insights from qualitative metrics:
  - Contexts/narrative
  - Next steps to improve a process
  - Validation for quantitative metrics
- Final step:
  - Take action: improve tools & processes
  - Track result

## III - Processes
### 8. Style guides and rules
- Rule: not strictly prescriptive: might need judgement
- Guidance (dif vs rule): best practice, not strictly enforced
- Goals:
  - Sustainability
  - Productivity: let dev focus on dev, not style
- Rule creation:
  - Focus on goal
  - Principles:
    - Brief: imp point only -> easy to remember & apply
    - Optimized for readers, not writers
    - Consistent:
      - Easy to understand, esp for people who switch projects
      - Take adv of tools to scale
      - Avoid having to decide everytime
    - -> Think long-term, adhere to widely accepted standard
    - Avoid error-prone/complex features: easy to understand & avoid bugs
    - Concede to optimization, practicalities & interoperability -> adjustment
  - Record decisions leading to the rule
  - -> Easy to reevaluate when assessing change proposal
- Changing rule process: identify existing problems -> solutions
- Enforcing rules:
  - Socially: teaching & training
  - Technically:
    - Tooling: error checker, code formatter.
    - Advs:
      - Correctness
      - Scalability
    - Disadv: can't apply to rules requiring judgement

### 9. Code review
- Require:
  - Process
  - Supporting tools
- Shouldn't: debate previous design decisions
- 3 types of approval needed from 3 roles (goal: flexibility -> scalable):
  - Other engineer: functional correctness & understandability
  - Code owner: suitable for the repo
  - Readability: consistency of style
- -> Usually done by 1 person or the author perform both role 2 & 3
- Benefits:
  - Code correctness
  - Comprehensibility: optimized for readers
  - Consistency
  - Psychological & cultural benefits:
    - Responsibility
    - Openness to criticism
    - Validation/recognition of one's work
    - Being more careful
  - Knowledge sharing
- Best practices:
  - Be polite & professional:
    - Ask for reason before assuming sth is wrong
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
      limit comments to concern specific to local code, not the tool -> scalable

# Criticism
- Chap 1 discuss at quite a high level: need familiarity with many concepts to understand the examples
- 2 chaps about leadership are high level and self-help style
- -> Need real life experiments to see whether the strategies work & how to apply them in specific situations