# Distributed Datastore
## Project 3 - MVP
- Implements raft consensus algorithm
- For reads of data which have uncommitted writes, the read is blocked until the
  write is committed (this is done using redirects)