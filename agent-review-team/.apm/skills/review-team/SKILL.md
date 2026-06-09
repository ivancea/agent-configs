---
name: review-team
description: Review by coordinating specialized agents, consolidating findings, and returning a validated final report.
---

# Review Team

Use this skill to run a multi-agent review workflow with specialized reviewer roles.

## Workflow

1. Determine the review target scope (current diff by default, or explicit prompt target).
2. Start all sub-agents in parallel using that same scope.
3. Wait for all sub-agent outputs before any consolidation.
4. Consolidate findings: merge only true duplicates and validate each issue.
5. Return the final report with confirmed issues and ignored issues.

## Review scope

- By default, review the changed code in the current diff.
- If the prompt explicitly defines a different target, use that target instead.
- Pass the exact same target scope to every sub-agent.

## Sub-agents (run in parallel)

- `investigator`: only investigate how the targeted changes are usually tackled externally, including internet research.
- `standardizer`: only check whether the targeted changes match existing repository patterns, conventions, and similar implementations.
- `architect`: only assess architecture-level concerns in the targeted changes (maintainability, extensibility, structural risks).
- `reviewer`: only perform a baseline general review on the targeted changes.
- `adversarial`: only perform a strict adversarial pass on the targeted changes, including edge cases and nitpicks.

For each sub-agent invocation, require output entries with:

- `file`
- `line`
- short explanation
- required context

## Consolidation rules

- Keep each sub-agent finding unless it is a true duplicate.
- Merge issues only when location and root problem are equivalent.
- If two findings are similar but not identical, keep both.
- For each ignored finding, explain why it was rejected.
- When duplicates are merged, keep the merged context inside the confirmed issue entry.

## Final output

Return two sections:

1. `Confirmed Issues`
2. `Ignored Issues`

Each issue entry must include: `file`, `line`, short explanation, and the minimum context needed to understand or reproduce the concern.
