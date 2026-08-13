# ThinkingOS V0.2 产品需求文档

**文档类型**：v0.2 North Star 产品定义
**版本**：V0.2
**状态**：已接受的长期产品契约；不是当前施工图

> ⚠️ **本文档不是 v0.1 的施工图。** v0.1 的建造契约是 [MVP-v0.1.md](MVP-v0.1.md)，二者冲突时以后者为准。
> 本文定义的 8 道 fail-closed Gate、状态机与 17 段 schema 是 v0.2 North Star；v0.1 将 Gate 作为 Full 收尾检查清单，不执行迁移阻塞，并以 GPT Work 作为默认自由协作入口。当前权威见 Decision Log `D-023`、`D-024`、`D-025`。

**产品类别**：案例式认知运行时（Case-based Cognitive Runtime）/ Decision Intelligence
**目标形态**：能把高利害、模糊或来源复杂的情境推进为可审计判断、行动与复盘的 `ThinkingCase` runtime

## 0. 文档控制

### 0.1 目的

本 PRD 定义 v0.2 North Star 的长期产品行为：目标主权、`Clarity Triage`、竞争性诊断、证据可追溯性、关系语境、并行计划、参数化 Gate、`Teach-back`、`Unresolved Issues` 与 `Advisor Incentives`。

本文档定义产品行为和概念 Contract，有意不规定 UI、存储类型、API 形状、Prompt 原文或替代 framework kernel。它不定义 v0.1 的完成条件、落盘规则或迁移阻塞。

### 0.2 来源控制

| 来源 ID | 来源 | 作用 | 完整性 / 定位 |
|---|---|---|---|
| SRC-001 | 初始产品战略基线 | Decision Intelligence、`ThinkingCase` 闭环、可反证判断、行动、复盘与范围纪律。 | 受版本控制管理 |
| SRC-003 | Phase 0 产品定义确认 | 案例式认知运行时、目标主权、建议可反证、过程学习、`Clarity Triage` 与明确非目标。 | 只保留领域中立的产品约束 |
| SRC-004 | `PRODUCT-CONSTITUTION.md` | 不可妥协产品约束及其例外协议。 | 受版本控制管理 |
| SRC-005 | `CONTEXT.md` | 规范领域语言及版本作用域。 | 受版本控制管理 |
| SRC-006 | v0.1 产品方向确认 | 仅用于界定 v0.1 与本文 North Star 的关系。 | 领域中立摘要见 Decision Log |

来源材料是证据，不是真理。任何导入内容在独立验证前仍属有归属的来源主张；来源歧义和转录不确定性必须保持可见。真实 Case 的人物、业务、数字、标题、时间戳与互动细节不得进入本 PRD。

### 0.3 需求语言与追溯

- **MUST / P0**：v0.2 North Star 的核心 Contract；不代表 v0.1 当前执行要求。
- **SHOULD / P1**：对 v0.2 可靠运行重要，但可在核心 Contract 验证后完成。
- **MUST NOT**：范围或安全边界。
- 功能需求使用 `FR-*`，非功能需求使用 `NFR-*`，验收标准使用 `AC-*`，Gate 使用 `G-*`，产品决策在 Decision Log 中使用 `D-*`。
- 一条验收标准可以验证多条需求，但每条 P0 需求至少要映射一条验收标准。

### 0.4 规范变更边界

`Advisor` 答复或专家复审结果只能先作为有归属的证据、假设、启发式（heuristic）或证据缺口进入 Case，不得直接修改产品规则、宪法、Gate Contract 或验收标准。任何规范性变更必须同时具备：`Case Owner` 确认、独立证据或已观察 `Outcome` 支持，以及一条保留原裁决和重访条件的 Decision Log 记录。

## 1. 产品定义

### 1.1 产品命题

ThinkingOS 是一个案例式认知运行时，它将模糊情境与建议转化为可审计判断、已承诺行动、已观察 `Outcome` 与已赚得学习。其可防御资产不是更大的答案或框架集，而是 `Case Owner` 知道什么、相信什么、选择什么、做了什么、学到什么的版本化历史。

### 1.2 v0.2 产品命题

ThinkingOS 能否通过以下方式，帮助 `Case Owner` 比普通对话或静态笔记更好地处理重大或来源复杂的情境？

1. 保留 `Owner Goal` 并显示目标冲突；
2. 分离证据、诊断、建议和激励；
3. 将建议转化为可反证判断与现实可行的 `Parallel Track Plan`；
4. 要求理解和承诺，而不是被动表示赞同；
5. 真实 `Outcome` 出现后，诊断推理过程。

### 1.3 角色与权限

| 角色 | 权限 | 责任 | 不得替代 |
|---|---|---|---|
| **Case Owner** | 拥有目标、最终判断、承诺与后果。 | 陈述或修订 `Owner Goal`；更正证据；`Teach-back`；承诺 `NOW Actions`；报告 `Outcomes`；确认学习。 | 不能将责任委托给 `Advisor` 或 `Copilot`。 |
| **Advisor** | 贡献有归属的经验、诊断、主张与建议。 | 在可用时说明推理与适用性；在已知时披露重大激励。 | 不能默默定义成功，也不能成为权威记录。 |
| **Copilot** | 结构化并挑战 `ThinkingCase`。 | 运行 Triage；维护追溯；暴露替代项、矛盾、证据缺口、激励与 Gates；支持复盘。 | 不能冒充 `Advisor`、虚构证据、选择 `Owner Goal` 或自主承诺行动。 |

同一个人可以占据多个角色，但每次贡献必须保留其发出时的角色归属。

### 1.4 产品价值与反价值

**价值链**：模糊输入 → `Clarity Triage` → 证据与竞争性诊断 → 可反证判断 → `Parallel Track Plan` → `Teach-back` 与承诺 → 行动 → `Outcome` → `Learning Diagnosis` → `Judgment Update`。

