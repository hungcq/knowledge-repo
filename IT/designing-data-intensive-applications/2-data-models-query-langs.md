## 2. Data models & query languages
- Represent real world in terms of data models
- Each data model has assumption about usage
### 2.1. Relational vs Document DB
- | Relational                                                              | Document                                                                    |
  |-------------------------------------------------------------------------|-----------------------------------------------------------------------------|
  | Transaction & batch processing                                          | Scalability                                                                 |
  | Need to map to object<br>(languages are object-oriented)                | Specialized query operation                                                 |
  | Now support JSON & XML fields with query & index                        | Dynamic schema                                                              |
  | Query optimizer handle the access path for join                         | Suitable for self-contained document<br>-> Better locality (no join needed) |
  | Normalize (no duplicate)<br>-> Handle one to many & many to many better | Denormalize (one to many)<br>-> Handle by application code -> costly        |
- Considerations:
  - Simplicity of application code: self-contained or many to many?
  - Schema flexibility: schema-on-read or schema-on-write (costly when update schema)
  - Data locality:
    - Need large part of doc at the same time?
    - Join or write the whole document costly?
- Convergence trend
### 2.2. Query languages
- Imperative: specify the step of the query
- Declarative: specify the result (pattern of data). The query optimizer decides “how”.
- -> Can be optimized/parallelized easily
- *On the web: CSS (declarative) vs JS code (imperative)
- Map-reduce:
  - Intermediate between declarative & imperative
  - Need to write 2 coordinated functions (map & reduce)
### 2.3. Graph-like data model: focus on highly connected data (many to many)
- Property graph model:
  - 1 vertex – many edges
  - Vertex:
    - ID
    - Outgoing edges
    - Incoming edges
    - Properties
  - Edge:
    - ID
    - Start vertex
    - End vertex
    - Label (relationship)
    - Properties
  - Heterogeneous: anything could be vertex & edge
  - Cypher query language
  - Query in SQL
- Triple-stores: subject – predicate – object
  - Subject: vertex
  - Predicate: property key/edge
  - Object: property value/vertex
  - SPARQL query language
- Data log: foundation of SPARQL, Hadoop query languages
