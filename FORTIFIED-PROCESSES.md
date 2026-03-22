# Fortified Processes
# This file holds mutable fortified-process entries for GENERAL.
# Do not duplicate the foundational self-education fortified process here. That entry is inlined in `AGENTS.md` and is authoritative there.
# Entry format:

{ name: concise one-line human-readable fortified-process name
- match:
     ```content here```
- become:
     ```content here```
}

# Add mutable fortified-process entries below this line. Nothing above this line counts as an entry, nothing below this line counts as commentary to interpret outside of the actual listings.

{ name: Code-Architecture Sync
- match:
     ```update source code```
- become:
     ```after updating source code, determine whether any architecture docs became inaccurate or incomplete; if so, update them as needed to restore accuracy and completeness```
}

{ name: Architecture-Code Reconciliation
- match:
     ```update architecture/ contents not as a result of a fortified code update```
- become:
     ```after updating architecture docs, ensure the source code still reflects the updated architecture; if it does not, notify the user and create a task describing the source-code changes required for architectural compliance; express that task as a natural-language higher-level programming assignment describing what must be implemented in the codebase, not as a source diff and not merely as a statement to update code to match architecture```
}

{ name: Project-Journal Sync
- match:
     ```perform a meaningful project-state-changing action```
- become:
     ```if the action is a journal update, do nothing; then determine whether the project's operational history materially changed; if so, append a concise entry to notes/journal.md capturing what changed, why it mattered, and any immediate consequence for future work; treat the journal as a historical trace rather than a source of truth, and do not log trivial chatter or insignificant edits```
}

{ name: Knowledge-Document Reference Check
- match:
     ```write Atlas knowledge```
- become:
     ```ensure Atlas knowledge derived from documents references the corresponding document path/filename```
}

{ name: Document-Knowledge Sync Check
- match:
     ```update canonical repo documentation```
- become:
     ```ensure Atlas knowledge referencing the updated documentation is updated as needed```
}

{ name: Canonical Surface Sync
- match:
     ```ingest source material into canonical project information surfaces```
- become:
     ```update canonical repo docs, Atlas knowledge (referencing repo docs if applicable), Atlas tasks, and project_state as applicable using established conventions```
}
