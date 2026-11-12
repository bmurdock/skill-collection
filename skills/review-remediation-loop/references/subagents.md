# Subagent guidance

Use only when delegation materially benefits the authorized remediation. The parent owns consequential decisions, critical-path diagnosis, integration, final validation, and completion.

For independent investigation or re-review, give the agent the exact baseline, finding IDs, allowed files, read/write boundary, required checks, and compact output schema. Require file or command references and observed results rather than exploration logs. Wait for requested results and validate actionable claims before accepting them.

The `remediation_explorer` and `remediation_reviewer` roles are useful when installed and suitable. They are optional environment choices, not requirements. Use another suitable available agent when needed. If delegation is unavailable or inappropriate, perform the separate re-review in the parent and report that it was not independent.

Treat a configured `sandbox_mode = "read-only"` as a requested default, not proof of the effective boundary. Confirm the active permissions. If parent permissions may override isolation, state the no-edit rule and compare the worktree before and after. Do not delegate when hard read-only isolation is required but unavailable.

Default to one writer. Parallel writers require disjoint files, tests, generated artifacts, dependencies, and ownership. Avoid overlapping edits, recursive fan-out, delegation of the immediate blocker, and work whose next step depends on the delegated result.
