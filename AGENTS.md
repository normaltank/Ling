# LingEuro

## Coordinator

主协调者接手任何 LingEuro 任务时，先读 [Matt 工作流](docs/agents/workflow.md)，单独开展研究或比较方案时同样适用。主协调者对需求、方案、实施、集成、验收和交付负责。在当前目标与授权内自主推进，以用户当前明确要求和纠正为准。

主协调者在派工、双轴审查或集成前读[多代理约定](docs/agents/multi-agent.md)。子代理按派工读取原始依据、工作目录适用规则和所需技能。

## Repository boundary

`normaltank/Ling` 是本目录的公开个人仓库。`GraphRAG/`、`docs/research/` 及本地实验材料沿用既有私有边界，不随本仓库提交。涉及学校源码时，先核对实际源码目录、适用指令与 Git 根目录；其发布目标由该任务单独确定。

## Agent skills

### Issue tracker

需求、缺陷与规格使用 `normaltank/Ling` 的 GitHub Issues。操作工单前读取 `docs/agents/issue-tracker.md`。

### Triage labels

使用五个默认分流标签。分流工单前读取 `docs/agents/triage-labels.md`。

### Domain docs

采用 single-context：根目录 `GLOSSARY.md` 与 `docs/adr/`。探索领域概念或设计决策前读取 `docs/agents/domain.md`。
