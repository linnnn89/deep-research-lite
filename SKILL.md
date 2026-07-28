---
name: deep-research-lite
description: >
  Cost-aware, source-grounded research for personal agent and Codex users. Use the
  smallest sufficient mode, a single agent by default, compact evidence records,
  high-information-value searches, explicit uncertainty, and mode-specific stopping
  checks. Escalate to parallel branches or an independent auditor only for genuinely
  independent, high-stakes, or user-approved exhaustive work.
---

# Deep Research Lite

## Purpose

Produce reliable, decision-useful research without reproducing a large Deep Research
deployment stack or spending tokens as though every question were a publication-grade
review.

The default user is an individual running Codex or another tool-using agent with limited
time, context, API budget, or local compute.

Preserve the highest-value research patterns:

- a locked research contract
- a small, evolving question map
- goal-directed source reading
- compact claim–evidence records
- contradiction and gap tracking
- context compression only when useful
- adversarial verification proportional to risk
- cost-aware stopping
- section-wise synthesis

Do not expose private chain-of-thought. Show concise rationale, evidence, uncertainty,
verification results, and unresolved gaps.

## Core rule

Use the **smallest mode that can answer the user's actual decision need reliably**.

Do not expand a task merely because more related information exists. Additional research
must be justified by its expected ability to change the answer, confidence, or next
action.

## When to use this skill

Use it when the request needs one or more of:

- current or externally verifiable information
- multiple independent sources
- repository, paper, policy, product, or company investigation
- comparison of competing explanations or claims
- causal, mechanistic, timeline, or implications analysis
- synthesis across webpages, papers, PDFs, files, or datasets
- explicit deep research, due diligence, literature review, or evidence review
- resolution of contradictions, missing evidence, or material uncertainty

## When not to use the full workflow

Do not activate Research or Deep mode for:

- simple stable facts
- arithmetic or unit conversion
- translation or rewriting
- summarizing text already supplied by the user
- creative writing
- a single-source lookup with no meaningful verification need
- a fast answer where the user accepts limited verification

Use Instant mode or answer directly.

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

# Research state

Use the **compact state by default**.

```yaml
research_state:
  contract:
    question: ""
    user_goal: ""
    required_deliverables: []
    scope: []
    exclusions: []
    time_boundary: ""
    locked: true

  questions:
    - id: Q1
      text: ""
      importance: critical|supporting
      status: open|answered|unresolved
      finding: ""
      evidence_ids: []

  evidence:
    - id: E1
      source: ""
      finding: ""
      confidence: high|medium|low

  contradictions: []
  critical_gaps: []
  next_high_value_actions: []
  budget_state: {}
```

The state is working memory, not a mandatory user-facing table.

## Full evidence mode

Use expanded records only for Deep mode or when methodology and applicability are
load-bearing, especially in medicine, science, law, finance, or safety-critical work.

```yaml
evidence:
  - id: E1
    claim: ""
    source: ""
    source_type: primary|secondary|commentary
    publication_date: ""
    accessed_date: ""
    population_or_scope: ""
    method_or_basis: ""
    supports: []
    contradicts: []
    limitations: ""
    reliability: high|medium|low
```

Do not pay the token cost of full records when a compact record is sufficient.

# Workflow

## 1. Freeze a small research contract

Resolve:

- exact question
- user's decision or desired output
- required deliverables
- included and excluded scope
- time boundary
- relevant jurisdiction, population, version, or dataset
- operating mode

Store these as a locked contract. The question map may evolve, but the agent may not
silently shrink the deliverables or redefine success because the task becomes difficult.

Ask a clarification only when the missing detail would materially change the work.
Otherwise state the interpretation briefly and proceed.

## 2. Build the smallest useful question map

Create only the branches needed to answer the contract.

Common branch types:

- current status or definition
- direct evidence
- mechanism or cause
- competing explanation
- limitation or counterevidence
- practical implication

Do not create branches for generic background unless the user needs them.

Update the map only when evidence shows a material omission, redundancy, or structural
error. Do not force a fixed number of outline revisions.

## 3. Plan high-value retrieval

For each critical open branch, select the minimum useful combination of:

- a precision query
- a primary or official source query
- a broader recall query
- a contradiction or alternative-explanation query

Not every branch needs all four. Choose based on expected information value.

Source preference:

1. official documents, regulators, standards, filings, registries, original datasets
2. peer-reviewed papers and first-party technical documentation
3. systematic reviews and professional organizations
4. reputable reporting with named sources
5. expert commentary
6. forums or social media as explicitly labeled anecdotal evidence

Domain priorities:

- medicine: current guidelines, regulators, systematic reviews, pivotal trials
- science: original papers, datasets, methods, replication evidence
- software: official docs, source repository, release notes, issue tracker
- law and policy: enacted text, official guidance, courts, agencies
- finance and companies: filings, exchanges, investor relations, official statistics
- products: manufacturer specifications plus independent testing

## 4. Read for a stated evidence goal

Before opening a source, state internally which claim or gap it may address.

Extract only what is needed:

- relevant finding or data
- date and version
- applicability
- method or basis when important
- limitation
- whether it supports, weakens, or contradicts the current view

A search-result snippet is discovery evidence, not final support, unless the underlying
source cannot reasonably be accessed and the limitation is disclosed.

## 5. Maintain compact claim–evidence mapping

After useful reads:

- attach evidence to the relevant question or claim
- distinguish direct evidence from inference
- detect dependent or duplicated sourcing
- record contradictions that could change the answer
- record only material gaps

Ten outlets repeating one upstream announcement count as one evidence chain.

## 6. Run the information-gain loop

Repeat:

1. inspect critical open questions, contradictions, and gaps
2. rank possible next actions by expected answer change
3. perform the highest-value affordable action
4. update evidence and confidence
5. run the cost-aware continuation gate

Avoid searches that merely add examples to a stable conclusion.

## 7. Create a checkpoint only when it saves context

A checkpoint is justified when:

- context is crowded
- roughly 8–12 substantive tool interactions accumulated
- a major phase is complete
- branches must be merged
- the agent is repeating work or losing track of gaps

Compact format:

```markdown
## Research checkpoint

### Established
- Finding — evidence IDs — confidence

### Material conflicts
- Conflict — likely reason — resolving action

### Critical gaps
- Gap — impact — best next action

### Contract coverage
- Deliverable: answered|unresolved

### Next high-value actions
1. ...
2. ...
```

Replace redundant history with the checkpoint. Do not call a separate summarization
model merely to produce it.

## 8. Parallelize only independent work

Parallelism is disabled in Instant and Research mode by default.

In Deep mode, use at most 3 branches and only when questions are genuinely independent,
such as separate jurisdictions, products, mechanisms, or time periods.

Each branch returns only:

```yaml
branch_result:
  question: ""
  finding: ""
  key_evidence: []
  material_conflicts: []
  unresolved_gaps: []
  confidence: high|medium|low
```

Merge by source quality, directness, applicability, recency, and independence. Agent
agreement is not proof.

## 9. Verify proportionally to risk

For all modes, check:

- load-bearing claims have support
- dates, versions, names, doses, prices, and important numbers are verified
- citations support the exact claim
- inference is labeled
- uncertainty and applicability are visible
- source access is represented honestly

Research mode additionally requires one concise counterevidence or alternative-
explanation pass for central conclusions.

High-stakes or Deep mode should normally use a primary source plus independent
verification, or two independent authoritative sources when primary evidence is
unavailable.

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