以下项目本身不构成价值：摘要逐字稿、生成精美报告、同意专家、复制竞品、列举框架，或在没有行动的情况下完成计划。

## 2. 目标情境与通用发现模式

### 2.1 目标 Case

目标 `ThinkingCase` 是一个由明确 `Case Owner` 承担后果的真实情境。它可以来自自我判断、他人建议、访谈、文档或多来源材料，但必须能进入行动与复盘。

> 工程纪律：真实素材是 Case fixture，不是产品源码。产品文件必须领域中立、可交给任何人使用。

### 2.2 需求来源的一般模式

下列是产品要处理的跨领域模式：

- **目标权限冲突**：`Case Owner` 所要的现实变化与 `Advisor Default Goal` 不同，但冲突没有显示或裁决。
- **语境外推**：一种关系、阶段、对象或渠道中的证据被直接外推到另一种语境。
- **解法先于诊断**：在成功函数与因果解释未澄清时先选解法或交付形态。解法是选项或 `Product Form Hypothesis`，不是 `Competing Diagnosis`。
- **类比缺少可迁移性检查**：类比对象与当前 Case 在阶段、对象、资源或渠道上存在未说明的差异。
- **门槛缺 Contract**：建议门槛缺少来源、分母、观察窗口、适用语境或决策后果。
- **赞同不等于理解**：表示认可没有证明 `Case Owner` 已形成自己的问题模型与改变判断条件。
- **建议者激励未并置**：可能影响问题框定的利益、压力或承诺没有与受影响建议一起显示。

### 2.3 待完成工作（Jobs to be done）

- **JTBD-01**：当来源材料同时含有建议、假设、类比与压力时，在我采纳计划前帮我看见它们各自是什么。
- **JTBD-02**：当我所要的结果与建议者默认目标不同时，在不丢失有效洞见的前提下让我的目标保持主导。
- **JTBD-03**：当建议依赖阶段、关系语境或基准时，将它转成适用于我现实的可检验条件。
- **JTBD-04**：当几条工作流可同时进行时，为每条定义独立学习目标与 Gate，而不是把它们藏进单一线性清单。
- **JTBD-05**：在我承诺前，让我解释自己如何理解问题和权衡；行动后，帮我从自己如何推理中学习，而不是检查是否照抄答案。

## 3. 范围

### 3.1 v0.2 North Star In Scope

- 一个明确 `Case Owner`、一个活跃 Case，以及一条或多条可追溯来源输入路径。
- 来源材料导入，包含来源谱系与贡献者归属。
- `Clarity Triage` 与显式 `Owner Goal` 确认。
- 具有规范 `claim_type`、独立来源/证据形态、矛盾、置信度和 `Unresolved Issues` 的 `Evidence Ledger`。
- 当证据允许多个解释时，至少两个 `Competing Diagnoses`。
- 分开表达 Advisor 主张、建议、默认目标和已知激励。
- `Relationship Temperature` 与竞品/阶段适用性检查。
- 一个可反证的当前最优判断（Current Best Judgment）。
- 一个具有参数化 Threshold 与显式 Gates 的 `Parallel Track Plan`。
- 行动前的 `Teach-back` 与 `Case Owner` 承诺。
- `Decision Snapshot`、`Outcome` 录入、`Learning Diagnosis` 和经 `Case Owner` 确认的 `Judgment Update`。
- 可通过现有对话或命令行表面实现的文本或结构化报告。

### 3.2 v0.2 North Star Out of Scope

- 新图形 UI、dashboard、设计系统或多设备应用。
- 复制、fork 或重建现有 framework kernel；产品只通过 Contract 编排可用推理能力。
- 多 Agent 辩论、自主 Advisor 模拟或人格委员会。
- 全领域覆盖、领域 marketplace 或通用专家系统。
- 自动网络研究、无人值守执行，或代替 `Case Owner` 做高风险行动。
- 企业协作、权限、计费、增长自动化或 Advisor marketplace 功能。
- 完整 Cognitive History Graph、自动人格/偏差画像或通用第二大脑。
- 将来源文本、Advisor 逸事或类比指标视为已验证事实。

### 3.3 范围 Gate

一项功能只在缺少它会阻止目标 Case 达到已承诺 `NOW Action`、可比较 `Outcome` 或可审计 `Learning Diagnosis` 时，才有资格进入 v0.2 核心范围。便利性和视觉精美不能通过此测试。

## 4. 端到端 Workflow

### 4.1 Workflow 总览

| 阶段 | 状态 | 必需结果 | Gate |
|---|---|---|---|
| 1. 创建与分流 | `DRAFT` | Case 归属、来源谱系、初步 `Owner Goal`、利害与路由。 | `G-01 Clarity Triage` |
| 2. 澄清现实 | `CLARIFYING` | 已确认 `Owner Goal` 与 `Success Contract`；`Evidence Ledger`；角色、关系和激励语境；`Unresolved Issues`。 | `G-02 Reality Sufficiency` |
| 3. 建模问题 | `MODELED` | 由 Owner 确认的问题陈述，包含 `Competing Diagnoses` 与区分性证据。 | `G-03 Problem Model` |
| 4. 形成判断 | `DECIDING` | 选项、权衡、可反证的 `Current Best Judgment` 和计划草案。 | `G-04 Teach-back / Decision Confirmation` |
| 5. 计划 | `PLANNED` | 已接受 `Parallel Track Plan`、参数化 Gates，以及至少一个候选 `NOW Action`。 | `G-05 NOW Commitment` |
| 6. 行动 | `ACTING` | `Decision Snapshot` 冻结；已承诺行动接收真实观察。 | `G-06 Review Readiness` |
| 7. 复盘 | `REVIEW_DUE` | 将预测与已观察 `Outcome` 比较，不改写过去。 | `G-07 Learning Integrity` |
| 8. 学习 | `REVIEWED` | `Learning Diagnosis` 与经 `Case Owner` 确认的 `Judgment Update`。 | `G-08 Closure` |
| 9. 保存 | `ARCHIVED` | 已闭环 Case 在保持开放问题和谱系完整的情况下存续。 | — |

