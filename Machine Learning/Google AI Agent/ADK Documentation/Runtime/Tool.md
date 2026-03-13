# Tool

A **Tool** is a modular component within the Execution Logic that provides specific capabilities or functions to an [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md).

## Definition

A Tool is a wrapper around a specific function or external API call (e.g., `BaseTool`, `FunctionTool`). It allows the agent to interact with the outside world (e.g., searching the web, querying a database) or perform deterministic computations.

## Purpose

The purpose of a Tool is to extend the capabilities of the core language model. Since LLMs are restricted to text generation, Tools provide the "hands" for the Agent to perform actions and retrieve dynamic information.

## Key Attributes

- **Definition**: Includes a name, description, and schema for arguments, allowing the LLM to understand how and when to use it.
- **Execution**: Contains the actual code to perform the task.
- **Result Wrapping**: When a Tool executes, its result is wrapped in an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md). This ensures that the result is treated consistently by the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) and added to the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md) history.

## Relationships

- **Called By**: Tools are typically invoked by an [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) (or the Runner on behalf of the Agent).
- **Yields**: The execution of a tool results in an [Event](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Event.md) containing the tool output.
- **Integration**: Tools operate within the same Event Loop managed by the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md).
