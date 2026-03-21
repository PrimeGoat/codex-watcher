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
