# LingEuro

本仓库保存 LingEuro 的个人工程协作配置。需求、缺陷与持续规格使用 [normaltank/Ling Issues](https://github.com/normaltank/Ling/issues)。

## 使用方式

在本项目中直接向主代理描述目标，例如“检查这个问题并修好”或“把这个需求拆分后实现并验收”。主代理作为唯一统筹，按已安装的通用 Matt 技能选择路线、组织工作并统一交付；用户无须逐个指定技能或管理子代理。

子代理默认使用 **GPT-6.1 Sol / high**。项目提供原生默认配置和六个角色说明；当前客户端缺少角色选择器时，统筹将角色说明放进实际派工正文。

## 配置入口

- [AGENTS.md](AGENTS.md)：项目统筹入口。
- [Matt 工作流](docs/agents/workflow.md)：通用技能的选路、实施与交付约定。
- [多代理约定](docs/agents/multi-agent.md)：模型、角色、派工与交接。
- [Issue tracker](docs/agents/issue-tracker.md)、[分流标签](docs/agents/triage-labels.md)、[领域文档](docs/agents/domain.md)：Matt 工程方法使用的项目约定。

流程与 ReviewProject、DataBase、OpenSource 一致：方案文档核对内容、证据、链接和状态；单个明确代码任务走 `implement`，按 `tdd` 验证并由 `code-review` 做双轴审查；跨任务建设走 `to-spec` → `to-tickets` → `implement-spec`。阶段流程以实际读取的已安装技能为准，项目 Markdown 保存接入与协作约定，不维护专属阶段技能。

本地学校源码、研究和实验材料保留在公开仓库之外；其协作与发布范围由对应任务确定。
