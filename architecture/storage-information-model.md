# codex-watcher Storage and Information Model

## Storage Split

The intended storage split is:

- Codex local history
  - session log
  - what was said
  - what happened

- database truth/state
  - structured truth-oriented project and runtime state
  - not mere transcript dumping

This project is expected to use SurrealDB as the likely database substrate for truth/state and other structured runtime data.

Transcript logging and truth-state storage should remain conceptually separate even if both are written during a request.

## Information Placement Doctrine

Necessary project knowledge comes from authoritative project-information surfaces, not from chat alone.

Before project-relevant reasoning or action, load the necessary authoritative context for the current matter unless current context already reflects that knowledge with sufficient accuracy after authoritative loading and any subsequent authoritative adjustments.

Current-session directives and decisions override previously recorded state immediately.

Project information should be stored in the surface where future lookup will actually look for that kind of information.

`project_state` is the compact machine-readable aggregate of current project truth, not a dump of full docs, architecture, or chat history.

Codex local history should be treated as the session log of what was said and what happened.

The database should store truth/state.

Raw transcript logging should exist first, with DB-update connectors designed modularly so components remain self-contained.
