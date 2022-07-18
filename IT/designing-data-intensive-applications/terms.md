# Transactions
- Anomalies:
  - Dirty read: read uncommitted value:
    - T1: set x = 1->2                       set y = 1->2
    - T2:              read x = 2, read y = 1
    - -> Inconsistent. x must = y
    - Problems:
      - Read partially updated state
      - Read value of aborted trans
  - Dirty write: overwrite uncommitted value:
    - T1: set x = 1->2                          set y = 1->2
    - T2:             set x = 1->3, set y = 1->3
  - -> Inconsistent: x = 3, y = 2
  - Read skew (timing anomaly/non-repeatable read): observe the DB in an inconsistent state
    - T1: read acc1 = 500                                        read acc2 = 400
    - T2:                set acc1 (500) += 100, acc2 (500) -= 100
    - Problems:
      - Inconsistent backups
      - Inconsistent analytic queries & integrity checks
  - Lost update: 2 concurrent trans do read-modify-write cycle (e.g., counter increment):
    - T1: read x = 1                         set x = x + 1
    - T2:           read x = 1, set x = x + 1
  - -> Inconsistent: x = 2 instead of 3
  - Write skew: 2 trans read same objects, then update some of those objects:
    - T1: count  check valid count OK                       write
    - T2: count                       check valid count OK  write
  - -> When write change result of count, premise is no longer true (phantom)
  - Phantom read: check for the absence of row matching some search condition (eg booking, check username existed)
  - -> No row to lock to
- Types of concurrency control mechanisms:
  - Pessimistic (eg 2PL): wait until safe to execute trans
  - Optimistic (eg SSI): continue trans without blocking, check for isolation violation when committing, abort if needed