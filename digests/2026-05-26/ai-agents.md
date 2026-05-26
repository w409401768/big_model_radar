# OpenClaw 生态日报 2026-05-26

> Issues: 478 | PRs: 500 | 覆盖项目: 12 个 | 生成时间: 2026-05-26 01:52 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyclaw)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [EasyClaw](https://github.com/gaoyangz77/easyclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报（2026-05-26）

---

## 1. 今日速览

OpenClaw 社区在 2026-05-26 继续保持高活跃度，过去24小时内共处理 **478 条 Issues**（新开/活跃 196，关闭 282）和 **500 条 PR**（待合并 274，已合并/关闭 226），显示出高效的协作节奏与问题响应能力。尽管无新版本发布，但核心团队正集中修复关键稳定性问题，尤其在会话状态管理、网关资源泄漏和跨平台兼容性方面取得显著进展。多个高优先级 P1 Bug 已关联修复 PR 并进入验证阶段，项目整体健康度良好。

---

## 2. 版本发布

**无新版本发布**。当前开发重点集中于修复 2026.5.x 系列中的回归问题，为后续稳定版做准备。

---

## 3. 项目进展

今日多个关键修复被合并或进入待审状态，推动核心稳定性提升：

- **会话锁泄漏修复**：PR [#86427](https://github.com/openclaw/openclaw/pull/86427) 确保嵌入式代理运行退出时释放会话文件锁，解决 `#85953` 中因锁未释放导致的子代理回调超时问题。
- **网关文件描述符泄漏修复**：PR [#86701](https://github.com/openclaw/openclaw/pull/86701) 针对 `#86613` 报告的问题，优化 `memory_search` 工具对 `.md` 文件的监听机制，避免单次调用打开上万只读 FD。
- **Discord 消息投递加固**：PR [#86716](https://github.com/openclaw/openclaw/pull/86716) 增强 Discord 回复投递的会计逻辑，防止过期交互被误计为成功投递。
- **iMessage 历史记录支持**：PR [#86706](https://github.com/openclaw/openclaw/pull/86706) 引入可选的 DM 历史种子功能，改善新会话上下文连续性。

此外，ClawSweeper 自动化流程成功合并多个小型修复（如 [#86714](https://github.com/openclaw/openclaw/pull/86714)、[#86712](https>//github.com/openclaw/openclaw/pull/86712)），体现自动化测试与合并机制的有效性。

---

## 4. 社区热点

以下 Issues 引发高度关注，反映用户核心痛点：

- **[#86613](https://github.com/openclaw/openclaw/issues/86613)**（6 评论）：网关因 `memory_search` 工具积累超 12K 文件描述符，已被复现并关联修复 PR。
- **[#86599](https://github.com/openclaw/openclaw/issues/86599)**（7 评论）：Windows 测试版用户报告本地模型调用阻塞事件循环，单次推理耗时约 4 分钟，标记为 **Beta 发布 blocker**。
- **[#85251](https://github.com/openclaw/openclaw/issues/85251)**（5 评论）：Codex 应用服务器发出 `turn/started` 通知后静默，导致会话卡死直至强制恢复，影响用户体验。
- **[#83184](https://github.com/openclaw/openclaw/issues/83184)**（4 评论）：心跳驱动回复遗留 `pendingFinalDelivery` 状态，阻塞后续心跳，已由 PR [#86427] 部分解决。

这些讨论凸显用户对 **可靠性、资源管理与跨平台一致性** 的强烈诉求。

---

## 5. Bug 与稳定性

按严重程度排序的关键 Bug：

| 严重等级 | Issue | 描述 | 修复状态 |
|--------|------|------|--------|
| 🦞 Diamond Lobster (P1) | [#86613](https://github.com/openclaw/openclaw/issues/86613) | 网关 FD 泄漏，单次 `memory_search` 调用打开 >12K 文件句柄 | ✅ 修复中（PR [#86701](https://github.com/openclaw/openclaw/pull/86701)） |
| 🦞 Diamond Lobster (P1) | [#86599](https://github.com/openclaw/openclaw/issues/86599) | Windows 本地模型调用阻塞事件循环，推理延迟 ~4 分钟 | 🔄 调查中（需更多日志） |
| 🦞 Diamond Lobster (P1) | [#85251](https://github.com/openclaw/openclaw/issues/85251) | Codex 应用服务器静默导致会话卡死 | 🔄 需进一步诊断 |
| 🦐 Gold Shrimp (P1) | [#84038](https://github.com/openclaw/openclaw/issues/84038) | `doctor --fix` 错误迁移 OpenAI-Codex 配置，导致 token 消耗暴增 3–4 倍 | 🔄 需产品决策 |
| 🐚 Platinum Hermit (P1) | [#85953](https://github.com/openclaw/openclaw/issues/85953) | `sessions_yield` 后父会话锁未释放，子代理回调失败 | ✅ 已修复（PR [#86427](https://github.com/openclaw/openclaw/pull/86427)） |

> 注：多个 P1 问题已关联 `clawsweeper:fix-shape-clear` 标签，表明修复方案清晰且可执行。

---

## 6. 功能请求与路线图信号

用户提出的功能需求中，以下具备较高落地可能性：

- **Channel Broker 架构推进**：PR [#86165](https://github.com/openclaw/openclaw/pull/86165)（XL 规模）试图统一多通道（Telegram/Discord/iMessage 等）的维护逻辑，减少重复回归。若通过审查，将显著降低长期维护成本。
- **结构化 Provider 错误描述**：PR [#86642](https://github.com/openclaw/openclaw/pull/86642) 引入 `ProviderErrorDescriptor`，允许插件标准化错误分类，提升调试体验，已进入待审状态。
- **Xiaomi MiMo Token 支持**：Issue [#86169](https://github.com/openclaw/openclaw/issues/86169) 请求官方支持小米令牌计划，反映亚洲市场集成需求，但需验证 API 稳定性。

此外，**Direct Exec Mode for Cron Jobs**（[#18160](https://github.com/openclaw/openclaw/issues/18160)）持续获得点赞，表明用户对绕过 LLM 解释、直接执行简单命令有强烈需求，可能纳入下一版本优化。

---

## 7. 用户反馈摘要

从 Issues 评论提炼的真实声音：

- **痛点**：
  - “Telegram 消息无声丢失，日志里根本没有 `sendMessage` 调用”（[#80520](https://github.com/openclaw/openclaw/issues/80520)）
  - “Windows 上跑个 `hi, how are you` 要等 4 分钟，完全不可用”（[#86599](https://github.com/openclaw/openclaw/issues/86599)）
  - “dashboard 里每条消息都重复显示，全是 `delivery-mirror` 惹的祸”（[#85669](https://github.com/openclaw/openclaw/issues/85669)）

- **满意点**：
  - 对 ClawSweeper 自动化修复流程表示认可（如 [#86714](https://github.com/openclaw/openclaw/pull/86714) 被赞“高效”）
  - 赞赏 iMessage 自动确认功能提案（[#10737](https://github.com/openclaw/openclaw/issues/10737) 虽关闭但仍获讨论）

- **使用场景**：
  - 企业用户依赖 cron 任务进行邮件/日历同步，对超时敏感（[#14747](https://github.com/openclaw/openclaw/issues/14747)）
  - 多通道运营者（如同时使用 Discord + Telegram）遭遇消息路由混乱（[#51947](https://github.com/openclaw/openclaw/issues/51947)）

---

## 8. 待处理积压

以下重要 Issue 长期未获响应，建议维护者优先关注：

- **[#77340](https://github.com/openclaw/openclaw/issues/77340)**（自 2026-05-04 起）：稳态聊天流量下 deferred turn-maintenance 发生 livelock，导致 assistant 消息单调累积，影响会话一致性。
- **[#60858](https://github.com/openclaw/openclaw/issues/60858)**（自 2026-04-04 起）：三个 `hasRealConversationContent` 守卫静默阻止 compaction，致使 `session.messages` 为空，上下文无法更新。
- **[#44925](https://github.com/openclaw/openclaw/issues/44925)**（自 2026-03-13 起）：子代理完成结果静默丢失，无重试/通知/自动重启，标记为 P1 但长期未分配。

这些积压问题涉及核心会话生命周期管理，若不解决可能引发更广泛的可靠性危机。

--- 

**报告生成时间**：2026-05-26 UTC  
**数据来源**：OpenClaw GitHub Repository (github.com/openclaw/openclaw)

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告  
**报告时间：2026-05-26 UTC**

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态呈现 **高活跃度、强分化、安全优先** 的整体态势。核心项目如 OpenClaw、NanoBot、Zeroclaw 等均处于快速迭代期，日均处理 PR 超 50 条，反映出开发者对多智能体协作、工具调用安全、跨平台兼容性的高度关注。生态整体从“功能可用”向“生产可靠”演进，安全加固（如沙箱隔离、权限控制）、长期记忆、流式交互成为共性诉求。同时，项目间生态融合趋势初现，如 LobsterAI 已实现与 OpenClaw 的插件/技能自动同步。

---

## 2. 各项目活跃度对比

| 项目名称     | Issues（24h） | PR（24h） | 新版本发布 | 健康度评估 | 备注 |
|--------------|---------------|-----------|------------|------------|------|
| **OpenClaw** | 478           | 500       | ❌         | ⭐⭐⭐⭐☆     | 高负载修复关键稳定性问题 |
| **NanoBot**  | 6             | 118       | ❌         | ⭐⭐⭐⭐☆     | 多智能体架构深化 |
| **Zeroclaw** | 27            | 50        | ❌         | ⭐⭐⭐⭐      | 安全加固与插件化推进 |
| **PicoClaw** | 10            | 8         | ✅ nightly | ⭐⭐⭐        | 模型兼容性修复中 |
| **NanoClaw** | 4             | 15        | ❌         | ⭐⭐⭐⭐      | Slack 多工作区需求积压 |
| **IronClaw** | 19            | 50        | ❌         | ⭐⭐⭐⭐      | attested-signing 安全子系统落地 |
| **LobsterAI**| 1             | 29        | ❌         | ⭐⭐⭐⭐☆     | OpenClaw 集成完成 |
| **Moltis**   | 5             | 6         | ✅ v20260525.01 | ⭐⭐⭐⭐☆ | 安全修复+非阻塞代理 |
| **CoPaw**    | 43            | 43        | ✅ v1.1.9-beta.1 | ⭐⭐⭐⭐ | UI 实时性问题待解 |
| **EasyClaw** | 0             | 0         | ✅ v1.8.15 | ⭐⭐⭐⭐☆     | 客服会话管理优化 |
| **TinyClaw** | 0             | 0         | ❌         | ⭐⭐         | 无活动 |
| **ZeptoClaw**| 0             | 0         | ❌         | ⭐⭐         | 无活动 |

> 注：健康度基于活跃度、响应速度、技术债、用户反馈综合评估（5星制）

---

## 3. OpenClaw 在生态中的定位

OpenClaw 是生态中 **规模最大、协作最密集的核心基础设施级项目**，其优势体现在：
- **社区规模**：单日处理 478 Issues + 500 PR，远超同类（次高为 CoPaw 的 43+43），反映其作为“事实标准”的采纳广度；
- **技术路线**：坚持“会话即状态机”设计，强调跨平台一致性（Windows/macOS/Linux）、资源泄漏防护与网关稳定性，与 NanoBot 的“轻量 AgentLoop”或 Zeroclaw 的“Everything is a Plugin”形成差异化；
- **生态辐射力**：LobsterAI、Moltis 等项目主动集成其插件/技能体系，形成事实上的扩展标准。

---

## 4. 共同关注的技术方向

| 技术方向               | 涉及项目                          | 具体诉求 |
|------------------------|-----------------------------------|----------|
| **工具调用安全防护**   | Zeroclaw、IronClaw、Moltis        | 强制 allowed/denied tools 校验、防绕过审计（#6920、#4021、#1071） |
| **长期记忆与会话连续性** | LobsterAI、CoPaw、OpenClaw        | 跨 session 历史感知、消息压缩导致上下文丢失（#2046、#4652、#85251） |
| **流式交互体验**       | PicoClaw、NanoClaw、CoPaw         | 实时 token 输出、避免 UI 刷屏（#2853、#2618、#4644） |
| **多通道会话隔离**     | NanoClaw、CoPaw、IronClaw         | 定时任务不被用户消息中断、Discord/Telegram 路由混乱（#4653、#51947、#4030） |
| **模型兼容性适配**     | PicoClaw、Zeroclaw、OpenClaw      | DeepSeek-V4 thinking mode、Claude 参数格式、GLM-5 错误码处理 |

---

## 5. 差异化定位分析

| 项目       | 功能侧重                     | 目标用户               | 技术架构关键差异 |
|------------|------------------------------|------------------------|------------------|
| **OpenClaw** | 企业级多通道网关稳定性       | 中大型团队、运维敏感场景 | 会话状态机 + 资源泄漏防护 |
| **NanoBot**  | 多智能体协同与轻量执行       | 开发者、研究型用户     | AgentLoop 驱动 + 内存单阶段重构 |
| **Zeroclaw** | 安全优先的插件化架构         | 金融/合规场景          | “Everything is a Plugin” + MCP 工具强制鉴权 |
| **LobsterAI**| OpenClaw 生态前端与记忆增强  | 个人用户、知识工作者   | 浏览器 IndexedDB + 子代理树形管理 |
| **Moltis**   | 抗漂移代理路由与异步任务编排 | 复杂工作流用户         | Per-turn tool_choice + 非阻塞 spawn_agent |
| **EasyClaw** | 客服工单与会话生命周期管理   | 企业客服团队           | 显式会话结束 + 工单快照同步 |

---

## 6. 社区热度与成熟度

- **快速迭代层**（日均 PR > 30）：  
  **OpenClaw、NanoBot、IronClaw、CoPaw** 处于功能爆发期，聚焦架构重构与核心能力补全，适合早期采用者。
  
- **质量巩固层**（PR 少但 Release 频繁）：  
  **Moltis、EasyClaw、LobsterAI** 更注重稳定性与用户体验，适合生产环境部署。

- **边缘/休眠层**：  
  TinyClaw、ZeptoClaw 无活动，PicoClaw 虽发 nightly 但修复缓慢，存在用户流失风险。

---

## 7. 值得关注的趋势信号

1. **安全可观测性成为刚需**：Landlock 调试日志（Moltis #868）、工具调用审计（IronClaw #4021）等需求表明，开发者不再满足于“黑盒安全”，要求内核级事件可见。
2. **记忆系统从存储转向智能**：用户明确反对“信息堆砌”（CoPaw #4652），呼吁“总结-关联-提醒”机制，预示 RAG 将向主动认知演进。
3. **流式架构统一化**：PicoClaw、NanoClaw、CoPaw 同时推进 ChatStream 支持，反映低延迟交互已成体验底线。
4. **生态互操作加速**：LobsterAI 自动同步 OpenClaw 技能，标志开源 AI 助手进入“插件联邦”时代，开发者应优先兼容主流扩展协议（如 MCP）。

> **对开发者的建议**：在实现功能创新的同时，务必投入资源构建 **可观测性基础设施** 与 **跨会话状态管理**，这两者将成为下一阶段产品差异化的关键。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报（2026-05-26）

---

## 1. 今日速览

NanoBot 在过去24小时内表现出极高的开发活跃度，共处理 **118 条 Pull Requests** 和 **6 条 Issues**，其中 PR 合并/关闭率达 **8.5%**（10/118），Issue 关闭率达 **50%**（3/6）。尽管无新版本发布，但核心功能持续演进，重点集中在 **多智能体协作、工具调用稳定性、第三方服务集成（如 StepFun、Kagi）以及终端体验优化**。项目整体处于快速迭代与架构深化阶段，社区贡献者活跃，技术债逐步清理。

---

## 2. 版本发布

**无新版本发布**。  
当前主干分支仍在集成多项关键功能（如 AgentLoop 重构、跨智能体通信），预计下一版本将包含重大架构改进。

---

## 3. 项目进展

今日共 **10 个 PR 被合并或关闭**，推动多个核心模块演进：

- **🔧 多智能体系统增强**  
  - [`#3992`](https://github.com/HKUDS/nanobot/pull/3992)：实现跨智能体实例的消息总线，支持分布式协作（已开放，测试完成）。  
  - [`#3978`](https://github.com/HKUDS/nanobot/pull/3978)：修复子智能体并发数配置未生效问题，提升多任务调度能力（已合并）。

- **🛠️ 工具调用与循环防护机制**  
  - [`#3985`](https://github.com/HKUDS/nanobot/pull/3985)（已关闭，标记为 invalid）：提出“循环检测 v2.0”硬阻断机制，虽未合并但引发对通用工具循环防护的讨论，相关逻辑可能影响后续设计。  
  - [`#3999`](https://github.com/HKUDS/nanobot/pull/3999)：修复 AgentRunner 在持续目标活跃时提前退出的问题，保障长任务稳定性（已合并）。

- **🌐 第三方服务集成扩展**  
  - [`#3988`](https://github.com/HKUDS/nanobot/pull/3988)：新增 StepFun Step Plan 专用 Provider，解决其 API 路径不兼容问题（已合并）。  
  - [`#3867`](https://github.com/HKUDS/nanobot/pull/3867)：修复 OpenRouter 网关下 MiMo 模型无法禁用思考模式的问题（已合并）。

- **📚 文档与开发者体验优化**  
  - [`#3850`](https://github.com/HKUDS/nanobot/pull/3850)：修正贡献指南中 `ruff format` 命令误导问题，避免新贡献者提交无关格式化变更（已合并）。  
  - [`#3866`](https://github.com/HKUDS/nanobot/pull/3866)：扩展配置文件 secrets 示例，提升配置可读性（已合并）。

> 项目整体向 **更稳定、可扩展、多平台兼容** 的方向迈进，尤其在 Agent 生命周期管理与外部服务适配方面取得实质性进展。

---

## 4. 社区热点

### 🔥 高关注度 PR（评论数最多 / 提案新颖）

| PR | 主题 | 链接 | 分析 |
|----|------|------|------|
| **#4005** | GitAgent Protocol (GAP) 支持 | [链接](https://github.com/HKUDS/nanobot/pull/4005) | 提出引入轻量级 AI 代理标准协议（`agent.yaml` + `SOUL.md`），旨在提升 nanobot 的可发现性与可移植性。虽标记为 `invalid`，但反映了社区对 **标准化代理描述格式** 的强烈兴趣，可能成为未来生态集成方向。 |
| **#3990** | Dream 单阶段内存重构 | [链接](https://github.com/HKUDS/nanobot/pull/3990) | 将 Dream 的两阶段分析合并为单阶段 AgentLoop 驱动流程，引入目标状态生命周期管理。这是对核心记忆系统的重大重构，显著提升执行效率与一致性，获核心维护者积极 review。 |
| **#3992** | 跨智能体消息总线 | [链接](https://github.com/HKUDS/nanobot/pull/3992) | 实现多 nanobot 实例间通信机制，为构建分布式 AI 工作流奠定基础。技术实现完整，已自测通过，是迈向“AI 协作网络”的关键一步。 |

> 社区正从单一智能体向 **多智能体协同架构** 演进，标准化与互操作性成为新焦点。

---

## 5. Bug 与稳定性

| Issue | 严重程度 | 描述 | 状态 | 修复 PR |
|-------|----------|------|------|--------|
| **#3469** | 高 | DeepSeek-v4 在多轮思考时因 `reasoning_content` 未正确返回导致 API 错误 | ✅ 已关闭 | 无显式 PR，可能由 provider 层通用修复覆盖 |
| **#3995** | 中 | PowerShell 中流式输出异常换行，导致终端刷屏 | ✅ 已关闭 | 无显式 PR，推测为渲染逻辑热修复 |
| **#3999**（原问题） | 高 | AgentRunner 在 sustained goal 活跃时错误退出 | ✅ 已修复 | [`#3999`](https://github.com/HKUDS/nanobot/pull/3999)（已合并） |

> 当前无未修复高危 Bug，终端渲染与长任务稳定性问题已闭环。

---

## 6. 功能请求与路线图信号

| Issue | 类型 | 潜在路线图影响 | 关联 PR |
|-------|------|----------------|--------|
| **#4000** | 新增 StepFun ASR 支持 | 高 | 用户无法使用 Step Plan 内置转录功能，[`#3988`](https://github.com/HKUDS/nanobot/pull/3988) 已部分解决 provider 层问题，ASR 可能为下一优先级 |
| **#3958** | Weather Skill 示例化 | 中 | 提议将天气技能移出内置，转为示例，体现“lean and mean”设计哲学，可能影响技能架构 |
| **#3993** | Anthropic content block 类型强制校验 | 中 | 需确保所有工具输出符合 Anthropic 格式要求，[`#3993`](https://github.com/HKUDS/nanobot/issues/3993) 提出 coerce 方案，预计将纳入 provider 层统一处理 |

> **StepFun 生态集成** 和 **Anthropic 兼容性** 将成为近期重点，Weather Skill 重构可能引导技能模块化方向。

---

## 7. 用户反馈摘要

- **痛点**：  
  - PowerShell 用户遭遇流式输出刷屏（#3995），影响终端使用体验。  
  - Step Plan 用户无法使用内置语音转录（#4000），因 API 路径不兼容。  
  - 模型频繁陷入工具调用循环（#3986），浪费 token 且无自动恢复。

- **满意点**：  
  - 多 provider 支持灵活（如 OpenRouter、StepFun），用户可自由切换模型。  
  - 轻量级设计受开发者欢迎（#2155 提及“资源消耗非常小”）。

- **使用场景**：  
  - QQ 频道、Telegram 等 IM 平台集成（#3996 新增 webhook 模式）。  
  - 本地 TUI 终端交互（#2155 持续开发中）。

---

## 8. 待处理积压

| Issue/PR | 类型 | 创建时间 | 状态 | 提醒 |
|----------|------|----------|------|------|
| **#1443** | PR | 2026-03-02 | OPEN | 心跳代理推理与通知解耦，涉及核心通信逻辑，需维护者评估是否纳入默认行为 |
| **#2155** | PR | 2026-03-17 | OPEN | TUI 终端交互功能，用户呼声高，但长期未合并，建议明确 roadmap 定位 |
| **#2271** | PR | 2026-03-19 | OPEN | 工具调用循环检测基础实现，与 #3985 形成互补，可考虑整合进主线防护体系 |

> 建议维护团队对 **TUI 支持** 和 **循环检测机制标准化** 做出明确决策，避免功能碎片化。

---

**项目健康度评估**：⭐⭐⭐⭐☆（4.5/5）  
高活跃度、快速响应、架构持续优化，社区驱动特征明显，具备成为主流开源 AI 助手框架的潜力。

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报（2026-05-26）

---

## 1. 今日速览

Zeroclaw 项目在过去24小时内保持高活跃度，共产生 **27条 Issues 更新**（新开/活跃20条，关闭7条）和 **50条 PR 更新**（待合并35条，已合并/关闭15条），显示出社区贡献与核心团队维护的双重活跃。尽管无新版本发布，但多个高优先级 Bug 修复与安全增强 PR 正在推进，尤其在 **AI 提供商兼容性、沙箱安全、工具权限控制**等关键领域取得实质性进展。项目整体处于快速迭代与架构演进阶段，技术债务清理与功能扩展并行。

---

## 2. 版本发布

**无新版本发布**。当前主干（`master`）仍在为 v0.7.6 版本做准备，重点聚焦于技能系统 UX 改进与安全性加固。

---

## 3. 项目进展

今日有 **15个 PR 被合并或关闭**，其中多项涉及核心架构改进：

- **安全加固**：  
  - [`#6942`](https://github.com/zeroclaw-labs/zeroclaw/pull/6942) 移除了 Canvas iframe 的 `allow-same-origin`，防止 XSS 导致 token 泄露（响应 GHSA-f385-f6h2-3gqj），显著提升 Web 前端安全性。  
  - [`#6920`](https://github.com/zeroclaw-labs/zeroclaw/pull/6920) 实现了 MCP 工具在执行时强制校验 `allowed_tools/denied_tools`，补全了此前仅过滤列表但未拦截调用的安全缺口。

- **运行时与网关增强**：  
  - [`#6933`](https://github.com/zeroclaw-labs/zeroclaw/pull/6933) 支持 WebSocket 会话持久化完整对话转录，解决断连后上下文丢失问题，提升长会话稳定性。  
  - [`#6908`](https://github.com/zeroclaw-labs/zeroclaw/pull/6908) 修复 OpenAI 配置中 Codex OAuth 订阅认证无法使用的问题，使非 API Key 用户可正常接入。

- **配置与兼容性修复**：  
  - [`#6913`](https://github.com/zeroclaw-labs/zeroclaw/pull/6913) 统一策略测试中的路径处理逻辑，支持 Windows 绝对路径（如 `C:\...`），避免跨平台构建失败。  
  - [`#6935`](https://github.com/zeroclaw-labs/zeroclaw/pull/6935) 恢复 `RouterModelProvider::stream_chat_with_system` 方法，修复系统提示流在路由场景下的中断问题。

> 整体来看，项目在 **安全、稳定性、多平台兼容性** 方面迈出关键步伐，为后续插件化架构（见下文）打下基础。

---

## 4. 社区热点

以下 Issues/PRs 引发最多讨论与关注：

- **[#6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059)**（12 评论，👍4）：  
  DeepSeek-V4 API 格式不兼容导致调用失败，涉及“thinking mode”参数序列化问题。用户反馈强烈，维护者已标记为 `in-progress`，需紧急适配。

- **[#6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489)**（1 评论）：  
  提出“Everything is a plugin”长期架构愿景，主张将 Integrations 与 Plugins 统一为单一插件目录。该提案获 `accepted` 状态，预示未来版本将进行重大架构重组。

- **[#6914](https://github.com/zeroclaw-labs/zeroclaw/issues/6914)**（1 评论）：  
  要求在主代理循环中强制执行 `allowed_tools/denied_tools`，虽已有 PR #6920 部分实现，但此 Issue 强调需覆盖所有代码路径，凸显社区对最小权限原则的高度关注。

> 社区核心诉求集中于：**AI 提供商兼容性扩展、细粒度工具权限控制、架构统一性**。

---

## 5. Bug 与稳定性

按严重程度排序的高危问题：

| 严重性 | Issue | 描述 | 修复状态 |
|--------|------|------|--------|
| **S1** | [#5636](https://github.com/zeroclaw-labs/zeroclaw/issues/5636) | `zai-cn` 提供商调用 `glm-5-turbo` 时因上下文预修剪返回 1214 错误 | ❌ 无 PR |
| **S2** | [#6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) | DeepSeek-V4 API 格式不兼容（thinking mode） | 🔄 `in-progress` |
| **S2** | [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) | Gemini 模型因历史序列化违反“首个非系统轮次不能是 assistant”而报 400 | 🔄 `in-progress` |
| **S2** | [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) | `web_fetch` 的 `allowed_private_hosts` 对解析到私有 IP 的域名无效 | ❌ 无 PR |
| **S2** | [#6923](https://github.com/zeroclaw-labs/zeroclaw/issues/6923) | OpenAI Codex OAuth 成功后仍回退到 `OPENAI_API_KEY` | ✅ 已有 PR #6938 |

> 注：S1=功能完全失效，S2=功能降级。

---

## 6. 功能请求与路线图信号

以下功能请求已获 `accepted` 或进入开发阶段，极可能纳入 **v0.7.6 或 v0.8.0**：

- **技能系统增强**：  
  - [#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253) 作为 v0.7.6 主题，协调 CLI、沙箱、测试工具链等技能支持改进。  
  - [#6924](https://github.com/zeroclaw-labs/zeroclaw/pull/6924) 引入 `builtin`/`composio` 工具类型，支持技能临时提权，是权限模型关键演进。

- **计算机使用（Computer-Use）能力**：  
  - [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) 提议添加屏幕截图、鼠标键盘控制功能，对标 OpenAI Codex，已获 `accepted`。

- **插件化架构统一**：  
  - [#6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489) 推动 Integrations → Plugins 统一，长期将简化扩展机制。

- **新提供商支持**：  
  - [#6456](https://github.com/zeroclaw-labs/zeroclaw/issues/6456) 请求集成 Arcee AI（专注小模型），反映用户对轻量化模型的需求上升。

---

## 7. 用户反馈摘要

从 Issues 评论提炼真实用户声音：

- **痛点**：  
  - “DeepSeek-V4 完全无法使用，官方文档没提 thinking mode 要特殊处理”（#6059）  
  - “Windows 下 `setup.bat --minimal` 构建体积是宣称的 4 倍，浪费磁盘和 CI 时间”（#6836）  
  - “Telegram 图片消息会卡在 precheck 阶段，只能重启”（#6912）

- **满意点**：  
  - “Codex OAuth 终于能用了！不用再硬编码 API Key”（#6908 相关讨论）  
  - “技能临时提权设计很巧妙，既安全又灵活”（#6924 评论）

- **使用场景**：  
  - 金融合规场景（如 InvestorClaw）依赖沙箱隔离与工具审计（#5722）  
  - 企业部署关注浏览器兼容性（#6921）与 Nix 支持（#6906）

---

## 8. 待处理积压

以下重要 Issue/PR 长期未响应，建议维护者优先处理：

- **[#4710](https://github.com/zeroclaw-labs/zeroclaw/issues/4710)**（2026-03-25 创建，10 评论）：  
  请求设计新 Logo，虽为低风险，但影响品牌形象，且社区已有投稿，可快速闭环。

- **[#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)**（2026-04-24 创建）：  
  审计 153 个被误 revert 的提交，涉及 bug 修复与功能丢失，需制定恢复计划。

- **[#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122)**（2026-03-29 创建）：  
  `web_fetch` 私有主机白名单失效，属安全相关缺陷，至今无修复 PR。

> 建议：对 #6074 启动专项恢复审计，对 #5122 分配安全团队评估。

--- 

**报告生成时间**：2026-05-26  
**数据来源**：GitHub Zeroclaw 仓库公开数据

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报（2026-05-26）

---

## 1. 今日速览

PicoClaw 项目在过去24小时内保持较高活跃度，共产生 **10条 Issues 更新** 和 **8条 PR 更新**，并发布了一个 nightly 构建版本。社区对 Anthropic 模型配置错误、路径安全校验逻辑缺陷及历史消息显示异常等问题反馈集中，反映出用户对生产环境稳定性和多端兼容性的高度关注。尽管无 PR 被合并，但多个关键修复（如 PID 校验、Claude 模型参数适配）已进入代码审查阶段，项目整体处于“问题暴露—修复推进”的健康迭代周期。

---

## 2. 版本发布

✅ **Nightly Build v0.2.9-nightly.20260526.ab6d3946 已发布**  
此为自动化构建版本，可能包含不稳定变更，建议仅用于测试。  
**主要变更范围**：涵盖近期未合并 PR 中的功能增强与 bug 修复，包括但不限于：
- 新增 Server酱³ Bot 渠道支持（#2893）
- 修复 macOS 下符号链接导致的路径验证失败（#2890）
- 优化技能目录 token 使用效率（#2781）

> ⚠️ **注意**：该 nightly 版本尚未经过完整回归测试，生产环境慎用。  
🔗 [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

---

## 3. 项目进展

今日 **无 PR 被合并或关闭**，但以下重要修复已进入最终审查阶段，预示下一版本将显著提升稳定性：

- **#2813**：修复 PID 文件检查逻辑，防止因系统重用 PID 导致网关启动崩溃（对应 Issue #2720，高优先级）  
- **#2942**：修正默认配置中 `claude-sonnet-4.6` 模型 ID 格式错误（使用点号而非 Anthropic 要求的连字符）  
- **#2940**：为 `claude-opus-4-7` 模型移除废弃的 `temperature` 参数，避免 API 返回 400 错误  

这些修复直接回应了用户在新安装或特定模型调用时的核心痛点，预计将在下一个稳定版中集成。

---

## 4. 社区热点

### 🔥 最活跃 Issue：#1042 — exec 工具 guardCommand 路径校验误报  
- **评论数**：14 | **👍**：2 | 最后更新：2026-05-25  
- **核心问题**：当 `restrict_to_workspace=true` 时，`guardCommand` 对非路径命令（如 `curl wttr.in/Beijing`）错误解析出相对路径 `../../../../Beijing?T`，触发安全拦截。  
- **用户诉求**：希望路径校验逻辑更智能，区分真实文件路径与 URL/参数中的字符串，避免误杀合法网络请求。  
🔗 [Issue #1042](https://github.com/sipeed/picoclaw/issues/1042)

> 💡 该问题影响天气查询等常见技能，暴露了安全机制与功能可用性之间的平衡难题，亟需重构正则匹配逻辑。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|--------|------|------|-------------|
| 🔴 高 | #2720 | 单例 PID 检查未验证进程身份， stale PID 导致启动崩溃循环 | ✅ #2813 |
| 🟠 中 | #2941 | 默认配置中 `claude-sonnet-4.6` 使用点号，Anthropic API 要求连字符 | ✅ #2942 |
| 🟠 中 | #2939 | `claude-opus-4-7` 模型拒绝 `temperature` 参数，返回 400 错误 | ✅ #2940 |
| 🟠 中 | #2796 | 历史对话中仅显示最后一条用户消息，其余丢失 | ❌ 无 |
| 🟡 低 | #2944 | Termux 环境下因 CA 证书路径未设置导致 HTTPS 失败 | ❌ 无（建议文档补充） |
| 🟡 低 | #2943 | 微信渠道发送图片触发智谱 GLM-5 API error 1210（参数错误） | ❌ 无 |

> 📌 高优先级崩溃问题已有修复方案，其余模型兼容性问题亦获响应，整体修复覆盖率达 50%。

---

## 6. 功能请求与路线图信号

### 高潜力功能（已有 PR 支持）：
- **#2853**：为 pico 通道添加 ChatStream 支持，实现实时 token 流式输出 → 满足用户对低延迟交互体验的需求  
- **#2696**：MCP 支持从通道上下文动态传递请求头 → 提升企业级集成灵活性  
- **#2893**：新增 Server酱³ Bot 渠道 → 扩展国内通知生态覆盖  

### 待评估需求：
- **#2404**：在配置中添加 `"streaming": true` 支持流式 HTTP 请求 → 与 #2853 形成互补，可能合并为统一流式架构  
- **#1950**（已关闭）：Web Chat 流式输出 → 虽标记为“Nice-to-Have”，但反映前端体验优化方向  

> ✅ 流式处理已成为明确技术趋势，多个相关 PR 表明团队正系统性构建实时交互能力。

---

## 7. 用户反馈摘要

- **痛点集中**：  
  - 新安装用户遭遇 **Anthropic 模型配置错误**（#2941），导致首次使用即失败，严重影响 onboarding 体验。  
  - **历史消息显示不全**（#2796）破坏对话连续性，用户质疑“消息压缩是否应作用于 UI 层”。  
  - **跨平台兼容性不足**：RISC-V .deb 包无法使用 OpenAI 模型（#2887）、Termux 证书问题（#2944）暴露对边缘环境支持薄弱。

- **满意点**：  
  - 社区对 **nightly 构建机制** 表示认可，便于快速验证修复。  
  - 开发者响应迅速，24 小时内即针对 Claude 模型问题提交修复 PR（#2940/#2942）。

---

## 8. 待处理积压

| 类型 | ID | 标题 | 积压时长 | 建议行动 |
|------|----|------|--------|--------|
| Issue | #2887 | .deb version on RISC-V is not functional with OpenAI model | 8 天 | 需确认是否为编译时依赖缺失或运行时兼容性问题 |
| Issue | #2796 | 历史记录中多次用户消息仅显示最后一条 | 19 天 | 高影响 UX 问题，建议优先排查消息序列化逻辑 |
| PR | #2893 | feat: add Server酱³ Bot channel support | 8 天 | 功能完整，建议 review 后合并以丰富渠道生态 |
| PR | #2853 | feat(pico): add ChatStream support | 15 天 | 核心体验升级，建议加速集成 |

> ⚠️ 维护者需重点关注 **#2796** 和 **#2887**，二者均涉及基础功能失效，可能影响用户留存。

---  
*数据截止：2026-05-26 23:59 UTC | 来源：GitHub API*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报（2026-05-26）

---

## 1. 今日速览

NanoClaw 社区活跃度显著回升，过去24小时内共产生 **19 条有效更新**（4 Issues + 15 PRs），其中 **12 个 PR 仍处于开放状态**，表明开发节奏紧凑且协作密集。尽管无新版本发布，但多个关键功能正在并行推进，包括 Slack 多工作区支持、健康探针恢复、线程上下文增强等。项目整体处于**高活跃开发期**，重点聚焦于 v2 架构的功能补全与稳定性修复。

---

## 2. 版本发布

**无新版本发布**。当前主干仍在持续集成中，未触发正式 Release。

---

## 3. 项目进展

今日有 **3 个 PR 被合并或关闭**，推动多项关键修复与功能落地：

- ✅ **#2526**（[链接](https://github.com/nanocoai/nanoclaw/pull/2526)）：修复了 `ncl groups delete` 因外键约束失败的问题，通过事务级联删除依赖行，解决了非空组的删除难题。
- ✅ **#2592**（[链接](https://github.com/nanocoai/nanoclaw/pull/2592)）：完善了 Teams CLI 的凭证自动发现路径文档，提升开发者集成体验。
- ✅ **#2612**（[链接](https://github.com/nanocoai/nanoclaw/pull/2612)）：新增 `debug-issue` 技能，支持端到端故障诊断与根因分析，增强平台可观测性。

此外，**#2610** 修复了 `ncl groups create` 后未初始化文件系统导致容器启动失败的问题，虽未合并但已进入审查尾声，预计将快速合入。

---

## 4. 社区热点

以下议题引发较高关注，反映核心用户诉求：

- 🔥 **#2404**（[链接](https://github.com/nanocoai/nanoclaw/issues/2404)）：**消息重复投递 Bug** —— 当 Agent 同时使用 `send_message` MCP 工具与 `<message>` 块时，消息被发送两次。该问题影响消息一致性，已有 3 条评论讨论根因（涉及子进程通信机制），亟待修复。
- 🔥 **#1804**（[链接](https://github.com/nanocoai/nanoclaw/issues/1804)）：**Slack 多工作区支持需求** —— 用户强烈呼吁支持单实例管理多个 Slack 工作区，避免重复部署。此需求已存在超 40 天，近期再次活跃，社区期待官方响应。
- 🔥 **#2506**（[链接](https://github.com/nanocoai/nanoclaw/issues/2506)）：**响应静默丢弃问题** —— 在 60 秒内完成多轮对话时，Agent 响应可能被去重逻辑误删，导致客户端超时。该 Bug 影响实时交互体验，严重性较高。

---

## 5. Bug 与稳定性

按严重程度排序如下：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|--------|------|------|-------------|
| ⚠️ **高** | #2506（[链接](https://github.com/nanocoai/nanoclaw/issues/2506)） | 响应在短时间内被静默丢弃，导致客户端超时 | ❌ 暂无 |
| ⚠️ **高** | #2404（[链接](https://github.com/nanocoai/nanoclaw/issues/2404)） | 消息双重投递，破坏一致性 | ❌ 暂无 |
| ⚠️ **中** | #2525（已关闭） | `ncl groups delete` 外键约束失败 | ✅ #2526 已修复 |
| ⚠️ **中** | #2610（[链接](https://github.com/nanocoai/nanoclaw/pull/2610)） | `groups create` 后未初始化文件系统 | ✅ PR 已提交，待合并 |

> 注：#2525 虽已关闭，但其修复 PR #2526 于今日合入，标志该问题闭环。

---

## 6. 功能请求与路线图信号

用户提出的新功能中，以下方向具备高优先级并被积极实现：

- **Slack 多工作区支持**（#1804）：虽无直接 PR，但 #2613（Socket Mode 支持）和 #2615（线程父消息获取）表明 Slack 适配器正被重构以支持更复杂场景，为多工作区铺路。
- **健康端点恢复**（#2619）：v1 的 `/health` 探针被重新引入，反映运维团队对生产可观测性的重视，可能成为下一版本标配。
- **多模态能力回归**（#2618）：图像、语音、PDF 支持及 `chat.onReaction` 被批量恢复，说明 v2 正补全 v1 缺失的核心交互能力，预计将纳入近期 Release。
- **CLI 上下文保持**（#2611）：安全审批后保留原始调用上下文，提升管理操作的安全性，属基础设施增强。

---

## 7. 用户反馈摘要

从 Issues 评论提炼真实用户声音：

- **痛点**：  
  > “我们无法在生产环境使用 `ncl groups delete`，任何有历史消息的组都会报错。” —— @glifocat（#2525）  
  > “两个 Slack 工作区必须跑两个实例，资源浪费严重。” —— @davekim917（#1804）

- **满意点**：  
  > “v2 的 MCP 架构比 v1 更清晰，工具调用更稳定。” —— 社区隐含反馈（基于 #2211 工具预览技能的高星标）

- **使用场景**：  
  企业用户普遍运行多租户 Agent 群组，依赖 CLI 批量管理；开发者关注 Slack/Teams 等主流通道的集成深度与稳定性。

---

## 8. 待处理积压

以下重要议题长期未获维护者响应，建议优先关注：

- ⏳ **#1804**（[链接](https://github.com/nanocoai/nanoclaw/issues/1804)）：Slack 多工作区支持（创建于 2026-04-16，超 40 天未响应）
- ⏳ **#2211**（[链接](https://github.com/nanocoai/nanoclaw/pull/2211)）：工具调用实时预览技能（PR 开放超 50 天，未 review）
- ⏳ **#2346**（[链接](https://github.com/nanocoai/nanoclaw/pull/2346)）：未知斜杠命令处理修复（PR 开放近 20 天）

> 建议维护团队对上述积压项进行 triage，避免社区贡献者积极性受损。

---  
**报告生成时间**：2026-05-26  
**数据来源**：GitHub NanoClaw 仓库公开数据

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报（2026-05-26）

---

## 1. 今日速览

IronClaw 项目在过去24小时内保持高度活跃，共产生 **19条 Issues 更新**（18条新开/活跃，1条关闭）和 **50条 PR 更新**（39条待合并，11条已合并/关闭），显示出核心团队在功能迭代与安全架构上的高强度投入。尽管无新版本发布，但项目正聚焦于 **attested-signing 安全子系统的完整落地** 和 **Reborn 架构的持续迁移**，技术债清理与生产 hardening 并行推进。社区反馈集中在 Discord 通道稳定性、Telegram 自定义 API 支持及计费透明度等用户体验问题。

---

## 2. 版本发布

**无新版本发布**。  
最新 GitHub 标签已至 `ironclaw-v0.27.0`（2026-04-29），但 crates.io 上仍为 `v0.24.0`，存在版本发布滞后问题（见 Issue #3259）。

---

## 3. 项目进展

今日 **11个 PR 被合并或关闭**，核心进展集中在 **attested-signing 安全子系统的多阶段交付**：

- **安全架构闭环**：PR #3961（已合并）完成了 attested-signing 的核心绑定机制 `ApprovedTxHash`，为后续身份验证与防重放攻击奠定基础；其后续 PR #4067 修复了 wire encoding 的 fail-closed 问题，强化了安全性。
- **多钱包支持推进**：PR #3992（WalletConnect v2 后端）与 PR #3993（NEAR 浏览器钱包重定向）实现了外部钱包集成，扩展了 attested-signing 的适用场景。
- **Reborn 集成深化**：PR #3995 将 attested gate 接入 Reborn WebUI 入口，使新架构支持安全签名流程；PR #3996 完成 PostgreSQL/libSQL 双后端持久化存储，提升生产可靠性。
- **工具执行安全加固**：PR #4021 引入 CI 边界测试，强制所有工具调用必须通过审计漏斗 `ToolDispatcher::dispatch`，防止绕过安全检查（响应 Issue #4019）。

> 整体来看，项目在安全关键路径上取得实质性突破，attested-signing 从设计文档走向可运行子系统。

---

## 4. 社区热点

### 🔥 高关注度 Issues

- **[#3259] Publish 0.25.0–0.27.0 to crates.io**  
  下游依赖因 wasmtime 28.x 的 CVE 被锁定在 `v0.24.0`，而 GitHub 已有 `v0.27.0`，导致安全更新无法传递。**9条评论**呼吁尽快同步发布，属高优先级运维阻塞项。  
  🔗 https://github.com/nearai/ironclaw/issues/3259

- **[#4030] Discord channel stops replying while tokio workers pinned at 100% CPU**  
  用户报告 WASM 通道在高负载下出现 CPU 占用飙升且无响应，疑似资源泄漏或死锁。**QA 复现确认**，影响生产可用性。  
  🔗 https://github.com/nearai/ironclaw/issues/4030

- **[#3701] v0.28.2 macOS prebuilt: gateway never binds despite config**  
  macOS 预编译版本存在配置失效问题，`doctor` 工具误报启用状态，影响本地开发体验。  
  🔗 https://github.com/nearai/ironclaw/issues/3701

> 社区诉求集中于 **发布流程规范化** 与 **跨平台稳定性保障**，反映项目进入生产部署阶段后的运维压力。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 修复状态 |
|--------|------|------|--------|
| ⚠️ 高 | #4030 | Discord WASM 通道 CPU 100% 且无响应 | ❌ 无 fix PR，需排查 tokio 任务调度 |
| ⚠️ 高 | #3701 | macOS 预编译版 gateway 绑定失败 | ❌ 无 fix PR，疑似构建脚本或权限问题 |
| ⚠️ 中 | #4022 | HTTP 响应错误错误地终止 agent 运行（#4014 引入回归） | ✅ 已有 fix PR #4022（待合并） |
| ⚠️ 中 | #3447 | Nightly E2E 测试持续失败 | ❌ 未定位根因，影响 CI 信心 |

---

## 6. 功能请求与路线图信号

- **Telegram 自定义 API 主机支持**（#4034）：用户希望支持自托管 Bot API 服务器，适用于企业内网部署场景。该需求明确且实现成本低，**可能被纳入下一版本**。
- **信用/速率限制透明度改进**（#4043）：用户反馈失败请求是否消耗 token 不清晰，建议增加日志与 UI 提示。属用户体验优化，**优先级 P1**。
- **Slack ProductAdapter MVP**（#3857）：Reborn 架构下新增 Slack 集成，使用预配置凭证支持 DMs 与应用提及。已有设计文档，**处于开发规划阶段**。

> 结合 PR 活动，**attested-signing 多租户模型**（#4051）与 **Reborn 通道迁移**（#3577）仍是核心路线图主线。

---

## 7. 用户反馈摘要

- **痛点**：
  - “Discord 用着用着就不回复了，CPU 跑满，只能重启服务。”（#4030）
  - “crates.io 版本太旧，我们被 CVE 卡住了，不敢升级。”（#3259）
  - “失败请求到底扣不扣费？文档没说清楚。”（#4043）
- **满意点**：
  - Reborn WebUI 的 beta 路径逐步可用，开发者认可架构演进方向（#3613、#3807）。
  - 安全团队对 attested-signing 的 fail-closed 设计表示认可（#4019）。

---

## 8. 待处理积压

- **[#3259] crates.io 版本发布滞后**：自 2026-05-05 提出，9条评论未解决，**阻塞下游安全更新**，需维护者优先处理。
- **[#3447] Nightly E2E 持续失败**：自 2026-05-10 起 nightly 失败，**CI 健康度受损**，需排查测试环境或 flaky test。
- **[#3577] Reborn 通道迁移跟踪**：涉及 29 个核心通道的迁移状态跟踪，**缺乏自动化工具支持**，易遗漏。

> 建议维护者本周内安排 crates.io 发布流程审计，并分配资源修复 macOS 构建问题以提升开发者体验。

---  
**数据截止：2026-05-26 23:59 UTC**  
*由 IronClaw 开源项目分析系统生成*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

**LobsterAI 项目动态日报（2026-05-26）**

---

### 1. 今日速览  
过去24小时内，LobsterAI 社区活跃度显著提升，共产生 **29条 PR 更新**（15条已合并/关闭，14条待合并）和 **1条新 Issue**，无新版本发布。开发重点集中在 **OpenClaw 集成优化、会话稳定性修复与技能同步功能增强**，反映出项目正从基础功能向跨系统协同与用户体验深化演进。维护者响应迅速，当日 PR 合并率达51.7%，整体开发节奏健康。

---

### 2. 版本发布  
*无新版本发布*

---

### 3. 项目进展  
今日共 **15个 PR 被合并或关闭**，核心进展包括：

- **OpenClaw 深度集成**：实现插件（#2042）与技能（#2045）从 OpenClaw 扩展目录的自动同步，打通双平台能力共享链路，提升用户插件管理效率。
- **会话稳定性修复**：解决会话冻结（#2047）、网关重启异常（#2043）及工具循环导致的 Token 浪费问题（#2049），显著提升长对话可靠性。
- **子代理体验优化**：完成子代理会话侧边栏展示与详情页开发（#2011），支持树形结构浏览与状态追踪，增强多代理协作可观测性。
- **配置交互改进**：上下文窗口滑块支持预设吸附与 K/M 简写输入（#2013），降低用户配置门槛。

> 项目在“多代理协同”与“跨系统一致性”方向迈出关键步伐，OpenClaw 生态融合初步成型。

---

### 4. 社区热点  
**唯一新 Issue #2046：[Agent 记忆体系产品建议](https://github.com/netease-youdao/LobsterAI/issues/2046)**  
用户 @X9-laser 基于实际使用提出高优先级需求：当前 Agent 无法跨 session 感知历史对话，导致信息孤岛与重复劳动。建议包括：
- Session 标题与元数据持久化至文件系统（使 Agent 可读）
- 历史对话自动检索与关联机制

该 Issue 虽仅1条评论，但直击个人 AI 助手的核心痛点——**长期记忆缺失**，可能预示下一阶段产品路线图方向。维护者尚未回应，需重点关注。

---

### 5. Bug 与稳定性  
以下为当日修复的关键问题（均已合并 PR）：

| 严重程度 | 问题描述 | 修复 PR |
|--------|--------|--------|
| 高 | 空闲期间工具循环导致 Token 持续消耗 | [#2049](https://github.com/netease-youdao/LobsterAI/pull/2049) |
| 高 | 会话界面冻结无响应 | [#2047](https://github.com/netease-youdao/LobsterAI/pull/2047) |
| 中 | GitHub Copilot Token 刷新引发网关重启 | [#2043](https://github.com/netease-youdao/LobsterAI/pull/2043) |
| 中 | 子代理清理钩子失败阻塞流程 | [#2044](https://github.com/netease-youdao/LobsterAI/pull/2044) |

> 所有高影响 Bug 均已闭环，系统稳定性显著增强。

---

### 6. 功能请求与路线图信号  
结合 Issue 与 PR，以下需求可能纳入近期版本：

- **Agent 记忆体系**（#2046）：用户强烈呼吁跨 session 记忆能力，与当前“子代理会话管理”（#2011）形成互补，有望成为 V2.5+ 核心特性。
- **动态模型列表同步**（#1522）：支持从厂商 API 自动拉取最新模型，减少手动配置负担，技术方案成熟，易落地。
- **会话颜色标注**（#1526）：提升多任务场景下的视觉区分度，UI 改动小、价值高，适合快速迭代。

> 维护者近期密集处理 OpenClaw 集成与稳定性问题，**记忆体系**或成下一阶段重点。

---

### 7. 用户反馈摘要  
从 Issue #2046 可提炼真实痛点：
- **不满意点**：Agent 无法记住历史对话，每次新 session 需重复上下文；手动维护成本高；浏览器 IndexedDB 存储的标题对 Agent 不可见。
- **使用场景**：长时间、跨多 session 的复杂任务（如项目规划、知识沉淀）。
- **期望**：系统级记忆能力，而非依赖用户手动复制粘贴。

> 用户已从“功能可用”转向“智能连贯”，对 Agent 的自主性提出更高要求。

---

### 8. 待处理积压  
以下长期未合并 PR 需维护者关注：

- **#1510**：[定时任务 IM 通知静默失败](https://github.com/netease-youdao/LobsterAI/pull/1510)（标记 stale，4月7日提交）  
  → 影响通知可靠性，需验证修复有效性。
  
- **#1514**：[QQ Bot 群组白名单 UI 缺失](https://github.com/netease-youdao/LobsterAI/pull/1514)（标记 stale）  
  → 功能完全不可用，阻碍 QQ 场景落地。

- **#1515**：[日志导出超时问题](https://github.com/netease-youdao/LobsterAI/pull/1515)（标记 stale）  
  → 涉及性能优化（DEFLATE 压缩瓶颈），需评估资源投入。

> 建议优先处理 #1514（UI 缺陷）与 #1510（功能失效），避免用户流失。

---  
*数据来源：LobsterAI GitHub 仓库（2026-05-25 24:00 UTC+8）*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报（2026-05-26）

---

## 1. 今日速览

Moltis 项目在 2026-05-25 继续保持高活跃度，社区与核心团队协同推进多项关键功能落地。过去24小时内共处理 **6 条 PR**（5 条已合并/关闭，1 条待合并）和 **5 条 Issues**（2 条新开，3 条已关闭），整体响应迅速，开发节奏紧凑。项目发布新版本 `20260525.01`，集成多项安全修复与功能增强。当前存在一个待合并的安全修复 PR，需优先关注。

---

## 2. 版本发布

### 🔖 新版本：`20260525.01`（2026-05-25）

本次发布为一次综合性更新，主要包含以下改进：

- **安全加固**：修复 CodeQL 扫描发现的多个高危问题，包括 DOM 注入风险、URL 构造漏洞、明文密钥传输及日志泄露（见 PR #1071）。
- **功能增强**：
  - 支持非阻塞式 `spawn_agent`，提升长任务场景下的父会话响应能力（PR #1067）。
  - 实现每轮对话粒度的 `tool_choice` 与 `active_tools` 控制，增强代理路由灵活性（PR #1069）。
  - 子代理预设支持可视化编辑（Markdown 驱动），降低配置门槛（PR #1070）。
- **开发者体验**：
  - 将 Moltis 版本号暴露至提示词上下文，便于工作流追踪更新（PR #1068）。
  - 修复 Docker 构建失败问题，确保 CI/CD 流程稳定（PR #1073）。

> ⚠️ **无破坏性变更**，但建议用户升级后验证自定义代理预设与工具调用逻辑是否兼容新行为。

[查看 Release 详情](https://github.com/moltis-org/moltis/releases/tag/20260525.01)

---

## 3. 项目进展

今日合并/关闭的 PR 显著推进了 Moltis 在 **安全性、代理控制与用户体验** 三大方向的能力：

- **#1067**（feat(tools): support nonblocking spawn agents）：实现后台子代理执行机制，解决父会话阻塞问题，提升复杂工作流响应性。
- **#1069**（feat(agents): support per-turn tool controls）：为 Anthropic、OpenAI 等主流 LLM 提供细粒度工具调用控制，支持漂移抵抗路由策略。
- **#1070**（Make sub-agent presets editable）：通过 Web UI 实现子代理预设的增删改，降低非技术用户使用门槛。
- **#1068**（Expose Moltis version to prompts）：增强可观测性，便于调试与版本追踪。
- **#1073**（Fix Docker build failures）：修复因路径引用错误导致的构建中断，保障部署稳定性。

> ✅ 上述 PR 均已合入主干，标志着 Moltis 在多代理协作、安全合规与易用性方面迈出关键一步。

---

## 4. 社区热点

### 🔥 最活跃 Issue：#868 — [Add Landlock access denial debug logging](https://github.com/moltis-org/moltis/issues/868)

- **作者**：@Cstewart-HC  
- **状态**：Open（已获 1 👍，1 条评论）  
- **讨论焦点**：请求为 Landlock 文件系统访问拒绝事件添加调试级日志，以提升沙箱环境下的故障排查能力。  
- **背景诉求**：用户在高安全隔离场景下难以定位权限问题，需更细粒度的审计日志支持。该需求契合 Linux 安全模块最佳实践，可能影响未来默认日志策略。

> 💡 该 Issue 虽非紧急，但反映了社区对 **可观测性与安全透明性** 的强烈关注，建议纳入下一轮安全增强计划。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 修复状态 |
|--------|------|------|--------|
| ⚠️ 中 | #1072 — [cron jobs marked "Execution Target: Host" run in a sandbox by default](https://github.com/moltis-org/moltis/issues/1072) | 用户配置为“Host”执行的定时任务仍被默认沙箱化，违背预期行为 | ❌ 无对应 PR，需排查配置解析逻辑 |
| ✅ 已修复 | #1022 — [WebSocket disconnected during LLM modes update](https://github.com/moltis-org/moltis/issues/1022) | LLM 模式切换时 WebSocket 异常断开 | 已关闭（推测由相关 PR 修复） |

> 🔍 #1072 为新报告 Bug，涉及核心调度逻辑，建议维护者优先复现并评估影响范围。

---

## 6. 功能请求与路线图信号

从近期 Issues 与 PR 可识别以下潜在路线图方向：

- **代理协作精细化控制**：#1011（Per-turn tool_choice）与 #1069 已实现部分功能，表明团队正聚焦于 **抗漂移代理路由**，未来可能扩展至动态技能加载。
- **异步任务管理**：#1004（Non-blocking spawn_agent）已由 #1067 实现，预示 Moltis 将向 **长时任务编排平台** 演进。
- **安全可观测性**：#868 提出的 Landlock 日志需求，可能推动内核级安全事件集成进统一监控体系。

> 📌 建议将 **Landlock 调试日志** 与 **Host 模式执行一致性** 纳入 v0.2 里程碑。

---

## 7. 用户反馈摘要

从 Issues 评论提炼关键用户声音：

- **痛点**：
  - “Small/cheap LLMs 无法可靠处理工具选择，导致路由失败”（#1011）→ 推动 per-turn 控制需求。
  - “spawn_agent 阻塞主会话，无法并行处理”（#1004）→ 催生非阻塞实现。
  - “Docker 构建频繁失败，阻碍本地开发”（#1073）→ 已修复，提升开发者体验。
- **满意点**：
  - 版本号暴露至提示词（#1068）被赞“对审计和回滚非常有用”。
  - 子代理预设可视化编辑（#1070）获积极反馈，“终于不用手动写 YAML 了”。

> 💬 用户普遍认可 Moltis 在 **多代理架构** 上的创新，但对 **配置一致性与错误反馈清晰度** 仍有改进期待。

---

## 8. 待处理积压

| 类型 | 编号 | 标题 | 创建时间 | 状态 | 提醒 |
|------|------|------|--------|------|------|
| Issue | #868 | Add Landlock access denial debug logging | 2026-04-24 | Open | 已超 30 天未响应，涉及安全可观测性，建议分配资源 |
| PR | #1071 | fix(security): resolve code scanning alerts | 2026-05-25 | Open（待合并） | 安全修复 PR，应优先 review 并合并 |

> ⚠️ **紧急提醒**：#1071 为关键安全补丁，虽已创建但尚未合并，存在潜在风险窗口，建议今日完成合入。

---

**报告生成时间**：2026-05-26  
**数据来源**：[Moltis GitHub Repository](https://github.com/moltis-org/moltis)  
**分析师备注**：项目整体健康度良好，开发活跃，社区参与积极。建议加强安全类 Issue 的响应时效，并持续优化配置语义一致性。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报（2026-05-26）

---

## 1. 今日速览

CoPaw 项目在 2026-05-26 继续保持高活跃度，过去24小时内共处理 **43 条 Issues**（新开/活跃 15 条，关闭 28 条）和 **43 条 PRs**（待合并 11 条，已合并/关闭 32 条），社区参与度显著。项目发布新版本 **v1.1.9-beta.1**，重点优化了插件安装体验与前端交互逻辑。当前核心问题集中在 **控制台 UI 实时性缺陷** 和 **多通道会话管理一致性** 上，开发团队正通过集成测试扩展与架构重构积极应对。

---

## 2. 版本发布

### 🔖 v1.1.9-beta.1（[Release Link](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.9-beta.1)）

**主要更新内容：**
- ✅ **feat(console)**：插件成功安装/卸载后自动刷新页面，提升用户体验（#4588）
- ✅ **chore(version)**：版本号升级至 1.1.9b1（#4589）
- ✅ **test(integration)**：初步集成测试覆盖增强（部分提交）

> ⚠️ **无破坏性变更**，但建议用户在测试环境中验证插件管理流程的稳定性。

---

## 3. 项目进展

今日共 **合并/关闭 32 个 PR**，关键进展包括：

| 类别 | 说明 | 链接 |
|------|------|------|
| **架构重构** | 统一访问控制系统上线，支持跨通道白名单/黑名单管理，Matrix 通道完成标准化改造 | #4565 |
| **桌面端增强** | Tauri 2.x 桌面应用支持已合并，新增自动更新机制（#4669），解决 Windows 任务栏图标显示异常问题（#3729） | #3813, #4669 |
| **通道稳定性** | 修复钉钉 DM 会话 webhook 键冲突问题（#4665），为 QQ 通道添加交互式工具审批卡片（#4667） | #4665, #4667 |
| **UI/UX 改进** | 编码模式支持深色主题（#4671），Markdown 表格换行渲染修复（#4379），宠物导入拖拽区适配暗色模式（#4599） | #4671, #4379 |
| **测试覆盖** | 集成测试框架扩展，新增 P0 级安全、Provider、Backend 测试，CI 引入三级门禁机制 | #4674 |

> 项目整体向 **企业级稳定性** 和 **多端一致性体验** 迈出关键一步。

---

## 4. 社区热点

### 🔥 高讨论度 Issues（评论数 ≥ 4）

| Issue | 主题 | 讨论焦点 | 链接 |
|------|------|--------|------|
| #4644 | 控制台工具调用不实时显示 | 用户反馈除 `read_file` 外多数工具调用需手动刷新才可见，影响调试效率 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/4644) |
| #4653 | 定时任务与用户消息共享 session 导致中断 | 定时任务被用户消息抢占，破坏自动化流程可靠性 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/4653) |
| #4650 | GLM-5.1 模型思维链不显示 | 特定模型通过 OpenAI 兼容接口使用时 reasoning_content 丢失，其他模型正常 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/4650) |
| #4652 | 记忆系统缺乏“总结-关联-提醒”机制 | 用户指出当前记忆仅为“信息堆砌”，缺乏知识提炼与状态管理 | [查看](https://github.com/agentscope-ai/QwenPaw/issues/4652) |

> 💡 **社区核心诉求**：提升 **实时交互可靠性**、**任务执行隔离性** 与 **长期记忆智能化**。

---

## 5. Bug 与稳定性

### 🚨 严重 Bug（按优先级排序）

| 问题 | 严重程度 | 状态 | 相关 PR |
|------|--------|------|--------|
| #4644 控制台工具调用延迟显示 | 高 | 🔴 未修复 | — |
| #4653 定时任务被用户消息中断 | 高 | 🔴 未修复 | — |
| #4675 Assistant 消息含 file block 导致 reasoning 注入永久失效 | 中高 | 🟡 有分析，无 PR | — |
| #4666 新建会话后 Models 配置丢失 | 中 | 🔴 未修复 | — |
| #4556 语音转录忽略配置的 Whisper 提供商 | 中 | ✅ 已关闭（疑似修复） | — |

> ⚠️ 建议优先处理 **#4644** 和 **#4653**，二者直接影响核心用户体验与自动化能力。

---

## 6. 功能请求与路线图信号

### 📌 高潜力功能需求（已有对应 PR 或社区强烈关注）

| 功能 | 状态 | 关联 PR/Issue | 预期版本 |
|------|------|--------------|--------|
| 消息时间戳显示 | 🟢 有 Issue，无 PR | #4662 | v1.2.0 |
| 记忆系统智能总结与关联 | 🟡 深度讨论中 | #4652 | v1.3.0+ |
| OpenCode 模型列表精简（仅保留 Zen ∩ Go 交集） | 🟢 PR 已提交 | #4660 | v1.1.10 |
| 文件操作回滚机制 | 🟡 长期任务，PR 待审 | #3346 | v1.2.0 |
| 每轮对话 Token 使用统计 | 🟢 PR 待合并 | #4433 | v1.1.10 |

> ✅ **短期路线图清晰**：v1.1.10 将聚焦 **配置稳定性** 与 **资源可见性**；v1.2.0 探索 **记忆智能化** 与 **操作可逆性**。

---

## 7. 用户反馈摘要

### 🗣️ 真实用户声音提炼

- **痛点**：
  - “控制台工具调用看不到，得刷新才能确认是否执行” → 实时性差（#4644）
  - “定时提醒做着做着就被我新消息打断了” → 会话隔离缺失（#4653）
  - “Windows 启动要40秒，还没个加载界面，以为卡死了” → 启动体验差（#4664）
  - “记忆记了一堆，但下次遇到同样问题还是不会用” → 记忆无提炼（#4652）

- **满意点**：
  - 编码模式集成 VS Code 风格编辑器，开发者体验佳（#4578）
  - Tauri 桌面端图标终于不是 Python 默认图标了（#3729）
  - Markdown 表格换行终于正常了（#4379）

---

## 8. 待处理积压

### ⏳ 长期未响应重要事项（>7天无进展）

| 事项 | 类型 | 创建日期 | 状态 | 建议 |
|------|------|--------|------|------|
| #3346 文件操作回滚支持 | PR | 2026-04-13 | 🔄 Under Review | 需安全团队评估风险后合并 |
| #4267 macOS 文件路径白名单 | PR | 2026-05-13 | 🔄 Under Review | 安全增强，建议加速 review |
| #4467 安全+Agent 单元测试（967 测试） | PR | 2026-05-17 | 🔄 Under Review | 关键质量保障，应优先合并 |
| #2584 前端代码结构混乱问题 | Issue | 2026-03-30 | ❓ Invalid（但仍有参考价值） | 建议归档为技术债文档 |

> 📢 **维护者提醒**：#4467 和 #4267 是提升项目安全基线的关键 PR，建议本周内完成 review。

---

**报告生成时间**：2026-05-26  
**数据来源**：GitHub CoPaw (QwenPaw) 仓库公开数据  
**分析师备注**：项目整体健康度良好，活跃度处于上升通道，建议加强 **实时通信可靠性** 与 **任务调度隔离性** 的专项优化。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

**EasyClaw 项目动态日报**  
📅 日期：2026-05-26  
🔗 项目主页：[github.com/gaoyangz77/easyclaw](https://github.com/gaoyangz77/easyclaw)

---

### 1. 今日速览  
EasyClaw 在 2026-05-26 整体活跃度较低，无新 Issue 提交或 Pull Request 活动，社区互动趋于平稳。项目通过发布 v1.8.15 版本持续推进核心客服会话管理能力的优化，体现出维护团队对稳定性和用户体验的持续投入。尽管开发节奏放缓，但版本迭代仍聚焦于关键工作流改进，项目健康度良好。

---

### 2. 版本发布  
🎉 **v1.8.15 已发布**  
🔗 [Release v1.8.15](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.8.15)  

**更新亮点：**  
- **会话生命周期管理增强**：支持客服人员显式结束会话，确保对话在完成工作后能干净关闭，避免“僵尸会话”残留。  
- **升级工单流转机制**：优化升级（escalation）与派单（dispatch）流程，提供更清晰的对话快照、更安全的提示路由（hint routing）以及更可靠的会话状态同步，降低误操作风险。  
- **客服工作台体验打磨**：对客服操作界面进行细节优化，提升可用性与操作流畅度。  

**破坏性变更**：无。本次更新为向后兼容的功能增强与体验优化。  
**迁移建议**：现有用户可直接升级，无需配置变更；建议测试环境验证会话结束与工单流转行为是否符合预期。

---

### 3. 项目进展  
今日无 Pull Request 合并或关闭，无新增功能代码合入主分支。项目进展主要体现在 v1.8.15 的版本发布上，属于对现有功能的精细化迭代，未引入结构性变更。

---

### 4. 社区热点  
今日无新 Issue 或 PR 提交，社区讨论活跃度为零。过去24小时内无高互动议题，用户反馈渠道保持静默，表明当前版本稳定性较高，未引发集中性问题或功能诉求。

---

### 5. Bug 与稳定性  
今日未报告任何 Bug、崩溃或回归问题。结合 v1.8.15 对会话状态与工单流转的强化处理，推测此前可能存在的会话泄漏或状态不一致问题已得到缓解。目前项目处于稳定运行状态。

---

### 6. 功能请求与路线图信号  
无新功能请求提出。从本次 v1.8.15 的更新方向（显式会话结束、工单流转优化）可推断，项目短期路线图仍聚焦于**客服会话生命周期管理**与**工单系统可靠性**，未来版本可能继续深化自动化清理、多通道会话同步或 SLA 监控等能力。

---

### 7. 用户反馈摘要  
今日无用户评论或反馈记录。但从 v1.8.15 更新内容反推，此前用户可能反馈过“会话无法正常关闭”“工单升级后信息丢失”或“客服操作中断”等问题，本次更新可视为对这些痛点的响应，体现出以客服实际工作流为中心的设计导向。

---

### 8. 待处理积压  
经核查，项目当前无长期未响应的重要 Issue 或 PR。Issue 与 PR 列表均为空，积压风险极低，维护负担轻，项目处于良好维护状态。

---  
📊 **健康度评估**：⭐⭐⭐⭐☆（4.5/5）  
- 优势：版本迭代有序，聚焦核心场景，无技术债务积压  
- 建议：可适度增加社区 engagement 机制（如定期路线图同步），以激发用户参与感

</details>

---
*本日报由 [Big Model Radar](https://github.com/gsscsd/big_model_radar) 自动生成。*