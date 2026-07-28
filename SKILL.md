---
name: deep-research-lite
description: >
  Conduct rigorous, source-grounded, multi-step research for complex questions that
  require web search, document reading, cross-source verification, evolving research
  structure, or synthesis across multiple evidence types. Use one research agent by
  default and add parallel branches only when subquestions are genuinely independent.
---

# Deep Research Lite

## Purpose

Produce reliable, decision-useful research without reproducing a large model-training,
benchmark, or deployment stack.

Preserve the most reusable long-horizon research patterns:

- a locked research contract
- a dynamic question map
- goal-directed source reading
- an explicit claim–evidence ledger
- contradiction and evidence-gap tracking
- periodic context checkpoints
- selective parallel exploration
- adversarial verification
- an auditable stopping gate
- section-wise synthesis

Do not expose private chain-of-thought. Show concise rationale, evidence, uncertainty,
and verification results instead.

## Use this skill when

Use this skill when the request requires one or more of the following:

- current or externally verifiable information
- multiple independent sources
- a complex question with several subquestions
- comparison of competing explanations, products, policies, papers, or claims
- investigation of causes, mechanisms, implications, or timelines
- synthesis of webpages, papers, PDFs, repositories, datasets, or uploaded documents
- explicit deep research, due diligence, literature review, or evidence review
- resolution of contradictions, missing evidence, or uncertain claims

## Do not use this skill when

Do not activate the full workflow for:

- simple stable facts
- arithmetic or unit conversion
- translation or rewriting
- summarizing text already supplied by the user
- a single-source lookup with no meaningful verification need
- creative writing
- tasks where the user explicitly requests a fast, non-researched response

For borderline cases, choose Light mode rather than expanding scope.

## Operating modes

Choose the smallest mode that can answer the question reliably.

### Light

For focused current-information questions.

- 1–3 research branches
- usually 3–6 high-quality sources
- no parallel workers
- one verification pass
- no checkpoint unless context becomes crowded

### Standard

Default for complex research.

- 3–6 research branches
- usually 6–15 high-quality sources
- dynamic outline
- explicit evidence ledger
- contradiction and gap review
- a checkpoint when needed
- optional parallel work for independent branches

### Heavy

Use only when the user explicitly requests exhaustive research or when several
independent, high-stakes branches must be investigated.

- maximum 3 parallel branches at a time
- branch-specific evidence records
- checkpoint after each major phase
- dedicated adversarial verification
- final integration based on evidence quality, not agent voting

Do not use Heavy merely because a topic is interesting.

## Research state

Maintain a compact internal state.

```yaml
research_state:
  research_contract:
    original_question: ""
    user_goal: ""
    required_deliverables: []
    included_scope: []
    excluded_scope: []
    time_boundary: ""
    jurisdiction_or_population: ""
    locked: true

  outline:
    - id: Q1
      question: ""
      importance: critical|supporting
      status: open|partial|answered|unresolved
      finding_ids: []
      unresolved_reason: ""

  claims:
    - id: C1
      text: ""
      importance: critical|supporting
      evidence_ids: []
      verification_status: unverified|verified|inferred|disputed

  evidence:
    - id: E1
      claim: ""
      source: ""
      source_type: primary|secondary|commentary
      publication_date: ""
      accessed_date: ""
      supports: []
      contradicts: []
      reliability: high|medium|low
      notes: ""

  contradictions:
    - id: X1
      claim_ids: []
      impact: critical|moderate|low
      status: open|resolved|unresolved
      resolution: ""

  gaps:
    - id: G1
      description: ""
      impact: critical|moderate|low
      status: open|resolved|unresolved
      attempts: []
      effect_on_answer: ""

  adversarial_review:
    completed: false
    strongest_counterevidence_id: ""
    effect_on_conclusion: ""

  saturation:
    consecutive_low_yield_actions: 0
    query_diversity_verified: false

  stop_request: false
  stop_report: {}
  stop_status: continue|approved|rejected
```

This state is working memory, not a mandatory user-facing table.

## Workflow

### 1. Freeze the research contract

Before searching, resolve:

