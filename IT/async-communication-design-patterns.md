# Design Patterns For Asynchronous API Communication

## Info
- Type: blog
- URL: https://stackoverflow.blog/2022/07/21/event-driven-topic-design-using-kafka/
- Broker technology: Kafka

## Content

### Intro
- Structure the data using Avro/Protobuf
- Every message in a topic should use the same schema
- 3 situations:
  - Entity topic (current state of an object)
  - Event topic (a particular thing happened)
  - Request/response topic

### Entity topic: source of truth
- Common usage: async data replication
- Key: entity ID. Partition by key.
- Tombstone to compact messages of deleted key
- Export as little info as possible
- -> Can add fields & republish if needed later on since it is the source of truth
- Adv: flexibility in how consumer store data (eg CQRS), loosely coupled services
- Disadv: eventual consistency

### Event topic: record of facts
- 2 common usages:
  - Collect user/app behavior -> analytics & manual/automatic decision-making
  - Trigger some task/function when a particular event occur
  - -> used in choreography architecture (a decentralized design where each system only knows its own inputs)
- Add as many field as possible since each event is a snapshot of state at one moment -> can't add to it later
- Related events should be in the same partition for ordering guarantee

### Request/response topic
- Common usages: orchestration architecture (a service explicitly tells other services what to do):
  - Low coupling, highly available req/res
  - Long-running task (can request synchronously & response asynchronously)
  - Already using message broker for most inter-service communication
- Disadv: don't know the result immediately
- Consumer owns the schema

### Additional info: considerations when using stream-stream join
- Topics must have the same key schema to avoid expensive re-partitioning
- Topics must have equal throughput,
otherwise might need to join large, slow with fast, small into large, fast, which affect downstream
- Lots of temporary messages/topics resulting in high load on the broker
- -> Recommendation: stream-DB join: use partial writes to data stores: store to local DB & produce again depending on usage