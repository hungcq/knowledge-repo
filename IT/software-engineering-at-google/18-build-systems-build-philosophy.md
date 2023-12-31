## 18. Build systems and build philosophy
### Overview
- Function: transform source code written by engineers into executable binaries that can be read by machines
- Goal:
  - Fast
  - Consistent across machine
- Without a build system: slow, unreliable build & complex script
### 2 types of modern build systems
- Task-based (eg Maven, Ant):
  - Mechanism:
    - Unit of work: task: script that can execute any logic
    - Build file: each task specifies dependencies tasks
  - Function:
    - Allow engineers to write build scripts in principled, modular way as tasks
    - Provide tools for executing those tasks & managing dependencies among them
  - Adv: flexible
  - Disadvs:
    - Too liberal -> complex script
    - Difficulty in parallelizing build steps: risk of conflict resource usage
    - Always have to build from scratch or risk having bugs
    - High effort in maintaining & debugging scripts
- Artifact-based:
  - Declarative style: engineer determines what to build, system determines how to build
  - Advs:
    - Can be parallelized while maintaining correctness
    - Can reuse output of prev build, only rebuild changed files/libs
  - Implementation details:
    - Control tools & OS dependency: declare tools & set of tools (toolchain for each OS)
    - Allow flexibility: use rules, limit to action, input & output
    - Avoid conflicting uses of resource: ~containerization
    - Distributed builds:
      - Remote caching: cache built artifacts -> don't have to build on local
      - -> Need to ensure download is faster than build
      - Remote execution: local -> build master -> workers -> shared cache
### Considerations when choosing build system
- Use shell scripts or invoke tools directly:
  - Small project
  - Languages with built-in build system (eg Go)
- At scale: choose artifact over task-based because migration effort of big project is high
### Manage modules & dependencies
- Manage module:
  - Use fine-grained modules
  - -> Parallelize & distribute build -> faster
  - Minimize module visibility: public shared libs only
- Manage deps:
  - Internal deps:
    - Transitive dep must be listed explicitly (C in A build file if A -> B -> C)
    - -> Automate to reduce effort
    - Don't public internal code as artifact: dif artifact versions violate one-version rule
    - -> Cache build results instead
  - External deps:
    - Automatic versioning (eg v1+): can't ensure compatibility
    - -> Manual versioning (specify the exact version): more reliable
    - Use one-version rule
    - Transitive dep: manage manually: generate workspace file listing all deps (~go.mod)
    - -> Explicit, easier to track & debug
    - Cache build results
    - Ensure security & reliability (deterministic): 3 options:
      - Use a cryptographic hash for each external dep
      - -> Ensure the dep is not changed without ack
      - Mirror all deps into your servers -> increase reliability
      - Vendor the project's deps: download into project repo as third_party dir
      - -> Disadv: burden the VCS