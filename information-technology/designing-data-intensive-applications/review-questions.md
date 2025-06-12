# Review questions
- What are the main differences between relational & document data model? What should be considered when choosing data model?
- What are the 2 types of query languages?

# Storage & retrieval
- What are the main primary-key index structures? How are they implemented? What are the main advs & disadvs of each?
- How is secondary index implemented?
- What is clustered index, covering index, concatenated (composite) index, multi-dimensional index?
How is concatenated index implemented?

# Encoding & evolution
- What are the common encoding formats? What are the advs & disadvs of each? How is versioning handled by each?

# Replication
- What are the advs of distributed data?
- What are the dif algorithms to replicate data across nodes? How are they implemented, including read, write, replication?
- What are the problems related to replication lag? How to deal with them?
- What are read and write quorum? What should be considered when choosing read & write quorum values?
- What are the dif ways to implement replication logs?

# Partitioning
- What is the main difficulty with partitioning?
- What are the dif strategies to partition key-value data? What are the tradeoffs of each approach?
- How to handle celebrity key problem?
- What are the dif ways to partition secondary index? How are read & write handled in each case?
- What are the dif ways to assign partition to node? How is rebalancing handled in each case, with what tradeoff?
- What are the dif places where partitioning knowledge can be kept? How is routing & discovery handled?

# Transactions
- What is a trans? Goal of using trans.
- Explain 4 concepts in ACID with examples. How to ensure durability in: 1 node & multi nodes?
- What are the situations when retrying aborted trans is not effective?
- What are dirty read, dirty write, read skew (non-repeatable read), lost update, write skew, phantom? Provide examples.
- What are the isolation levels? What anomalies does each level prevent? How are they implemented?

# Distributed system issues & consensus
- What are the common issues in distributed system?
- -> Unreliable network, unreliable clock
- What is the mechanism to reach consensus despite those issues (eg implemented by ZooKeeper/etcd)?
- -> Total order broadcast

# Batch processing
- What are the other 2 types of systems beside online system?
- Provide some example outputs of batch processing job.
- How does MapReduce operate at a high level?
- What is the advantage of dataflow engines (eg Spark) over MapReduce?

# Stream processing
- What is data stream? [What is it commonly used for?](./11-stream-processing.md#113-processing-streams)
- What are the advs of log-based message broker over traditional message broker?
- How to parallelize processing using log-based message broker?
- What is the common use of replication logs? How to optimize replication logs?
- What are the dif types of stream joins? Provide an example for each.

# Future of data systems
- How are new data systems usually implemented? How dif tools are combined?