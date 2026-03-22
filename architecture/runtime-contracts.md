# codex-watcher Runtime Contracts and Execution Semantics

## Orchestrator and Watcher Contract

The orchestrator creates a request-scoped stream sink, passes an emitter handle into the watcher, and invokes the watcher synchronously.

The watcher may emit visible events while running, but it separately returns a result payload that the orchestrator uses for control flow.

Modules do not write raw protocol frames directly to the transport. They emit structured events through the stream sink.

## Blocking Versus Queued Work

Blocking is determined by dependency.

A thing is blocking only if the filter output depends on it.

Examples of non-blocking work:

- raw transcript logging
- journal updates
- metrics and event logging
- post-turn summarization
- non-essential state updates
- topic-tree updates that do not affect the current request

Examples of blocking work:

- request routing decisions that affect forwarding
- context injection needed before forwarding
- watcher or model analysis whose result changes the outgoing request
- safety or policy behavior that must resolve before forwarding

Examples of conditional work:

- watcher analysis can be non-blocking if it only emits sidecar metadata
- watcher analysis becomes blocking if its result changes routing, prompt shaping, or required context

## Module System Expectations

The module system must support pluggable blocking and queued modules from the start, even though some later phase features remain unresolved.

The architecture must support later ContextOS-derived modules generically instead of hardcoding special cases for them.
