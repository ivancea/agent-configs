# agent-review-team

A multi-agent review module that runs specialized reviewer agents and consolidates their findings into one final report.

## Workflow

The `/review-team` skill runs a small team of reviewer agents, collects every issue they report (`file + line + short explanation + context`), merges only true duplicates, validates which findings are valid, and returns a final report. Findings rejected during consolidation are listed in a dedicated "ignored issues" section.

## Included agents

- `investigator`: checks relevant changes and researches common external approaches on the internet.
- `standardizer`: checks whether changes align with existing repository patterns and conventions.
- `architect`: checks high-level architecture quality, maintainability, and extensibility risks.
- `reviewer`: performs a baseline general review pass.
- `adversarial`: performs a strict edge-case and nitpick-focused pass.
