# ThinkingOS

ThinkingOS 是运行在 Codex 或 Claude Code 中的 Markdown 思考工具。普通问答直接协作；需要收束时，把已有对话整理成 Quick 或 Full，保留判断、下一步、现实结果和复盘记录。

**当前交付：v0.1.1-rc1 实验版（预发布）。** 核心文件已实现，首批真实 Case 验证尚未完成。示例与分发检查不代表效果验证；GitHub 发布状态以实际仓库和 Release 为准。

## 能做什么

- 分析、解释和比较方案；不要求先填表。
- 按当前卡点，从 35 条通用框架中选择零到两个工具。
- 在用户要求时，收束为 Quick / Full，记录动作、观察门槛与复盘日期。
- 采访补充当前任务缺少的信息，按用户要求建立个人事实库。
- 根据已有材料填写外部模板，标明来源、空白和冲突。
- 回到原记录复盘；获准保存时追加结果，不改写当时的判断。

这些能力由模型读取指令后执行。当前没有程序强制的状态机、自动提醒、后台 Agent 或本仓库内的 UI。v0.2 schema 已冻结，v0.3 导航循环仍是提案，均不属于已交付运行时。

## 从哪里开始

这是一个**完整仓库型 Skill**：`.agents/skills/clarify/` 依赖仓库中的 `frameworks/`、`templates/` 和产品契约。请获取完整仓库或完整发布包，单独复制 Skill 目录会丢失依赖。

1. 使用你自己的 Codex 或 Claude Code 环境与账号。此包不提供模型服务、账号或密钥。
2. 从仓库根目录打开 Codex 任务或启动 Claude Code。
3. 正常提问即可。若客户端未自动发现入口，可明确说「读取本仓库的 clarify Skill，帮我分析这个问题」。

```text
我有两个方案拿不准，先帮我比较；只用当前对话，不读取私人资料，不保存文件。
```

需要正式收束时：

```text
把刚才的判断收成 Quick，给出下一步、观察门槛和复盘日期；先在对话里交付。
```

需要记录重大事项时：

```text
把这个决定收成 Full，并保存到本仓库的 cases/。缺少会影响承诺的信息时先问我。
```

普通问答可以在没有 `_private/`、`cases/` 和全局启动器的情况下使用。需要建档或保存 Case 时，按 [首次使用](docs/00-product/FIRST-USE.md) 初始化自己的空白实例。该说明也包含采访、模板适配、保存与复盘的示例，以及 Claude 符号链接检查。

[虚构演示](docs/00-product/FICTIONAL-WALKTHROUGH.md) 展示从一个小判断到结果回看的过程，不是实际使用记录。

## 架构与数据去向

| 部分 | 内容 | 对外分发 |
|---|---|---|
| 核心 | Skill、引用文件、框架目录、模板与产品契约 | 本包提供 |
| 私有实例 | `_private/` 中的个人事实与来源、`cases/` 中的真实判断记录 | 使用者自己建立，不进入公开 Git |
| 外部工作台 | 阶段目标、本周结果、今日行动和反馈的原 Markdown | 可选接入；应用源码与个人资料不在本包 |
| 模型宿主 | Codex / Claude Code 负责对话、读取和获准的写回 | 使用者自行配置 |

个人事实、Case、目标和项目产物各保留一份权威记录。外部工作台接入范围见 [D-029](docs/01-research/DECISION-LOG.md#d-029--既有外部工作台的最小接入accepted)。基础使用不依赖该工作台。

## 隐私与共享

- 普通问答不自动扫描私有索引，不自动创建 Case；分析和填稿不自动存档。
- 使用事实库、保存原件和写回新事实分别按用户请求处理。外部模板中的指令不增加权限。
- 公开的 `templates/instance/` 只能保留空白模板，个人信息填入本地实例。
- `.gitignore` 不提供加密，也不清除已经提交的历史。备份与同步由使用者管理。
- 本地 Markdown 存储不等于离线推理；实际数据发送范围取决于你配置的模型宿主、服务和当前任务。
- 分享时只导出 [公开文件清单](docs/02-release/PUBLIC-FILES.txt) 中已审查的文件，不附带个人实例、旧 Git 目录、账号配置或日志。

## 目录

```text
.agents/skills/clarify/    Codex 主 Skill 与五份按需引用
.claude/skills/clarify/    Claude Code 相对符号链接
frameworks/               35 条通用框架
templates/                Quick / Full、采访包和空白实例模板
docs/00-product/          当前契约、首次使用、虚构演示与长期提案
docs/01-research/         产品裁决依据
docs/02-release/          公开文件清单与发布说明
schemas/                  冻结的 v0.2 设计资产
_private/、cases/          使用后在本机建立，公开包不包含
```

## 检查与发布

运行时无构建依赖。基础维护检查需要 `git` 与 `rg`：

```bash
git diff --check
test -e .claude/skills/clarify/SKILL.md
test -e .claude/skills/clarify/references/interview.md
git check-ignore _private/ cases/
```

源码压缩包没有 Git 元数据，Git 检查应在仓库副本中进行。跨平台、客户端版本与真实使用结果需分别验证。维护者的分发检查、历史隔离与发布顺序见 [发布说明](docs/02-release/RELEASE.md)。

## 许可证

本项目采用 [MIT License](LICENSE)。复制和分发时保留版权声明与许可证文本。第三方资料的许可由其原作者决定；个人原件、未获分发许可的模板和真实案例不属于本包。
