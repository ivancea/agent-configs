---
name: review-team
description: Coordinate specialized review agents, consolidate findings, and return a validated final review report.
---

# Review Team

Use this skill to run a multi-agent review workflow with specialized reviewer roles.

## Objectives

- Run all configured sub-agents against the same change set.
- Collect every reported issue with `file`, `line`, short explanation, and context.
- Merge findings only when they are clearly the same issue.
- Validate findings before returning results to the user.
- Include a dedicated "Ignored Issues" section for rejected findings.

## Sub-agent order

1. `investigator`
2. `standardizer`
3. `architect`
4. `reviewer`
5. `adversarial`

## Consolidation rules

- Keep each sub-agent finding unless it is a true duplicate.
- Merge issues only when location and root problem are equivalent.
- If two findings are similar but not identical, keep both.
- For each ignored finding, explain why it was rejected.

## Final output

Return three sections:

1. `Confirmed Issues`
2. `Merged Duplicates`
3. `Ignored Issues`

Each issue entry must include: `file`, `line`, short explanation, and the minimum context needed to understand or reproduce the concern.
