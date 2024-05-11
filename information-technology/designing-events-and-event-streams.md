# Designing Events And Event Streams

## Info
- Type: course
- URL: https://developer.confluent.io/courses/event-design/intro/

## Content

### Intro
- Main content:
  - Dimensions of event and event stream design & how to apply them to real world problems
  - Best practices: schemas, naming, IDs...
- 2 ways of producing events:
  - Connector: automatically convert extracted data into events
  - Event-driven app: produce native events
- Event:
  - Def: a record of something that has happened in the business
  - Contain: imp business details about what happened and why
  - Name: based on past-tensed terminology (eg order_created)
  - Chars: durable, replay-able & immutable
  - Stream: contain events. Also immutable.
- Design event content: start with boundaries (bounded context):
  - Internal: encapsulate business logic & data models
  - -> Data is private, fluid & changeable
  - External: communicate via APIs
  - -> Data is deliberately made available for other to use/consume. Events as data transfer objects.
  - -> Need to understand the use case & design events carefully due to contractual requirements & backward compatibility
- -> Focus of course: design outside events
- Design issues:
  - Content of event
  - Transformation: inside data -> outside events
- 4 dimensions to consider when designing events:
  - Facts vs delta events
  - Normalization vs denormalization
  - Single vs multiple event types per topic
  - Discrete vs continuous event flows

### 

Schema registry (eg Confluence schema registry)
Should standardized headers across the org
EventID: should be structured: service.type.entity_id.sequence_id
-> Sequence ID can be used to know about ordering & whether there is missing event. EventID can be used for deduplication.