### 4.2 Gate Contract

#### G-01 — Clarity Triage

**完成条件**：已命名 `Case Owner` 与决策范围；初步 `Owner Goal`、利害、可逆性、时间范围、来源类型和角色分配已显式化；`Owner Goal` 与 `Advisor Default Goal` 的任何冲突均可见；并记录 `gate_decision`、`route_status`、`route_handling` 与 `next_state`。合法 `gate_decision` 为 `full_case`、`evidence_first`、`small_reversible_action`、`no_framework_needed` 或 `cannot_proceed`。前四种为 ready disposition；当 blocker 使安全路由暂时无法确定时，使用 `cannot_proceed` 并将 Triage 保持为 blocked。

**共同约束**：只有 `full_case` 可令 `next_state = CLARIFYING` 并触发 `DRAFT → CLARIFYING`；其他四种路由的 `next_state` 均为 `DRAFT`，由路由子生命周期表达执行、阻塞、完成或取代。所有路由都必须记录理由和下一处理，且不得在 Triage 前发布重大建议。

#### G-01A — 非 full-case 路由生命周期

| `gate_decision` | 适用含义 | Case 状态 / `next_state` | 路由闭环与重进 |
|---|---|---|---|
| `evidence_first` | 某项证据缺口阻止当前判断，但补证据行动明确可行。 | 保持 `DRAFT`；`next_state = DRAFT`。 | 记录补证据行动、负责人与完成/停止条件。证据获得、被拒绝或证实无法获得后，关闭本次 route episode 并重跑 `G-01`。 |
| `small_reversible_action` | 一个低代价、可逆行动比继续分析更能增加信息。 | 保持 `DRAFT`；`next_state = DRAFT`。 | 记录有边界行动、观察窗口与停止条件。观察或未尝试处置录入后，关闭 route episode；若仍有重大决策，用新证据重跑 `G-01`，否则以路由完成结束，但不声称完成了全部 `ThinkingCase` 闭环。 |
| `no_framework_needed` | 问题低风险、信息充分，可用直接事实答复或一步低风险处理解决，无需进入认知框架或完整 Case。 | 保持 `DRAFT`；`next_state = DRAFT`。 | 记录直接处理与 Owner 确认，即可关闭 route episode；不产生 `Decision Snapshot` 或 Case 学习声称。若利害、不确定性或问题范围后续变化，重跑 `G-01`。 |
| `cannot_proceed` | 身份/权限、安全、关键信息或其他 blocker 使当前无法安全路由。它是合法 blocker disposition，不是成功闭环。 | 保持 `DRAFT`；`next_state = DRAFT`；Triage 为 blocked。 | 记录 blocker、解除条件与可行负责人。blocker 解除后重跑 `G-01`；若 Owner 放弃输入，仅可将 route episode 标为 abandoned，不计为完成 Case。 |

#### G-02 — Reality Sufficiency

**通过条件**：重大主张已按谱系和类型进入 `Evidence Ledger`；当暖/冷/未知 `Relationship Temperature` 会改变适用性时已明确；已知 `Advisor Incentives` 和矛盾已记录；关键 `Unresolved Issues` 已有负责人或补证据行动；`Case Owner` 已确认 `Owner Goal` 及其 `Success Contract`。该 Contract 至少包含 desired outcome、至少一项可观察 success criterion、可接受及不可接受的 workload/cost，以及 non-goals/failure conditions；空泛的成功表述不能通过。

**未通过处理**：指出证据缺口与下一个补证据行动。“当前无法判断”是合法输出。

#### G-03 — Problem Model

**通过条件**：症状与决策问题已区分；当歧义重大时至少存在两个描述“为什么当前现象发生”的因果性 `Competing Diagnoses`；每个都有支持、反证和区分性证据；`Case Owner` 确认该问题现在值得决策。在任何解法或交付形态判断之前，必须命名目标对象 × 待解决任务 × 可观察结果，或显式建模多个独立任务；若任务仍未分清，解法或形态判断必须保持 `provisional`，且下一行动必须是区分性研究。解法、产品形态或行动名称不能用来通过本 Gate。

**未通过处理**：返回澄清，或运行一个区分性补证据行动。

#### G-04 — Teach-back / Decision Confirmation

这是 `DECIDING` 迁移到 `PLANNED` 的唯一合法路径。**通过条件**：`Case Owner` 用自己的话说明 `Owner Goal`、问题、已选判断、被拒绝替代项、主要权衡、关键 Threshold、最强反方和改变判断条件。`Copilot` 检查语义覆盖，不做字句匹配；异议或修订是 Gate 的成功用法。

**未通过处理**：显示不匹配或缺失概念并邀请更正。不得提供供复读的标准答案，也不得从表示赞同推断理解。

#### G-05 — NOW Commitment

这是 `PLANNED` 迁移到 `ACTING` 的唯一合法路径。**通过条件**：至少一个 `NOW Action` 已被 `Case Owner` 明确接受，且具有负责人、开始条件、观察窗口、验证信号、关联 Track 与停止/继续/修订条件。

**未通过处理**：保持 `PLANNED`；区分建议与承诺。

#### G-06 — Review Readiness

**通过条件**：行动已尝试、有意拒绝、被阻塞，或已到观察窗口；原始预测和 `Decision Snapshot` 可用；至少一项观察可与之比较。

**未通过处理**：继续行动或记录显式阻塞。不得把缺少数据转成成功或失败。

#### G-07 — Learning Integrity

