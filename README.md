# ThinkingOS

ThinkingOS 是一个运行在 Codex 或 Claude Code 中的 Markdown 思考工具。普通问答直接使用模型能力；需要正式收束时，可将已有对话整理成 Quick 或 Full Case，保留判断、行动、现实结果和复盘记录。

当前版本用于验证一件事：这套工具能否在真实问题中被反复使用。它没有 UI、状态机或自动提醒服务。

## 能做什么

- 直接分析、解释、比较方案和调整计划，不要求先填表。
- 在需要时把对话收成 Quick 或 Full，并复用已经提供的背景。
- 从 35 条通用框架中按当前卡点选择零到两个工具。
- 记录动作、观察门槛、复盘日期和后续判断更新。
- 将真实 Case 留在本地，避免混入产品文件和 Git 历史。

## 使用边界

这是一个**完整仓库型 Skill**。`.agents/skills/clarify/` 会读取仓库里的 `frameworks/`、`templates/` 和产品契约，单独复制 Skill 目录会导致链接失效。

当前支持：

- Codex：从仓库根目录打开任务。
- Claude Code：从仓库根目录启动，并确保 Git 正确保留 `.claude/skills/clarify/SKILL.md` 符号链接。

Windows、ZIP 解压工具和部分同步软件可能把符号链接变成普通文本。使用 Claude Code 前运行：

```bash
test -e .claude/skills/clarify/SKILL.md
```

## 开始使用

克隆完整仓库并从根目录启动 Codex 或 Claude Code。正常提问即可，无需先输入激活命令。

```text
帮我分析一下这两个方案，我现在拿不准。
```

模型默认保持自由协作。需要形成可复盘记录时，再明确提出：

```text
把刚才的判断收成 Quick，并给出下一步和复盘日期。
```

重大、高代价或难以撤回的事项可使用：

```text
把这个决定收成 Full，保存 Case。
```

到期后手动重开原记录：

```text
复盘 cases/THK-NNN-example.md
```

## 数据与隐私

- GPT Work 对话不会自动写入 ThinkingCase。
- 正式记录保存在仓库根目录的 `cases/`，该目录已被 Git 忽略。
- `_private/` 用于维护者的私有来源、精确隐私词表和可选知识索引，也已被 Git 忽略。
- `.gitignore` 只能防止误提交，不能加密文件。备份、同步和删除由使用者自行管理。
- 对外分享前只导出公开文件，不能连同未经清理的 `.git/`、`cases/` 或 `_private/` 一起发送。

可选的私有知识索引不会随公开仓库分发。缺少它时，ThinkingOS 仍会使用模型能力与 `frameworks/CATALOG.md`；领域增强能力会因使用者自己的知识源而不同。

## 目录

```text
.agents/skills/clarify/   Codex 主 Skill
.claude/skills/clarify/  Claude Code 入口
frameworks/               通用框架目录
templates/                Quick / Full Case 模板
docs/                     v0.1 契约、长期 PRD 与决策记录
schemas/                  冻结的 v0.2 schema 资产
cases/                    本地真实 Case，不进入 Git
_private/                 本地私有材料，不进入 Git
```

## 验证

维护检查需要 `git` 与 `rg`：

```bash
git diff --check
test -e .claude/skills/clarify/SKILL.md
git check-ignore _private/ cases/
```

项目维护者发布前还需运行本机 `_private/privacy-tripwire-patterns.txt`，并人工检查所有公开文件。精确词表包含历史事故证据，因此不会提交。

## 许可证

本项目采用 [MIT License](LICENSE)。允许使用、复制、修改、合并、发布、分发、再许可和销售，但必须在副本或主要部分中保留版权声明与许可证文本。软件按现状提供，不附带担保。
