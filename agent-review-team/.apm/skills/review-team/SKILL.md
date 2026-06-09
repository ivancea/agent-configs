---
name: review-team
description: Review by coordinating specialized agents, consolidating findings, and returning a validated final report.
---

# Review Team

Use this skill to run a multi-agent review workflow with specialized reviewer roles.

## Workflow

1. Determine the review target scope from the explicit prompt target. An explicit scope is required; if none is provided, stop and report `missing scope`.
2. Start all sub-agents in parallel using that same scope.
3. Wait for all sub-agent outputs before any consolidation.
4. Consolidate findings: deduplicate true duplicates and merge their context.
5. Validate the consolidated findings. Rejected findings move to `Ignored Issues` with the reason for rejection.
6. Return the final report.

## Review scope

- An explicit scope is required for every run; do not fall back to any default.
- Pass the exact same target scope to every sub-agent.

## Sub-agents (run in parallel)

- `investigator`: only investigate how the targeted changes are usually tackled externally, including internet research.
- `standardizer`: only check whether the targeted changes match existing repository patterns, conventions, and similar implementations.
- `architect`: only assess architecture-level concerns in the targeted changes (maintainability, extensibility, structural risks).
- `reviewer`: only perform a baseline general review on the targeted changes.
- `adversarial`: only perform a strict adversarial pass on the targeted changes, including edge cases and nitpicks.

Each sub-agent must output its findings as markdown, with `file`, `line`, a short description that lets a reader understand and localize the issue, and the minimum context needed to reproduce it.

## Consolidation rules

- Deduplicate findings: merge entries only when location and root problem are equivalent.
- If two findings are similar but not identical, keep both.
- When duplicates are merged, keep the merged context inside the surviving entry.

## Validation rules

- Validate each consolidated finding for correctness and relevance to the scope.
- Rejected findings go to `Ignored Issues` with a short rejection reason.

## Final output

Return the report in markdown with these sections:

1. `Confirmed Issues`
2. `Ignored Issues`
3. `Failed Agents` — only include this section if at least one sub-agent explicitly reported a failure or reported that no expected files were found. List the failing agents by name with a short reason.

Each issue entry (in both `Confirmed Issues` and `Ignored Issues`) must include:

- `file`
- `line`
- A short description that is enough to understand and localize the issue.
- The minimum context needed to understand or reproduce it.
- `Reporting Agents`: a plain list of the sub-agent names that reported the issue (e.g. `reviewer`, `architect`).

