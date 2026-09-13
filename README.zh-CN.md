# Deep Research Lite

[English](README.md)

面向个人 Codex 与工具型 Agent 的低成本、证据可追溯研究 Skill。

## 工作模式

| 模式 | 适用场景 | 默认行为 |
|---|---|---|
| **Instant** | 聚焦问题、单点核查 | 通常 1–5 次有效操作；不建账本，不生成 checkpoint，不启用 Auditor |
| **Research** | 多来源比较与调查 | 单 Agent、简短结论—来源记录；通常 4–10 次有效操作；按风险评估反证 |
| **Deep** | 穷尽式交付，或 Research 无法充分处理的重要独立分支 | 按需使用详细记录；在授权且工具可用时采用独立分支与完成审查 |

预算是软范围，不是需要凑满的次数。批量调用按内部实际检索和来源读取计数。关键缺口或必要核验可以支持继续；无法支持必需答案时应报告部分完成。

## 普通任务只需入口

`SKILL.md` 已包含普通 Instant 和 Research 的必要规则。选择 Research、维护简短证据记录或完成普通任务，不要求读取参考文件。

参考文件按具体需要加载：

- `operating-modes-and-cost.md`：安排 Deep 任务和已授权的独立分支。
- `research-state-and-workflow.md`：详细证据账本或可恢复的任务交接。
- `completion-and-synthesis.md`：Deep 审查或宿主要求的结构化停止报告。
- `foundations.md`：无法确定触发边界或需要适配其他宿主。

## 成本控制

- 优先权威来源，复用已读证据；多篇报道重复同一上游来源只算一条证据链。
- 在单 Agent 内批量执行独立查询和读取；有依赖的操作保持顺序。
- 搜索默认简短返回，来源先读相关段落；方法、表格或上下文影响解释时扩大读取范围。核心结论不能只靠搜索摘要。
- 只更新变化的发现，避免反复生成完整契约、预算和账本；保留影响结论的数字、方法、人群、效应量和不确定性。
- 已读证据充分时即可完成反证评估；追加检索应对应具体缺口。
- 检索无效时调整策略；只有出现新的成功依据才重试同一失败路径。
- 仅在实际上下文压力或恢复需要时生成 checkpoint。追加总结不会移除旧消息，真正压缩取决于宿主。
- 输出与交付需求相称；方法说明和独立章节应提供新增信息。

这些规则用于减少无效工作，不保证固定的提速或 token 节省比例。实际表现取决于模型、工具、任务和宿主。

## 完成状态与不确定性

必需工作应已覆盖，核心结论有证据，重要冲突已评估并披露。充分核查后仍可得出“证据尚不确定”的结论。必要核验尚未执行，或缺失证据导致必需问题无法回答时，应标记 **partial／部分完成**。不能隐藏缺口或擅自缩小范围。

普通任务使用简短自检。Deep 使用结构化报告，并在授权且工具可用时进行独立审查。用户明确要求的独立审查，未执行前仍属未完成。本技能提供指令，不包含可执行的完成校验器或研究模型。

## 文件与安装

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

安装时一起复制入口与完整 `references/` 目录。具体技能目录取决于宿主。

```bash
mkdir -p ~/.agents/skills/deep-research-lite
cp SKILL.md ~/.agents/skills/deep-research-lite/SKILL.md
cp -R references ~/.agents/skills/deep-research-lite/
```

## 致谢与许可

本项目参考了 [Alibaba-NLP/DeepResearch](https://github.com/Alibaba-NLP/DeepResearch) 生态中的证据驱动综合与长程检索思路，是独立的方法整理，与 Alibaba-NLP 不存在隶属、合作或官方背书关系，也不复现专用研究模型的能力或 benchmark 表现。

采用 [MIT License](LICENSE)。
