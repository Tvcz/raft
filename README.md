# Distributed Datastore
## Project 2 - MVP

- Currently, the datastore relies on the leader not failing to maintain
  consistency
- The leader is responsible for maintaining and updating the log and uses it to
  construct the state of the system as needed
- The followers elect the leader and redirect all client requests to the leader