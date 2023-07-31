# II. Distributed data
- Why distribute data:
  - Scalable
  - Available
  - Reduce latency: multi locations
- Shared-nothing architecture (horizontal scaling)

## 5. Replication
- Keeping a copy of the same data on multiple machines connected via a network (replica)
- Difficulty: handle changes to replica 
- -> Algos:
  - Single leader
  - Multi leader
  - Leaderless
- Other trade-offs:
  - Sync vs async replication
  - Handle failed replicas

### 5.1. Leader-based replication
- 1 leader handle all writes 
- -> Send change to followers
- All nodes can handle reads
- Set up new followers:
  - Copy from a consistent snapshot
  - Connect to the leader and get all changes since the snapshot
  - Process changes normally after catching up
- Async replication (vs sync replication): leader notifies the client before the followers' confirmation of the write 
- -> Faster write but risk of reading inconsistent data
- -> Usually only 1 follower is sync (semi-sync)
- Handle node failures:
  - Follower failure: catch-up recovery: request all changes during disconnected period
  - Leader failure: failover: set up new leader
    - Process:
      - Determine leader has failed
      - Choose a new leader
      - Reroute write to the new leader
    - Potential problems:
      - Loss of writes in async mode
      - Side-effect
      - 2 nodes promoted to be leader
      - Choose timeout period

### 5.2. Problem with replication lag & solutions
- Eventual consistency: when stop writing to DB for a while, followers will eventually catch up
- Replication lag is high when:
  - Network problem
  - System capacity near maximum
#### Read your write
- Problem: read from a not updated replica
- -> Users not see their update
- Need read-after-write (i.e., read your write) consistency
- Implementations:
  - Read from leaders when reading sth user might have modified (eg read user profile from leader)
  - Track last update time: read from leader 1 min after the update
  - Client track timestamp/version of last write -> read from updated replica or wait till it has caught-up
- Cross-device consistency issues: need centralized last-write tracking
#### Monotonic reads
- Problem: user see time go backward when reading from dif replicas: read updated replica then read not updated replica
- Implementation: 1 user always read from the same replica
#### Consistent prefix reads
- Problem: violation of causality
- Involve sharding: some partitions are replicated slower than other:
user see some parts of data in older & some parts in newer state
- <img src="./resources/5.5.png" width="500">
- Implementation: causally related writes are written to the same partition

### 5.3. Multi-leader replication
- More than 1 node accept writes 
- -> No single point of failure
- Use cases:
  - Multi data center operation: 1 leader in each center
  - Clients with offline operation
  - Collaborative editing
- Difficulty: handle write conflicts
#### Handle write conflicts
- Avoid conflict (preferred solution): all writes for a record go to the same leader
- Converge toward a consistent state:
  - Last write win: use ID/timestamp -> prone to data loss
  - Highest replica ID win -> data loss
  - Merge values
  - Save the conflict -> let app resolve (can ask user):
    - On write
    - On read
#### Replication topologies
- Circular & star: prone to node failures
- All to all: message ordering problem

### 5.4. Leaderless replication
- Client send write:
  - Directly to several replicas
  - Indirectly via a coordinator node: not enforce write order
- Read from several nodes: use version number to choose newer value
- Use case: high availability, low latency, can tolerate stale reads
- Update data to failed nodes:
  - Read repair: client read -> write new value to old node 
  - -> Only in frequently-read app
  - Anti-entropy process: background process looks for differences in data between replicas to update/copy data
- Read (r) & write (w) quorums:
  - w + r > n (num replicas that have the data) -> high probability of getting new value when read
  - Usually read/write still sent to n replicas 
  - -> w & r is num of acks for the operation to be considered successful
  - w & r small: higher availability & lower latency, but stale values
- Hard to monitor staleness in the system
#### Sloppy quorums & hinted handoff
- Sloppy quorums: in case of sharding, when not enough w available nodes, write to other not-designated nodes
- Hinted handoff: when designated nodes are available, copy data back 
- -> Read could be from stale data, until handoffs complete
#### Handle concurrent writes
- Concurrent: no causal dependency
- Last write win: data loss
- Merge & resolve conflict: using version vector:
  - Keep version numbers of all replicas for each key
  - DB sends data of dif versions to client
  - Client sends version vector back when write 
  - -> DB choose which value to overwrite, which to keep as siblings

### Additional info
- Replication logs implementations:
  - Statement-based: problems:
    - Non-deterministic function calls (eg NOW(), RAND())
    - Order of execution
    - Side-effect (eg triggers)
  - -> Replace with fixed value, but many edge cases
  - Write-ahead log shipping (byte sequence): safe, but depend on the storage engine & version
  - Logical (row-based) log replication (eg MySQL binlog):
    - Logical log: sequence of record describing writes to DB. Log info:
      - Insert: all new values of all columns
      - Update: row ID, new values of all/updated columns
      - Delete: row ID
    - Advs:
      - Independent of internal implementation
      - Readable & easy to parse
  - Trigger-based replication: application handle replication logic by:
    - Reading replication logs
    - Read change log table saved by custom DB trigger
  - -> Flexible but slower & not reliable