# go_microservice_eventsourcing
This is a small demo of GO microservice and event sourcinglients never 

### Summary: Writing with Commands
1. Clients never write the events directly
2. Clients express an intent to do something via commands
3. Commands are validated by Aggregates. An aggregate is a DDD concept.
4. Aggregates fetch events from the Event Store, and replay them to reconstitute their current state
5. If the Aggregate accepts the Command, it returns in an event.

### The Circulur Architecture
        ----------------------
       |        Client        |
        ----------------------
         |                |
         |                |
         |                |
         |                |
  ----------------    ------------------
  | Query Handler |   | Command Handler |
  -----------------   ------------------
                  |   |
                  |   |
                  |   |
          ----------------------
          |    Event Store     |
          ----------------------
