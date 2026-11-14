# LingEuro

## Coordinator

主代理是用户的唯一统筹入口。收到本项目的开发、维护、规格、排障或审查任务时，按 [Matt 工作流](docs/agents/workflow.md)直接读取并使用已安装的通用 Matt 技能，沿用 ReviewProject、DataBase、OpenSource 的接入方式；本项目只维护入口、协作约定和证据，不另设专属阶段技能。用户可以直接描述目标，无须逐个指定技能或管理子代理。

统筹按任务规模主动委派临时子代理，负责需求、任务图、集成、验收和最终汇报。派工前读取 `docs/agents/multi-agent.md`。子代理只执行获派角色，向统筹返回结果。

所有子代理默认 `gpt-6.1-sol`，思考强度 `high`，使用新上下文。实际调用显式传入 `model`、`reasoning_effort` 与 `fork_turns="none"`；原生默认值见 `.codex/config.toml`，角色见 `.codex/agents/`。角色选择器不可用时，把相应角色说明加入派工正文。

沿用当前对话已经确认的范围与决定；常规技术选择自主推进。只有影响结果且现有信息无法解决的业务问题才交用户决定。历史计划和其他聊天的“下一步”只作背景，当前请求决定本次范围。

## Repository boundary

`normaltank/Ling` 是本目录的公开个人仓库。`GraphRAG/`、`docs/research/` 及本地实验材料沿用既有私有边界，不随本仓库提交。涉及学校源码时，先核对实际源码目录、适用指令与 Git 根目录；其发布目标由该任务单独确定。

## Agent skills

### Issue tracker

需求、缺陷与规格使用 `normaltank/Ling` 的 GitHub Issues。操作工单前读取 `docs/agents/issue-tracker.md`。

### Triage labels

使用五个默认分流标签。分流工单前读取 `docs/agents/triage-labels.md`。

### Domain docs

采用 single-context：根目录 `GLOSSARY.md` 与 `docs/adr/`。探索领域概念或设计决策前读取 `docs/agents/domain.md`。
