# 子代理协作

## 模型与派工

主协调线程默认 Sol `high`，见[项目配置](../../.codex/config.toml)。派工模型只选 `gpt-6.2-sol` 和 `gpt-6.2-astra`。Sol 负责实施、操作、验证与常规判断，Astra 主动处理复杂决策、系统设计和独立全局审查。由主协调者直接完成的步骤沿用主线程设置。

每次用 `fork_turns="none"` 开新上下文，显式传模型和推理档位。配置优先级依次为角色 TOML、派工参数、`[agents]` 默认值、父线程设置。派工前核对工具公开的角色绑定。角色和参数匹配且工具接受两者时同时传入。工具锁定角色参数、绑定不一致或角色不可选时，用通用角色显式传参，并附对应角色的 `developer_instructions`。`spawn_agent` 的参数为 `model` 和 `reasoning_effort`，TOML 的档位字段为 `model_reasoning_effort`。目标模型不可用时报告受限事项，并在主线程继续独立工作。

- `implement-spec` 的 exploration subagent 使用 [ling_explorer](../../.codex/agents/ling_explorer.toml)，按勘察范围选 Sol `low` 或 `medium`。implementer subagent 使用 [ling_implementer](../../.codex/agents/ling_implementer.toml)，merger subagent 使用 [ling_merger](../../.codex/agents/ling_merger.toml)，两者默认 Sol `medium`。实施者沿用模型执行 `tdd`，复杂任务升到 `high`，极复杂工单可选 Astra。
- `research` 定向取证、`improve-codebase-architecture` 代码勘察、`codebase-design` 局部设计及 `diagnosing-bugs` 常规疑难诊断使用 Sol `high`。定向取证用 [ling_researcher](../../.codex/agents/ling_researcher.toml)，常规规格和拆票草案用 [ling_planner](../../.codex/agents/ling_planner.toml)。
- 用 [ling_analyst](../../.codex/agents/ling_analyst.toml) 让 Astra `high` 独立处理跨来源方案比较、`wayfinder` 重大决策与全局依赖、架构评估、长期系统边界、基础领域模型、复杂 `to-spec`、跨模块根因及 `retro` 系统性分析。复杂 `to-tickets` 独立核查可用 Astra `medium` 或 `high`。同一决策可并行安排 Sol 取证和实验。
- `code-review` 的 Standards 使用 [ling_standards_reviewer](../../.codex/agents/ling_standards_reviewer.toml)（Sol `high`），Spec 使用 [ling_spec_reviewer](../../.codex/agents/ling_spec_reviewer.toml)（Astra `high`）。
- 委派 `prototype`、`triage`、`pr`、`wizard`、`to-questionnaire`、`writing-for-agents` 时用 Sol `medium`。`handoff` 由主协调者以 `high` 组织。

Astra 直接读取原始问题、代码、任务或研究材料。分析类派工按 [ling_analyst](../../.codex/agents/ling_analyst.toml) 的交付要求执行，Spec 审查按自身角色的交付要求执行。主协调者核实后作最终决定。实施者拿到明确任务后尽快产生可检验结果。分析停滞时补信息或换证据来源。只对复杂问题定向使用 `xhigh`，保留常规默认档位。

## 并发与交接

- 按 ready frontier 派工。根据独立性、worktree、分支、数据库、端口、测试环境、CPU、内存和 API 额度调整并行度，服从客户端实际容量。项目配置沿用客户端默认容量，默认容量影响可并行工单时核对受支持的设置。独立工单可与分析并行。共享集成分支始终由一位 merger 串行写入。
- 派工写明决策问题或验收条件、固定版本、工作目录、写入范围、原始依据、适用技能与应跑的检查。通过路径提供需要的内容。审查者各自读取原始依据，汇报前保持独立。
- 交接写明实际版本、文件、已验证行为、失败或未跑的检查和遗留事项。审查发现给出位置、规则或需求依据、触发情形和影响。配置解析、客户端角色绑定和实际派工结果各自注明证据。
