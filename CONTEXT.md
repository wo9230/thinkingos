# ThinkingOS

ThinkingOS 是将模糊情境与建议转化为可审计判断、已承诺行动和结果学习的限界上下文。本词汇表定义产品、研究、评估与实现工作共用的统一语言。

**版本作用域**：除非条目另有说明，Gate、状态迁移与完整 Contract 描述的是 `PRD-v0.2.md` 的 North Star 语义。v0.1 的执行语义由 `MVP-v0.1.md` 与 Decision Log `D-024`、`D-025`、`D-026` 决定；默认 GPT Work 只是正式 Case 之前的自由协作态，不是第三档、路由或状态，专门方法只作为按需检索的证据层。

## 核心

**ThinkingOS**:
一个以 GPT Work 提供自由协作入口、并在需要时将对话正式化为可审计 `ThinkingCase` 的思考工具。持久学习价值仍来自判断、行动与结果的可追溯历史。
_Avoid_: 第二大脑、框架库、全知顾问

**GPT Work**:
v0.1 中正式 Case 之前的默认自由协作态，可直接问答、探索、推演、反驳或自然结束，也可先给暂停、延迟、补证据等可逆安全动作。它不自动创建 `ThinkingCase`，不进入 Quick / Full 档位、路由、状态或验证计数；重大事项确认不可逆承诺前需经用户同意转入正式化。
_Avoid_: 第三档、Case 类型、状态、免审高风险通道

**ThinkingCase**:
一个重大情境从初始模糊，到判断、行动、结果与学习的完整历史。
_Avoid_: 对话、报告、任务、项目

**Cognitive Runtime**:
一个可重复的决策语境：`ThinkingCase` 在其中被澄清、挑战、付诸行动并复盘，同时保持推理历史完整。
_Avoid_: 对话会话、答案生成器

**Decision Intelligence**:
通过证据、显式预测、真实行动和已观察结果，持续做出并更新判断的能力。
_Avoid_: 答案质量、智力分数

**Clarity Triage**:
一项正式化入口评估：在澄清利害、归属与目标冲突的同时，判定当前情境应进入完整 Case、先补证据、先做小型可逆行动、无需框架直接解决，还是当前无法继续。v0.1 的 GPT Work 可隐性使用同样判断，但不要求在普通问答前显式记录。
_Avoid_: 录入表、即时诊断

**Specialist Method**:
从有归属的外部或私有知识源按需检索、用于补足某个具体问题形状的领域方法。它必须保留来源、必要输入、适用语境与禁用条件；在本案中只能产生候选观察、方案或判断，不能自动成为通用框架、产品规则或已验证事实。
_Avoid_: `CATALOG` 框架、`domain-pack`、老师答案、强制流程

## 角色与权限

**Case Owner**:
对 `ThinkingCase` 的目标、最终决策、行动承诺与后果负责的人。普通 GPT Work 不要求先把用户标记为该角色。
_Avoid_: 用户、病人、被建议者

**Advisor**:
提供诊断、经验或建议的人类来源；其判断可影响但绝不拥有 `Case Owner` 的决策。
_Avoid_: 决策者、权威记录

**Copilot**:
在 `ThinkingCase` 内结构化、挑战与追溯推理的辅助角色；目标与最终承诺仍归 `Case Owner`。
_Avoid_: Advisor、自主 Agent、决策者

**Owner Goal**:
`Case Owner` 为一个 `ThinkingCase` 选定的现实变化、可接受代价、约束与成功含义。
_Avoid_: Advisor 目标、通用最佳实践

**Success Contract**:
`Case Owner` 在正式化 Quick / Full 时，对所期望结果、至少一项可观察成功标准、可接受及不可接受的工作量或代价、非目标与失败条件的显式确认。GPT Work 中不要求先填这份 Contract。
_Avoid_: 空泛愿景、Advisor 默认成功定义

**Advisor Default Goal**:
`Advisor` 在 `Case Owner` 尚未采纳时隐含优化的目标，例如增长、收入、速度或规模。
_Avoid_: Owner Goal、已共识目标

**Advisor Incentive**:
可能在 `Owner Goal` 之外影响 `Advisor` 问题框定或建议的利益、压力、承诺或冲突。
_Avoid_: 偏见指控、恶意

## 证据与判断

**Evidence Ledger**:
用于支持或挑战 `ThinkingCase` 判断的可审计观察、证言、文档、估算、推断与未知集合。
_Avoid_: 笔记堆、来源清单

**Competing Diagnosis**:
两个或以上对当前情境的合理解释之一；它们在证据或行动将其区分之前保持竞争。
_Avoid_: 头脑风暴、已证实根因

**Product Form Hypothesis**:
一项关于何种产品或服务形态更能承载所需价值与交付约束的待检验主张。
_Avoid_: Competing Diagnosis、已决定产品形态

