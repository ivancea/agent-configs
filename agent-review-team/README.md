# agent-review-team

A multi-agent review module that runs specialized reviewer agents and consolidates their findings into one final report.

## Workflow

The `/review-team` skill runs a small team of reviewer agents on an explicit scope (required, no default), collects every issue they report (`file + line + short description + context + reporting agents`), deduplicates true duplicates, validates the consolidated findings, and returns a final markdown report. Findings rejected during validation are listed in a dedicated `Ignored Issues` section. If any sub-agent reports a failure or no expected files were found, a `Failed Agents` section is appended at the end.

## Included agents

- `investigator`: checks relevant changes and researches common external approaches on the internet.
- `standardizer`: checks whether changes align with existing repository patterns and conventions.
- `architect`: checks high-level architecture quality, maintainability, and extensibility risks.
- `reviewer`: performs a baseline general review pass.
- `adversarial`: performs a strict edge-case and nitpick-focused pass.
