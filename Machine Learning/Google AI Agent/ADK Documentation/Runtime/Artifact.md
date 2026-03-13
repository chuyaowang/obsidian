# Artifact

An **Artifact** represents a piece of binary or large data generated during the runtime execution that needs to be persisted but is unsuitable for direct inclusion in the textual conversation history.

## Definition

Artifacts are distinct data objects, such as images, audio files, PDF documents, or large datasets, that are generated or retrieved by an [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) or [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md). Unlike standard state variables (which are small text/numbers), Artifacts are handled by a dedicated service.

## Origin

Artifacts are typically created in two ways:
1.  **Tool Output**: A tool might generate a chart (`.png`) or download a file.
2.  **Agent Generation**: An agent might synthesize speech (`.mp3`) or generate an image.

## Lifecycle and Storage

The lifecycle of an Artifact is managed by the `ArtifactService` (a component of [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md)).

1.  **Creation**: The execution logic calls a method (e.g., `save_artifact`) on the [Invocation Context](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Invocation_Context.md).
2.  **Delta Signal**: Similar to state changes, the creation of an artifact is signaled to the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) via an `artifact_delta` in the yielded [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md).
3.  **Persistence**: The Runner uses the `ArtifactService` (e.g., `GcsArtifactService` for cloud storage or `InMemoryArtifactService` for testing) to write the binary data to the storage backend.
4.  **Reference**: A reference to the stored artifact (e.g., a URI or ID) is typically saved in the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) history or state, linking the large binary data to the conversation flow.

## Types

While the system handles "binary artifact data" generally, common types include:
- **Images**: PNG, JPG (e.g., generated plots).
- **Documents**: PDF, CSV, TXT (e.g., reports).
- **Audio/Video**: Media files generated or processed by the agent.
