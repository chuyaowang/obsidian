# State Delta

**State Delta** (`state_delta`) is a key concept within the ADK Runtime used to manage and propagate changes to the application's state during an execution cycle.

## Definition

`state_delta` is a component of the `EventActions` object, which is itself part of an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md). It represents a *proposed* change or update to the persistent [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) state.

## Format

Technically, `state_delta` is formatted as a **dictionary** (or map) of key-value pairs.
- **Keys**: Strings representing the names of the state variables to be updated.
- **Values**: The new values for those variables.

Example (Conceptual Python):
```python
state_delta = {
    "current_step": "verification",
    "user_intent": "purchase",
    "retry_count": 2
}
```

## Update Mechanism

The update process follows a strict "yield-commit" pattern to ensure consistency:

1.  **Proposal**: When the [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) or [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md) logic modifies the state (e.g., `ctx.state['key'] = 'val'`), this change is initially recorded locally within the [Invocation Context](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Invocation_Context.md).
2.  **Yielding**: The agent yields an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) containing the `state_delta` in its `actions` field.
3.  **Processing**: The [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) receives the event.
4.  **Committing**: The Runner passes the `state_delta` to the `SessionService` (see [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md)). The service applies these updates to the persistent [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) object.
5.  **Synchronization**: When the agent resumes execution after the yield, the `state_delta` has been fully committed, ensuring the agent sees the most up-to-date, persisted state.

## Dirty Reads

[Dirty Reads](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runtime_Behaviors.md#Dirty%20Reads)

Code running within the same [Invocation](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Invocation.md) *before* the event is yielded may see "dirty" (uncommitted) local changes. However, relying on these is risky. If the invocation crashes before the event is yielded and processed, these local changes are lost. The only guarantee of persistence is the successful processing of the `state_delta` by the Runner.