**通过条件**：`Learning Diagnosis` 已考虑证据质量、框定、替代项、Threshold 适用性、承诺、执行和偶然；过程质量与 `Outcome` 好坏分开评估；没有原始判断被覆盖。

**未通过处理**：保持 `REVIEW_DUE` 并点明什么阻止了可靠诊断。

#### G-08 — Closure

**通过条件**：`Case Owner` 已确认、修订或拒绝建议的 `Judgment Update`；重大 `Unresolved Issues` 已解决、结转或被有意接受；下一次决策日期或关闭理由已明确。

### 4.3 Case 状态机

```text
DRAFT --G-01 full_case--> CLARIFYING --G-02--> MODELED --G-03--> DECIDING
  ^                  |                   |                   |
  |                  v                   v                   v
  +-------------- correction <------ correction <------ correction

DRAFT --G-01 evidence_first-----------> DRAFT --route close--> G-01
DRAFT --G-01 small_reversible_action---> DRAFT --observe------> G-01 / route close
DRAFT --G-01 no_framework_needed-------> DRAFT --direct handling--> route close
DRAFT --G-01 cannot_proceed------------> DRAFT --unblock------> G-01

DECIDING --G-04 decision confirmation--> PLANNED --G-05 NOW commitment--> ACTING
    ^                              |                              |
    +----------- revise -----------+                              |
                                                                  v
ACTING --G-06--> REVIEW_DUE --G-07--> REVIEWED --G-08--> ARCHIVED
  ^                  |                   |
  +-- more evidence--+                   +-- new version --> CLARIFYING
```

更正必须创建或保留历史；不得删除先前已接受版本。`Clarity Triage` 是 `DRAFT` 内第一个 Gate，不是独立持久 Case 状态。

### 4.4 Parallel Track Plan

一个复杂 Case 应能表达彼此独立又可协调的 Tracks，例如：

- **问题验证 Track**：测试当前因果诊断能否解释关键观察，不把解法名称当作原因。
- **语境迁移 Track**：测试一项判断从原语境迁移到新对象、阶段、关系或渠道时是否仍成立。
- **解法验证 Track**：测试候选解法能否产生预期现实变化，并保留停止或修订条件。
- **补证据 Track**：针对关键 `Unresolved Issue` 获取区分性证据，而不把活动量替代问题解决。

在容量允许时，Tracks 可并行。只有证据显示时依赖才是显式的；不得仅因 `Advisor` 按某顺序叙述就推断全局顺序。

每个 Track 必须陈述：目标、假设、相关 `Relationship Temperature`、负责人、容量预算、依赖、计划的补证据行动、观察、Threshold、当前状态与下一个 Gate。

### 4.5 参数化 Threshold Contract

一个 Threshold 只有在陈述以下内容时才有效：

1. **measure**：计数或判断什么；
2. **operator and target/range**：什么比较会改变决策；
3. **denominator**：如适用，人群或机会分母；
4. **observation window**：何时评估度量；
5. **segment/context**：包括适用时的暖/冷、渠道或阶段；
6. **source and rationale**：Owner 选择、Advisor 主张、历史基线、基准或实验；
7. **confidence**：当前目标有多少支持；
8. **decision consequence**：继续、停止、修订、补证据或解锁另一行动；
9. **revision rule**：什么情况允许在不改写历史的前提下修改目标。

从外部来源导入、且未经本案校准的定量或定性门槛，只能标为 `threshold_candidate` 或 `expert_benchmark`，并映射为 `provenance_type: advisor_recommendation`、`status: provisional`。两者都不是默认值，也不能经由 `default_candidate` 语义暗示默认采纳；在 `Case Owner` 显式采纳且完整 Threshold Contract 成立之前，它必须保持 inactive，绝不得成为有效 `Track Gate`。`Lifecycle Gate` 依赖自身显式 Contract 与证据，不因本节而被强制数值化。

## 5. ThinkingCase 概念模型

本模型命名产品概念与关系；实现 schema 拥有字段类型、可选性、校验语法与迁移。名称应与规范词汇兼容，但本节不得被视为序列化 schema。

### 5.1 概念组

| 概念组 | 产品含义 | 代表性概念 |
|---|---|---|
| 身份与权限 | 谁拥有 Case，哪些角色有贡献。 | Case 身份、`Case Owner`、`Advisor`、`Copilot`、角色归属贡献 |
| 来源谱系 | 什么材料进入 Case，可信度如何。 | 来源引用、digest、捕获时间、说话者归属、逐字稿歧义 |
| 目标与利害 | `Case Owner` 想改变什么现实，可接受什么代价。 | `Owner Goal`、`Success Contract`、`Advisor Default Goal`、desired outcome、可观察 success criteria、可接受 workload/cost、non-goals/failure conditions、时间范围、可逆性、利害 |
| 证据与不确定性 | 什么支持或挑战 Case。 | Evidence Ledger 条目、规范 `claim_type`、来源/证据形态、来源链接、置信度、矛盾、证据缺口、`Unresolved Issue` |
| 问题模型 | 哪些对当前现象的因果解释在竞争，什么会区分它们。 | 症状、决策问题、`Competing Diagnosis`、支持、反证、区分性观察 |
| 语境 | 哪些情况下类比或建议可迁移或不可迁移。 | `Relationship Temperature`、阶段、受众、渠道、资源、`Competitor Analogy Hypothesis` |
| Advisor 审计 | Advisor 主张了什么，什么可能影响它。 | Advisor 主张、建议、经验主张、激励、冲突、适用条件 |
| 判断 | 当前相信什么，为什么；在哪些可行解法中如何选择。 | `Product Form Hypothesis`、选项、标准、权衡、`Current Best Judgment`、置信度、反方、改变判断条件 |
| 计划与承诺 | 并行工作如何进入现实。 | `Parallel Track Plan`、Track、`Lifecycle Gate`、`Track Gate`、Threshold、容量预算、`NOW Action`、`Teach-back`、承诺 |
| 复盘与学习 | 发生了什么，推理应如何更新。 | `Decision Snapshot`、预测、`Outcome`、`Learning Diagnosis`、`Judgment Update`、结转问题 |
| 审计历史 | 意义如何变化又不删除以前状态。 | 状态、迁移、版本、行为人、时间戳、理由、取代链接 |

