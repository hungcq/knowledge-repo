## 8. URL shortener
### Requirements
- Give example of how it works
- Req/s
- URL length
- Support update/delete?
- -> Calculate storage requirement
### High level design
- API:
  - POST: return short URL, add short-long URL mapping if not exist
  - GET: redirect to original URL
- Mapping by hash
### Details
- Data model:
  - ID
  - ShortURL
  - OriginalURL
- Hash string length = log(total number of records, num possible characters)
- Hash function:
  - Common hash function:
    - Handle hash collision by appending a string
    - Check hash exist in DB exist: use bloom filter for efficiency
  - Base 62 conversion of auto incremented ID: predictable
- Flow: Client <--> Load balancer -> Servers -> Cache -> DB
- Redirect codes:
  - 301: permanent: browser will cache & not send subsequent request to short URL
  - -> Reduce load
  - 302: temporary: browser won't cache
  - -> Better for tracking short URL usage
### Wrap up
- Rate limiter
- Scaling server & DB
- Analytic: number of click, scenario when click happens
- Availability, consistency, reliability