**Current Best Judgment**:
`ThinkingCase` 中记录的、在当前证据下最值得行动或继续检验的结论；它必须具备 `Falsifiable Judgment` 的性质。
_Avoid_: 最终答案、不可修订的结论

**Falsifiable Judgment**:
一项判断的质量要求：它陈述依据、置信度、最强反方及会实质改变它的观察；在 `ThinkingCase` 中由 `Current Best Judgment` 承载这项性质。
_Avoid_: 某个独立记录类型、确定性

**Competitor Analogy Hypothesis**:
一项关于“可从竞品或类比对象学到什么”的可检验主张，其前提是已纳入阶段、受众、资源和渠道差异。
_Avoid_: 竞品事实、复制指令

**Unresolved Issue**:
一个仍然开放、且可能影响判断、计划或结果解读的重大问题、冲突或证据缺口。
_Avoid_: 脚注、被遗忘的问题

## 关系语境

**Relationship Temperature**:
`Case Owner` 与另一方在相关互动中已存信任和熟悉程度，表达为暖、冷或未知。
_Avoid_: 线索质量、情感倾向

**Warm Relationship**:
具有与当前互动相关的事前信任或熟悉度，因而改变了行动所需证明和说服强度的关系。
_Avoid_: 必然购买者、朋友

**Cold Relationship**:
没有与当前互动相关的事前信任或熟悉度，因此价值主张及其证据必须在没有借来信心的情况下成立的关系。
_Avoid_: 敌对关系、低价值个体

## 计划与承诺

**Parallel Track Plan**:
一组可以并行推进、又各自保留目标、依赖、证据和决策 Gate 的独立工作流。
_Avoid_: 待办清单、强制串行顺序

**Track**:
`Parallel Track Plan` 内检验一项目标或能力、且不隐藏它与其他工作流依赖的连贯工作流。
_Avoid_: 步骤、杂项任务组

**Gate**:
在 v0.2 North Star 中，只有显式 Contract 和所需证据满足时才允许状态迁移或轨道处置的 fail-closed 决策边界。在 v0.1 中，同名 Gate 仅作为收尾检查清单，不实现状态机，也不阻塞迁移或 Case 完成。
_Avoid_: 确认按钮、默认通过、把 v0.1 检查项误写成迁移阻塞

**Lifecycle Gate**:
在 v0.2 North Star 中控制 `ThinkingCase` 主生命周期状态迁移的 `Gate`；它要求显式 Contract 与证据，但不以数值参数化为必要条件。v0.1 不执行 Lifecycle Gate 状态迁移。
_Avoid_: Track Gate、Threshold

**Track Gate**:
在 v0.2 North Star 中控制单个 `Track` 启动、继续、停止、修订或解锁的 `Gate`；当判定涉及度量时，它必须引用一个 `Threshold`。v0.1 可把相同问题用作检查，不要求 Gate runtime。
_Avoid_: Lifecycle Gate、无条件待办节点

**Threshold**:
一个有来源且可修订的比较条件，它包含显式度量、操作符、目标或范围、观察窗口与适用语境，用于参数化可度量的 `Track Gate` 或判断。
_Avoid_: 所有 Lifecycle Gate 的同义词、神奇数字、通用基准

**Threshold Candidate**:
一个尚未被 `Case Owner` 采纳为 Gate 的建议阈值，其价值是等待本案校准，而不是充当默认值。
_Avoid_: Default threshold, default candidate, hard gate

**Teach-back**:
`Case Owner` 在承诺计划前，用自己的话对问题、判断、权衡、门槛和改变判断条件所做的说明。它在 v0.2 North Star 中是 fail-closed Gate 的组成部分；v0.1 保留「赞同不等于理解」的意图，但不以正式 Teach-back 阻塞完成。
_Avoid_: 表示同意、复制 Advisor 摘要

**NOW Action**:
`Case Owner` 已明确承诺立即开始的行动，具有定义好的观察和继续、停止或修订条件。
_Avoid_: 建议、以后再做的任务

**Decision Snapshot**:
在承诺时刻保存的记录，包含 `Case Owner` 当时相信什么、选择什么、预测什么以及接受什么。
_Avoid_: 最新答案、可编辑结论

## 结果与学习

**Outcome**:
已承诺行动的已观察后果或结果，包括无结论或不利证据。
_Avoid_: 只有成功、产出物

**Learning Diagnosis**:
对推理动作、证据使用、假设与行动如何产生或未能产生某个 `Outcome` 的解释。
_Avoid_: 标准答案、Advisor 模仿

**Judgment Update**:
通过比较 `Decision Snapshot` 与 `Outcome` 所赚得，并由 `Case Owner` 确认的信念、决策规则或置信度变化。
_Avoid_: 事后改写、自动用户画像
