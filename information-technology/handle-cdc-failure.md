# Handle cdc failure
- Reconciliation: pending/published/failed state in outbox table
- Reconcile mess up event ordering: publish outbox primary id -> consumer can ignore
- Event publisher failure: kafka commited offset -> retry
- Idempotency
