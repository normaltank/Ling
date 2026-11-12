# LingEuro

本仓库保存 LingEuro 的个人工程协作配置。需求、缺陷与持续规格使用 [normaltank/Ling Issues](https://github.com/normaltank/Ling/issues)。

## 使用方式

在本项目中直接向主代理描述目标，例如“检查这个问题并修好”或“把这个需求拆分后实现并验收”。主代理作为唯一统筹，按 Matt Pocock 方法选择所需阶段，自动安排研究、规划、实施、集成和独立审查，再统一交付结果。小改动采用轻量路线。

子代理默认使用 **GPT-6.1 Sol / high**。项目提供自动统筹技能、原生默认配置和六个角色说明；当前客户端缺少角色选择器时，统筹将角色说明放进实际派工正文。

## 配置入口

- [AGENTS.md](AGENTS.md)：项目统筹入口。
- [工作流](docs/agents/workflow.md)：路线、阶段与完成依据。
- [多代理约定](docs/agents/multi-agent.md)：模型、角色、派工与交接。
- [Issue tracker](docs/agents/issue-tracker.md)、[分流标签](docs/agents/triage-labels.md)、[领域文档](docs/agents/domain.md)：Matt 工程方法使用的项目约定。

可直接修改 `docs/agents/*.md` 调整流程。显式调用某个 Matt 技能时仍采用该技能自己的要求；日常工程任务使用项目自动流程。

本地学校源码、研究和实验材料保留在公开仓库之外；其协作与发布范围由对应任务确定。
