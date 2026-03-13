# Invocation

An **Invocation** is a conceptual unit of work within the ADK Runtime, representing the complete processing cycle for a single user interaction.

## Definition

An Invocation encompasses everything that occurs from the moment the [Runner](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Runner.md) receives a user query until the [Agent](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Agent.md) has finished processing that query and is ready for new input.

## Trigger Conditions

- **User Query**: The primary trigger is an external input from a user (e.g., a chat message).
- **Automated Triggers**: In some advanced configurations, a system event or scheduled task might trigger an invocation, treating the system signal as the "query."

## Scope and Composition

A single Invocation is identified by a unique `invocation_id`. Within this single scope, multiple operations may occur:
- **Multiple Agent Runs**: The main agent might delegate tasks to sub-agents.
- **Tool Executions**: The agent may call multiple [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md) functions (e.g., search, calculate, summarize) in sequence.
- **LLM Calls**: The agent may make several round-trips to the Large Language Model to refine its answer.
- **Callbacks**: Pre- and post-execution hooks may run.

All these activities share the same [Invocation Context](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Invocation_Context.md) and contribute to the same transactional update of the [Session](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Session.md).

## Termination

The Invocation ends when the Agent yields a final event indicating it is done (e.g., returning the answer to the user) and ceases to yield further actions for that specific turn. Any temporary data scoped to the Invocation (variables prefixed with `temp:`) is then discarded.
