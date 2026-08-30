---
name: deep-research-lite
description: Conduct cost-aware, source-grounded research with the smallest sufficient mode. Use for current or contested multi-source questions, due diligence, literature review, comparison, or evidence synthesis where contradictions and uncertainty matter.
---

# Deep Research Lite

## Purpose

Produce decision-useful research without treating every question as an exhaustive review.

Core rule:

> Use the smallest mode that can answer the user's actual decision need reliably.

Additional research should be able to change the answer, confidence, or next action. Do not expand scope merely because adjacent information exists.

## Activation Boundary

Use this skill when the request needs current or externally verifiable information, multiple evidence chains, comparison of competing claims, repository or paper investigation, due diligence, literature review, or explicit treatment of uncertainty and contradictions.

For a stable fact, supplied-text summary, translation, arithmetic task, or focused single-source lookup, answer directly or use the lightest available path.

## Mode Selection

### Instant

Use for a narrow question answerable with a few authoritative lookups. Keep the question small, verify the load-bearing fact, and stop.

### Research

Use for most serious multi-source work: repository analysis, paper comparison, policy interpretation, technical decisions, and source-backed recommendations. Default to one agent, compact evidence records, one counterevidence pass, and no separate auditor.

### Deep

Use only for user-approved exhaustive work or several genuinely independent high-stakes branches. It may add full evidence records, up to three non-overlapping parallel branches, checkpoints, adversarial review, and an independent completion audit.

The numerical budgets in [operating-modes-and-cost.md](references/operating-modes-and-cost.md) are soft envelopes, not quotas or permission to stop with unsupported claims.

## Core Workflow

1. Lock the question, user goal, required deliverables, scope, exclusions, and time boundary.
2. Build the smallest question map capable of answering that contract.
3. Retrieve the highest-value evidence, preferring primary and authoritative sources.
4. Attach evidence to claims and distinguish direct support, inference, contradiction, and unresolved gaps.
5. Test the strongest alternative explanation or counterevidence in proportion to risk.
6. Continue only while the next action could materially change the answer, confidence, or required deliverable.
7. Synthesize from the final evidence map, not from browsing chronology.

## Evidence Rules

- Source quality, directness, applicability, recency, and independence matter more than source count.
- Repeated reporting of one upstream source is one evidence chain.
- Search snippets discover sources; they do not normally support final critical claims.
- Verify important dates, versions, names, quantities, and quotations against the underlying source.
- Label inference and unresolved disagreement.
- If a source failure affects the answer, disclose the limitation and lower confidence accordingly.

## Cost and Parallelism

Before another substantial search, source read, branch, or review, ask what unresolved claim it addresses and what result could change the conclusion.

Use parallel work only when branches are genuinely independent. Do not send several agents after the same direction, and do not add a planner, writer, or auditor merely to repeat one evidence chain.

When the available budget cannot finish the contract, return a clearly labeled partial result with unmet deliverables and their effect on confidence.

## Completion Gate

Before claiming completion, confirm that:

- required critical deliverables are answered
- central claims have appropriate support
- no critical claim relies only on a search snippet
- material contradictions and access failures are disclosed
- required counterevidence was checked
- scope did not silently drift
- the next available action has low expected answer change

Use stricter structured checks for Deep mode. Resource exhaustion is a partial stop, not successful completion.

## Synthesis

Lead with the direct answer. Include only the analysis needed for the user's decision, place citations near claims, and distinguish established, inferred, disputed, and unresolved points. Add a compact research note when date coverage, evidence scope, or remaining gaps matter.

## Reference Routing

- Read [foundations.md](references/foundations.md) when resolving activation boundaries or adapting this framework to another host.
- Read [operating-modes-and-cost.md](references/operating-modes-and-cost.md) when selecting Research or Deep mode, budgeting retrieval, or deciding whether to parallelize.
- Read [research-state-and-workflow.md](references/research-state-and-workflow.md) for multi-source question maps, evidence records, checkpoints, retrieval planning, or proportional verification.
- Read [completion-and-synthesis.md](references/completion-and-synthesis.md) before closing a complex Research or Deep task, or when evidence conflicts, sources fail, or work must stop partially.

Do not load every reference for Instant mode.
