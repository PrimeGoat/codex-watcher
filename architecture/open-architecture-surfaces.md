# codex-watcher Open Architecture Surfaces

## Provider and Recursion Model

The system should forward to OpenAI directly first, while allowing future provider and routing flexibility.

Background LLM lanes should default to using the same provider behavior as the forwarded call, but they must not recursively pass back through the filter in a way that creates stack growth or infinite recursion.

The exact recursion-prevention mechanism remains unresolved and is a required design task.

## Tooling Exposure

Tool exposure is not fully decided.

It is under consideration that the filter may expose an MCP surface back to Codex for direct interaction where needed.

Because multiple LLM calls may exist in one request path, tool visibility must be designed explicitly rather than assumed.

## Metadata and Future Control Surface

The metadata contract from Codex to the proxy remains to be defined.

A future non-OpenAI-native admin/control API may be useful, but it is not part of the first external surface.
