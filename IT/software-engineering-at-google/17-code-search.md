## 17. Code search
### Functionalities
- Code search UI: ~IDE's search in files
- CLI
- Public API for integration
### Goal of code search: reading, understanding & exploring code at scale
- Where: find def, usage, file
- -> Functions: ranking, rich query language, filter, share result
- What: exploratory: what a specific part of the code base is doing
- -> Functions:
  - Browse via call hierarchies
  - Quick navigation between related files
- How: find example of how others have done sth (eg find the proper lib)
- Why: why some code was added, why it behaves in a certain way
- -> Function: search & explore the state of the codebase at a particular point in time
- Who & when: who & when someone introduced a certain piece of code
- -> History functions:
  - ~git blame
  - Jump to code review
### Advs of separate web tool
- Scale:
  - Big codebase -> can't be indexed by IDE
  - Indexing cost in each local machine
  - -> Single, centralized index, update once for each change
- Zero setup global code view -> efficiency
- Specialization: UX can be optimized for browsing & understanding code, not editing it
- Integration with other dev tools: large scale analysis, log search, error/exception report, documentation
- Reusable APIs & plugins
### Challenges
- Search query latency: critical to attention & productivity
- Index latency: low latency & consistency are critical when coding, fixing live issues, reviewing code
### Google implementation details
- Rely on cloud-based backends
- Search index optimization
- Ranking based on 2 types of signals:
  - Query independent:
    - Number of file views
    - The amount of references to a file
  - Query dependent: need to be cheap to compute realtime
  - -> Restricted to the query & info quickly accessible from the index
### Tradeoffs
- Completeness vs efficiency: 
  - Remove large, unreadable files from index
  - All vs most relevant results: allow both types of queries
  - Versions: head vs all branches vs all history vs workspace
- Expressiveness: token vs substring vs regex