### 5.2 核心关系与不变式

- 一个 `ThinkingCase` 同一时刻恰有一个负责的 `Case Owner`，可有零个或多个 `Advisors`。
- `Owner Goal` 与 `Advisor Default Goal` 相互分离，即使文字恰好相同。
- `Owner Goal` 只有在其 `Success Contract` 包含可观察成功标准、可接受代价、非目标和失败条件，且经 `Case Owner` 确认时，才能支持 `G-02`。
- 每个重大主张必须追溯到来源，或显式标为推断或未知。
- `Evidence Ledger` 条目可支持或挑战多个诊断和判断；不得通过复制条目制造确定性。
- `Competing Diagnosis` 必须解释当前现象为何发生，不能只因 `Advisor` 声称就被提升为已接受；也不得用解法或产品形态标签代替。
- `Relationship Temperature` 与对方和互动语境相关；同一人对一个价值主张可能是暖，对另一个却是冷。
- 竞品类比是可选语境，绝不是必需核心字段，也绝不是直接证明。
- 每个已承诺 `NOW Action` 属于一个 Track 和一份冻结 `Decision Snapshot`。
- 每个 Threshold 均有版本；变更必须有理由，且不改变承诺时激活的值。
- `Unresolved Issue` 必须具有处置：补证据行动、决策日期、接受不确定性、结转 Case 或解决证据。
- `Learning Diagnosis` 即使在 `Outcome` 为正向时也可以评估过程；幸运结果不能使弱推理变好。
- `Judgment Updates` 需要 `Case Owner` 确认，且不能覆盖其来源 `Decision Snapshot`。

## 6. 功能需求

### 6.1 Case 导入、角色与目标

| ID | 优先级 | 需求 | 验证 |
|---|---:|---|---|
| FR-001 | P0 | `Copilot` 必须能从一条或多条来源材料创建 `ThinkingCase`，同时保留审计所需的来源身份、digest、贡献者归属和原始措辞。 | `AC-001`, `AC-002` |
| FR-002 | P0 | `Copilot` 必须识别 `Case Owner`、`Advisor` 和 `Copilot` 贡献，并在角色归属模糊时请求更正。 | `AC-003` |
| FR-003 | P0 | `Copilot` 必须在重大建议前运行 `Clarity Triage`，并记录利害、可逆性、时间范围、初步 `Owner Goal`、五种合法 `gate_decision` 之一、`route_status`、`route_handling` 与 `next_state`。只有 `full_case` 可进入 `CLARIFYING`，其他路由均保持 `DRAFT`。 | `AC-004` |
| FR-004 | P0 | `Copilot` 必须将 `Owner Goal` 与 `Advisor Default Goal` 分开维护并显示冲突；在问题建模前，必须要求 `Case Owner` 确认 `Success Contract`，其至少包含 desired outcome、一项可观察 success criterion、可接受及不可接受的 workload/cost，以及 non-goals/failure conditions。 | `AC-005` |
| FR-005 | P1 | `Case Owner` 应能修订 `Owner Goal`，并保留可见理由与版本，不删除以前目标。 | `AC-006` |

### 6.2 证据、语境与诊断

| ID | 优先级 | 需求 | 验证 |
|---|---:|---|---|
| FR-006 | P0 | `Copilot` 必须将重大来源内容分解为有归属的 Evidence Ledger 条目，且 `claim_type` 必须精确为 `observed_fact`、`user_interpretation`、`self_label`、`expert_hypothesis`、`expert_heuristic`、`external_evidence`、`market_signal` 或 `recommendation` 之一。观察、证言、文档、估算等只能作为独立的来源/证据形态，不得混入 `claim_type`。 | `AC-007` |
| FR-007 | P0 | 诊断或判断使用的每个重大主张必须追溯到证据；不受支持的内容必须标为证据缺口，不得补造。 | `AC-008` |
| FR-008 | P0 | `Copilot` 必须保留矛盾、模糊转录和重大 `Unresolved Issues`，且每项都有显式处置。 | `AC-009` |
| FR-009 | P0 | 当关系温度会改变对信任、证明或行动结果的解读时，`Copilot` 必须按可操作 cohort 记录 warm、cold 或 unknown，且每个 cohort 都有可观察 `operational_definition`。不得将一个 cohort 的证据外推到另一个 cohort。 | `AC-010` |
| FR-010 | P0 | 当不止一个因果解释拟合当前现象时，`Copilot` 必须表达至少两个 `Competing Diagnoses`，并陈述支持、反证和区分性证据。解法、产品形态或行动名称不得当作诊断。解法判断前必须命名目标对象 × 待解决任务 × 可观察结果，或显式分开多个任务；任务未解时，解法只能保持 provisional，且必须安排区分性研究。 | `AC-011` |
| FR-011 | P0 | 竞品和 Advisor 自身类比必须表达为可选 `Competitor Analogy Hypotheses`，具有阶段、受众、渠道、资源和迁移性缺口。 | `AC-012` |
| FR-012 | P0 | 已知或有合理迹象的 `Advisor Incentives` 必须在受影响建议旁显示，不得断言意图；未知激励必须保持未知。 | `AC-013` |

### 6.3 判断与计划

