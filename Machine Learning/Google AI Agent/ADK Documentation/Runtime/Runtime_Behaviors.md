# Runtime Behaviors

This note details critical behaviors of the ADK Runtime, focusing on state management consistency and output handling.

## State Updates and Commitment Timing

The ADK Runtime employs a strict "Yield-Commit" model to ensure the consistency of the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) state.

### The Mechanism

1.  **Local Modification**: When [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) code modifies the state (e.g., `ctx.state['key'] = 'val'`), the change is initially recorded *locally* within the [Invocation Context](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Invocation_Context.md).
2.  **The Yield**: The agent yields an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) containing these changes (as a [State Delta](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/State_Delta.md)).
3.  **The Commitment**: The [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) processes the event and uses [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md) to persist the changes to the Session.

### Guarantee

Only code running **after** the agent resumes from the yield is guaranteed to see the committed state. This ensures that if the system crashes mid-execution, the state remains consistent with the last successfully processed event.

## Dirty Reads

A "Dirty Read" occurs when code reads a state variable that has been modified locally but not yet committed via a yield.

### Mechanics

- **Visibility**: Within a single [Invocation](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Invocation.md), components (like tools or callbacks) running *before* the state-changing event is yielded can often see the local, uncommitted changes.
- **Benefit**: This allows different parts of the logic (e.g., multiple callbacks) to coordinate using shared state without needing to pause execution for a full commit cycle.
- **Risk**: Relying on dirty reads is risky for critical logic. If the invocation fails before the event is processed, the uncommitted change is lost. **Best Practice:** Critical state transitions should always be associated with an event that is immediately yielded.

## Streaming vs. Non-Streaming Output

The Runtime supports both streaming (token-by-token) and non-streaming (atomic) responses from LLMs.

### Streaming

- **Process**: The LLM generates small chunks of text. The framework yields multiple `Event` objects, mostly marked with `partial=True`.
- **Runner Handling**:
    - **Partial Events**: The Runner forwards these immediately upstream (for UI display) but **skips** processing side effects like [State Delta](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/State_Delta.md).
    - **Final Event**: The stream concludes with a final event (where `partial=False`). The Runner **fully processes** this event, committing all accumulated state changes and artifacts.
- **Purpose**: This allows users to see the text being typed out while ensuring state changes happen atomically only once the full response is available.

### Non-Streaming

- **Process**: The LLM generates the entire response at once.
- **Handling**: The framework yields a single, non-partial `Event`. The Runner processes it fully, committing state and forwarding the message in one go.
