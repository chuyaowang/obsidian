# Runner

The **Runner** is the central coordinator and orchestrator of the Google Agent Development Kit (ADK) Runtime architecture. It serves as the engine that drives the execution of an agent application during a user invocation.

## Definition

The Runner is a runtime component responsible for managing the **Event Loop**. It acts as the intermediary between the **Execution Logic** (such as [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) and [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md)) and the supporting infrastructure (like [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md)).

## Purpose

The primary purpose of the Runner is to ensure the orderly execution of the agent's logic and the consistent application of state changes. It abstracts the complexity of state management and event propagation away from the agent logic, allowing developers to focus on the decision-making capabilities of the agent.

## Key Attributes

- **Event Loop Management**: The Runner implements a "yield, pause, process, resume" cycle. It starts the execution, waits for an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) to be yielded, pauses the agent, processes the event, and then resumes the agent.
- **State Coordination**: Upon receiving an event with side effects (such as a state change request), the Runner coordinates with [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md) (specifically the Session Service) to commit these changes to the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md).
- **Upstream Forwarding**: After processing an event internally, the Runner forwards it upstream to the calling application or User Interface (UI), ensuring the user sees the agent's progress (e.g., intermediate thoughts, tool calls, or final answers).
- **Invocation Scoping**: The Runner manages the lifecycle of a single "Invocation" (processing one user query), initializing the context and handling the flow until the agent completes its task.

## Relationships

- **Controls**: The Runner invokes and controls the execution flow of the [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md).
- **Receives**: It receives [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) objects yielded by the Execution Logic.
- **Uses**: It utilizes [Services](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Services.md) to persist state and history.
- **Updates**: Through the services, it ensures the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) is updated before the agent resumes.