| ID | 优先级 | 需求 | 验证 |
|---|---:|---|---|
| FR-013 | P0 | `Copilot` 必须在因果诊断之后产生真正不同的选项，在可行时包括保持现状或停止，并按源自 `Owner Goal` 的标准比较。任何 `Product Form Hypothesis` 或候选解法都属于本需求下的选项，不属于 `FR-010` 的诊断。 | `AC-014` |
| FR-014 | P0 | 每个 `Current Best Judgment` 都必须具备 `Falsifiable Judgment` 性质，包含证据、置信度、最强反方、重大风险和改变判断条件。 | `AC-015` |
| FR-015 | P0 | `Copilot` 必须支持 `Parallel Track Plan`，且不得在没有记录理由时强制 Tracks 之间的依赖。 | `AC-016` |
| FR-016 | P0 | 每个 Track 必须拥有自己的目标、假设、语境、容量、补证据行动、依赖、Threshold、状态和下一个 Gate。 | `AC-017` |
| FR-017 | P0 | 每个 Threshold 必须符合参数化 Threshold Contract，并保留来源与采纳状态；参数化要求适用于可度量的 `Track Gate`，不得强迫所有 `Lifecycle Gate` 数值化。 | `AC-018` |
| FR-018 | P0 | Advisor 提供的数字目标在 `Case Owner` 采纳或修订前必须保持为 `threshold_candidate` 或 `expert_benchmark`，且映射为 `provenance_type: advisor_recommendation`、`status: provisional`并保持 inactive；只有 Owner 显式采纳且完整 Threshold Contract 成立后才能激活。不得使用 `default_candidate` 命名，也不得将其变成硬编码产品默认值。 | `AC-019` |
| FR-019 | P0 | `Copilot` 必须让重大 `Unresolved Issues` 在计划中持续可见，并说明哪些行动在不确定性下仍然安全。 | `AC-020` |

### 6.4 理解与承诺

| ID | 优先级 | 需求 | 验证 |
|---|---:|---|---|
| FR-020 | P0 | `DECIDING` 到 `PLANNED` 的迁移必须要求 `Case Owner` 完成覆盖 `G-04` Contract 的 `Teach-back`。 | `AC-021` |
| FR-021 | P0 | `Teach-back` 评估必须检查概念覆盖和矛盾，必须接受修订或拒绝，且不得用复制答案或表示赞同作为理解证据。 | `AC-022` |
| FR-022 | P0 | `PLANNED` 到 `ACTING` 的迁移必须要求至少一个显式承诺且满足 `G-05` 的 `NOW Action`。 | `AC-023` |
| FR-023 | P0 | 承诺时，系统必须冻结一份 `Decision Snapshot`，包含判断、置信度、预测、活跃 Threshold 版本、已接受权衡和 `NOW Actions`。 | `AC-024` |

### 6.5 复盘与学习

| ID | 优先级 | 需求 | 验证 |
|---|---:|---|---|
| FR-024 | P0 | `Case Owner` 必须能将 `Outcome` 记录为成功、不利、混合、无结论、被阻塞或有意未尝试，且不改写 `Decision Snapshot`。 | `AC-025` |
| FR-025 | P0 | `Learning Diagnosis` 必须在框定、证据、替代项、Threshold、承诺、执行、外部变化和偶然方面比较预测与 `Outcome`。 | `AC-026` |
| FR-026 | P0 | `Learning Diagnosis` 必须将推理过程质量与 `Outcome` 好坏分开评分或描述，且不得以匹配 Advisor 答案判断成功。 | `AC-027` |
| FR-027 | P0 | `Judgment Update` 必须链接证据，并在成为跨 Case 学习前由 `Case Owner` 确认、修订或拒绝。 | `AC-028` |
| FR-028 | P1 | 系统应将未解或新发现问题带入新 Case 版本或关联后续 Case，且谱系完整。 | `AC-029` |

### 6.6 报告与审计

| ID | 优先级 | 需求 | 验证 |
|---|---:|---|---|
| FR-029 | P0 | Thinking Report 必须呈现 `Owner Goal`、角色/激励语境、证据、`Competing Diagnoses`、`Current Best Judgment`、`Parallel Track Plan`、`Teach-back` 结果、`Decision Snapshot`、`Unresolved Issues` 和复盘 Contract。 | `AC-030` |
| FR-030 | P0 | 每个已接受状态迁移与重大更正必须保留行为人、时间、理由和上一版本。 | `AC-031` |
| FR-031 | P0 | 系统必须支持 `evidence_first`、`small_reversible_action`、`no_framework_needed` 和 `cannot_proceed` 四种非 full-case 路由，并按 `G-01A` 在 `DRAFT` 内记录它们的处理、闭环或重进。前三种是合法非答案/Direct-handling disposition，不得当作失败；`cannot_proceed` 是合法 blocker disposition，不得当作成功闭环。 | `AC-032` |

## 7. 非功能需求

| ID | 优先级 | 需求 | 验证 |
|---|---:|---|---|
| NFR-001 | P0 | **可追溯性**：每个重大判断与计划 Gate 必须能追溯到来源证据或显式 `Case Owner` 选择。 | `AC-033` |
| NFR-002 | P0 | **历史完整性**：已接受目标、`Decision Snapshots`、Threshold 版本和 `Outcomes` 的意义必须只追加；更正和取代必须可审计。 | `AC-034` |
| NFR-003 | P0 | **认识论标记**：生成文本必须以 `Case Owner` 能理解的语言区分证据、推断、建议、未知和矛盾。 | `AC-035` |
| NFR-004 | P0 | **目标安全**：未经 `Case Owner` 显式确认修订，任何 Advisor 或模型目标都不得取代已确认 `Owner Goal`。 | `AC-036` |
| NFR-005 | P0 | **Gate 失败关闭**：缺失必需 Gate 证据必须阻止迁移并保留工作；系统不得静默自动通过。 | `AC-037` |
| NFR-006 | P0 | **角色透明**：人类与 `Copilot` 贡献必须可区分；`Copilot` 不得虚构 Advisor 意图、披露或原话。 | `AC-038` |
| NFR-007 | P0 | **最小暴露**：只能保留 Case 所需来源材料；报告必须避免不必要的个人或第三方数据。 | `AC-039` |
| NFR-008 | P1 | **可恢复性**：被中断运行应能从最后已接受状态恢复，不丢失来源谱系、开放问题或未承诺修订。 | `AC-040` |
| NFR-009 | P0 | **实现中立**：概念 Contract 必须在不需要新 UI、多 Agent runtime、图数据库或替代 framework kernel 的情况下可用。 | `AC-041` |
| NFR-010 | P1 | **评估可重复性**：给定固定 Case fixture 和来源 digest，评估者应能复现哪些证据和 Gate 规则支持每次迁移，同时允许措辞变化。 | `AC-042` |

