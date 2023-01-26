# Category
- Software engineering

# Structure
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

# Author's goals
- Problem: most effort is spent after a software is built
- -> SRE: focus on whole life cycle of software objects. Vs SE: design & build software systems.
- Explain how SREs do things at Google

# Presentation & styles
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

# Terms
- Chap 2

# Content
## Preface
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
### Additional info
- Small org should also have an early reliability structure: expand later on is less costly
- -> Can adopt best practices in part 4: management

# Criticism

# Takeaway