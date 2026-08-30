# Operating Modes and Cost Control

# Operating modes

## Instant — default for focused questions

Use when one narrow question can be answered with a small number of authoritative
lookups.

Typical limits:

- 0–2 research branches
- 1–5 tool calls
- usually 1–4 useful sources
- no formal evidence ledger
- no checkpoint
- no separate auditor
- one concise verification pass

Instant mode may exceed these soft limits only when one additional action is clearly
likely to resolve a material uncertainty.

## Research — default for genuinely complex work

Use for multi-source analysis, repository review, paper comparison, technical decisions,
policy interpretation, and most serious personal research tasks.

Default cost envelope:

- 2–5 top-level branches
- usually 4–10 high-value tool calls
- normally no more than 12 without an explicit reason
- single agent
- compact evidence ledger
- one checkpoint only if context becomes crowded
- one counterevidence pass
- self-audit with deterministic hard checks
- no separate stop auditor by default

Exceed the envelope only when:

- a critical claim remains unresolved
- a primary source is missing
- a contradiction could change the conclusion
- the user explicitly requests deeper coverage
- the topic is high stakes and additional verification is necessary

## Deep — opt-in or high-stakes escalation

Use only when the user explicitly requests exhaustive research, or when several
independent high-stakes branches cannot be handled responsibly in Research mode.

Deep mode may add:

- up to 3 parallel independent branches
- full evidence records
- checkpoints after major phases
- dedicated adversarial review
- an independent stop auditor
- broader source coverage

Do not enter Deep mode merely because the topic is interesting, because the repository
is large, or because more sources are available.

# Cost and token control

## Budget before breadth

At the start, set a soft budget appropriate to the mode:

```yaml
budget_state:
  mode: instant|research|deep
  tool_call_soft_limit: 5
  tool_calls_used: 0
  remaining_high_value_actions: []
  checkpoint_allowed: false
  parallelism_allowed: false
  external_auditor_allowed: false
```

The budget is not a license to stop with unsupported claims. It is a guard against
low-value expansion. When the budget is insufficient, either:

1. justify one or more additional high-value actions; or
2. return a clearly labeled partial answer with unresolved items.

## Information-value test

Before each nontrivial search, source read, branch, or reviewer call, ask:

1. What unresolved claim or decision will this action address?
2. What result could change the conclusion, confidence, or recommendation?
3. Is there a cheaper source or query that can answer the same question?
4. Is this action duplicating an evidence chain already covered?

Skip the action when its expected answer change is low and it only adds examples,
background, or repeated confirmation.

## Search efficiency

- Batch closely related queries when supported.
- Prefer primary or official sources early.
- Open sources with an explicit evidence goal.
- Do not read several articles that repeat the same upstream source.
- Do not run parallel workers over overlapping questions.
- Do not create a checkpoint unless it will replace more context than it costs.
- Do not invoke a separate writer merely to restate the same evidence.
- Do not invoke an external auditor outside Deep mode unless risk justifies the cost.

## Cost-aware continuation gate

Continue researching only when at least one is true:

- the next action may change a central conclusion
- it may materially change confidence
- it may resolve a critical contradiction
- it may replace weak evidence with primary evidence
- it may answer a required deliverable
- it is necessary to disclose a high-stakes limitation accurately

Otherwise synthesize the answer.