## 8. 验收标准

### 8.1 端到端产品验收

| ID | 验收标准 |
|---|---|
| AC-P01 | 一个领域中立的基准 Case 从 `DRAFT` 推进到至少 `ACTING`，同时保留来源 digest、贡献者归属和重大来源歧义。 |
| AC-P02 | 基准 Case 的 `Success Contract` 由 `Case Owner` 确认，且至少包含 desired outcome、一项可观察 success criterion、可接受及不可接受的 workload/cost 与 non-goals/failure conditions；它表达 Owner 的目标与约束，而不是默认采用 Advisor 目标。 |
| AC-P03 | 基准 Case 包含至少两个合理因果诊断、证据链接 `Current Best Judgment`、由 `Case Owner` 以自己的话通过的 `Teach-back`，以及至少一个已承诺 `NOW Action`。解法判断前，已命名目标对象 × 待解决任务 × 可观察结果，或显式建模多个独立任务；若仍未解，解法保持 provisional 并以区分性研究为下一行动。 |
| AC-P04 | 不同关系或运行语境的证据未被混淆；可独立学习的 Tracks 能够并行，且依赖与容量显式。 |
| AC-P05 | 至少一个后续 `Outcome` 可与冻结 `Decision Snapshot` 比较，并产生一份将过程质量与运气、答案匹配区分的 `Learning Diagnosis`。 |
| AC-P06 | 审核者可将每个重大建议、Threshold 和 Gate 决定追溯到证据、Advisor 主张或显式 `Case Owner` 选择。 |
| AC-P07 | 完成 `AC-P01` 至 `AC-P06` 不依赖任何 Out of Scope 能力。 |

### 8.2 需求级验收

| ID | 验收标准 |
|---|---|
| AC-001 | 从一条或多条测试来源创建 Case，具有稳定来源引用和 digest。 |
| AC-002 | 至少一个引用或转述主张可导航回贡献者与来源位置；来源措辞不被规范化覆盖。 |
| AC-003 | `Case Owner`、`Advisor` 和 `Copilot` 的陈述可区分，包括设备/说话者不确定性。 |
| AC-004 | `G-01` 之前不出现重大判断；已记录五种合法 Triage 路由之一、理由、`route_status`、`route_handling` 与 `next_state`；只有 `full_case` 可进入 `CLARIFYING`。 |
| AC-005 | `Owner Goal` 与 `Advisor Default Goal` 之间的冲突可见，并需要 Owner 裁决；缺少 desired outcome、可观察 success criterion、可接受或不可接受 workload/cost、non-goals 或 failure conditions 任一项时，`G-02` 失败。 |
| AC-006 | 修订 `Owner Goal` 会创建新已接受版本，并保留以前文字与理由。 |
| AC-007 | 来源中的重大陈述按其认识论地位分类为有归属证言、观察、推断或其他规范类型，不被错误提升为已验证事实。 |
| AC-008 | 诊断与 `Current Best Judgment` 暴露其支持的 `Evidence Ledger` 条目；缺失链接被标记。 |
| AC-009 | 矛盾标签与模糊来源术语保持可见，直到处置。 |
| AC-010 | 会改变证明强度的不同 cohort 各有可观察 `operational_definition` 与独立 `Relationship Temperature`；一个 cohort 的证据不得直接外推到另一个 cohort。 |
| AC-011 | 至少两个合理因果解释可作为具有区分性证据的 `Competing Diagnoses` 共存；任何解法、产品形态或行动标签都不能使 `G-03` 通过。缺少目标对象 × 待解决任务 × 可观察结果且未显式分开多个任务时，解法必须保持 provisional，并产生区分性研究行动。 |
| AC-012 | 竞品和 Advisor 自身指标陈述阶段/资源迁移缺口，且不是直接证明。 |
| AC-013 | 已知或有迹象的 `Advisor Incentive` 与受影响建议并置，不被忽略或用于断言恶意。 |
| AC-014 | 选项包含至少一条实质不同路径和保持/停止选项；标准追溯至 `Owner Goal`。 |
| AC-015 | `Current Best Judgment` 包含置信度、证据、最强反方、风险和改变判断条件。 |
| AC-016 | 两个相互独立的学习 Tracks 可并行，除非有记录的依赖理由阻塞其中之一。 |
| AC-017 | 每个 active Track 在产品层暴露 4.4 节所有属性。 |
| AC-018 | 缺少分母、观察窗口、来源或决策后果的 Threshold 校验失败。 |
| AC-019 | 任一未经本案校准的外部建议门槛只标为 `threshold_candidate` 或 `expert_benchmark`，不使用 `default_candidate`；其 `provenance_type` 为 `advisor_recommendation`、`status` 为 `provisional`，且在 Owner 采纳与完整 Threshold Contract 同时成立前保持 inactive。 |
| AC-020 | 每个重大 `Unresolved Issue` 都有补证据行动、日期、接受不确定性处置或结转链接。 |
| AC-021 | 没有满足 `G-04` 的已记录 `Teach-back`，`DECIDING` 不能迁移到 `PLANNED`。 |
| AC-022 | 重复 `Copilot` 措辞或只说“明白”失败；实质正确的释义或有理异议可通过。 |
| AC-023 | 没有一个显式接受且满足 `G-05` 的 `NOW Action`，`PLANNED` 不能迁移到 `ACTING`。 |
| AC-024 | 录入 `Outcome` 后，active `Decision Snapshot` 仍可不变地取回。 |
| AC-025 | 六种 `Outcome` 处置均可记录，不虚构二元结果。 |
| AC-026 | 复盘显式考虑框定、证据、替代项、Threshold、承诺、执行、外部变化和偶然。 |
| AC-027 | 幸运的正向 `Outcome` 仍可产生弱过程诊断；健全过程遇到不利 `Outcome` 仍可保持健全。 |
| AC-028 | 没有 `Case Owner` 行为，建议 `Judgment Update` 不能成为已确认学习。 |
| AC-029 | 结转问题链接回来源 Case，并保留之前状态。 |
| AC-030 | 报告包含 `FR-029` 要求的每个区块，或说明某行动后区块为何尚不可用。 |
| AC-031 | 迁移历史识别行为人、时间、理由、先前状态和结果状态。 |
| AC-032 | `evidence_first`、`small_reversible_action`、`no_framework_needed` 和 `cannot_proceed` fixtures 都保持 `DRAFT`，且按 `G-01A` 产生合法的路由处理、闭环/阻塞状态与重进条件；`cannot_proceed` 不被计为成功。 |
| AC-033 | 追溯审计未发现孤立重大判断或 Gate。 |
| AC-034 | 编辑已接受 snapshot 意义的尝试会创建更正/取代历史，而不是静默替换。 |
| AC-035 | 非作者评估人可在报告中区分证据、推断、建议、未知和矛盾。 |
| AC-036 | 未经 `Case Owner` 显式确认，Advisor 或 `Copilot` 建议不能修订 `Owner Goal`。 |
| AC-037 | Gate 输入缺失会返回未满足条件并保留状态。 |
| AC-038 | 生成分析标记为 `Copilot` 贡献，不虚构未披露 Advisor 意图。 |
| AC-039 | 输出排除来源 fixture 中的无关个人或第三方数据。 |
| AC-040 | 中断后，Case 带着最后已接受状态、来源 digest 和开放问题完整恢复。 |
| AC-041 | 基准 Case 可通过文本或现有命令表面，用一个推理 runtime 和普通结构化持久化完成。 |
| AC-042 | 重新运行固定 fixture 会产生等价证据链接和 Gate 结果，即使措辞不同。 |

