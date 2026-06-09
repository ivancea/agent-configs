# agent-review-team

A draft multi-agent review module that runs specialized reviewer agents and consolidates their findings into one final report.

## Workflow

The `/review-team` skill runs a small team of reviewer agents, collects every issue they report (`file + line + short explanation + context`), merges only true duplicates, validates which findings are valid, and returns a final report. Findings rejected during consolidation are listed in a dedicated "ignored issues" section.

## Included agents

- `investigator`
- `standardizer`
- `architect`
- `reviewer`
- `adversarial`
