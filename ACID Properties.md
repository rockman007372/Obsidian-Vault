---
tags:
  - database
---

- Atomicity: All or nothing - transaction is either executed or not at all
- Consistency: XACT preserves database consistency (e.g. reads must reflect the most recent writes, 2 reads at the same time must give the same state...)
- Isolation: Execution of a XACT is isolated from other XACTS => Prevents a XACT from reading from another XACT that may be aborted
- Durability: Once committed, a XACT effect persists.