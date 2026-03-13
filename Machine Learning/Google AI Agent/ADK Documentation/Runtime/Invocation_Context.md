# Invocation Context

The **Invocation Context** (often abbreviated as `ctx` in code) is a temporary object that serves as the interface between the executing code and the runtime environment during a specific [Invocation](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Invocation.md).

## Definition

The Invocation Context is a context object prepared by the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) at the start of a request. It is passed to [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) methods, [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md) functions, and callbacks, providing them with access to data and capabilities.

## Accessible Data and Scope

The `ctx` object provides access to several critical resources:

### 1. Session State

- **Access**: `ctx.session.state`
- **Description**: The current persistent state of the conversation. It reflects changes committed from previous events.
- **Behavior**: Reading this gives the most up-to-date committed state. Writing to it (locally) prepares a [State Delta](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/State_Delta.md) that will be committed when the next event is yielded.

### 2. Temporary Variables

- **Access**: Variables with keys prefixed by `temp:` (e.g., `ctx.session.state['temp:loop_counter']`).
- **Scope**: Strictly scoped to the current **Invocation**.
- **Lifecycle**: These variables are initialized when the invocation starts and are automatically discarded/cleaned up when the invocation ends. They are useful for loop counters or intermediate flags that do not need to persist across different user queries.

### 3. Services and Utilities

- **Service Access**: It exposes methods to interact with [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md), such as `ctx.save_artifact(...)` to store binary data.
- **Metadata**: It contains the `invocation_id` and other metadata relevant to the current execution run.

## Lifecycle

1.  **Creation**: Created by the Runner when a user query is received.
2.  **Usage**: Passed into `_run_async_impl` (Agent) and `run` (Tool).
3.  **Destruction**: Destroyed (garbage collected) once the invocation concludes.
