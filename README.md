# Deep Research Lite

[简体中文](README.zh-CN.md)

A cost-aware, platform-neutral research skill for personal Codex and tool-using agent
workflows.

Deep Research Lite keeps the most useful ideas from long-horizon research agents while
removing the assumption that every task deserves many searches, multiple agents, a
separate writer, and an external reviewer.

## What changed in v1.1

The project is now optimized for individual users with limited token, API, context, or
local-compute budgets:

- **Instant / Research / Deep** operating modes
- single-agent execution by default
- soft tool-call and research budgets
- an information-value test before additional retrieval
- compact evidence records for ordinary work
- full evidence records only when methodology is load-bearing
- no external stop auditor in normal Research mode
- independent auditing and parallel branches reserved for Deep mode
- cost-aware stopping when more research is unlikely to change the answer

The aim is not to make research shallow. It is to spend tokens where they can change the
conclusion, confidence, or next action.

## Operating modes

| Mode | Best for | Default behavior |
|---|---|---|
| **Instant** | Narrow current questions and focused lookups | 1–5 tool calls, no ledger, no auditor |
| **Research** | Repository reviews, paper comparisons, policy and technical analysis | Single agent, compact evidence, usually 4–10 high-value tool calls |
| **Deep** | User-approved exhaustive or high-stakes multi-branch work | Full evidence, selective parallelism, independent stop audit |

All limits are soft. They may be exceeded when a critical uncertainty, contradiction, or
missing primary source justifies the cost.

## Core workflow

```text
Freeze a small research contract
→ build the minimum useful question map
→ retrieve the highest-value evidence
→ maintain compact claim–evidence records
→ test counterevidence proportionally to risk
→ stop when the next action has low expected answer change
→ synthesize only what the user needs
```

## Cost-control principles

- Evidence quality matters more than source count.
- Ten outlets repeating one announcement are one evidence chain.
- Search-result snippets are discovery aids, not final evidence.
- Additional retrieval must be able to change the answer, confidence, or recommendation.
- Checkpoints should save more context than they cost.
- Parallel agents should not research overlapping questions.
- A separate auditor is a Deep-mode expense, not a default ritual.
- Token or tool exhaustion must be reported as partial completion, never success.

## Anti-premature-stopping design

Cost control does not allow unsupported conclusions.

Instant and Research modes use compact deterministic completion checks. Deep mode adds a
structured `STOP_REPORT`, an independent adversarial auditor, and blocker validation.

Universal blockers include:

- unanswered critical deliverables
- unsupported or snippet-only critical claims
- hidden contradictions or evidence gaps
- missing counterevidence review where appropriate
- scope drift from the original contract
- concealed source-access failure
- mistaking resource exhaustion for completion

## Files

```text
.
├── SKILL.md
├── README.md
├── README.zh-CN.md
└── LICENSE
```

## Installation

Copy `SKILL.md` into the skill directory used by your agent or include it through the
host's instruction-loading mechanism.

```bash
mkdir -p ~/.agent/skills/deep-research-lite
cp SKILL.md ~/.agent/skills/deep-research-lite/SKILL.md
```

The exact directory depends on the host platform.

## Recommended use for personal Codex users

- Use **Instant** for a focused version check, factual lookup, or one-repository question.
- Use **Research** for most serious repository analysis, technical comparisons, and
  source-backed recommendations.
- Use **Deep** only when the user explicitly wants exhaustive work or when independent
  high-stakes branches justify the extra cost.
- Keep one agent unless parallel work is clearly independent.
- Prefer official documentation, repository files, papers, filings, or primary records
  before reading many secondary summaries.
- Return a partial result rather than spending indefinitely on a source that remains
  inaccessible.

## Scope

This repository provides an orchestration skill, not a trained research model. It does
not reproduce the intrinsic capabilities or benchmark performance of specialized
Deep Research models.

## Acknowledgment

The design was informed by research patterns explored in the
[Alibaba-NLP/DeepResearch](https://github.com/Alibaba-NLP/DeepResearch) ecosystem,
including dynamic outlines, evidence-grounded synthesis, context compression, and
long-horizon information seeking.

This is an independent workflow distillation and is not affiliated with or endorsed by
Alibaba-NLP.

## License

Released under the [MIT License](LICENSE).
