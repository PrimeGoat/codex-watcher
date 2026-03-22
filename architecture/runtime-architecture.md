# codex-watcher Runtime Architecture

## Core Runtime Parts

The runtime consists of these core parts:

- `filter` / `proxy`
  - the main interception and routing runtime
  - handles each Codex API request by coordinating internal components, emitting observable events to Codex when needed, forwarding the original or adjusted request upstream, and returning the upstream response in streamed or non-streamed form

- `watcher`
  - a subsystem of the filter
  - analyzes requests and may produce meta outputs, routing guidance, module invocations, warnings, or other sidecar decisions

- `orchestrator`
  - the request-scoped controller inside the filter
  - creates request context, initializes the stream sink, invokes the watcher, manages blocking versus queued work, forwards upstream calls, and tears down the request cleanly

- `stream sink`
  - the request-scoped serialized output channel for visible activity and forwarded streamed events
  - modules emit structured events through it instead of writing raw transport output directly

- `modules`
  - pluggable subsystems invoked by the filter
  - each module can declare whether it is blocking or queued
  - ContextOS methods 19 and 20 are intended to become later modules, but the module system must support them generically from the start

## Settled Architectural Decisions

- the interception path is `config.toml` plus proxy
- the system is passthrough-first
- the watcher exists from the start, but v1 watcher behavior can remain simple and passthrough-compatible
- the proxy is the filter, and the watcher is a subsystem of that filter
- control flow is synchronous and blocking where needed
- communications and visible-event flow are asynchronous
- the proxy process stays alive globally while each request-scoped orchestration flow drains, closes, and tears down its own resources cleanly
- the system should support the Responses API and current protocol surfaces; Responses-only is acceptable
- streaming is required
- local HTTP is acceptable for the initial implementation; local TLS is unnecessary
- fortified-process-like behavior should live in the filter/runtime rather than as a Codex-visible concept

## Execution Model

1. the proxy receives a Codex-facing request
2. the orchestrator creates request context
3. the orchestrator creates a request-scoped stream sink
4. the orchestrator invokes the watcher synchronously
5. the watcher may emit structured visible events through the sink while running
6. the watcher returns its result payload
7. the orchestrator uses that result to decide what blocking work must happen before forwarding
8. queued and non-blocking work is enqueued
9. the upstream call is forwarded as needed
10. upstream streamed output may also be forwarded through the sink
11. the request completes
12. the request-scoped sink drains and closes cleanly
13. the request context is torn down
14. the proxy remains alive for the next request
