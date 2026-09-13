# Deep Work and Cost Control

Ordinary mode budgets and retrieval rules are in [SKILL.md](../SKILL.md). This reference is for Deep scheduling and delegation, not a prerequisite for Research.

## Escalation

Use Deep for an explicitly exhaustive deliverable, or independent high-stakes branches that cannot be handled responsibly in Research. A large repository, a medical topic, or available extra sources alone does not require Deep. Additional scrutiny should follow the unresolved claim and its consequences.

Keep one agent unless independent work offers a concrete benefit and delegation is authorized and available. Use at most three non-overlapping branches. Do not add separate planners or writers to repeat the same evidence chain.

Before delegating, assign each branch a question, scope, relevant date/version, source boundary, and concise return format. Share only the context the branch needs. Agent agreement is not independent evidence.

## Budget and retrieval

Choose a soft action or time envelope appropriate to the deliverable. Keep a brief note of remaining critical work; a YAML budget object is unnecessary unless the host needs one. This skill cannot directly enforce token limits, change model settings, or control host compaction.

Count the substantive searches and source reads inside a batch. Track returned text size and sequential round trips as well as operation count. A single wrapper returning many full documents is not a cheap operation.

Prefer source identifiers, findings, and relevant passages to copied documents. Request more context when a passage omits a load-bearing definition, method, denominator, comparator, or limitation. Read complete tables or methods when necessary; a text cap must not hide evidence that could reverse the answer.

When a search yields no material evidence, change source or query strategy before repeating it. After an access failure, try the most promising alternative first. Further attempts need a specific reason, such as an official mirror or a corrected identifier; a critical gap does not justify repeating an unchanged failing path.

Continue beyond the initial envelope only for a concrete unanswered deliverable, weak critical evidence, consequential contradiction, or necessary independent verification. If the needed evidence remains unavailable or the user budget is reached, preserve findings and report the unmet work as partial.

## Branch results and review

Each branch returns only:

```text
Question and finding
Key claims with source identifiers and applicability
Material conflicts, limitations, and unresolved gaps
Verification performed and remaining critical work
```

Merge by source quality, directness, applicability, recency, and independence. Preserve material disagreement; do not vote across agents or duplicate upstream reports.

For Deep completion, use [completion-and-synthesis.md](completion-and-synthesis.md). If an independent reviewer is used, give it the evidence and contract before polished prose. Limit follow-up to identified blockers; do not restart the whole investigation after each review.
