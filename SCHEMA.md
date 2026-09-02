# Trading Brain Note Schema

Use this schema for durable knowledge added to the vault.

## Frontmatter

```yaml
---
type: strategy
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
confidence: validated
tags:
  - nq
---
```

## Allowed `type` values

- `strategy`
- `concept`
- `decision`
- `research`
- `backtest`
- `architecture`
- `data-source`
- `project-state`
- `glossary`
- `source`

## Suggested `status` values

- `draft`
- `active`
- `validated`
- `deprecated`
- `superseded`

## Suggested `confidence` values

- `hypothesis`
- `observed`
- `tested`
- `validated`

## Note body

Prefer small, focused notes instead of large catch-all documents.

A durable note should normally contain:

1. A clear title.
2. What the concept or decision means.
3. Confirmed rules or findings.
4. Relevant `[[wikilinks]]` to related concepts.
5. Implementation references when applicable.
6. Evidence/source references when applicable.
7. Open questions if uncertainty remains.

## What belongs in the brain

Save information that would prevent future re-investigation, preserve important context, or materially reduce the chance of a future mistake. Examples include:

- stable strategy definitions;
- validated backtest findings;
- architecture decisions and rationale;
- important rejected approaches and why they were rejected;
- durable external API/data-source knowledge;
- canonical terminology;
- known pitfalls;
- important implementation rationale.

## What does not belong

Do not create permanent notes for:

- routine pytest output;
- ordinary commits;
- temporary debugging notes;
- one-off shell commands;
- transient errors with no durable lesson;
- intermediate model reasoning.

## Authority and conflicts

The brain is supporting knowledge, not implementation truth.

For implemented behavior, prefer the current `jenozu/trade-alerts` `main` branch, source code, tests, and configuration. If the vault and implementation disagree, identify the conflict and investigate it. Do not silently overwrite either interpretation.

## Retrieval rule

Do not load the entire vault into context. Search first, open the smallest set of relevant notes, and follow `[[wikilinks]]` only when additional context is needed.