## 9. 评估计划

### 9.1 评估集

1. **基准 Case**：使用领域中立的固定 fixture 端到端运行完整生命周期。
2. **对抗 fixtures**：表示赞同但未理解；Advisor 目标覆盖 `Owner Goal`；证据跨语境外推；无来源 Threshold；幸运成功；健全推理遇到不利 `Outcome`；隐藏 `Advisor Incentive`；证据不足。
3. **迁移 fixtures**：使用跨领域重大 Case 检测过拟合，不用于声称全领域就绪。

### 9.2 基线对比

将同一来源分别交给：

- 普通来源摘要；
- 一次性通用 AI 建议；
- ThinkingOS v0.2 North Star runtime。

盲审人评估目标忠实度、证据追溯、替代项质量、可反证性、计划可执行性、Gate 完整性和学习质量。更长输出或更多框架不是正向指标。

### 9.3 v0.2 接受 Gate

v0.2 North Star 只有在所有 `AC-P*` 标准和所有 P0 需求级标准都在基准 Case 或其适用对抗 fixture 中通过时才接受。P1 失败需记录负责人与重访条件，不得静默消失。

## 10. 交付顺序

| Slice | 产品切片 | 退出条件 |
|---|---|---|
| Slice 1 | 来源导入、角色、`Clarity Triage`、`Owner Goal` | 基准 Case 带着来源 digest 和显式目标冲突通过 `G-01`。 |
| Slice 2 | `Evidence Ledger`、关系/激励语境、`Competing Diagnoses` | 基准 Case 通过 `G-02` 和 `G-03`；孤立主张审计通过。 |
| Slice 3 | 判断、`Parallel Track Plan`、参数化 Threshold | 存在可反证判断与计划，不存在硬编码逐字稿基准。 |
| Slice 4 | `Teach-back`、`NOW` 承诺、`Decision Snapshot` | 基准 Case 只通过 `G-04` 和 `G-05` 到达 `ACTING`。 |
| Slice 5 | `Outcome`、`Learning Diagnosis`、`Judgment Update` | 一个 fixture 到达 `REVIEWED`；历史完整性和幸运结果测试通过。 |
| Slice 6 | 基准 Case 审核与基线对比 | `AC-P01` 至 `AC-P07` 通过；P1 缺口与产品决策已记录。 |

## 11. 开放产品问题

以下问题在 Phase 0 中被有意保持未解，实现不得猜测：

- **OQ-001**：不同利害与可逆性层级下，什么最少证据足以通过 `G-02`？
- **OQ-002**：如何评估 `Teach-back` 语义覆盖，同时不把 Gate 变成不透明评分或答案模仿？
- **OQ-003**：什么容量表达既能防止过多并行 Tracks，又能避免虚假全局顺序？
- **OQ-004**：哪些 `Advisor Incentives` 必须显式请求，哪些只在发现时记录？
- **OQ-005**：可审计 Case 已形成后，原始来源材料的合理数据保留期是多久？
- **OQ-006**：什么基线 rubric 与审核人协议能在不自评的前提下，建立相对普通对话的可信优势？

## 12. 最终产品约束

ThinkingOS v0.2 North Star 只有在帮助 `Case Owner` 保留自己的目标、挑战建议、承诺一个已理解行动，并从现实中诚实学习时才成功。如果它只是让来源材料看起来更有组织，它就失败了。
