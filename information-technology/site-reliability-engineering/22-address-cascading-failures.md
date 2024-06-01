## 22. Address cascading failures
### Causes of cascading failures
- Server overload: most common cause
- Resource exhaustion:
  - CPU
  - Memory
  - Threads
  - File descriptors
  - Dependencies among resource: resource exhaustion scenarios feed from one another
  - -> Difficult to debug due to many secondary symptoms
- Service unavailability: difficult to escape because as soon as servers come back online
they are bombarded with an extremely high rate of requests and fail almost immediately
### Strategies to preventing server overload: in rough priority order
- Load test the server's capacity limits, and test the failure mode for overload
- -> Prefer realistic env
- Graceful degradation: serve degraded results:
  - Eg: use cache, change algo
  - Use service-specific strategy
- Load shedding: instrument the server to reject requests when overloaded: approaches:
  - Per-task throttling based on CPU, memory, queue length; limit queue length
  - Changing the queuing method (eg FIFO to LIFO)
  - -> Reduce load by removing requests that are unlikely to be worth processing
  - -> Work well with propagating PRC deadlines throughout the stack
  - Prioritize requests based on client type/request char
- Instrument high-level systems to reject requests, rather than overloading servers: rate-limiting layers:
  - Reserve-proxies: limit the volume of requests by criteria (eg IP address) to mitigate attempted DoS attacks and abusive clients
  - Load balancers:
    - Drop requests when the service enters global overload
    - Can be indiscriminate or more selective depending on the service
  - Individual tasks: to prevent random fluctuations in LB from overwhelming the server
- Perform capacity planning
### Considerations to avoid server overload
- Queue size considerations (in producer-worker model):
  - Steadiness of traffic
  - Current number of threads in use
  - Processing time for each request
  - Size and frequency of bursts
- Load shedding & graceful degradation considerations:
  - Overload metric
  - Triggering method: auto/manual
  - Action taken in degraded mode
  - Action point: entry point or every layer
- Retries:
  - Issue: retries increase QPS gradually in case of overload
  - Best practices:
    - Use strats to prevent server overload (above)
    - Use randomized exponential backoff
    - Limit retries per request
    - Retry budget on server-side client process
    - Avoid amplifying retries by issuing retries at multiple level
    - Separate retriable & non retriable error codes
- RPC latency and deadlines:
  - Considerations:
    - Picking apt deadline
    - Checking deadline to decide whether to handle the request
    - Deadline & cancellation propagation (ie reduce deadline by processing time at each point in the stack)
    - -> Can account for network transit & client processing time
  - Bimodal latency:
    - Problem: error requests take longer time, consume more FE resources
    - Best practices:
      - Detection: monitor for latency distribution
      - Fail fast
      - Use shorter deadline
      - On server side: limit, track abuse by client type
- Avoid intra-layer communication in the user request path: possibility of cycles
- -> Let the client do the comm
(eg when client guess the wrong BE, client retries to call the correct BE, not BE proxying each others)
### Triggering conditions for cascading failures
- Process death
- Process updates/new rollouts (new binary version, config update, infra change)
- -> Solutions: over provision, canary, avoid peak hour, reverting changes
- Organic growth
- Request profile changes
- Cluster outage/shift
- Dep services down
- Slow startup & cold caching. Solutions:
  - Overprovision the service -> can handle empty cache
  - Employ general cascading failure prevention techniques (eg rejection, degradation, restart, scenario testing)
  - When adding load to a cluster, slowly increase the load -> warm up cache
### Testing for cascading failures
- Goals:
  - Gain exp of service behavior
  - Determine breaking point -> capacity planning
  - Know how to fix
- Test non-critical backends
- -> Ensure service/FE can handle their unavailability
### Immediate mitigations
- Increase resources
- Stop healthcheck failures/deaths (eg when healthcheck kills starting service instances)
- Restart servers: when deadlocked/holding requests
- Drop traffic:
  - Temporary solution, to buy time & fix root cause
  - Can drop bad, unimp traffic if possible
- Enter degraded modes
- Eliminate bad traffic

### Additional info
- 