# OpenClaw 生态日报 2026-07-03

> Issues: 196 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-03 06:24 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告



---

## 横向生态对比

好的，作为资深技术分析师，基于您提供的2026-07-03各项目动态，以下是横向对比分析报告：

---

### 1. 生态全景

当前个人AI助手与自主智能体开源生态正处于 **“裂变与收敛并存”** 的高强度演化期。以 OpenClaw 为核心的架构体系正经历快速分化：衍生项目（Zeroclaw、PicoClaw）在追求前沿功能和企业级安全的同时，也深受核心稳定性与跨平台问题的困扰。生态内玩家普遍将目光从基础的“聊天”转向 **有状态的自主任务执行**（Goal Mode、SOP），并迫切寻求通过与 OpenAI API / OIDC 等标准协议的对齐，融入更广泛的企业软件栈。整体呈现“上游激进创新，下游质量巩固，全行业补安全课”的态势。

### 2. 各项目活跃度对比

| 项目 | Issues (新开/活跃) | PRs (合并/创建) | Release | 健康度评估 |
|---|---|---|---|---|
| **Zeroclaw** | ~15+ (含S0/S1严重Bug) | 100+ (20+已合并) | v0.8.3 冲刺中 | ⚠️ 极高活跃但Bug积压严重，处于“大爆炸”式迭代阶段 |
| **QwenPaw** | 16 (12活跃) | 54 (25合并) | **v2.0.0-beta.2** | 🟢 迭代迅猛，v2新功能密集合并，但Beta阶段稳定性存疑 |
| **PicoClaw** | ~1 (关键Bug现场修复) | 27 (14合并) | 无 | 🟢 稳定维护状态，渠道扩展（DeltaChat）和依赖更新为主 |
| **OpenClaw (参照)** | 未提供当日数据 | 未提供当日数据 | 未发布 | 🟤 生态基线，推测以稳定保守迭代为主（非激进开发期） |
| **Hermes-Agent** | 未提供 | 未提供 | 未发布 | ⚪ 动态不明，推测当日无显著社区活跃或仍处早期阶段 |

### 3. OpenClaw 在生态中的定位

OpenClaw 被明确定义为“核心参照”，在生态中扮演 **架构标准制定者** 和 **稳定性基准** 的角色。

*   **优势**：作为派系之源，其核心架构（Gateway、Skill 系统、MCP 集成）是 Zeroclaw 和 PicoClaw 的底层基石

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是基于您提供的 Zeroclaw 项目数据生成的 2026-07-03 项目动态日报。

---

# Zeroclaw 项目动态日报 | 2026-07-03

## 1. 今日速览

随着 `v0.8.3` 版本的临近，Zeroclaw 项目今日呈现出极高的开发活跃度。过去 24 小时内，社区提交了超过 100 条 Pull Requests，其中安全修复、新的“目标模式”（Goal Mode）功能以及 OpenTelemetry 可观测性集成是今日的核心推进项。围绕着 MCP 工具在 TUI 界面中的可见性问题、OIDC 认证的支持以及新的 OpenAPI 兼容端点，社区讨论非常热烈。项目整体健康状况良好，正处于密集的功能和稳定性冲刺阶段。

## 2. 版本发布

(无)

## 3. 项目进展

今日合并/关闭了多个关键 PR，标志着项目在多个维度上取得了实质性进展：

