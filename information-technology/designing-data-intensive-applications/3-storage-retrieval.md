## 3. Storage & retrieval

### 3.1. Index structures
- Keep additional metadata to help locate the data 
- -> Need space. Write overhead.
#### Hash indexes (hash table)
- Basic in-memory hash map of key - disk offset
- Break data into append-only segment files. Compact & merge segments periodically to remove duplicate old keys.
- 1 hash map for each segment. Search all the map from newer to older.
- Append-only advs:
  - Fast sequential write
  - Easy concurrency & recovery control: no overwrite
  - No fragmented data
- Disadvs:
  - Hash map must fit in memory, otherwise access is slow
  - Can't do range queries: must read all keys
#### Log-structure merge tree (LSM tree)
- Implementation:
  - Based on hash indexes
  - Use segment files whose keys are sorted (sorted string table - SS table)
  - How to maintain sorted segment:
    - Keep new write in memtable (in-memory tree (eg AVL))
    - When tree reach threshold, write to disk
    - Read request: check memtable -> check in-memory index of segments (newer to older)
    - Handle crash: keep a log file to restore memtable
- Advs over hash table:
  - Efficient merge (like merge sort)
  - Can use sparse in-memory index, range index for each segment (using BST like AVL)
  - -> Reduce memory usage
    -  <img src="./resources/3.5.png" width="500"/>
  - Compress-able blocks (between keys in sparse index)
  - -> Reduce size & disk IO
- Advs over B-tree:
  - Higher write throughput: sequential writes & usually lower write amplification
  - Less fragmentation -> less space
- Disadvs:
  - Unpredictable response time (effect of compaction operation)
  - Compaction can't keep up with write -> out of disk space
- Optimizations:
  - Bloom filter to check if key exists
  - Compaction strategy
#### B-tree
- Implementation:
  - Break DB into fixed-size blocks/pages
  - Pages refer to other pages' address on disk
  - Read: traverse tree until reaching leaf. Leaf contains key's value or address of page containing key's value.
    - <img src="./resources/3.6.png" width="500"/>
  - Update: search for the page containing the key, update & write the whole page to disk
  - Insert: if page reaches its maximum capacity -> break into 2 pages & update tree
    - <img src="./resources/3.7.png" width="500"/>
- Adv: can attach locks to tree to lock key range -> strong transaction semantics
- Ensure reliability:
  - Write-ahead log (redo log): use to restore the tree in consistent state if crash when updating multiple pages
  - Latch (light-weight lock): handle concurrent access
- Optimizations:
  - Copy-on-write updated page, then point to it after finishing
  - -> Don't need to maintain write-ahead logs
  - Abbreviate keys in internal pages (B+ tree): only need range info
  - -> More keys in 1 page, fewer levels
  - Make leaf pages sequential on disk
  - -> Fast scan in sorted order
  - Pointer to siblings in leaf pages (B+ tree)
  - -> Scanning without jumping back to parent pages
  - Fractal tree: borrow log-structured ideas
#### Other indexing structures
- Secondary index:
  - Implementation similar to primary index
  - Handle 1 key/multirow (eg dif userids, same age):
    - Store all rows as a list
    - Make key unique by append row ID
- Clustered index (store row within index) & covering index (store needed columns of the row within index)
- -> No need to jump from index to heap file
- Multi-column index:
  - Concatenated index (eg firstname, lastname): implemented by concat 2+ fields into 1 key
  - Multi-dimensional index (eg geospatial): allow range searching for 2+ fields
- Full text search & fuzzy index (similar keys). i.e., using trie
- In-memory DB: handle durability via:
  - Logs
  - Periodic write (weak durability)
- -> Faster not because don't read from disk, but no overhead of encoding data to write to disk

### 3.2. Transaction processing vs Analytics
- OLTP vs OLAP (online analytic processing):
- | OLTP                            | OLAP                      |
  |---------------------------------|---------------------------|
  | Small number of records/queries | Large number of records   |
  | Random, low latency write       | Bulk import/event stream  |
  | Used by end users               | Used by business analysts |
  | Latest data                     | History of events         |
  | Size: GB-TB                     | Size: TB-PB               |
- Data warehouse:
  - Separate heavy analyzing query from OLTP system
  - OLTP DBs -> extract -> transform -> load -> data warehouse
- Analytic schemas:
  - Star:
    - 1 fact table: contain events
    - Many dimension tables: eg product info, customer info (wh/how questions)
  - Snowflake: dimension table broken down to sub-dimension tables
- Column-oriented storage:
  - Many columns, but query only select several columns
  - Data saved by columns, same orders in each
  - Column compression:
    - Bitmap encoding
    - Run-length encoding
  - Sort frequently queried column
  - Duplicate data for dif sort orders
  - Writing: LSM tree
- Aggregation:
  - Pre-computed (materialized) aggregates for fast query
  - Data cube/OLAP cube: grid of aggregates grouped by dif dimensions 
  - -> Faster but less flexibility. Write more expensive
  - <img src="./resources/3.12.png" width="500"/>
  