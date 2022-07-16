## 3. Storage & retrieval
### 3.1. Index structures
- Keep additional metadata to help locate the data 
- -> Need space. Write overhead
- Hash indexes (hash table):
  - Basic in-memory hash map of key – disk offset
  - Break file into append-only segments. Compact periodically to remove duplicate old keys
  - 1 hash map for each segment. Search all the map from newer to older
  - Append-only advs:
    - Fast sequential write
    - Easy concurrency & recovery control
    - No fragmented data
- Log-structure merge tree (LMS tree):
  - Based on hash indexes
  - Sorted string table (SS table): keys in segment file are sorted:
    - Efficient merge (like merge sort)
    - Sparse memory index, range index
    - Compress-able blocks (between keys in sparse index)
  - How to maintain sorted segment:
    - Keep new write in memtable (in-memory tree (AVL…))
    - When tree reach threshold, write to disk
    - Read request: check memtable -> check segments (newer to older)
    - Handle crash: keep a log file to restore memtable
  - Optimizations:
    - Bloom filter to check if key exists
    - Compaction strategy
- B-tree:
  - Break DB into fixed-size blocks/pages
  - Write: search for the page containing the key, update & write the whole page to disk
  - Ensure reliability:
    - Write-ahead log (redo log): use to restore the tree in consistent state if crash when updating multiple pages
    - Latch (light-weight lock): handle concurrent access
  - Optimizations:
    - Copy-on-write instead of write-ahead logs
    - Abbreviate keys in internal pages (B+ tree)
    - -> More keys in 1 page, fewer levels
    - Data pointers only at leaf pages (B+ tree)
    - Make leaf pages sequential on disk 
    - -> Fast scan in sorted order
    - Pointer to siblings in leaf pages (B+ tree)
    - -> Scanning without jumping back to parent pages
    - Fractal tree: borrow log-structured ideas
- B-tree vs LSM tree (only in theory, empirical tests needed):
  - Write amplification: 1 write to DB lead to multiple writes to disk
  - LSM advs & problems:
    - Advs:
      - Higher write throughput
      - Less fragmentation -> less space
    - Problems:
      - Unpredictable response time (effect of compaction operation)
      - Compaction can’t keep up with write -> out of disk space
  - B-tree: strong transaction semantics
- Other indexing structures:
  - Handle 1 key/multirow (e.g., secondary index):
    - Store all rows as a list
    - Make key unique by append row ID
  - Clustered index: store row within index 
  - -> No need to jump from index to heap file
  - Multi-dimensional index vs multi-column index
  - Full text search & fuzzy index (similar keys). i.e., using trie
  - In-memory DB: handle durability via:
    - Logs
    - Periodic write (weak durability)
  - -> Faster not because don’t read from disk, but no overhead of encoding data to write to disk
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
    - 1 fact table (events)
    - Many dimension tables: product info, customer info… (wh/how questions)
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
  - <img src="./resources/3.12.png" width="500">
 