- the exact original question
- the decision or output the user needs
- required deliverables
- included and excluded scope
- time boundary
- jurisdiction, population, product version, or dataset
- desired depth and output format

Store these fields as a locked `research_contract`.

The outline may evolve, but the agent may not silently remove a deliverable, narrow the
scope, or redefine success merely because the task becomes difficult.

Ask a clarification only when a missing detail would materially change the research.
Otherwise state the interpretation briefly and proceed.

### 2. Build a provisional question map

Create a small hierarchical map of answerable subquestions.

Useful branches often cover:

- definitions and current status
- direct evidence
- mechanisms or causes
- competing explanations
- risks, limitations, or counterevidence
- practical implications

The map is provisional. Update it only when evidence shows that the structure is
incomplete, redundant, or misleading. Do not force a fixed number of revisions.

### 3. Plan high-yield searches

For each open branch, prepare a compact search set:

- one precision query
- one broader recall query
- one query targeting primary or official sources
- one contradiction or alternative-explanation query when relevant

Batch closely related searches when supported.

Prefer source classes in this order unless the task requires otherwise:

1. official documents, regulators, standards, filings, registries, or original datasets
2. peer-reviewed papers and first-party technical documentation
3. systematic reviews or professional organizations
4. reputable reporting with named sources
5. expert commentary
6. forums and social media only as clearly labeled anecdotal evidence

Domain priorities:

- medicine: current guidelines, regulators, systematic reviews, pivotal trials
- science: original papers, datasets, methods, replication evidence
- software: official docs, source repository, release notes, issue tracker
- law and policy: enacted text, official guidance, courts, agencies
- finance and companies: filings, exchanges, investor relations, official statistics
- products: manufacturer specifications plus independent testing

### 4. Read with an explicit evidence goal

Never open a source without a stated goal.

For each source, extract only:

- the claim or data relevant to the current branch
- date and version
- population, jurisdiction, or applicability
- methodology or basis of the claim
- limitations
- whether it supports, weakens, or contradicts existing evidence

Do not preserve large page summaries when a compact evidence record is sufficient.

A search-result snippet is discovery evidence, not final support, unless the underlying
source cannot reasonably be accessed and this limitation is disclosed.

### 5. Update the claim–evidence ledger

After meaningful source reads:

- attach evidence to one or more branches and claims
- classify the source as primary, secondary, or commentary
- identify duplicated or dependent sourcing
- separate direct evidence from inference
- record contradictions explicitly
- revise confidence only when evidence quality changes

Ten outlets repeating one upstream press release count as one evidence chain.

### 6. Run the research loop

Repeat:

1. inspect open branches, contradictions, and important gaps
2. choose the next highest-value query or source
3. collect evidence
4. update claims, gaps, contradictions, and the question map
5. judge whether another search is likely to change the answer

Prioritize searches that can:

- resolve a load-bearing contradiction
- verify a central numeric or temporal claim
- replace a weak source with a primary source
- fill a branch required by the research contract
- test a plausible alternative explanation

Avoid searches that merely add examples to an already stable conclusion.

### 7. Create context checkpoints when needed

Create a checkpoint when any condition is met:

- context is becoming crowded
- roughly 8–12 substantive tool interactions have accumulated
- a major research phase is complete
- parallel branches are about to be merged
- searches are becoming repetitive
- the agent is losing track of contradictions or gaps

Checkpoint format:

```markdown
## Research checkpoint

### Established
- Finding — evidence IDs — confidence

### Contradictions
- Conflict — why sources differ — next resolving action

### Remaining gaps
- Gap — impact — best next source or query

### Current outline
- Q1: answered
- Q2: partial
- Q3: open

### Next actions
1. ...
2. ...
3. ...
```

Replace redundant interaction history with the checkpoint while preserving evidence IDs,
contradictions, unresolved issues, and the locked contract. A separate summarization
model is optional, not required.

### 8. Use parallel branches selectively

Parallelize only when subquestions are independent enough to be researched without
repeatedly sharing intermediate state.

Good branches:

- separate jurisdictions
- separate products or companies
- independent mechanisms
- distinct time periods
- evidence review versus implementation review

Bad branches:

- tightly coupled causal reasoning
- several workers reading the same sources
- tasks where one branch determines the next branch's queries
- small questions answerable in a few tool calls