- **核心安全加固**:
    - PR [#8637](https://github.com/zeroclaw-labs/zeroclaw/pull/8637) **已合并**: 修复了 `skill_http` 中的 SSRF 漏洞，通过拒绝 URL 中的用户信息（userinfo）来关闭解析器级别的安全缺口。这对于防止内部网络探测至关重要。
    - PR [#8305](https://github.com/zeroclaw-labs/zeroclaw/pull/8305) **已合并**: 修复了 Web 仪表盘中无法显示已配置的 MCP 服务器工具列表的问题。该补丁解决了 `v0.8.3` 中的一个关键体验问题。

- **核心功能演进**:
    - PR [#8638](https://github.com/zeroclaw-labs/zeroclaw/pull/8638) **已合并**: 实施了重大变更，移除了硬编码的 ClawHub 技能安装源，替换为通用的、基于 Git 目录的技能选择器。这增强了技能分发系统的灵活性和可扩展性。
    - PR [#8641](https://github.com/zeroclaw-labs/zeroclaw/pull/8641) **已创建**: 修复了 WASM 插件系统的特性依赖图，确保了安装时配置种子数据（config seeding）的正确性，使插件系统的构建更加健壮。
    - PR [#8640](https://github.com/zeroclaw-labs/zeroclaw/pull/8640) **已创建**: 引入了 `ScopedToolRegistry`，为 Gateway 的工具注册引入了一个统一的组装接口，有助于统一不同来源工具的生命周期管理。

- **开发者体验与质量**:
    - PR [#8613](https://github.com/zeroclaw-labs/zeroclaw/pull/8613) **已创建**: 在文档中增加了关于“压缩合并新鲜度基础”（squash-merge freshness basis）的说明，旨在通过确保提交头匹配来提升合并流程的可靠性。
    - PR [#8604](https://github.com/zeroclaw-labs/zeroclaw/pull/8604) **已创建**: 为 Windows 构建添加了静态链接 MSVC CRT，解决了在没有安装对应运行时环境的 Windows 机器上无法运行的问题。

## 4. 社区热点

今日社区讨论高度集中，主要围绕以下几个热点：

- **MCP 工具在 TUI 中的可见性问题** (Issue [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193)): 这是今日最活跃的议题，有 14 条评论。用户报告了 MCP 服务器成功连接后，其暴露的工具在 TUI 界面中无法显示，但 Gateway API 却能正常识别。这导致了工作流被阻塞的严重问题，社区正积极讨论根因及解决方案。这反映了用户对“所见即所得”的核心体验需求。
- **项目工作流程与标签治理** (Issue [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)): 作为一个治理相关的 RFC，该议题持续吸引 13 条评论。社区成员正在深入讨论如何优化工作标签、自动化看板管理，以提升项目维护效率和贡献指引清晰度。这表明社区正在从代码贡献延伸到项目治理的参与。
- **OIDC 认证与 OpenAPI 兼容端点** (Issue [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) 和 Issue [#8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)): 围绕这两个议题的讨论显示出社区对 Zeroclaw 可集成性和企业级功能的需求日益增长。用户希望 Zeroclaw 能够作为标准基础设施的一部分，无缝接入现有的 OpenID Connect 认证体系和通过业界标准的 OpenAI API 协议与现有工具链（如 Open WebUI, Continue.dev）对接。

## 5. Bug 与稳定性

今日报告了若干关键 Bug，项目组已迅速响应：

- **严重性 S0 (数据丢失/安全风险)**:
    - **WSL2 连续 OOM** (Issue [#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)): 自 4 月 9 日以来的老问题，今天仍在讨论中。该问题会导致 Zeroclaw 进程被系统 OOM Killer 杀死，存在潜在数据丢失风险。
    - **SSRF 漏洞修复 (已修复)**: PR [#8637](https://github.com/zeroclaw-labs/zeroclaw/pull/8637) 与 [#8635](https://github.com/zeroclaw-labs/zeroclaw/pull/8635) 今日分别修复了 `skill_http` 和 `text_browser` 工具中的 SSRF 安全漏洞，体现了项目对安全问题的快速响应。

- **严重性 S1 (工作流阻塞)**:
    - **MCP 工具 TUI 不可见** (Issue [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193)): 持续发酵，需要优先解决。
    - **Headless SOP 执行错误** (Issue [#8631](https://github.com/zeroclaw-labs/zeroclaw/issues/8631)): 新报告的 Bug，当确定性 SOP 由无头触发器（如 cron）启动时，步骤被错误地标记为“已完成”而实际未执行。这会生成虚假的审计轨迹，影响系统可靠性。**暂无关联修复 PR**。

- **严重性 S2 (降级行为)**:
    - **多 Agent 运行时技能管理混乱** (Issue [#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)): `skills install/list/remove` 命令错误地操作在 `data_dir` 上，而多 Agent 运行时实际并不加载该目录，导致核心功能流程断裂。
    - **Provider 内容静默删除** (Issue [#8615](https://github.com/zeroclaw-labs/zeroclaw/issues/8615)): 兼容性 provider 存在 bug，无条件地剥离 `<think>` 标签，可能导致内容被静默删除或产生空回复，严重影响用户使用体验。
    - **WSL2 重启风暴** (PR [#8633](https://github.com/zeroclaw-labs/zeroclaw/pull/8633)): 新提出的修复 PR，解决了 WSL2 环境下组件监督器因重启退避逻辑错误导致的“重启风暴”和潜在 OOM 问题。
    - **Windows 74 个测试失败** (Issue [#7462](https://github.com/zeroclaw-labs/zeroclaw/pull/8633)): Windows 平台上的大量测试失败问题依然存在，是向多平台发布迈进的关键阻碍。

## 6. 功能请求与路线图信号

今日涌现了多个重要的功能请求，并与已有 PR 形成呼应，强烈暗示了项目未来的演进方向：

- **OIDC 认证升级**: Issue [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) 的 RFC 正在推进，同时追踪 Issue [#8289](https://github.com/zeroclaw-labs/zeroclaw/issues/8289) 和 PR [#8289](https://github.com/zeroclaw-labs/zeroclaw/issues/8289) 显示出这是一个已被纳入路线的、高优先级的企业级特性。PR [#8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486) 和 Issue [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) 共同指向了增加 **OpenAI Chat Completions 兼容端点** 的需求，这将是项目提升互操作性的关键一步。
- **目标模式 (Goal Mode)**: Issue [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) 描述的“目标模式”是一个重大功能请求，旨在支持有界的自主任务执行。对应的 PR [#8393](https://github.com/zeroclaw-labs/zeroclaw/pull/8393) 已经进入实施阶段，说明该功能已是 `v0.8.3` 的候选功能。
- **插件作者指南完善**: PR [#8621](https://github.com/zeroclaw-labs/zeroclaw/pull/8621) 添加了插件作者指南系列，而 Issue [#8636](https://github.com/zeroclaw-labs/zeroclaw/issues/8636) 跟进第三方验证后的改进项，表明项目正致力于完善和完善 WASM 插件系统的开发者体验。
- **可观测性升级**: PR [#8567](https://github.com/zeroclaw-labs/zeroclaw/pull/8567) 为运行时增加了 OTel 内容策略，这对于企业级部署中的监控和审计至关重要，同时也是 RFC #8462 的实现落地。

## 7. 用户反馈摘要

- **集成与互操作性**: 用户对 Zeroclaw 接入现有企业基础设施有强烈诉求。具体表现在：
    - **痛点**: “无法直接连接 OpenAI 兼容客户端（如 Open WebUI, LobeChat）”。
    - **反馈**: “多模型提供者（如 Openrouter）场景下，需要一个简单的方法在聊天中快速切换不同模型”。
- **核心体验与稳定性**:
    - **痛点**: MCP 工具在 TUI 中不可见，导致用户对核心功能产生困惑。用户评论指出“即使在 TUI 中看不到，但 Gateway 却能看到，体验割裂”。
    - **反馈**: 用户对 SOP 引擎概念表示赞赏，但指出“文档缺少足够详尽的示例”（Issue [#8587](https://github.com/zeroclaw-labs/zeroclaw/issues/8587)）。
- **安全问题**:
    - **反馈**: “Agent 的 `/model --agent` 命令缺乏授权检查，任何能发送消息的用户都可以改变整个 Agent 的模型”，社区成员敏锐地指出了此类权限滥用漏洞（Issue [#8044](https://github.com/zeroclaw-labs/zeroclaw/issues/8044)）。

## 8. 待处理积压

- **OOM 与跨平台问题**: 4 月报告的 **WSL2 连续 OOM** (Issue [#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)) 和 6 月报告的 **Windows 74 测试失败** (Issue [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)) 依然是长期未解决的关键问题，对用户基础和平台兼容性构成严重威胁，需要维护者给予更高优先级关注。
- **技能管理流程阻塞**: **多 Agent 环境下技能管理功能断裂** (Issue [#8334](https://github.com/zeroclaw-labs/zeroclaw/issues/8334)) 是一个核心流程的阻塞性 Bug，直接影响了用户“下载并立即使用”技能的体验，亟待解决。
- **阻塞的 RFC**: Issue [#7952](https://github.com/zeroclaw-labs/zeroclaw/issues/7952) (发布全渠道预构建物) 和 Issue [#8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550) (OpenAI 兼容端点) 处于 `status:blocked` 状态，可能需要核心维护者的决策或资源调度来推动。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-07-03

---

## 1. 今日速览

项目今日整体活跃度较高，主要精力集中在 **v2→v3 配置迁移 Bug 的快速响应**、**新渠道功能（DeltaChat）合并** 以及 **大量依赖例行更新** 上。  
- 24 小时内处理了 27 个 Pull Requests，其中 14 个已合并/关闭，13 个仍开放，合并率超过 50%。  
- 关键配置 Bug [#3206](https://github.com/sipeed/picoclaw/issues/3206) 在报告当日即收到贡献者修复 PR [#3218](https://github.com/sipeed/picoclaw/pull/3218)，社区响应敏捷。  
- 历时近一个月的 **DeltaChat 网关**（[#3063](https://github.com/sipeed/picoclaw/pull/3063)）今日正式合并，项目渠道生态进一步扩展。  
- 安全加固方面合并了跨站请求防护 ([#3160](https://github.com/sipeed/picoclaw/pull/3160)) 和白名单绕过修复 ([#3161](https://github.com/sipeed/picoclaw/pull/3161))，稳定性得到提升。  
- 自动化依赖更新（dependabot）仍占 PR 多数，但维护者能及时批量合并，依赖健康度保持良好。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

### 🎉 新功能合并
- **DeltaChat 网关**（

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

# QwenPaw 项目动态日报（2026-07-03）

## 今日速览

过去 24 小时项目极高度活跃：共处理 16 条 Issue 更新（新开/活跃 12 条，关闭 4 条）、54 条 PR 更新（待合并 29 条，已合并/关闭 25 条），并发布一个预发布版本。社区提交集中在 v2.0.0 beta 系列的功能增强与稳定性修复，同时 v1.1.x 用户持续反馈内存泄漏、上下文错乱等关键问题。整体上项目迭代节奏紧凑，但 `scroll` 上下文压缩误折叠、Agent 挂起等严重 Bug 仍在修复中，生产环境仍需谨慎。

## 版本发布

### v2.0.0-beta.2

- 发布链接：https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0-beta.2
- 类型：Beta 预发布，早期开发版本，**不推荐生产使用**
- 新增内容：
  - `feat(cli): add cron up` —— CLI 新增 cron 相关命令
    （注：Release 正文仅显示该行，更多变更内容未完全列出）
- ⚠️ 破坏性变更与迁移注意：该版本仍处于快速迭代期，API 与配置可能发生变动。Beta 用户需留意 changelog 并及时更新配置。
- 紧随其后，昨日报中已提交版本号提升至 v2.0.0b3 的 PR（#5760），表明团队正向下一个迭代前进。

## 项目进展

### 合并/关闭的重要 PR

- **#5760 – chore(version): bump version to 2.0.0b3**  
  将版本号升级至 v2.0.0b3，为下一轮 CI/CD 做准备。  
  https://github.com/agentscope-ai/QwenPaw/pull/5760

- **#5287 – fix(context): don't crash compaction when summary exceeds schema maxLength**（已关闭）  
  修复上下文压缩时总结字段超长导致 schema 校验崩溃的问题。  
  https://github.com/agentscope-ai/QwenPaw/pull/5287

- **#5533 – Avoid treating content safety image errors as media capability failures**（已关闭）  
  修复内容安全审核错误被误判为模型媒体能力不足而进入 fallback 路径的问题。  
  https://github.com/agentscope-ai/QwenPaw/pull/5533

### 关键合并的 Issue（非 PR 但反映修复落地）

- **#5403 – [BUG] Browser autofill hijacks search input**（已关闭）  
  模型配置页面搜索框被浏览器误认为是密码字段的问题已解决。  
  https://github.com/agentscope-ai/QwenPaw/issues/5403

- **#5709 – [Bug]: 飞书通道硬丢弃 Bot 消息**（已关闭）  
  飞书通道不再错误丢弃 `sender_type="bot"` 的 @ 消息。  
  https://github.com/agentscope-ai/QwenPaw/issues/5709

### 今日提交但尚未合并的重要 PR

- **#5749 – fix(channel): add consumer timeout and typing auto-stop to prevent agent hang**  
  解决 Agent 因工具调用异常挂死问题，涉及消费者超时与 typing 指示器自动停止。  
  https://github.com/agentscope-ai/QwenPaw/pull/5749

- **#5747 – Protect active turn from scroll context eviction**  
  避免 `scroll` 上下文压缩误将当前进行中的任务折叠，导致模型回复陈旧消息。  
  https://github.com/agentscope-ai/QwenPaw/pull/5747

- **#5741 – feat(config,agents): env var resolution for config + dialog log sanitization**  
  实现配置文件中环境变量占位符 `${ENV_VAR}` 解析，dialog 日志脱敏（回应 #5705）。  
  https://github.com/agentscope-ai/QwenPaw/pull/5741

- **#5745 – fix(security): redact secrets in persisted dialog artifacts**  
  对持久化对话文件（`dialog/*.jsonl`、`/dump_history` 导出等）中的密钥令牌进行脱敏。  
  https://github.com/agentscope-ai/QwenPaw/pull/5745

- **#5726 – feat(agents): implement vision fallback for text-only models**  
  当模型不支持视觉时自动调用视觉模型生成图片描述并注入对话（针对 #5615）。  
  https://github.com/agentscope-ai/QwenPaw/pull/5726

- **#5597 – feat(backend): per-agent and global LLM model fallback with safe retry boundaries**  
  为 LLM 调用添加模型 fallback 支持，在重试耗尽后可自动切换至备用模型。  
  https://github.com/agentscope-ai/QwenPaw/pull/5597

- **#5637 – feat(subagent): add event-driven background lifecycle and parent wakeup**  
  将后台子智能体从轮询改为事件驱动，支持心跳检测与父取消。  
  https://github.com/agentscope-ai/QwenPaw/pull/5637

整体推进态势：v2.0.0 新功能（视觉 fallback、模型 fallback、子智能体事件化、Tauri 桌面端）与安全加固（密钥脱敏、环境变量注入）同步进行，同时社区贡献者积极修复稳定性 Bug。

## 社区热点

| 议题 | 评论数 | 标签 | 关注点 |
|------|--------|------|--------|
| **#5403** Browser autofill hijacks search input | 7 | bug（已关闭） | 用户反映浏览器自动填充干扰模型配置页面，最终得到修复 |
| **#5705** 密钥脱敏与安全存储 | 6 | enhancement | 社区系统评估了现有密钥安全机制，指出覆盖率与日志脱敏缺失，已有 PR #5741 跟进 |
|

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*