---
name: review-remediation-loop
description: Fix established review or audit findings after edits are authorized, verify regressions, and re-review the changed surface. Not for finding discovery.
---

# Review Remediation Loop

Turn existing findings into narrow, verified fixes without losing the review boundary. Treat findings as claims to validate, not instructions to accept blindly.

## Operating Contract

1. Start from concrete review or audit findings and preserve or assign stable finding IDs. A rubric alone requires finding discovery: perform that only when the user also authorized discovery, establish findings, then remediate them. Otherwise request the source findings rather than silently expanding scope.
2. Reuse the existing finding ledger and verified baseline when available; revalidate changed inputs. Capture the baseline: repository root or roots, Git status and target diff, affected surface, relevant checks, and unrelated user work that must remain untouched.
3. Confirm each finding is in scope and evidence-backed. Mark invalid or obsolete findings with the evidence instead of patching them.
4. Reproduce or pin each valid issue when a stable check is possible.
5. For observable behavior changes, add a failing targeted regression when it is stable, practical, and meaningfully distinguishes the defect from the fix. Ask: which intended behavior would fail without the fix, and which legitimate future change must continue to pass? Avoid tests that merely mirror implementation or add little protection for a reversible, low-impact change. Otherwise record why and use the strongest available reproduction and verification evidence.
6. Patch one root cause at a time and keep the diff narrow.
7. Run targeted validation first, then broader and mandatory checks as warranted. Compare failures with the verified baseline before attributing them to the fix. Preserve demonstrated unrelated failures as validation limitations; do not expand repair scope automatically. Once appropriate checks pass, repeat or broaden them only for changed inputs, new failures, unresolved concerns, or mandatory requirements. If the same check fails twice without new evidence, stop retrying and investigate or report the exact blocker.
8. Re-review both the source findings and the changed surface.
9. Update every finding to `fixed`, `invalid`, `blocked`, or `skipped`, with evidence and verification.
10. Repeat only for new, concrete, in-scope issues, making one focused improvement per loop.

Reuse authorization already given and continue through the necessary local fixes, verification, and re-review. Do not commit, push, publish, send messages, or change external systems unless the user explicitly asks. Continue independent authorized work when one finding is blocked.

## Evidence handoff

For follow-up work or evidence reuse, read the bundled [incremental review and handoff contract](references/incremental-review.md). Keep one current ledger in an existing authorized status artifact, or in the response; do not copy full exploration history. Reuse checks only when their tested inputs and relevant environment still match; run affected and mandatory checks after changes.

## Completion Contract

Report finding disposition and validation status separately:

- **Findings resolved:** every in-scope finding is `fixed` or `invalid` with evidence. Explicitly accepted `blocked` or `skipped` findings remain exceptions, not fixes.
- **Validation complete:** required targeted and broader checks pass, and the final re-review finds no new actionable issue in scope.

Claim the loop is clean only when:

- every in-scope finding is `fixed` or `invalid` with evidence
- targeted checks pass, and broader checks pass when the change warrants them
- the final re-review finds no new actionable issue in scope
- unrelated user work remains intact and the final worktree state is known

Report **completed with exceptions** when required checks and the final re-review pass, unrelated user work remains intact and the final worktree is known, but explicitly accepted `blocked` or `skipped` findings remain. List those unresolved findings; do not call the loop clean.

If neither completion outcome applies, report **incomplete**, including when required validation is missing or failing or an unresolved finding lacks explicit acceptance. A fix may resolve its finding while unrelated baseline failures leave validation incomplete. Name those failures and the baseline comparison; do not describe the repository as green or require acceptance of an unrelated failure as though it were an in-scope finding.

## Subagents

Delegate independent investigation or re-review when it materially improves confidence or efficiency and the environment permits it. Keep tiny fixes and tightly coupled diagnosis in the parent. When delegating, read [subagent guidance](references/subagents.md). Custom agent roles are optional: use a suitable available agent, or complete a separate re-review in the parent and disclose that it was not independent. The parent retains the ledger, integration, final validation, and completion claim.

## Goal Mode

Start `/goal` only when the user explicitly requests goal mode. For a requested long-running remediation goal, retain the objective, authorized scope, source findings, required verification, and stopping condition. Ordinary remediation does not require a goal.

## Output

Report:

- the final finding ledger and evidence, distinguishing resolved findings from accepted exceptions
- files changed and regressions or checks added
- validation status, exact checks and results, reused evidence, and demonstrated unrelated baseline failures
- re-review result, including an independent pass when used
- final worktree state
- remaining risks, blockers, or user-accepted skipped findings
