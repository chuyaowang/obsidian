# Event

An **Event** is the fundamental unit of communication within the ADK Runtime architecture. It represents a single, atomic occurrence or message passed from the Execution Logic back to the Runner.

## Definition

An Event is a data structure yielded by components like the [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) or [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md) to signal that something has happened or that a specific action needs to be taken.

## Purpose

The purpose of an Event is to decouple the agent's logic from the system's state management and side effects. Instead of modifying the global state directly, an agent yields an Event describing the desired change. This allows the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) to handle the persistence and synchronization of that change reliably.

## Key Attributes

- **Content**: The payload of the event, which could be a text message for the user, a tool call request, or the result of a tool execution.
- **Actions (Side Effects)**: Events often carry a set of actions, such as `state_delta` (requests to update the session state) or artifact creation requests.
- **Atomic Nature**: Each event is treated as a discrete unit. The Runner processes one event at a time, ensuring that the state changes associated with it are committed before moving to the next step.

## Relationships

- **Yielded By**: Events are created and yielded by the **Execution Logic** ([Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md), [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md), or Callbacks).
- **Processed By**: The [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) consumes events to update the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) via [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md).
- **Carries**: It carries data that eventually propagates to the User Interface.
