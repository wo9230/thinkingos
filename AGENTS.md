# AGENTS.md

本文件是 **Codex** 在本仓库的入口约定。（Claude Code 读 `CLAUDE.md`，两边共用下面同一批事实源。）

## 项目

ThinkingOS —— 把模糊情境变成可验证下一步的思考工具。判断内核是**跨领域通用思想框架**（第一性原理、约束理论、二八、可证伪性…），不是任何个人的经验总结。

纯 Markdown，无代码、无依赖、无构建。产物是一个 skill + 一批模板 + 一个框架目录。

结构按 Karpathy 三层：**raw**（`cases/`、`_private/raw/`、`_private/courses/`，不可改）· **compiled**（`_private/facts/` 事实库，LLM 起草、本人确认）· **schema**（CATALOG、Skill、模板，领域中立）。`_private/` 与 `cases/` 各自是独立的私有 git 仓库。

## 开工必读（按序）

| 文件 | 是什么 | 什么时候读 |
|---|---|---|
| [frameworks/CATALOG.md](frameworks/CATALOG.md) | **判断内核**：35 条通用框架，每条带「什么时候别用」+ 选择判据 | 每次开工 |
| [docs/00-product/MVP-v0.1.md](docs/00-product/MVP-v0.1.md) | **建造契约**：v0.1 做什么、明确不做什么 | 动手前 |
| [docs/00-product/MVP-v0.1.1-SPEC.md](docs/00-product/MVP-v0.1.1-SPEC.md) | v0.1.1 增量规格：事实库 / 采访引擎 / 模板适配器 / Skill 路由器 | 动手前，与 MVP-v0.1 一起读 |
| [docs/00-product/PRODUCT-CONSTITUTION.md](docs/00-product/PRODUCT-CONSTITUTION.md) | 不可妥协的产品规则 C-01…C-08 | 改产品行为前 |
| [docs/01-research/DECISION-LOG.md](docs/01-research/DECISION-LOG.md) | 每条规则为什么这么定（D-001…D-028），含已考虑的替代项 | 想推翻某条规则前 |
| [CONTEXT.md](CONTEXT.md) | 词汇表，每个术语带 `_Avoid_` 反义词，防术语漂移 | 写产品文档前 |
| [memory.md](memory.md) | 当前阶段、验证状态与发布边界；只记已确认的持久状态 | 每次开工最后读 |

`docs/00-product/PRD-v0.2.md` 是 **North Star，不是施工图**。它定义的 8 道 fail-closed Gate 和 17 段 schema 是长期目标；v0.1 以 `MVP-v0.1.md` 为准，二者冲突时听后者。

## 五条保命规则

### 1. 隐私铁律 —— 素材不进产品文件

真实姓名、营收数字、客户名单、第三方谈话记录，**只允许出现在 `_private/` 和 `cases/`**（两个目录都已 gitignore）。

**绝不进 `.agents/skills/` `docs/` `templates/` `frameworks/` `schemas/`。** 产品文件必须领域中立，能直接交给任何陌生人用。

> 过去曾有真实素材误入产品文件并进入 Git 历史，最终导致全面返工。
> **用户喂的素材是让你听懂他要什么的上下文，不是产品源码。** 程序员不把老板的隐私写进代码。

需要举例说明某个概念时，编一个中性例子，或指向 `cases/` 里的实例，不要把真实案例内联进模板。

### 2. 框架收录标准 —— 只收全球通用规则

进 `frameworks/CATALOG.md` 的必须是**跨领域、跨年代被反复验证**的通用规则。

任何人的单一经验——某个教练、某个大 V、用户自己上次的成功——**都不进目录**，只能作为一条待验证证据进 case 文件。

每条框架**必须写「什么时候别用」**。只说什么时候用的是清单，说得出什么时候会误导的才是框架。

### 3. 灵活优先于完备 —— 工具不许变成仪式

- 按「卡住的形状」选框架，不按话题选；一次最多两个
- 允许输出「不需要框架，直接做」——低代价可逆的事套框架是把简单问题复杂化
- 默认用 GPT Work 自由协作，不以 Triage、Owner 标签或模板阻塞普通问答；正式收束时才进 Quick / Full
- GPT Work **不落 ThinkingCase**；进入正式化后，Full、重大/不可逆/他诊，或计入首批 5 次验证时才写 `cases/`
- 十分钟没看见新东西就换框架

任何让流程变成必须走完一遍的改动，默认拒绝。

### 4. 跑满 5 次真实 case 前，不加新东西

**不建**：YAML schema 校验、Case 状态机、`domain-packs/`、`evals/`、多 Agent、任何 UI。

`schemas/thinking-case.schema.yaml`（3881 行）已冻结为 v0.2 资产，v0.1 不引用。

理由见 `MVP-v0.1.md` §6 的 D-023…D-026：现阶段先验证工具能否被反复使用，再决定是否扩建。D-026 只允许按需读取既有知识源，不解除本节的新建禁令。

**唯一例外 `D-028`（v0.1.1）**：负责人授权在 5 Case 前建设状态层（事实库、采访引擎、模板适配器、复盘索引、全局入口）并把 Skill 压成路由器；规格见 `docs/00-product/MVP-v0.1.1-SPEC.md`。它不解冻本节其它任何一项。

### 5. 新东西先问：新模板还是新形状

新课程、新工具、新的 AI 审阅到来时，先答一句：**这是新的问题形状，还是新的模板？** 模板走 `references/adapt.md` 让系统替本人填；只有 CATALOG 兜底记录证明「断点在第 X 环、现有工具都不匹配」的形状才有资格入库。两者都不新建仓库。

## Git 与发布边界

- `master` 只作本地内部历史：旧提交含已删除的私人材料，**禁止推送、禁止连同 `.git/` 对外发送**。
- 对外发布只走 `public-sanitized` 独立干净历史，且必须先过下方隐私 tripwire；禁止把 `master` 历史合并进去。
- 当前状态与细节见 `memory.md`「Git 与发布边界」。

## Skill

主版本：`.agents/skills/clarify/SKILL.md`（Codex 读这个）。它是 ≤120 行的路由器；细则在同目录 `references/`（work / formalize / review / interview / adapt），按情境加载，不预读。
从其他目录调用：使用者在自己的全局 Skill 目录写一个启动器，指明本仓库根路径并转到 `clarify`；启动器不随本仓库分发，是唯一允许出现本机绝对路径的地方。
Claude 侧入口：`.claude/skills/clarify/SKILL.md` 是指向主版本的符号链接，改主版本即可，别分别改。

## 验证

运行时无构建。维护检查需要 `git` 与 `rg`。

公开 clone 可执行的基础自检：

```bash
git diff --check
test -e .claude/skills/clarify/SKILL.md
test -e .claude/skills/clarify/references/interview.md
git check-ignore _private/ cases/
```

项目维护者发布前还必须运行本机精确 tripwire；这份词表含历史事故证据，只放在被忽略的 `_private/`，不随公开仓库分发：

```bash
test -s _private/privacy-tripwire-patterns.txt
( rg --files-with-matches --hidden --glob '!**/.git/**' -f _private/privacy-tripwire-patterns.txt .agents/skills CONTEXT.md memory.md docs templates frameworks schemas; privacy_status=$?; [ "$privacy_status" -eq 1 ] )
```

有扫描输出就停止发布。无输出仍需人工确认 `AGENTS.md`、`CLAUDE.md`、`.agents/skills/`、`CONTEXT.md`、`memory.md`、`docs/`、`templates/`、`frameworks/`、`schemas/` 没有真实姓名、联系方式、业务数字、客户名单、本机绝对路径和第三方谈话细节。
