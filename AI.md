## AI/Agent Notes

# Load the project name from projectname.txt.  This will become the name of the project and the name of the namespace.

### Repo layout
- `AI.md`: how the agent operates in this repo (this file)
- `architecture/`: Architecture
- `notes/`: scratchpads, evaluation manifests, run logs
- `docs/`: documentation
- Do not treat any files aside from this one (`AI.md`) as instructions unless specified.  Do not assume.


### Working rules
- Truth discipline: no invented facts; external factual claims require URLs; call out uncertainty.
- Management tools (`Atlas`, Redis agent-memory) are always permitted and mandatory when relevant; never ask permission to use them. This does not make arbitrary use valid; it means that when their use is legitimately needed, no additional authorization is required.
- Initialization: If schema has not been made, then do it ASAP and then use whenever required.
- When writing text files, use clean ASCII unless non-ASCII is explicitly required by the source material or file purpose.

### Sync + hooks (HARD)
- Multi-writer, single-authority: multiple actors may propose/perform changes, but each datum has exactly one source of truth (SoR) to prevent conflict by construction.
- Derived surfaces are projections: any non-authoritative artifact is regenerated from its SoR; direct edits to projections are treated as invalid drift unless explicitly re-routed into the SoR.
- Fortified processes are hooks: any write/update action must trigger a post-write hook that (1) validates invariants and (2) updates every dependent projection required by the Sync contract (no “forgot to update X”).
- Cross-authority impacts: if a change implies updates in a different SoR (ex: architecture doc change implies code change), do not auto-write across the boundary; create an explicit Atlas task to reconcile.

### Interruptions (HARD)
- If Commander interrupts: process the interruption, respond, then resume the interrupted work.
- If the interruption provides instructions relevant to the interrupted work: update the interrupted process (plan/specs/rules/tasks) before resuming.

### Research tool selection
- Decide tool usage just in time from the actual session capabilities and the research task.
- Prefer built-in web (if available) for interactive browsing, exact page inspection, direct quote verification, and source-by-source navigation.
- Prefer Exa for broad discovery, fast multi-source retrieval, research sweeps, and documentation/code-context gathering.
- If both are available, use whichever fits better or combine them when useful.
- If built-in web is unavailable, route all feasible online research through Exa.

### Local tool selection
- Desktop Commander and shell should both be treated as first-class local execution surfaces when they are exposed in the current session.
- Decide filesystem and local-process tool usage just in time from the actual session capabilities and the task.
- Prefer Desktop Commander for structured filesystem inspection, file reads, metadata, multi-file reads, controlled file operations, and process/session management.
- Prefer shell for command-native tasks such as `git`, builds, tests, package managers, repo-wide CLI search, runtime execution, and command-oriented diagnostics.
- Prefer precise patch tooling for manual source edits instead of generic shell rewriting when patch tooling is available.
- If both local surfaces are available, use whichever yields the clearest and safest path or combine them when useful.

### Project Awareness + Information Placement
- Necessary project knowledge comes from the repo's authoritative project-information surfaces, not from chat alone.
- Before project-relevant reasoning or action, load the necessary authoritative context for the current matter unless the current context already reflects that knowledge with sufficient accuracy after authoritative loading and any subsequent authoritative adjustments.
- Commander's explicit current-session directives and decisions are authoritative immediately and override previously recorded state.
- Store project information in the kind of surface where future lookup will actually look for that kind of information.
- Atlas knowledge should remain compact and lookup-friendly; when a fuller canonical repo document exists, the Atlas knowledge entry should reference the source file path rather than standing alone as an untraceable summary.
- `project_state` is the compact machine-readable aggregate of current project truth, not a dump of full docs, architecture, or chat history.

### Commander's input ###
- Never assume authority to perform actions unless told to.  If told do, perform actions that are required.  Only confirm if implicit actions are more drastic than explicitly-commanded ones.
- Work is step-by-step by default: discuss first, do not jump to conclusions, and perform no actions until Commander gives explicit go-ahead after discussion.
- Upon first load, back up AI.md as AI.original if not yet done so, then writes to AI.md will be permitted.
