# Completion, Synthesis, and Failure Handling

# Stopping without self-deception

The agent may request completion only after passing the checks required by the selected
mode.

## Instant completion check

Confirm internally:

```yaml
instant_check:
  question_answered: true
  central_claim_supported: true
  key_date_or_version_verified: true
  material_uncertainty_disclosed: true
```

No STOP_REPORT or external auditor is required.

## Research completion check

Use a compact self-audit:

```yaml
research_stop_check:
  required_deliverables_unanswered: 0
  unsupported_critical_claims: 0
  snippet_only_critical_claims: 0
  unresolved_critical_conflicts: 0
  open_critical_gaps: 0
  counterevidence_checked: true
  scope_drift_detected: false
  material_access_failures_disclosed: true
  next_action_expected_answer_change: low
```

A deterministic host check may reject completion when any blocking field is nonzero or
false. A separate LLM auditor is not required by default.

## Deep completion gate

Deep mode uses the full gate:

```text
researcher requests stop
→ structured STOP_REPORT
→ independent adversarial auditor
→ deterministic blocker check
→ approve or return required next actions
```

The auditor receives the contract, question map, evidence records, contradictions, gaps,
and STOP_REPORT. It should not see polished final prose first.

It returns only:

```yaml
decision: approve|reject
blockers: []
required_next_actions: []
```

## Universal hard blockers

Do not claim successful completion when:

- a required critical question remains open
- a critical claim lacks evidence
- a critical claim relies only on a search snippet
- a critical contradiction or gap is hidden
- no appropriate counterevidence check was performed
- the scope drifted from the locked contract
- material source failures were concealed
- tool, token, context, or time exhaustion is being mistaken for completion

A user budget may force a partial stop. Label it `partial`, list unmet deliverables, and
explain how the limitation affects confidence.

# Synthesis

Write from the final question map, not chronological browsing history.

For each section:

1. answer the branch directly
2. present the strongest evidence
3. explain the implication
4. address material counterevidence or limitation
5. state what the user should conclude or do

Retrieve only evidence relevant to that section.

## Default output

```markdown
# Bottom line

Direct answer.

## Analysis

Only the sections needed for the user's decision.

## Uncertainty and limitations

Established, inferred, disputed, and unresolved items.

## Research note

- Checked through: date and timezone
- Evidence scope: concise source range
- Unresolved issues: none or short list
```

Place citations close to supported claims.

# Quality rules

- Do not fabricate facts, citations, quotations, or source access.
- Do not imply a source was read when only a snippet was seen.
- Do not conceal conflicting evidence.
- Do not replace uncertainty with false certainty.
- Do not expand scope without expected decision value.
- Do not use fixed source counts as a substitute for evidence quality.
- Do not require separate planner and writer models.
- Do not require local model serving or a particular framework.
- Do not expose private chain-of-thought.
- Do not invoke an external auditor by default.
- Do not treat resource exhaustion as successful completion.
- Prefer compact records over copied passages.
- Keep the answer proportional to the user's need and budget.
- Respect copyright and quotation limits.

# Failure handling

When a source cannot be accessed:

1. try an official mirror, alternate format, repository file, abstract, or archive
2. seek the same claim in an independent authoritative source
3. lower confidence if primary evidence remains unavailable
4. disclose the limitation when material

When evidence conflicts:

1. verify definitions, dates, versions, and populations
2. compare methods, jurisdictions, and applicability
3. prefer more direct and relevant evidence
4. present unresolved disagreement honestly

When tools fail or budget is exhausted:

- preserve verified findings
- answer partially rather than pretending completion
- state exactly what remains unchecked
- do not launch replacement branches unless their expected value justifies the cost
