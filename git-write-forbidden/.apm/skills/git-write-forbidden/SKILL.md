---
name: git-write-forbidden
description: Guards Git, gh, GitHub, and other version-control writes. Use whenever a requested or implied version-control task may change the Git index, branches, remotes, configuration, pull requests, issues, assignments, or similar state. Pure read-only operations do not require this skill.
---

# Git Write Forbidden

Never perform a Git, `gh`, GitHub, or other version-control write operation unless the user explicitly and unambiguously requested that operation.

## Consent rule

- Consent must come from the user's request. Do not infer it from context, intent, workflow conventions, prior read-only instructions, or the fact that a write would be a useful next step.
- A request to inspect, check, review, compare, explain, assess readiness, or determine whether something is safe to write authorizes read-only operations only.
- If explicit consent is absent, do not execute the write. Answer the request using read-only information.
- If the request is ambiguous and cannot be completed read-only, ask the user to explicitly confirm the specific write operation.
- Consent for one write operation does not authorize additional writes.

## Write operations

Treat as writes anything that changes version-control or hosting state, regardless of the command or tool used. This includes:

- Changing the Git index or working tree through Git, including staging, unstaging, applying patches, restoring, or removing tracked content.
- Creating, amending, rebasing, merging, reverting, cherry-picking, or otherwise changing commits or history.
- Creating, deleting, renaming, switching, resetting, or updating branches or tags.
- Fetching into or otherwise updating local refs, pulling, pushing, or changing remotes.
- Changing Git configuration, hooks, submodules, worktrees, notes, or repository metadata.
- Creating, editing, closing, reopening, merging, labeling, reviewing, commenting on, or assigning pull requests.
- Creating, editing, closing, reopening, labeling, commenting on, or assigning GitHub issues.
- Creating or changing releases, repository settings, workflows, checks, discussions, projects, or any similar GitHub state.

This list is illustrative, not exhaustive. When in doubt whether an operation writes state, treat it as a write and require explicit consent.

## Read-only exception

This skill does not apply to operations that only read state, such as inspecting status, diffs, logs, branches, remotes, pull requests, issues, or checks.

## Examples

- `Check the git staged files, to know if they're fine to push` authorizes inspection and an answer only. It does not authorize a commit or push.
- `Commit the changes and push them` explicitly authorizes committing and pushing the relevant changes.
- `Review this PR` authorizes reading and reporting only. It does not authorize comments, reviews, labels, assignments, edits, merges, or closure.
