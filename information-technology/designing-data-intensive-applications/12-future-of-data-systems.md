## 12. The future of data systems
### 12.1. Data integration
- Understand adv of each product -> combine to complex app
- -> Combine tools using derived data
- Derived data vs distributed transactions:
  - Distributed transactions:
    - Locks for mutual exclusion
    - Atomic commit to ensure exactly-once
    - Provide linearizability (eg timing guarantee, read-your-write)
  - Derived data systems:
    - Use a log for ordering
    - Use deterministic retry & idempotent to ensure exactly-once
    - Async: no linearizability
- Limit of total ordering:
  - Single leader -> no order when there are multi partitions
  - Events originated in dif services/data centers
  - Client update before receiving response -> dif order in client
- Ensure casual order:
  - Logical timestamp: recipient has to handle out of order events, metadata has to be passed around
  - Log system state the user saw before making decision: unique ID for read event
  - Use conflict resolution algo
- Advs of batch & stream processing:
  - Ensure data in right form & right place: deterministic functions with well-defined inputs & outputs
  - Async operations: more fault-tolerant
  - Reprocessing data for app evolution:
    - Not limited to simple changes
    - Allow gradual, reversible evolution
### 12.2. Unbundling databases
- SQL & transaction (high level abstraction) vs Unix & NoSQL (low level abstraction)
- Similarity: building index in traditional database & maintaining materialized view
- Composing dif storage & processing tools into coherent system:
  - Unifying reads: query integrated system with a single high level query language
  - Unifying writes (like unbundling database index feature): ensure all changes are captured even in case of faults 
  - -> Async event log with idempotent writes instead of distributed trans
- Missing tools: uniform interface to integrate dif systems & propagate changes
- Separate app code & storage
- Dataflow: interplay between state, state changes & app code:
app code subscribes to changes instead of polling for changes
#### Observing derived state
- Read path: only compute when user acts
- Write path: precomputed, done as data come in
- Derived data set: where read path meets write path 
- -> Trade off between computation at read & write time
- Extend write path: can push state changes to end-user device 
- -> From request/response interaction to publish/subscribe dataflow
- Reads as stream of events: merge with write events 
- -> Can track read events & derive meaningful data, merge data across partitions
### 12.3. Aiming for correctness
- Avoid duplication: need to be enforced at end-user device using unique ID for each operation
- Ensure uniqueness constraint in log-based messaging:
process each partition in a single thread, scale out by hash unique field & map to partition
- Multi-partition request processing: money transfer example:
  - Client gen request ID
  - Validation processor (partition by payer ID) maintain & check account balance
  - Append request mes to a partition based on request ID (represent content of the write operation as a single message)
  - A stream processor read the request mes, emit debit & credit event 
- -> Idea: transaction as a single event
- Consistency:
  - Timeliness: no stale read: ensured by linearizability
  - Integrity: data not in inconsistent state
  - -> Can be achieved by dataflow (stream processing) system with high performance & robustness 
- -> Sync, distributed transaction only needed in small scope
- Client can:
  - Wait for constraint validation pass
  - Go ahead & perform operation, but risk having to apologize for constraint violation
- Ensure consistency in case of software & hardware bugs: frequent auditing (check integrity of data)
- -> Design for auditability: event-based system, explicit dataflow
- Tool for integrity checking: potential of blockchain (distributed ledger)
