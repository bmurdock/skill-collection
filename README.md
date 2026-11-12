# Skill collection

A curated selection of Brian Murdock's Codex skills, shared publicly for others
to inspect and use. Skills are selected individually; this repository contains
only the skills chosen for publication. See [PURPOSE.md](PURPOSE.md) for the
repository's goals and curation standard.

## Available skills

| Skill | Purpose |
| --- | --- |
| [review-remediation-loop](skills/review-remediation-loop/SKILL.md) | Validate existing review or audit findings, make focused fixes, verify the changes, and re-review the affected code or documentation. |

## Install review-remediation-loop

You need Git and a Codex installation that supports local skills. The commands
below use a POSIX shell, such as Bash or Zsh on macOS or Linux.

1. Clone this repository and open its directory:

   ```sh
   git clone https://github.com/bmurdock/skill-collection.git
   cd skill-collection
   ```

2. Copy the entire skill directory into your user skills directory:

   ```sh
   mkdir -p "$HOME/.agents/skills"
   mkdir "$HOME/.agents/skills/review-remediation-loop" &&
     cp -R skills/review-remediation-loop/. "$HOME/.agents/skills/review-remediation-loop/"
   ```

   The second command stops if that skill directory already exists. Review or
   back up your existing copy before replacing it. Keep `SKILL.md`, `agents/`,
   and `references/` together so the bundled guidance remains available.

3. Open the project you want to work on in Codex. If the skill does not appear,
   restart Codex.

For installation in just one project, copy the skill directory into that
project's `.agents/skills/` instead. The user and project locations follow the
[official OpenAI skills documentation](https://developers.openai.com/codex/skills/#where-to-save-skills).
Cloning this repository alone does not install its `skills/` directory.

## Use review-remediation-loop

Start with concrete findings from an existing review or audit and authorize the
edits you want. Include finding IDs, affected files, reproduction details, and
required checks when available. A checklist or review rubric alone is not a set
of findings; discovering issues requires its own authorization.

In Codex CLI or the IDE extension, mention `$review-remediation-loop` in your
prompt, or select it with `/skills`. For example, in your target project:

```text
Use $review-remediation-loop to fix findings R1 and R2 in docs/review.md.
You are authorized to edit the affected code and add focused regression tests.
Preserve unrelated work, run the relevant checks, and re-review the changes.
Report each finding's disposition and the validation results.
```

The skill guides Codex through validating each finding, reproducing valid issues
where practical, making narrow fixes, running appropriate checks, and reviewing
the final changes. Each finding receives a disposition: `fixed`, `invalid`,
`blocked`, or `skipped`, with supporting evidence.

Finding resolution and validation are reported separately. A clean result
requires all in-scope findings to be fixed or invalid, required checks to pass,
and the final re-review to find no new actionable issue in scope. Accepted
blocked or skipped findings remain explicit exceptions. Missing required
validation leaves the workflow incomplete.

The workflow requires explicit user authorization for commits, pushes,
publication, messages, or external-system changes. Custom subagent roles are
optional; Codex can perform a separate re-review itself when delegation is
unavailable or unnecessary.

Read the [full skill instructions](skills/review-remediation-loop/SKILL.md),
[evidence handoff guidance](skills/review-remediation-loop/references/incremental-review.md),
and [subagent guidance](skills/review-remediation-loop/references/subagents.md)
for the complete operating contract.
