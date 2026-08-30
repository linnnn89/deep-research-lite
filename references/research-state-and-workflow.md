# Research State and Workflow

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
