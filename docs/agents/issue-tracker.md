# Issue tracker: GitHub

本仓库的需求、缺陷和规格位于 https://github.com/normaltank/Ling/issues 。优先使用已连接的 GitHub 工具；工具能力不足时，使用已认证的 `gh` CLI。以下 CLI 示例与连接工具指向同一个仓库。

## 目标仓库

在本仓库内先运行 `gh repo view --json nameWithOwner`，确认结果为 `normaltank/Ling`。以下命令显式指定 `--repo normaltank/Ling`。

`gh` 不在路径时，可检查本机忽略目录 `logs/tools/gh/bin/gh.exe` 中的已有便携版本。连接工具使用显式仓库参数，并核对返回的仓库身份。只在用户自己的目标仓库记录工作。

## 常用操作

- 创建：`gh issue create --repo normaltank/Ling --title "标题" --body-file <UTF-8正文文件>`。
- 读取：`gh issue view <编号> --repo normaltank/Ling --json number,title,body,labels,comments`。
- 列出：`gh issue list --repo normaltank/Ling --state open --json number,title,body,labels`。
- 评论：`gh issue comment <编号> --repo normaltank/Ling --body-file <UTF-8正文文件>`。
- 加减标签：`gh issue edit <编号> --repo normaltank/Ling --add-label <标签>` / `--remove-label <标签>`。
- 关闭：先用评论记录完成或关闭依据，再运行 `gh issue close <编号> --repo normaltank/Ling`。

多行正文通过 UTF-8 文件与 `--body-file` 传入，保留真实换行。标签含义见 `triage-labels.md`。

## 依赖与子任务

优先使用 GitHub 原生子议题和依赖关系；通过当前 `gh ... --help` 检查可用命令。若仓库或客户端不支持，在子任务正文首行写 `Part of #<父编号>`，并用 `Blocked by: #<编号>` 明确阻塞项。

原生关系需要数据库 ID 时，先读取工单的 `id`，与可见工单 `number` 区分。选择可派工项时，读取实际阻塞状态；标签 `ready-for-agent` 本身不代表依赖已经满足。共享任务先认领再派工，避免重复实施。

## Pull requests as a triage surface

**PRs as a request surface: no.**

## 工程技能约定

技能要求“发布到 issue tracker”时，创建本仓库的 GitHub Issue；要求“获取相关 ticket”时，读取对应 Issue 及其评论。

## Wayfinding operations

用户显式使用 `wayfinder` 时，地图是带 `wayfinder:map` 标签的 Issue，决策票作为其子议题；票型使用 `wayfinder:research`、`wayfinder:prototype`、`wayfinder:grilling` 或 `wayfinder:task`，与实现任务的五个分流标签区分。

- 地图保存目标、Notes、Decisions so far、Not yet specified 和 Out of scope；明细保留在决策票中。
- 先建立工单，再用真实编号或数据库 ID 连父子与阻塞关系；原生功能不可用时使用上面的正文约定。
- 前沿是地图中仍开放、所有阻塞项已关闭且无人认领的子议题；按地图顺序选择。认领使用负责人字段，例如 `gh issue edit <编号> --repo normaltank/Ling --add-assignee @me`。
- 解决后先发布带证据的结论评论，再关闭决策票，并给地图的 Decisions so far 追加带标题的链接及一句结论。
- 按实际需要建立 `wayfinder:*` 标签。未调用这条路线时无须预建地图或决策票。
