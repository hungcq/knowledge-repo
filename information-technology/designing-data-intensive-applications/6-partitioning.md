## 6. Partitioning
- Break data into partitions (shards)
- Each piece of data belongs to exactly 1 partition
- Adv: scalability
- Difficulty: complex query across many nodes
- Usually combined with replication
- Independent of replication scheme

### 6.1. Partitioning of key-value data
- Aim: spread data & query load evenly across nodes
- Partition by key range:
  - Adv: can keep key in sorted order in each partition
  - Difficulty: choose key range to balance load
- Partition by hash of key:
  - Hash key -> assign each partition a range of hashes
  - -> More evenly distributed
  - Problem: inefficient range query
  - -> Concatenated PK (eg (userid, ts)), hash & partition main column, sort by other columns
  - -> Can handle search with a particular primary key (eg all messages of userid 1 in a ts range)
- Skew workloads & hot spots:
  - Partially handled by hashing
  - Celebrity key problem: num of reads & writes of 1 key extremely high
  - -> Add a random number to the key to spread: complex combination logic & need to track which keys are spread

### 6.2. Partitioning & secondary indexes
- Local index (index by document):
  - Each partition maintains its own secondary indexes of documents in that partition
  - Write to 1, read from all
- Global index (index by term):
  - Cover data in all partitions
  - Distribute across nodes by terms (using range or hashes): eg 1->10, a->e in partition 1
  - Write to several (1 partition/index field), read from 1
  - Problem: async index update, stale read

### 6.3. Rebalancing
- Aim:
  - Data distributed evenly after rebalanced
  - DB available while rebalancing
  - Minimize amount of moved data
- Automatic vs manual rebalancing: need human to avoid wrong detection of node failure while rebalancing
#### Strategies
- Hash mod n: most keys will be moved
- Fixed num of partitions, map partitions to nodes:
  - Move entire partition
  - Advs:
    - Easy to operate
    - Can assign partitions by node's capacity
  - Problem: choose num of partition:
    - Large: overhead
    - Small: big partitions -> can't add more nodes, hard to rebalance
- Dynamic partitioning:
  - Split/merge partition when larger/smaller than threshold
  - Problem: only 1 partition when create DB -> all load to 1 node 
  - -> Create DB with several partitions (pre-splitting)
- Partitioning proportionally to nodes:
  - Fixed num of partitions per node
  - When new node joins: choose a fixed num of partitions to split 
  - -> Consistent hashing idea

### 6.4. Request routing
- 3 ways to keep partitioning knowledge:
  - In client
  - In routing tier
  - In DB nodes -> reroute client when don't have data
- Problem: update when add/remove nodes:
- -> Use coordination service (eg ZooKeeper) to keep track of cluster metadata (mapping of partitions to nodes)
- -> Client/routing tier subscribe to coordination service, get notified when partitions moved or nodes added/removed
