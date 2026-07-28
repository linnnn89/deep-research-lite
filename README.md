# Deep Research Lite

[简体中文](README.zh-CN.md)

A compact, platform-neutral agent skill for rigorous, source-grounded research.

Deep Research Lite distills several high-value patterns from long-horizon research agents into a practical `SKILL.md`:

- dynamic research outlines
- goal-directed source reading
- explicit claim–evidence mapping
- contradiction and gap tracking
- context checkpoints
- selective parallel research
- adversarial verification
- auditable stopping gates

The default design uses a **single research agent**. Parallel branches are added only when subquestions are genuinely independent.

## Why this project exists

Many deep-research systems combine a specialized model, custom search services, long-running ReAct loops, summarization models, benchmark infrastructure, and large deployment stacks. Those systems can be powerful, but their workflows are difficult to reuse as a lightweight agent skill.

Deep Research Lite separates the reusable research method from the original engineering stack. It is designed to work with any agent environment that can:

1. read a Markdown skill or system instruction;
2. search or retrieve external information;
3. inspect source content;
4. maintain a small structured research state.

No particular model, search API, agent framework, or local inference server is required.

## Core workflow

```text
Frame the research contract
→ build a provisional question map
→ search and read with explicit evidence goals
→ maintain a claim–evidence ledger
→ resolve contradictions and important gaps
→ run counterevidence review
→ request termination
→ pass an auditable stopping gate
→ synthesize section by section
```

## Anti-premature-stopping design

The research agent cannot approve its own completion.

Before stopping, it must generate a structured `STOP_REPORT`. A separate auditor or deterministic gate checks for:

- unanswered top-level questions
- unsupported critical claims
- unresolved critical gaps or contradictions
- missing primary-source searches
- missing counterevidence searches
- search saturation based on redundant queries
- scope drift from the original research contract
- hidden source-access failures

Resource exhaustion, context limits, or two weak searches are not treated as successful completion.

## Files

```text
.
├── SKILL.md
├── README.md
├── README.zh-CN.md
└── LICENSE
```

## Installation

Copy `SKILL.md` into the skill directory used by your agent platform, or include its contents in the agent's instruction-loading mechanism.

Example:

```bash
mkdir -p ~/.agent/skills/deep-research-lite
cp SKILL.md ~/.agent/skills/deep-research-lite/SKILL.md
```

The exact path depends on the host platform.

## Operating modes

- **Light**: focused current-information questions
- **Standard**: default for complex multi-source research
- **Heavy**: exhaustive or high-stakes work with selectively parallel branches

The skill is designed to choose the smallest mode that can answer the task reliably.

## Design principles

- Evidence quality matters more than source count.
- Search-result snippets are discovery aids, not final evidence.
- The outline may evolve; the locked research contract may not silently shrink.
- Conflicting evidence must be resolved or clearly presented.
- Parallel agents do not vote facts into existence.
- A result may be partial when evidence or tool access is genuinely insufficient.
- Uncertainty must be disclosed rather than replaced with false certainty.

## Scope

This repository provides an orchestration skill, not a trained research model. It does not reproduce the intrinsic capabilities or benchmark performance of any specialized deep-research model.

## Acknowledgment

The design was informed by research patterns explored in the [Alibaba-NLP/DeepResearch](https://github.com/Alibaba-NLP/DeepResearch) ecosystem, including dynamic outlines, evidence-grounded synthesis, context compression, and long-horizon information seeking. This repository is an independent workflow distillation and is not affiliated with or endorsed by Alibaba-NLP.

## Contributing

Issues and pull requests are welcome. Useful contributions include:

- platform-specific installation examples
- stronger deterministic validators
- evaluation cases for premature stopping
- domain-specific source hierarchies
- compact research-state implementations
- multilingual improvements

## License

Released under the [MIT License](LICENSE).