Limit default parallelism to 3 branches.

Each branch returns:

```yaml
branch_result:
  question: ""
  answer: ""
  key_evidence: []
  contradictions: []
  unresolved_gaps: []
  confidence: high|medium|low
```

Merge branches by source quality, directness, applicability, recency, and independence.
Never treat majority agreement among agents as proof.

### 9. Verify before requesting termination

Check:

- Are all load-bearing claims supported?
- Are dates, versions, names, doses, prices, and numeric results verified?
- Are primary sources used where reasonably available?
- Do citations support the exact sentence?
- Are sources compatible with the required time boundary?
- Are conflicting results explained by population, method, definition, jurisdiction,
  version, or time?
- Is inference labeled as inference?
- Is absence of evidence being mistaken for evidence of absence?
- Are limitations and applicability boundaries visible?

For high-stakes topics, seek at least two independent authoritative sources for central
conclusions when feasible.

### 10. Request termination and pass the stopping gate

The research agent may request termination but may not approve its own completion.

Do not accept statements such as “the information seems sufficient” as proof.

Use this control flow:

```text
Research agent requests stop
→ generate STOP_REPORT
→ run an adversarial stop audit
→ apply deterministic gate checks
→ approve, or return explicit blockers
```

#### 10.1 Hard rejection gates

Reject termination if any condition is true:

- a required top-level question remains `open`
- a critical branch remains `partial`
- an unresolved branch lacks a documented reason and impact assessment
- a critical claim has no supporting evidence
- a critical claim relies only on search-result snippets
- a critical date, version, name, dose, price, or number is unverified
- a critical gap remains `open`
- a critical contradiction remains unresolved without transparent presentation
- no deliberate counterevidence or alternative-explanation search was completed
- claimed saturation is based on duplicate or near-duplicate queries
- final scope no longer matches the locked research contract
- material source-access failures are hidden

For high-stakes work, a critical conclusion should normally have either:

1. one directly applicable primary source plus an independent verification source; or
2. two independent authoritative sources when a primary source is unavailable.

#### 10.2 Mandatory adversarial review

Before requesting termination, actively search for the strongest evidence that could
weaken or overturn the current conclusion.

Examples:

- medicine: null findings, adverse effects, guideline disagreement, population limits
- science: negative results, failed replication, methodological criticism
- software: known issues, regressions, incompatible versions
- policy and law: enacted text versus messaging, opposing interpretation
- products and companies: independent tests, failures, regulatory actions

Record the strongest counterevidence and state whether it changes the conclusion,
reduces confidence, or is not applicable.

#### 10.3 Search saturation must be demonstrated

Two low-yield actions count toward saturation only when:

- they use meaningfully different strategies
- primary-source searching has been attempted
- counterevidence searching has been attempted
- no critical gap remains open
- neither action merely rephrases the same query

Saturation means the remaining search space has low expected information value. It does
not mean the last two weak queries returned little information.

#### 10.4 STOP_REPORT

Every termination request must provide a structured completion proof:

```yaml
stop_report:
  requested: true

  contract:
    required_deliverables_total: 0
    required_deliverables_covered: 0
    scope_drift_detected: false

  coverage:
    top_level_total: 0
    answered: 0
    unresolved_with_reason: 0
    open: 0

  central_claims:
    total: 0
    verified: 0
    inferred: 0
    disputed: 0
    unsupported: 0
    snippet_only: 0

  source_quality:
    primary_source_search_completed: false
    independent_evidence_chains: 0

  contradiction_review:
    completed: false
    unresolved_critical_conflicts: 0

  adversarial_review:
    completed: false
    strongest_counterevidence_id: ""
    effect_on_conclusion: ""

  gaps:
    critical_open: 0
    moderate_open: 0
    low_open: 0

  saturation:
    consecutive_low_yield_actions: 0
    queries_were_nonredundant: false

  access_failures:
    disclosed: false
    affects_central_conclusion: false

  proposed_status: completed
```

#### 10.5 Independent stop auditor

When role separation is available, give the auditor:

- the original research contract
- the final question map
- the claim–evidence map
- contradictions
- gaps
- the STOP_REPORT

