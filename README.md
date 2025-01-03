# Distributed Datastore

This project was submitted as my final project for my Fall 2024 Distributed Systems class.

## High-Level Approach
For this project, functionality was implemented in the `Replica` and `LogEntry` classes. These are defined and instantiated in the `4730kvstore` file.

### `Replica`

The `Replica` class is responsible for handling key-value store operations and
maintaining consistency using the Raft consensus algorithm. It handles client
requests, manages the state machine, and coordinates with other replicas to
ensure data consistency.

#### Key Methods

- `handle_message`: Processes incoming messages and determines the appropriate action.
- `send`: Sends messages to other replicas.
- `run`: Main loop to run the replica.
- `start_election`: Initiates an election to become the leader.
- `handle_get`: Processes GET requests from clients.
- `handle_put`: Processes PUT requests from clients.
- `make_commits`: Commits pending log entries to the state machine up to the commit index.
- `request_vote`: Requests votes from other replicas to become the leader.
- `handle_request_vote`: Handles incoming vote requests and responds accordingly.
- `append_entries`: Sends append entries requests to other replicas to replicate log entries.
- `handle_append_entries`: Handles incoming append entries requests and updates the log and state machine.

### `LogEntry`

The `LogEntry` class represents an entry in the Raft log. It contains the
command, the term in which the command was received, and the index the entry has
in the log.

#### Key Methods

- `apply`: Applies a command to the state machine.
- `serialize`: Serializes a command for transmission.

## What I think is good about the design

- The design ensures strong consistency using the Raft consensus algorithm while
  allowing for fault tolerance in networks and servers.
- The system efficiently and reliably handles leader elections.
- The logging mechanism provides detailed insights into the system's operations
  right up until the failure of a replica.
- The profiling functionality which allowed me to determine what was sending the
  most messages and how to reduce the number of messages sent.
- The design of the classes in making methods short and understandable, or when
  they are longer having them be explained step by step in comments.
- The use of a separate `LogEntry` class to encapsulate the details of log
  entries and make the code more modular and easier to understand, while
  allowing flexibility in what information is stored in those entries (for
  instance making index a part of the object instead of relying on the order of
  the list).

## Challenges

- Consistency issues when a leader crashes after receiving a command but before
  committing it.
- Deadlocking when multiple replicas try to become the leader simultaneously
- Correctly comparing log entries to determine the most up-to-date state during
  elections and in response to append entries rpcs
- Handling edge cases in the Raft protocol so that the system can operate
  robustly and overcome failures without complicating the codebase.
