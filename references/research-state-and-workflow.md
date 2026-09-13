# Detailed Evidence and Resumable State

Use this reference when a detailed evidence ledger or handoff is required. Ordinary Research uses the brief claim–source notes in [SKILL.md](../SKILL.md).

## Detailed records

Store shared scope, deliverables, date coverage, population, and jurisdiction once. Link individual claims to their sources; do not copy the shared contract into every record. Use identifiers only when they simplify cross-references.

Keep fields that affect interpretation. For example:

```yaml
evidence:
  - id: E1
    claim: ""
    finding: ""
    source: "URL, DOI, document section, or file and lines"
    source_type: primary|secondary|commentary
    publication_date_or_version: ""
    population_or_scope: ""
    method_and_comparator: ""
    estimate_and_uncertainty: ""
    limitations: []
    related_conflicts: []
```

Omit inapplicable fields. Retain exact units, denominators, effect estimates, intervals, endpoint definitions, and follow-up when they are load-bearing. Absence of reported data is not a zero result. A confidence label does not replace an account of study design, applicability, or uncertainty.

For medical or scientific evidence, preserve the distinction between primary studies, syntheses, and guidance. Check population, intervention/exposure, comparator, outcomes, design, and bias when relevant. Do not combine incompatible estimates or treat repeated publications of one study as independent verification.

## Updating the evidence map

For each required question, retain its current finding, linked evidence, and only the conflicts or gaps that could affect the answer. Update changed entries rather than reproducing the whole map after each read.

An evidence conflict may remain after adequate investigation. Record its likely basis and implications without forcing agreement. A missing required result remains a gap; do not substitute a related outcome, population, or date to make the map appear complete.

## Handoffs and context pressure

Create a compact handoff only when actual context pressure, resumption, or transfer makes it useful. Tool-call counts and phase boundaries do not trigger one by themselves. Do not call a separate summarization agent just to rewrite the current notes.

Use the smallest sufficient format:

```text
Contract: question, required outputs, scope and time boundary
Verified: findings with source IDs and essential applicability
Conflicts: assessed disagreements and their effect on the answer
Unmet: required verification or evidence still missing
Next: specific actions likely to change an answer or fill a required gap
```

In an append-only conversation, a checkpoint adds tokens; it does not evict prior messages. If the host supports compaction, use its actual mechanism when appropriate. Otherwise the handoff is a recovery aid, not a claimed reduction in context size.

Recover from the handoff and cited sources. Reopen a source only for missing detail, changed versions, or a new claim; do not replay the complete browsing history.
