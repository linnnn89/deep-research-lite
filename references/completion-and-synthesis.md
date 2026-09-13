# Deep Completion and Structured Stop Reports

Ordinary Instant and Research tasks use the finish rule in [SKILL.md](../SKILL.md). Do not load this file solely because sources disagree or an ordinary task has an access failure.

## Complete, inconclusive, and partial

A research task may be complete with an inconclusive finding when the required investigation was performed, relevant conflicts were assessed, and the evidence supports no stronger answer. Disagreement does not have to disappear.

A task is partial when required verification is unperformed, or missing evidence prevents a required answer. Name the unmet deliverable and its effect on the conclusion. Do not relabel unfinished work as scientific uncertainty, silently change scope, or treat resource exhaustion as successful completion.

When some deliverables are answered and others are not, state their status separately. An unavailable source matters according to the claim it was needed to verify; disclose material access limitations even when adequate independent evidence answers the question.

## Structured report

Use this report for Deep review or when the host requires it, not as routine user-facing output:

```yaml
STOP_REPORT:
  deliverables:
    - question: ""
      status: answered|answered_inconclusive|unmet
      finding_and_evidence: ""
  unsupported_critical_claims: []
  snippet_only_critical_claims: []
  unassessed_material_conflicts: []
  required_verification_not_performed: []
  counterevidence_assessment: "evidence examined and result, or what remains unchecked"
  residual_uncertainty_and_access_limits: []
  scope_drift: []
  next_high_value_action: "specific action, or none with a brief evidence-based reason"
```

Residual uncertainty is not automatically a blocker. Unmet deliverables, unsupported or snippet-only critical claims, unassessed consequential conflicts, missed required verification, or scope drift prevent a claim of complete work. Counterevidence must be checked to the extent required by the task's risk.

This package provides instructions, not an executable completion checker. If a host implements validation, it may check the report fields; a valid schema alone does not establish evidence quality.

## Independent Deep review

Use an independent completion reviewer in Deep when delegation is authorized and available. Give it the contract, evidence map, conflicts, gaps, and stop report before polished final prose. It returns:

```yaml
decision: approve|reject
blockers: []
required_next_actions: []
```

The reviewer should identify specific unsupported claims or unmet work. It must not require arbitrary source counts, agreement across studies, or further searches without an unresolved decision need. Respond only to concrete blockers, then reassess completion.

If independent review is unavailable or unauthorized, perform a self-check and disclose that independent review was not performed. Do not claim an auditor approved the work or repeatedly launch replacement reviewers. An explicitly required independent audit remains unmet until performed.

## Synthesis

Answer required questions directly, linking claims to evidence and explaining material uncertainty and practical implications. Include only sections that add information; combine repeated conclusions and limitations. Add methods, date coverage, and source scope when needed to interpret the result or when requested.

For conflicting evidence, verify definitions, dates, versions, populations, methods, and applicability before comparing results. Prefer direct and relevant evidence, and report any remaining disagreement accurately. Do not fabricate source access, findings, numbers, citations, or quotations; respect quotation and copyright limits.
