# ThinkingOS 项目记忆

> 最后核验：2026-09-02

本文件用于跨任务恢复项目当前状态。规范性产品规则以 `MVP-v0.1.md`、`PRODUCT-CONSTITUTION.md`、`DECISION-LOG.md`、`CONTEXT.md` 和 `frameworks/CATALOG.md` 为准；出现冲突时按 `AGENTS.md` 的事实源顺序处理。

## 当前阶段

- 当前版本：v0.1.1（`D-028`）：状态层已建，进入真实使用验证。首个真实使用 = 用采访引擎 + 适配器完成一份到期的外部模板。
- 当前目标：跑满 5 个正式验证 Case，其中 3 次自诊、2 次他诊；每次需要正常决策出口、落盘记录和复盘日期。
- V0.3「导航循环」已由 `D-027` 记录为 `Provisional North Star Candidate`，只进入无建设验证，不取代现行 North Star、MVP、产品宪法或 `ThinkingCase` 价值单元。
- 下一阶段：先裁决目标、项目和每日行动的单一事实源，再用现有 GPT Work、Quick / Full 与该事实源手工运行真实周循环；周循环与正式 Case 共享情境，但分别验收、逐案计数。
- 扩建边界：验证完成前不增加状态机、UI、domain pack、评测系统或多 Agent 运行时；`D-028` 是唯一例外，且规则层只减不增（ROF）。
- 第 3 个正式 Case 后做第一次 ROF；docs 在此之前冻结（只允许 Case 相关记录）。
- v0.2 schema 保持冻结，v0.1 运行时不读取它。

## 当前运行方式

- 普通对话默认使用 GPT Work，可直接分析、解释、规划和执行。
- 用户要求正式收束、落盘或处理重大承诺时，再复用已有对话进入 Quick 或 Full。
- 通用框架来自 `frameworks/CATALOG.md`，当前共 35 条。
- 专门方法属于可选增强。缺少私有知识索引时，模型能力与 CATALOG 仍可完成基础流程。
- 运行形态是完整仓库型 Skill；单独复制 `.agents/skills/clarify/` 会丢失框架、模板和产品契约。

## 已验证状态

- Codex 主入口：`.agents/skills/clarify/SKILL.md`（路由器 69 行 + `references/` 五文件）。
- 事实库 `_private/facts/` V1 已起草（五页 + INDEX，带四档置信度与空白清单）；`_private/` 与 `cases/` 各自 git 已初始化。
- 全局启动器已装在使用者的全局 Skill 目录（仓库外，不分发）。
- Claude Code 入口：`.claude/skills/clarify/SKILL.md`，相对符号链接已验证可解析。
- Quick / Full 模板已覆盖正常决策、三种非答案出口、到期复盘和 Case 谱系。
- 公开文件的精确隐私 tripwire 已通过。
- Markdown 相对链接已通过检查。
- schema YAML 可解析：3881 行、69 个 `$defs`、414 个本地 `$ref`，无缺失引用。
- 决策日志当前包含 D-001 至 D-027；其中 D-027 为 V0.3 导航循环的 provisional 方向裁决，不是施工授权。

## Git 与发布边界

- `master` 只作本地内部历史使用。旧提交曾包含已删除的私人材料和个人提交元数据，不得推送或连同 `.git/` 对外发送。
- `public-sanitized` 是公开用的独立干净历史，只包含领域中立文件和通用提交身份。
- 远程：`origin` 是维护者自己的私有 GitHub 仓库，只接收 `public-sanitized`（远程分支名 `main`）；`master` 不推送。
- 当前采用 MIT License，允许复制、修改、再分发和商业使用；副本或主要部分必须保留版权与许可声明。
- 对外同步新版本时，只把已完成脱敏检查的改动带入 `public-sanitized`；禁止合并 `master` 的旧历史。

## 下一次开工先看

1. 当前问题能否直接在 GPT Work 中解决。
2. 是否正在收集首批 5 个正式验证 Case 的真实使用证据。
3. 新功能是否来自反复出现的实际缺口。
4. 对外发布动作是否只涉及 `public-sanitized`。

## 记录纪律

- 只记录跨任务仍有价值、已经确认的状态。
- 临时想法、聊天摘要和一次性待办不进入本文件。
- 真实姓名、联系方式、业务数字、客户名单、第三方谈话和真实 Case 只进入 `_private/` 或 `cases/`。
- 状态变化时直接更新对应条目；产品裁决进入 `DECISION-LOG.md`，不在这里建立第二套规则。
