# Site Reliability Engineering

## Info
- Type: book
- Editors: Betsy Beyer, Chris Jones, Jennifer Petoff, Niall Richard Murphy

## Category
- Software engineering

## Structure
- Preface:
  - SRE def
  - Problems, goals
  - Reading suggestions
- Chap 1: introduction:
  - Sysadmin approach to service management: advs, disadvs
  - Google's SRE approach to service management: advs, challenges
  - SRE tenets
- Chap 2: the production env at Google: terms & services at Google
- Chap 3: embracing risk:
  - Overview
  - Metric to measure service risk
  - Considerations when define service's risk tolerance
  - Error budget: problems, goals, process, advs
- Chap 4: service level objective:
  - SLI
  - SLO
  - SLA
- Chap 5: eliminating toil:
  - Main types of SRE activities:
    - Toil: def
    - Engineering work: types
  - Process of eliminating toil
  - When toil is bad
- Chap 6: monitoring distributed systems:
  - Terms
  - Reasons to monitor a system
  - Principles:
    - Simplicity
    - Blackbox vs white-box monitoring
    - 4 golden signals
    - Use distribution, not average
    - Philosophy on pages & pagers
    - Consideration when creating monitoring & alerting rules
    - Issues of evolving systems & general approach
- Chap 7: the evolution of automation at Google:
  - Advs
  - Use cases & evolution of automation
  - Google examples & lesson learned
  - Imp of transparency
  - Recommendations
- Chap 8: release engineering:
  - Def & role
  - Best practices
  - Google processes & best practices for continuous build & continuous delivery
  - 4 dif approaches to config management
  - Recommendations
- Chap 9: simplicity: best practices
- Chap 10: practical alerting from time-series data:
  - Borgmon monitoring system: ~prometheus
  - Blackbox monitoring
  - Maintaining config
- Chap 11: being on-call
  - Main on-call activities
  - Practices:
    - Maintaining balance
    - Providing resources to make on-call engineers feel safe
    - Setting apt operational load
- Chap 12: effective troubleshooting:
  - Principles
  - Common pitfalls
  - Best practices

## Author's goals
- Problem: most effort is spent after a software is built
- -> SRE: focus on whole life cycle of software objects. Vs SE: design & build software systems.
- Explain how SREs do things at Google

## Presentation & styles
- Author's claim:
  - Collection of essays, shared a common vision
  - Personal account
  - Common themes & software systems
  - Document reasoning process & choices from dif perspectives
  - Separate generate principles from specific practices
  - Provide orienting material:
    - Description of Google production env
    - Mapping between some of Google's internal software & publicly available software
  - -> Conceptualize the content & make it more usable
- References: mainly papers. Other sources: blog posts, books, lectures.

## Terms
- In chap 2

## Content
### Preface
- SRE: def by main roles:
  - Engineering (E): apply the principles of computer science & engineering to
    the design & development of computing systems (usually large distributed ones):
    - Write software for those systems alongside the product development counterparts
    - Build all the additional pieces those systems needed (eg backup, load balancing), ideally to be reused across systems
    - Figure out how to apply existing solutions to new problems
  - System reliability (R): find ways to improve the design & operation of systems to make them more scalable, reliable & efficient
  - Services (sites) operation (S): operate services built atop the distributed computing systems
- Overall principles:
  - Thoroughness & dedication
  - Belief in the value of preparation & documentation
  - Awareness of what could go wrong, coupled with a strong desire to prevent it
- Reading suggestions:
  - At least start with chap 2 & 3
  - Can read whatever subject of interest
- Other reading resources:
  - Ref in each chap
  - [Website](https://g.co/SREBook): include code examples
#### Additional info
- Small org should also have an early reliability structure: expand later on is less costly
- -> Can adopt best practices in part 4: management

## Criticism
- Chap 6: not well-structured: too many headings that are all over the place
- Chap 9: mostly platitude

## Takeaway
