# Session

A **Session** is a data container that serves as the "memory" of a specific conversation or interaction instance.

## Definition

A Session is an object that holds the complete context of an interaction between a user and the agent application. It persists across the individual steps of the event loop.

## Purpose

The purpose of the Session is to maintain continuity. It ensures that the [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) remembers previous turns in the conversation, the results of past tool calls, and the current value of any state variables.

## Key Attributes

- **Event History**: A chronological list of all [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) objects that have occurred in the conversation.
- **State Dictionary**: A key-value store for application state (e.g., user preferences, current step in a workflow).
- **Artifact References**: References to binary data (images, files) managed by the Artifact Service.
- **Invocation Context**: Variables prefixed with `temp:` are scoped only to the current invocation (a single user query) and are cleared afterwards.

## Relationships

- **Managed By**: The lifecycle and persistence of the Session are managed by [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md) (specifically `SessionService`).
- **Updated By**: The [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) triggers updates to the Session whenever an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) with side effects is processed.
- **Read By**: The [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) reads the Session to understand the current context.
