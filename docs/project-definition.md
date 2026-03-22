# codex-watcher Project Definition

## Identity

`codex-watcher` is a Codex API filter/proxy runtime.

It sits in front of Codex's normal API usage, stays transparent where possible, and improves Codex for project-oriented work through structured interception, modular background behavior, stronger project awareness, and controlled observability.

This project came out of ChaiChat design work, where it became clear that several Codex limitations were better addressed by an external runtime layer than by prompting alone.

`codex-watcher` is not ChaiChat itself. It is a general Codex-facing support system intended to improve how Codex is used across projects.

## Purpose

The purpose of `codex-watcher` is to improve Codex as a working system by adding capabilities that should not depend entirely on Codex's native foreground session context.

The system is intended to provide:

- transparent API interception through `config.toml` plus proxy routing
- structured request and response logging
- externalized project and context awareness
- modular background processing
- watcher and meta-analysis outside the main foreground lane
- controllable visible activity streaming
- cleaner separation between transcript history and truth-state

## Scope Position

The project is meant to change how Codex is used in general, not only for one repo.

The initial external surface should be OpenAI-compatible first.

A future ChaiChat-native or project-native admin/control API may be useful later, but it is not part of the first surface.

## Initial Deliverables

The first deliverables are:

- architecture spec
- contract spec
- initial filter/watcher/runtime design
- storage model
- streaming/observability model
- provider recursion strategy
- task set and dependency structure

The first deliverables are explicitly not:

- premature full implementation
- management initialization from the exporting project
- overbuilt event-system architecture before it is earned
