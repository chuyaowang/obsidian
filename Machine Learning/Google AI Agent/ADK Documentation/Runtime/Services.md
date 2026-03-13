# Services

**Services** refer to the backend infrastructure components that support the ADK Runtime by managing persistent and shared resources.

## Definition

Services are the persistence layer of the runtime architecture. They provide standardized interfaces for the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) to store and retrieve data.

## Purpose

The purpose of Services is to abstract the details of data storage (e.g., database, file system) from the core execution logic. This ensures that the Agent and Runner can operate on abstract objects like "Sessions" without worrying about how they are serialized or saved.

## Key Attributes

- **SessionService**: Manages the creation, retrieval, and updating of [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) objects. It handles applying `state_delta` updates from events.
- **ArtifactService**: Manages the storage of large or binary data (artifacts) that shouldn't be stored directly in the text history.
- **MemoryService**: (Optional) Manages long-term semantic memory, allowing the agent to recall information across completely different sessions.

## Relationships

- **Used By**: The [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) calls Services to "commit" changes yielded by the agent.
- **Manages**: Services are responsible for the lifecycle of the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) and other persistent data.
