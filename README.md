# Deep Research Lite

[简体中文](README.zh-CN.md)

A cost-aware, source-grounded research skill for personal Codex and tool-using agents.

## Operating modes

| Mode | Best for | Default behavior |
|---|---|---|
| **Instant** | Narrow questions and focused lookups | Usually 1–5 useful operations; no ledger, checkpoint, or auditor |
| **Research** | Multi-source comparisons and investigations | One agent; brief claim–source notes; usually 4–10 useful operations; proportional counterevidence assessment |
| **Deep** | Exhaustive deliverables or consequential independent branches beyond Research's scope | Detailed records as needed; authorized independent branches and completion review when available |

Budgets are soft envelopes, not quotas. Count actual searches and source reads inside batches. Continue for a specific critical gap or required verification; report partial work when a required answer cannot be supported.

## Ordinary work stays in the entrypoint

`SKILL.md` contains the rules needed for ordinary Instant and Research tasks. Selecting Research, maintaining brief evidence notes, or finishing an ordinary task does not require opening reference files.

References are conditional:

- `operating-modes-and-cost.md`: Deep scheduling and authorized delegation.
- `research-state-and-workflow.md`: Detailed evidence ledgers or resumable handoffs.
- `completion-and-synthesis.md`: Deep audits or host-required structured stop reports.
- `foundations.md`: Unclear activation boundaries or adaptation to another host.

## Cost controls

- Prefer authoritative sources and reuse evidence already read. Repeated reports of one upstream source are one evidence chain.
- Batch independent queries and reads within one agent. Keep dependent work sequential.
- Request short search results and targeted passages; expand when methods, tables, or context are necessary. Search snippets alone cannot support critical final claims.
- Update changed findings instead of repeatedly generating full contracts, budgets, and ledgers. Preserve load-bearing numbers, methods, populations, effects, and uncertainty.
- Let existing evidence satisfy counterevidence checks when sufficient; search again for a specific remaining need.
- Change strategy after unproductive retrieval. Retry a failed path only when there is new reason to expect success.
- Generate checkpoints only for actual context pressure or recovery. Appending a summary does not remove previous messages; compaction depends on the host.
- Keep output proportional to the requested deliverable. Methods notes and separate sections should add information.

These controls reduce avoidable work; they do not guarantee a particular latency or token saving. Actual results depend on the model, tools, task, and host.

## Completion without false certainty

Required work must be covered, critical claims supported, and material conflicts assessed and disclosed. Adequately investigated evidence may remain inconclusive. Unperformed required verification or missing evidence that prevents a required answer is **partial**, not complete. Do not hide gaps or silently shrink scope.

Ordinary tasks use a brief self-check. Deep work uses a structured report and an independent reviewer when authorized and available. If an independent audit was explicitly required, it remains unmet until performed. The package contains instructions, not an executable completion validator or research model.

## Files and installation

```text
.
├── SKILL.md
├── references/
│   ├── foundations.md
│   ├── operating-modes-and-cost.md
│   ├── research-state-and-workflow.md
│   └── completion-and-synthesis.md
├── README.md
├── README.zh-CN.md
└── LICENSE
```

Install the entrypoint and complete `references/` directory together. The exact skill directory depends on the host.

```bash
mkdir -p ~/.agents/skills/deep-research-lite
cp SKILL.md ~/.agents/skills/deep-research-lite/SKILL.md
cp -R references ~/.agents/skills/deep-research-lite/
```

## Acknowledgment and license

The design was informed by research patterns explored in [Alibaba-NLP/DeepResearch](https://github.com/Alibaba-NLP/DeepResearch), including evidence-grounded synthesis and long-horizon retrieval. This independent workflow distillation is not affiliated with or endorsed by Alibaba-NLP, and does not reproduce a specialized research model's capabilities or benchmark performance.

Released under the [MIT License](LICENSE).