Do not show polished final prose first, because it can anchor the auditor toward
approval.

The auditor must look for blockers rather than grade whether the work feels generally
good. It returns only:

```yaml
decision: approve|reject
blockers: []
required_next_actions: []
```

When a separate agent is unavailable, run the same audit as a distinct adversarial pass
with a fresh checklist. It still may not waive hard gates.

#### 10.6 Deterministic gate

Use programmatic validation when the host supports it:

```python
def can_stop(state) -> tuple[bool, list[str]]:
    blockers = []

    if state.contract.scope_drift_detected:
        blockers.append("Research scope drifted from the locked contract")
    if state.outline.open_top_level_questions:
        blockers.append("Top-level questions remain open")
    if state.claims.unsupported_critical_claims:
        blockers.append("Critical claims lack evidence")
    if state.claims.snippet_only_critical_claims:
        blockers.append("Critical claims rely on search snippets")
    if state.gaps.open_critical_gaps:
        blockers.append("Critical evidence gaps remain open")
    if state.contradictions.unresolved_critical:
        blockers.append("Critical contradictions remain unresolved")
    if not state.adversarial_review.completed:
        blockers.append("Counterevidence review was not completed")
    if not state.saturation.query_diversity_verified:
        blockers.append("Search saturation was not demonstrated")

    return len(blockers) == 0, blockers
```

Only the gate or auditor may set `stop_status: approved`. The research agent may set
only `stop_request: true`.

A user-imposed budget or tool limit may force a partial stop. In that case:

- label the result `partial`
- list unmet deliverables
- disclose how the limitation affects confidence
- never represent resource exhaustion as successful completion

### 11. Synthesize section by section

Write from the final question map, not from chronological browsing history.

For each section:

1. state the answer or claim
2. present the strongest evidence
3. explain why the evidence supports the claim
4. address meaningful counterevidence or limitations
5. state the practical implication

Retrieve only the evidence relevant to the current section. This reduces context loss and
prevents irrelevant source dumping.

## Output contract

Unless the user requests another format, use:

```markdown
# Bottom line

Direct answer in 1–3 paragraphs.

## Analysis

Organized by the final research outline.

## Uncertainty and limitations

What is established, inferred, disputed, or still unknown.

## Conclusion

Decision-useful synthesis without introducing new evidence.

## Research note

- Checked through: YYYY-MM-DD, timezone
- Evidence range: source types and date range
- Unresolved issues: none, or concise list
```

Place citations close to supported claims. Do not provide a bibliography disconnected
from the prose.

## Quality rules

- Do not fabricate facts, citations, quotations, or source access.
- Do not imply a source was read when only a snippet was seen.
- Do not conceal conflicting evidence.
- Do not force certainty when evidence is uncertain.
- Do not use fixed minimum numbers of revisions, tables, sources, or tool calls.
- Do not require separate planner and writer models.
- Do not require local model serving, a particular search API, or a framework.
- Do not reproduce private chain-of-thought.
- Do not let the research agent approve its own termination.
- Do not treat resource exhaustion, context limits, or repeated weak queries as proof of
  completion.
- Do not silently alter the locked research contract.
- Prefer compact evidence records over copied passages.
- Respect copyright and quotation limits.
- Keep the answer proportional to the user's decision need.

## Failure handling

When a source cannot be accessed:

1. try an official mirror, alternate format, repository file, abstract, or archive
2. seek the same claim in an independent authoritative source
3. lower confidence if primary evidence remains unavailable
4. disclose the limitation if it affects a central conclusion

When evidence conflicts:

1. verify definitions and dates
2. compare populations, methods, jurisdictions, and versions
3. identify which source is more direct and applicable
4. present the disagreement if it cannot be resolved

When research tools fail repeatedly:

- preserve verified findings
- answer partially rather than pretending completion
- state exactly what could not be checked

## Optional extensions

Add these only when the environment supports them and the task benefits:

- PDF visual inspection for charts, tables, or scanned pages
- code execution for reproducible calculations
- repository inspection for software claims
- citation export
- reusable research-state persistence
- an adversarial reviewer branch
- user-approved exhaustive mode
