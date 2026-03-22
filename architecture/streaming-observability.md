# codex-watcher Streaming and Observability Model

## Observability Plane

The system must support visible streamed activity.

It should be able to expose:

- the filter's own visible activity
- forwarded streamed output from the primary upstream API call
- optionally, streamed thinking, tool activity, or other visible activity from the watcher's own API call when the watcher explicitly requests that visibility

This establishes an observability plane separate from the control plane.

## Visible Event Model

The filter should be able to emit visible events such as:

- request received
- watcher running
- routing decision in progress
- logging complete
- queued job created
- upstream stream started
- upstream tool activity
- watcher-requested visible analysis or tool activity

Visibility must be structured and controlled. Internal behavior is not automatically user-visible.

Modules must be able to request visible output without directly owning the transport.
