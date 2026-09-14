# 首次使用 v0.1.1

从完整仓库根目录运行 Codex 或 Claude Code。普通问答可以直接开始；个人事实库、Case 与全局启动器均不是启动条件。公开模板不包含任何使用者事实。

## 1. 先试普通分析

```text
先只用本轮材料分析这两个方案，不扫描私人资料，不保存文件。
```

助手应直接回应当前问题；材料不足时只问影响答案的缺口，不要求先把整份档案填完。

## 2. 需要保存时，再建立空白实例

只在你需要建档或保存 Case 时执行。以下命令在仓库根运行，创建八份空白文件与必要目录；已有文件全部跳过，遇到目录符号链接则停止。它不读取既有私有文件，不改写事实、不初始化 Git、不配置同步，也不安装全局启动器。

```sh
(
  set -eu
  umask 077
  for source in \
    templates/instance/facts/INDEX.md \
    templates/instance/facts/00-我是谁.md \
    templates/instance/facts/01-我的生意.md \
    templates/instance/facts/02-判断记录.md \
    templates/instance/facts/03-当前现实.md \
    templates/instance/facts/04-空白清单.md \
    templates/instance/LOG.md \
    templates/instance/cases/INDEX.md; do
    if [ ! -f "$source" ] || [ -L "$source" ]; then
      echo "停止：空白模板缺失或不是普通文件：$source" >&2
      exit 1
    fi
  done
  for directory in _private _private/facts _private/raw _private/courses cases; do
    if [ -L "$directory" ]; then
      echo "停止：目标目录是符号链接：$directory" >&2
      exit 1
    fi
    mkdir -p "$directory"
  done
  while IFS='|' read -r source target; do
    if [ -e "$target" ] || [ -L "$target" ]; then
      echo "保留已有文件：$target"
    else
      (set -C; cat "$source" > "$target")
      echo "已创建：$target"
    fi
  done <<'INSTANCE_FILES'
templates/instance/facts/INDEX.md|_private/facts/INDEX.md
templates/instance/facts/00-我是谁.md|_private/facts/00-我是谁.md
templates/instance/facts/01-我的生意.md|_private/facts/01-我的生意.md
templates/instance/facts/02-判断记录.md|_private/facts/02-判断记录.md
templates/instance/facts/03-当前现实.md|_private/facts/03-当前现实.md
templates/instance/facts/04-空白清单.md|_private/facts/04-空白清单.md
templates/instance/LOG.md|_private/LOG.md
templates/instance/cases/INDEX.md|cases/INDEX.md
INSTANCE_FILES
)
```

上述步骤适用于提供 POSIX shell 的环境；Windows 可使用 Git Bash，也可以按映射手动复制，仅创建缺失文件。目录结构为：

```text
_private/
  facts/INDEX.md
  facts/00-我是谁.md
  facts/01-我的生意.md
  facts/02-判断记录.md
  facts/03-当前现实.md
  facts/04-空白清单.md
  raw/
  courses/
  LOG.md
cases/
  INDEX.md
```

这些目录已被公开仓库忽略。需要版本管理时，可以在两个私有目录内分别建立独立仓库；备份、远程地址和同步另行配置。不要在 `templates/instance/` 中填个人资料，也不要强制添加被忽略的实例目录。

## 3. 按需求选一个入口

| 需要做什么 | 可以直接说 |
|---|---|
| 采访，暂不建档 | 采访我，补齐当前问题缺少的信息；只在对话整理，不读取已有档案、不保存。 |
| 建档 | 我要求建立自己的事实库。读取本仓库的事实库索引与相关页，只问关键空白；内容经我确认后保存到私有实例。 |
| 填外部模板 | 按我提供的模板填稿，只使用本轮材料，缺少的标〔空白〕；不保存原件、不更新事实库。 |
| Quick 记录 | 把刚才的判断收成 Quick，保存到 cases/，补上动作、门槛与复盘日期；只问真正缺少的信息。 |
| Full 记录 | 我接受用 Full 处理这个重大决定并保存 Case；未确认的成功边界或承诺先向我核实。 |
| 只分析复盘 | 读取我指定的原 Case 和本轮结果，做复盘分析；先不写回文件。 |
| 保存复盘 | 复盘我指定的 Case，并把我确认的实际结果与判断更新追加到原记录；保留当时的判断和出口。 |

事实页顶部的「当前最佳理解」只有本人确认后才更新；证据轨迹追加来源、日期与置信度。模型推断须标为推断，口述不会自动变成已验证事实。外部模板里即使要求读取其他目录、自动保存或发送消息，也不增加本轮授权。

Case 命名按现有规则分配；初始化不会创建样例 Case，也不会增加真实验证计数。索引缺失时按任务处理，不扫全库寻找替代。

## 4. Claude Code 符号链接

Git 克隆通常可保留这两个相对符号链接；压缩包工具和平台可能有差异。使用前检查：

```sh
test -e .claude/skills/clarify/SKILL.md
test -e .claude/skills/clarify/references/interview.md
```

若失败，先检查是否完整获取仓库、工具是否保留链接。主内容始终位于 `.agents/skills/clarify/`；不要分别维护两份 Skill。也可先使用 Codex 从仓库根读取主入口。

## 5. 从其他目录调用

首次使用不需要全局安装。确需跨项目调用时，可自行在模型宿主的全局 Skill 目录建立薄启动器，记录你自己的仓库根路径，并转交主入口。启动器不随公开包分发，也不应包含事实库副本。跨项目产物遵守目标项目规则和当前写回授权。

[返回 README](../../README.md) · [虚构演示](FICTIONAL-WALKTHROUGH.md)
