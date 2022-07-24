# 1. Scaling overall
## Overall Diagram
- <img src="./resources/1.23.png" width="600">
## Multi data centers diagram
- <img src="./resources/1.15.png" width="600">
## Notes
- Split DB server – service server: scale independently
- Limit of vertical scaling:
  - Hardware limit
  - No failover/redundancy
- Load balancer:
  - Distribute traffic, reduce load to single server
  - Redirect in case of failure
  - Add/remove server easily (auto-scaling)
- Master (write) – slave (read) DB replication:
  - Better performance
  - Availability
- Sharding DB: scale horizontally. Problems:
  - Reshard (move) data
  - Celebrity key
  - Join operation
- Cache tier:
  - Faster read
  - Lower DB read
- CDN for static content. When content expire, CDN request to server.
- Stateless server: move session data out to NoSQL, memcache/redis:
  - Scale servers
  - No need to direct same user to same server
- Multiple data centers: each with server, DB, cache. Need DB sync.
- Message queue:
  - Request not lost in case of failure
  - Scale producer/consumer independently
- Logging (monitoring), metric (system status, business) & automation

# 2. Interview framework
- Problem & design scope: clarify requirements & assumptions:
  - Scope: mobile/web?
  - Num users, CCU, request/s
  - Availability
  - Scalability
  - Existing services/stack
- High level design (10-15 min) & ask feedback
- Deep dive design (10-25 min): bottle neck/specific component
- Wrap up (3-5min). Further discussion:
  - Bottleneck, improvement
  - Error case

# 3. Rough estimation
- 1 ASCII char = 1 byte
- Compress data (fast) before send (slow network read)
- Write down assumption with unit
- Latency numbers:
  - <img src="./resources/2.2.png" width="600">

# 4. Consistent hashing
- Problem: use normal hash function eg hash(key) % num server
- -> Most key are redistributed when add/remove server
- Hash space -> connect 2 ends to create hash ring
- Basic approach:
  - Hash server by name or IP -> map to the hash ring
  - Find a server by going clockwise, get the closest server
  - Problem: server hashes distribute not uniformly when init/add/remove 
  - -> Most key end up in one server
- Virtual node approach:
  - Add virtual nodes for each server, num nodes depend on server capacity
  - Adv: balanced distribution, based on server capacity
- <img src="./resources/5.14.png" width="600">

# 5. URL shortener
## Problem & design scope
- Total URL
- Req/s
- URL length
## High level design
- API:
  - POST: add URL
  - GET: return original URL
- Redirect: 301 client cache, 302 not cache
- Mapping by hash
## Deep dive
- Data model:
  - ID
  - ShortURL
  - OriginalURL
- Hash function:
  - Common hash function:
    - Handle hash collision by appending a string
    - Check URL exist: bloom filter
  - Base 62 conversion of ID: predictable
- Flow: Client <--> Load balancer -> Servers -> Cache -> DB
## Wrap up
- Rate limiter
- Scaling server & DB
- Analytic
- Availability, consistency, reliability

# 6. Web crawler
- Used to discover new/updated content on the web
- Tree-like style
- Purpose:
  - Search engine indexing
  - Web archiving
  - Web mining
  - Web monitoring (e.g., copyright)
## Problem & design scope
- Purpose
- Num pages/s
- Content type: HTML, image
- Store data? Duplicate?
## High level design
- <img src="./resources/9.2.png" width="700">
## Deep dive
- Traversal algo: BFS
- URL frontier:
  - Ensure politeness
  - Prioritization
  - Freshness: ensure content updated 
- -> Distribute URL into queue to be downloaded
- HTML downloader:
  - Multi nodes
  - Cached DNS resolver
  - Geographically distributed
  - Timeout
- Avoid problematic content:
  - Redundant
  - Spider traps
  - Noise: ads, spam URL
## Wrap up
- Server-side rendering page
- Filter
- Scale: DB, downloader
- Availability, consistency, reliability
- Analytics

# 7. Noti system
## Problem & design scope
- Noti type
- Num noti/day
- Client/server-send?
- Real time?
## Design
- 2 flows:
  - Gather contact info
  - Send noti
- Gather info: 1 user -> N devices:
  - User -> Load balancer -> API servers -> DB
- Send noti:
  - <img src="./resources/10.14.png" width="700">

# 8. News feed system
## Problem & design scope
- Scope
- Features
- News feed order
- Num friends of user
- Traffic volume: num DAU
- Feed content: image, video?
## High level design
- 2 flows:
  - Feed publishing
  - Feed building
## Deep dive
- News feed cache: store post ID by user ID
- Post cache, DB: store post content by post ID
- User cache, DB: store user info, follow/unfollow info…
- Feed publishing design:
  - Fanout on write: fast retrieval, heavy computation, waste resource on inactive use
  - Fanout on read
  - <img src="./resources/11.4.png" width="700">
- Retrieval:
  - <img src="./resources/11.7.png" width="700">
- Cache architecture:
  - News feed: feed IDs
  - Content: hot, normal
  - Social graph: followers, following
  - Action: like, rep…
  - Counter: like, reply

# 9. Chat system
## Problem & design scope
- Type of chat app: 1-1/group
- Scope: mobile/web
- Num DAU
- Group size limit
- Text size limit
- Encryption
- Chat history storage duration
- Multi devices/user?
- Noti
## High level design
- Sender (HTTP keep-alive/web socket) -> Chat service (store, relay) (web socket) -> receiver
- Service -> receiver protocol:
  - Polling: inefficient when no new mes
  - Long polling:
    - Close when: new mes/timeout
    - Problem:
      - Multi servers
      - Can't detect disconnection
      - Inefficient
  - Web socket: need to manage connections
- API servers: auth, user profile, service discovery
- <img src="./resources/12.8-modified.png" width="700">
## Deep dive
- Service discovery (e.g., Zookeeper): pick chat server for client
- 1-1 chat flow:
  - <img src="./resources/12.12.png" width="600">
- Sync across device: use cur ID on device -> fetch new mes
- Group chat flow: mes sync queue for each user in group:
  - A -> C queue -> C 
  - A -> D queue -> D 
  - B -> C queue -> C
- Online status:
  - Heart beat
  - Friends sub to channel (e.g., A onl channel)
## Wrap up
- Media: compression, cloud storage, thumbnail
- Client-side caching
- Resend

# 10. Search auto complete system
## Problem & design scope
- Matching: beginning/middle?
- Num of suggestion
- Spell check?
- Multi languages?
- Case sensitive?
- Num users/day
- Sort by?
## High level design
- Data gathering service:
  - Query
  - Frequency
- Query service
## Deep dive
- Trie with optimizations:
  - Limit prefix max length
  - Cache top search query at each node 
  - -> No need to search and sort all children
  - <img src="./resources/13.8.png" width="600">
- Data gathering service:
  - <img src="./resources/13.9.png" width="600">
- Query service:
  - User -> Load balancer -> API servers -> Filter layer -> Trie cache -> Trie DB
  - Other optimizations:
    - Efficient dynamic content update (react)
    - Browser caching
