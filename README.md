

# go_microservice_eventsourcing
This is a small demo of GO microservice and event sourcinglients never 

### Event sourcing with CQRS:
1. Event sourcing makes you store business facts as a source of truth. These facts are immutable.

2. Event sourcing makes the system deterministic.

3. CQRS and the Circular architecture works well with event sourcing.'

        3.1 Clients express intent via commands, which if accepted become events and are appended to an event stream.
        3.2 Asynchronous projectors process the event stream and build up denormalised projections.
        3.3 Clients quey the projections when they want to know something.
        3.4 Asynchronous reactors process the event stream and reacts to the events according to business logic, outputting               more events. 
        
        
### Upside

1. This pattern treats the core of your business with respect.
2. You can place more respect to your data by placing it at the core of your system and then changing it.
3. Events represent business happenings that always have been of fundamental interset to the business.
4. We dont loose data
5. Rapid iteration and reinterpretation.
6. Keep the cost of change lower for longer.







### Summary: Writing with Commands
1. Clients never write the events directly
2. Clients express an intent to do something via commands
3. Commands are validated by Aggregates. An aggregate is a DDD concept.
4. Aggregates fetch events from the Event Store, and replay them to reconstitute their current state
5. If the Aggregate accepts the Command, it returns in an event.

### The Circulur Architecture

### Reactors
The Reactors are for all of the business logic in between. Reactors process events just like projectors do and they 
keep bookmark to where in the stream they are at, but rather than building up projrvtions they react to events, either by triggering some external behaviour or by emitting new  events to the event store or both.

Raising events at a diferent level of abstraction. Reactors subscribes to events and watch the events and 
besed on some rule it can emmit another event if some condition satisfies its rule. So it reacts to the event incoming 
based on some rule.

Reactors can be stateful. Reactors can hold some reference data, which are also sometimes called internal projections.
Reactors watches the stream of events and reacts when its conditions are met.

A Reactor can execute a side effect from something that has happened, and then emits that event to that effect.

### Event Store Features
1. Put event
2. Get all events, in order, from an offset
3. Get all events in order, scoped by aggregate..id

Reactors are decoupled from each other. They typically run as single threaded processes. They are small and isolated a typically do just one thing. Like projectors Reactors are asytnchronous and subject to Eventual Consistency. Reactors typically do not share any code, and state. Reactors do not share their internal projections. Nor do thay access any of the external projections that clients use.

If a reactor needs state, it should be responsible for managing that state itself. Reactors should be built so that they can be deleted with no loss of system intregrity.

Reactors behave a lot like Microservices. They ttend towards idempotence, they are not fully idempotent.Reactors will not 
trigger external behaviour when rebuilt against event history. 

Reactors should have single responsibility and should encourage a business-oriented decomposition of the system, rather than a technical one.

Reactors encourage a business-oriented decomposition of the system, rather than a technical one.

### Summary: Reactors

1. Reactors process the event stream, like projectors.
2. Reactors react to events in several ways:
        a) Reactors can raise new events at a different level of abstractions
        b) Reactors can trigger side effects that logicallt follow from an event.
3. Reactors leave an audit trail in the form of events.
4. Reactors are decoupled from each other and do not share states.
5. Reactors are often a source of necassary or accidental complexity.

















