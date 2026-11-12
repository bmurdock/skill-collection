# Incremental review and handoff

Use for follow-up remediation or reuse of prior review and check evidence. Keep the ledger in an existing authorized artifact or the response.

Identify the last reviewed baseline and current target. For uncommitted work, retain a diff/content fingerprint and relevant untracked inputs; HEAD alone is insufficient. If the baseline cannot be verified, re-establish the affected scope and disclose the coverage gap.

Re-review the delta, affected callers/contracts, unresolved findings, and previously uncovered risks. Expand within authorized scope when new evidence warrants it. An explicit full or independent review retains its requested coverage; prior clean results do not substitute for independent judgment.

Carry only what the next phase needs:

- Objective and authorized scope; repository/worktree and baseline/target fingerprints.
- Covered surfaces, known omissions, accepted decisions, and source references.
- Finding ID, disposition, location, evidence, and remaining question.
- Check command, result, timestamp, and tested code/dependency/configuration/environment identity.
- Changed inputs, validation limitations, remaining gates, next action, and stopping condition.

Reuse checks only for unchanged tested inputs and relevant environment. Rerun affected checks and complete mandatory repository checks. Label reused results as prior evidence, never as fresh runs. Keep source/log links instead of copied transcripts. Local validation does not establish hosted CI, publication, or external acceptance.
