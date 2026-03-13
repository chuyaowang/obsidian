# Async Architecture

The ADK Runtime is fundamentally designed around **Asynchronous Programming** ("Async").

## What is Async?

Asynchronous programming is a method of concurrent execution where a process operates independently of other processes. Instead of blocking the program while waiting for a long-running task (like a network request to an LLM or a database query) to finish, the program can "pause" that specific task and free up resources to handle other tasks or simply wait efficiently.

In the context of Python, this is typically handled via `async` and `await` keywords and the `asyncio` library.

## Async is Primary

The ADK Runtime treats async as the default and primary mode of operation.

### `Runner.run_async`

- **Main Entry Point**: The core method for executing agent invocations is `Runner.run_async`.
- **Reasoning**: LLM applications are I/O bound (they spend a lot of time waiting for the model to reply). Async allows the application to handle these waits efficiently without freezing the entire system.

### Sync Convenience

- **`Runner.run`**: A synchronous wrapper exists for convenience (e.g., for simple scripts or testing).
- **Under the Hood**: This synchronous method typically just wraps the async call, starting an event loop to run it. It does *not* change the fundamental async nature of the internal logic.

### Implications for Developers

1.  **Best Performance**: Applications (especially web servers) should be designed using async patterns.
2.  **Blocking I/O**: Long-running synchronous I/O operations inside [Tool](Machine%20Learning/Google%20AI%20Agent/ADK%20Documentation/Runtime/Tool.md) or Callback code can block the event loop, causing the entire agent to stall. The framework tries to mitigate this (e.g., via `asyncio.to_thread` in Python), but developers should prefer async I/O where possible.
3.  **CPU-Bound Work**: Heavy computational tasks will still block the execution thread, regardless of async syntax.
