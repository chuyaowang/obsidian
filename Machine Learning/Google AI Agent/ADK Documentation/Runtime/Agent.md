# Agent

The **Agent** is the primary component of the **Execution Logic** in the ADK Runtime. It encapsulates the core decision-making and computational capabilities of the AI application.

## Definition

An Agent is a Python class (inheriting from `BaseAgent` or `LlmAgent`) that implements the specific logic for processing user input and generating responses. It operates within the context provided by the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md).

## Purpose

The Agent's purpose is to "think" and "act." It takes the current context (user input, conversation history, and state) and determines the next step. This might involve generating a text response, deciding to call a [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md), or updating its internal state.

## Key Attributes

- **`_run_async_impl`**: The core method where the agent's logic resides. This method is designed to be a generator (using `yield`).
- **Yielding Events**: Instead of returning a final result immediately, the Agent yields [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) objects.
- **Pause and Resume**:
    1.  The Agent performs some logic.
    2.  It yields an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) (e.g., "I need to check the weather").
    3.  **Execution Pauses**: The Agent's code effectively freezes at the `yield` statement.
    4.  **Resumption**: Once the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) has processed the event and updated the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md), the Agent resumes execution on the very next line, now with access to the updated state.

## Relationships

- **Controlled By**: The [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) drives the Agent's execution.
- **Uses**: The Agent may utilize one or more [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md) components to perform actions.
- **Produces**: It generates [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) objects.
- **Reads**: It reads the state from the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) (via the context) to make informed decisions.
