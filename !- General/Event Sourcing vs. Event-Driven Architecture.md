# Event Sourcing vs. Event-Driven Architecture

## Event-Driven Architecture
- **Primary Focus**: Communication between systems/components
- **Purpose**: Components react to events as they happen
- **Events**: Represent notifications of something that happened
- **Storage**: Events are typically processed and not necessarily stored long-term
- **State**: Maintained separately in databases or services
- **History**: Not inherently focused on maintaining history

## Event Sourcing
- **Primary Focus**: State management pattern
- **Purpose**: Rebuild state from a sequence of events
- **Events**: Represent state changes that have happened
- **Storage**: Events are the source of truth and permanently stored
- **State**: Derived by replaying events; current state is a projection
- **History**: Complete audit history is a core feature

## Key Differences
- Event-Driven Architecture is about communication; Event Sourcing is about state storage
- EDA can exist without Event Sourcing, but Event Sourcing typically uses events for communication too
- In EDA, events notify; in Event Sourcing, events reconstruct

## Common Confusion
People often confuse these because both use events, but their purposes are fundamentally different. Event Sourcing is a specific approach to persistence, while Event-Driven Architecture is a broader system design pattern.

## When to Use
- Use Event-Driven Architecture when services need to react to changes without tight coupling
- Use Event Sourcing when audit trails, temporal queries, or complex state reconstruction are required

They can be used together in the same system, with Event Sourcing providing the persistence mechanism for some components within an Event-Driven Architecture.