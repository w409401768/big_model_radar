# OpenClaw 生态日报 2026-07-14

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-13 23:52 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)
- [AstrBot](https://github.com/AstrBotDevs/AstrBot)

---

## OpenClaw 项目深度报告

好的，以下是为您生成的 OpenClaw 项目动态日报（2026-07-14）。

---

# OpenClaw 项目动态日报 | 2026-07-14

## 1. 今日速览
过去 24 小时，OpenClaw 维持了极高的社区迭代频率：共处理 **500 条 Issue** 动态（活跃 312 / 关闭 188）与 **500 条 PR** 动态（待合并 268 / 已合并关闭 232）。项目发布了 v2026.7.1 稳定版与 beta.6，核心亮点为 **新增 Featherless、Claude Sonnet 5 等模型提供商**，并将新用户默认模型切换为 **GPT-5.6**。但与此同时，多项 P0/P1 级回归（如工具输出被替换为占位符 #104721、CLI 数据库损坏 #101290）引发社区高度紧张。项目当前处于 **“生态快速扩张”与“核心稳定性补课”并行** 的高强度冲刺期。

## 2. 版本发布
- **发布版本：** v2026.7.1 (Stable) & v2026.7.1-beta.6
- **核心亮点：**
  - **模型生态扩张：** 新增 Featherless、Claude Sonnet 5、Mythos 5、Meta Muse Spark 1.1 及 ClawRouter 提供商/模型接入。
  - **默认模型变更：** 新装机首次设置默认模型切换为 **GPT-5.6**。
  - **推理交互：** Sol 与 Terra 支持 `/think ultra`，Luna 支持 `max` 模式；完整支持 Z.AI 的 `max` 参数。
  - **体验优化：** OAuth 授权后自动刷新可用模型列表。
- **破坏性变更 / 迁移建议：** 本版本未发现明确的破坏性变更。建议所有使用 Beta 版本的用户升级至稳定版。

## 3. 项目进展
尽管评论最密集的 PR 尚为待合并状态，但通过已合并/关闭 PR 与公开提交，项目在过去 24 小时推进显著：

- **核心架构打磨：** 维护者 @steipete 将巨型的 `chat.send` 处理器按显式生命周期拆分为独立模块（#106555 已关闭），并切分了 5 个超过 4100 行的大运行时模块（#106503 已关闭）。这表明团队在为后续的模块化测试与低风险贡献铺路。
- **多 Agent 稳定性：** 修复了并发 agent-to-agent 对话导致会话树分叉，进而被 Anthropic 拒绝的“会话中毒”问题（#98790）。修复了 GPT-5.6 Sol 在 Codex 运行时中失败的问题（#103884）。
- **渠道修复密集提交：** 尽管大部分未合入，团队同时向 **Slack**（进度干扰 #102082、API 超时 #106643、用户缓存限制 #105978）、**WhatsApp**（媒体下载挂起 #106529）和 **多频道**（进度草稿阈值修复 #106026）提交了针对性修复。
- **开发者体验提升：** 沙箱 `stat` 命令现已兼容非英语环境（#106907）；删除了 IOS Talk Mode 中无用的冗余状态（#106881）；CI 构建移除了 `restart` 测试中不必要的硬休眠等待（#106906）。

## 4. 社区热点
- **“Linux/Windows 客户端何时来？”（#75）**：评论 112，👍 81。作为编号第 75 的 Feature Request，跨平台桌面应用是 OpenClaw 社区目前呼声最高、最长的遗留期望。
- **“工具结果爆炸，完全不可用”（#104721）**：评论 16。用户 @dennisd-hub 描述此 P0 Bug 为“完全破坏性回归”，所有工具调用结果（文件读取等）均被替换为纯字面量 `(see attached image)`，目前无修复 PR。
- **“聊得好好的，第二条消息就冲突了”（#102020）**：评论 13。用户发现 Signal 及 daemon 频道首个消息正常，第二条必报 `reply session initialization conflicted`，严重阻碍实际试用。
- **“Gateway 跑着跑着，数据库就碎了”（#101290）**：评论 11。macOS 用户的 `openclaw.sqlite` 在数天内损坏四次，社区对数据持久化的信任感受到冲击。

## 5. Bug 与稳定性
| 严重程度 | Bug 描述 | 状态 | 修复 PR |
|---|---|---|---|
| **P0 (关键)** | 所有工具调用结果返回 `(see attached image)` 字面量 | [OPEN](#104721) | 暂无 |
| **P0 (关键)** | CLI 健康检查命令会损坏运行中的 SQLite 数据库 | [OPEN](#101290) | 暂无 |
| **P0 (关键)** | 多处遗留状态迁移仍直接阻塞 Gateway 启动 | [OPEN](#103076) | 暂无 |
| **P1 (严重)** | 并发 Agent 对谈导致会话树分叉并被上游拒绝，对话静默中毒 | [OPEN](#98790) | 暂无 |
| **P1 (严重)** | Stuck Session Recovery 机制双重失效，Session 预处理耗时过长 | [OPEN](#76038) | 暂无 |
| **P1 (严重)** | Windows 上 Gateway 硬崩溃（`STATUS_STACK_BUFFER_OVERRUN`） | [OPEN](#71699) | 暂无 |
| **P1 (严重)** | 工具/执行调用失败直接吞没模型回复与错误信息 | [OPEN](#100121) | 暂无 |
| **P1 (严重)** | MCP 重试风暴无熔断，可耗尽虚拟机内存资源 | [OPEN](#68527) | 暂无 |

## 6. 功能请求与路线图信号
- **生态扩张信号：** **桌面端客户端的缺失**（#75）仍是项目当前最强的外部生态压力。若短期内无法实现，建议项目组给予社区明确的路标或解释。
- **Agent 安全体系正在成型：**
  - **按来源标记记忆可信度**（#7707）：用户要求区分“用户指令”与“Web 抓取”的记忆，防止恶意命令行注入。
  - **Exec-Approvals 黑名单机制**（#6615）：获 7 个 👍。用户需要“允许一切，除 X 之外”的策略，尤其是针对 `gog gmail send` 等危险命令。
  - **文件系统沙箱**（#7722）：用户尝试按路径限制 Agent 文件访问但遇到配置困难。
- **模型体验深度优化：**
  - **动态模型发现**（#10687）与 **上下文超限自动回退**（#9986）是重度 AI 用户的核心诉求。若实现，可大幅降低用户对上游 API 变更的运维成本。
  - **OpenRouter 费用追踪**（#9016）与 **TUI 无障碍**（#9637）表明用户群体从极客向更广泛的使用场景拓展。

## 7. 用户反馈摘要
- **最成功用例：** 家庭与个人自动化中枢。
  - > “We've been running it as a family and business assistant ... it has genuinely become part of our daily workflow.” —— #73537 用户
- **主要痛点：**
  - **“每次 Stable 版本都有大坑”：** 多名用户抱怨 2026.6.x 系列频繁出现破坏性回归，本次 P0 占位符问题彻底摧毁了用户对“稳定版”的信心。
  - **“无声丢失消息”：** Slack、Webchat、LINE 等在并发冲突时静默丢弃消息（#102400、#86012），用户无从得知消息未送达。
  - **“配置不够灵活”：** 用户希望按模型配置超时（#8724）、按频道配置 Stream 模式（#74077），以及终端多行输入（#10118）。
- **积极评价：** 模型更新速度极快（v2026.7.1 对 Sonnet 5 / Mythos 5 的支持广受好评），核心开发者 @steipete 的高频参与给予社区信心。

## 8. 待处理积压
- **P0 危机：** 工具输出占位符 Bug（[#104721](https://github.com/openclaw/openclaw/issues/104721)）与数据库损坏 Bug（[#101290](https://github.com/openclaw/openclaw/issues/101290)）目前均**无关联修复 PR**，项目核心功能处于受损状态，亟需维护者优先响应。
- **最长寿命 Feature：** 桌面端应用（[#75](https://github.com/openclaw/openclaw/issues/75)）自 2026 年 1 月 1 日提出，112 评论，获 81 个 👍，半年无实质性推进，建议社区或项目组明确开发状态。
- **待推进安全架构：** 内存信任标记（[#7707](https://github.com/openclaw/openclaw/issues/7707)）、文件沙箱（[#7722](https://github.com/openclaw/openclaw/issues/7722)）、Exec-Approvals 黑名单（[#6615](https://github.com/openclaw/openclaw/issues/6615)）均提交于 2 月初且无进展。配合 MCP 重放风暴（[#68527](https://github.com/openclaw/openclaw/issues/68527)）的现实风险，安全基座需要优先补课。
- **开放式模型生态：** 动态模型发现（[#10687](https://github.com/openclaw/openclaw/issues/10687)）与模型自定义超时（[#8724](https://github.com/openclaw/openclaw/issues/8724)）是多 API Key 用户的刚性需求，值得下一版本重点考量。

---

## 横向生态对比

好的，这是基于您提供的各项目社区动态摘要，生成的一份横向对比分析报告。

---

# 个人 AI 智能体开源生态横向对比分析报告（2026-07-14）

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **“能力高速扩张与基础稳定性博弈”** 的关键阶段。头部项目日处理 Issue/PR 高达 500 级别，模型提供商以周为单位快速接入（如 GPT-5.6、Claude Sonnet 5）。然而高频迭代带来显著副作用：多个项目同时报告 P0 级回归（工具调用占位符、消息队列消失、数据库损坏），社区对“稳定版”的信心出现动摇。与此同时，安全治理、跨平台桌面端、消息可靠性正从“增强特性”变为“基础设施级需求”，生态整体呈现 **由极客工具向生产级平台快速演进** 的态势。

## 2. 各项目活跃度对比

| 项目 | Issue 动态 (近24h) | PR 动态 | 版本发布 | 项目健康度 |
|------|-------------------|---------|----------|-----------|
| **OpenClaw** | 500 (总更新) | 500 (总更新) | v2026.7.1 Stable ✅ | ⚠️ P0 危机未解决; 生态扩张快但核心受损 |
| **hermes-agent** | 500 (总更新) | 500 (总更新) | ❌ 无 | ✅ 大量 bug 关闭，转向质量巩固期 |
| **QwenPaw** | 50 (更新) | 50 (更新) | v2.0.0.post1 | 🟡 回归抱怨较多，但团队修复迅速 |
| **Zeroclaw** | 50 (更新) | 50 (更新) | ❌ 无 | 🟡 交付瓶颈（45 个待审 PR），文档短板突出 |
| **AstrBot** | 22 (更新) | 33 (更新) | ❌ 无 | 🟢 问题响应快，但知识库等长期问题未决 |
| **PicoClaw** | 4 (新增) | 5 (新增) | ❌ 无 | 🟡 中等活跃但合并停滞，安全替换急需关注 |

> 注：Issue/PR 动态口径各项目不完全一致（OpenClaw/hermes 总更新量含关闭；PicoClaw 为净新增），但已如实反映。绝对值上的差异代表社区吞吐量分层。

## 3. OpenClaw 在生态中的定位

- **体量与广度第一**：模型提供商接入速度（Sonnet 5、Mythos 5 等）和通道覆盖（Slack、WhatsApp、LINE）是生态中最激进的，社区迭代总量与 hermes-agent 并列第一梯队。
- **技术路线比照**：
  - 与 **hermes-agent** 相比，OpenClaw 缺少成熟的桌面原生体验（#75 呼声极高），但模型和通道支持更广；hermes 侧重于桌面端的 All-in-One（Kanban、远程配置）。
  - 与 **QwenPaw** 相比，OpenClaw 不绑定单一模型生态，提供了更大的 BYOM（Bring Your Own Model）自由度，但因此在治理与权限系统上起步较晚（#7707、#7722 长期未合入）。
  - 与 **Zeroclaw** 相比，OpenClaw 覆盖更深的技术栈（CLI、自建运行时），而 Zeroclaw 强调配置驱动和低代码（ZeroCode），目标用户更偏向非开发者。
  - 与 **AstrBot** 相比，OpenClaw 是通用 Agent 框架，AstrBot 更偏向即时通讯 Bot 插件化场景。
- **当前最大风险**：P0 工具占位符 Bug（#104721）和数据库损坏（#101290）无修复 PR，如果持续可能动摇社区对“稳定版”的信任。

## 4. 共同关注的技术方向

以下需求在多个项目中同时涌现，已成为行业级驱动信号：

| 技术方向 | 涉及项目 | 代表性 Issue/PR |
|----------|----------|-----------------|
| **安全治理与权限管控** | OpenClaw, QwenPaw, Zeroclaw, PicoClaw | OpenClaw #7707(记忆信任), #7722(文件沙箱); QwenPaw #6063(桥接治理); Zeroclaw #7686(审批执行顺序); PicoClaw #3088(加密库替换) |
| **桌面端与跨平台** | OpenClaw, hermes-agent, AstrBot | OpenClaw #75(桌面客户端); hermes #41222(Kanban 集成); AstrBot WebChat 持续修复 |
| **消息可靠性与队列** | OpenClaw, QwenPaw, AstrBot, Zeroclaw | OpenClaw 消息丢失 (#102400); QwenPaw #6006(消息队列消失); AstrBot #9253(刷新卡队列); Zeroclaw #9027(AMQP幂等性) |
| **可观测性与费用/用量追踪** | OpenClaw, hermes-agent, AstrBot, Zeroclaw | hermes #33433(上下文条0%); AstrBot #9248(Token圆环修复); OpenClaw #9016(OpenRouter费用); Zeroclaw dashboard |
| **模型可扩展性与动态适配** | 所有六个项目 | OpenClaw 新增Sonnet5; hermes 修复Codex; QwenPaw 多模型兼容; PicoClaw Anthropic缓存; AstrBot 多 Provider |
| **配置动态化与多环境** | OpenClaw, Zeroclaw, QwenPaw | OpenClaw #10687(动态模型发现); Zeroclaw #8363(配置驱动策略); QwenPaw #6063(热加载) |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|-----------------|
| **OpenClaw** | 全能通用 Agent 框架 | 高级自部署用户、开发者 | 服务端 CLI+Gateway，模型和通道覆盖最广，运行时模块化拆分 |
| **hermes-agent** | 桌面生产力 All-in-One | 个人知识工作者、团队 | 原生桌面 App，集成 Kanban/远程网关，强调开箱即用体验 |
| **QwenPaw** | 企业级治理 + 通义生态 | 中国企业用户、AgentScope 使用者 | 深度绑定 Qwen 模型优化，Policy 引擎 + 热重载治理 |
| **Zeroclaw** | 零代码配置 Agent | 非开发者、低代码爱好者 | 配置驱动策略（ZeroCode），面向快速部署，治理 RFC 正在设计 |
| **AstrBot** | IM Bot 平台/个人助理 | 社区群聊管理、普通用户 | 多 IM 通道适配（微信/Discord/Telegram），WebChat UI，插件体系 |
| **PicoClaw** | 轻量嵌入式 AI Agent | Sipeed 设备用户、边缘场景 | 极小资源占用，依赖优化（libolm→vodozemac），适合嵌入式 Linux |

## 6. 社区热度与成熟度

- **极高活跃度（500 级，同时迭代+修复）**  
  **OpenClaw** / **hermes-agent** — 两者 Issue/PR 吞吐量远超其他。  
  hermes-agent 已进入质量巩固期（今日大量 bug 关闭），**成熟度更高**；  
  OpenClaw 虽然体量最大，但正在为高速扩张付出稳定性代价，处于 **“生态扩张与补课并行”** 的冲刺期。

- **高活跃度（50 级，特性开发与维护过渡）**  
  **Zeroclaw** / **QwenPaw** — 两者均处于大版本收尾/发布后的反馈消化期。  
  Zeroclaw 面临交付瓶颈（45个待审 PR），而 QwenPaw 修复响应速度极快（28 个 PR 一天合并），**QwenPaw 短期迭代效率更优**。

- **中高活跃度（20-30 级，快速修复迭代）**  
  **AstrBot** — 用户反馈响应迅速，核心 ChatUI 问题当天修复合并，项目健康度良好。知识库等长期积压是主要短板。

- **中低活跃度（个位数增长，节奏较慢）**  
  **PicoClaw** — 社区贡献持续但合并停滞，安全依赖替换（#3088）超过一个月未处理，存在外围衰减风险。

**总结分层**：
- **快速迭代阶段**：OpenClaw、QwenPaw、Zeroclaw（均有大量 opan 功能在推进）
- **质量巩固阶段**：hermes-agent（大量 bug close，开始关闭低优先级功能）
- **混合阶段**：AstrBot、PicoClaw（既有修复又长期积压）

## 7. 值得关注的趋势信号

1. **“稳定压倒功能”已成为社区共识**  
   OpenClaw #104721、QwenPaw #6013、AstrBot #9253 等均显示用户对回归零容忍。**对新入局开发者的启示**：在设计架构时优先考虑消息可靠性、工具调用幂等性和数据持久化，不要过度追赶模型数量。

2. **安全治理从“可选插件”变为“基础设施”**  
   超过4个项目并行推进权限管控（exec 黑名单、文件沙箱、审批门控、加密库替换）。**趋势信号**：AI Agent 正从实验玩具转向处理敏感任务的生产工具，安全设计必须在前端架构层内置，而非后期补丁。

3. **桌面端一体化是下一个争夺焦点**  
   OpenClaw #75（最老 Feature，81赞）、hermes #41222（今日最高赞12👍）均指向桌面原生体验。**对平台构建者**：CLI/Web 分离正在被用户抛弃，提供类似 Notion 或 Obsidian 的桌面一体化体验可能是获得高粘性用户的关键。

4. **消息队列与推送可靠性成为基本质量门槛**  
   从 OpenClaw 的消息无声丢失到 QwenPaw 队列完全消失再到 AstrBot 刷新卡死，底层通信可靠性是所有多轮交互 Agent 的阿喀琉斯之踵。**架构建议**：引入持久化工作队列、断线重连、消息幂等处理应作为 Agent 框架的默认组件。

5. **多模型动态适配决定生态上限**  
   动态模型发现、上下文超限自动回退、按模型配置超时/费用追踪在四个项目中同时被提出。**趋势**：单一模型绑定正在退出舞台，未来 Agent 中间件的核心竞争在于智能路由与成本控制能力。

6. **低代码配置（ZeroCode）正在降低门槛**  
   Zeroclaw 的 ZeroCode 路线、AstrBot 的 WebUI 配置、OpenClaw 的 OAuth 刷新列表——社区正努力降低使用门槛，**以吸引非开发者用户**，这预示 AI Agent 市场正在从小众极客向大众工具转变。

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是根据您提供的 GitHub 数据生成的 Zeroclaw 项目 2026-07-14 动态日报。

---

# Zeroclaw 项目动态日报 | 2026-07-14

## 1. 今日速览

过去 24 小时内，Zeroclaw 项目保持了极高的活跃度，共涉及 50 条 Issue 与 50 条 PR 更新。然而，数据反映出显著的 **交付瓶颈**：仅 5 个 PR 被合并/关闭，而多达 45 个 PR 仍处于待合并状态。项目当前正全力冲刺 v0.8.3 版本的收尾工作，多个功能跟踪器均已关闭，同时 v0.8.4 维护周期及 ZeroCode 强化路线图已开始前期规划。社区讨论焦点集中在治理 RFC（工作流泳道、轻量化核心）以及因文档缺失导致的入门体验问题上。项目技术上进展迅猛，但代码入库效率和用户开箱体验存在明显短板。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日项目在测试覆盖和功能特性收尾方面取得了扎实进展，主要得益于多个 v0.8.3 跟踪器的关闭以及大量增强测试的合入：

-   **v0.8.3 特性冻结**：核心功能跟踪器已大规模关闭，标志着 v0.8.3 的特性开发阶段基本完成。关闭的跟踪器涵盖：
    -   **Provider 序列化** (#8360)：Provider 请求/响应与原生工具消息序列化行为。
    -   **通道适配器** (#8362)：通道交互一致性、主动发送、回复路由等。
    -   **网关与 Web 端** (#8070)：Web 仪表盘、ZeroCode、Quickstart 与桌面端。
    -   **配置驱动策略** (#8363)：运行时路由、模型切换及工具策略。
-   **测试覆盖率加固**：大量针对边界情况的测试被合入，覆盖了内存存储读取器时间戳排序 (#7694)、运行时钩子恐慌恢复 (#7688)、Provider `responses-wire` 选项传播 (#7690) 及 ZeroCode 非安全 TLS 确认流 (#7693)，显著提升了项目健壮性。
-   **杂项修复**：Google Workspace 工具因仅接受小写方法名而导致 `batchUpdate` 等 camelCase API 调用失败的问题已修复 (#9044)，修复方式为当前注释提及的放宽校验逻辑。

## 4. 社区热点

本期讨论焦点体现了社区对项目长期治理和架构演进的深度思考，而非简单的用户提问。

-   **治理架构讨论（#6808）**：由 @Audacity88 发起的 “工作流泳道与板面自动化” RFC 以 **14 条评论** 位居榜首。该提案旨在优化维护工作流，避免引入过多手动负担。该项目是未来开发者协作方式的根基。
-   **核心理念辩论（#6165）**：@ilteoood 发起的 “通过外部集成保持核心轻量化” RFC 收获了 **9 条评论**。社区正在深入探讨究竟哪些功能该内置，哪些该交由 MCP 或插件托管，这直接决定了 ZeroClaw 的生态架构。
-   **文档引起的“民愤”（#7758）**：用户直言“代码再好在垃圾文档面前毫无意义”，该 Issue 获得了最多的 👍 反馈（2个）。虽然 Issue 已关闭，但它揭示了项目目前最大的用户感知痛点，维护者需要持续关注 documentation 质量的实质改善。
-   **功能呼声**：社区对**安全配对体验**（#8998 配对码 GUI）和**通道部署灵活性**（#9022 Slack Events API 模式）提出了具体建议，体现了社区对生产级部署和易用性的追求。

## 5. Bug 与稳定性

今日报告的 Bug 分布较广，影响面大。关键 Bug 的修复 PR 已开始并行推进，但仍有严重问题等待解决。

-   **S1 - 工作流阻塞**：
    -   **Telegram 通道配置失效 (#8505)**：用户按 Quickstart 配置后 Bot 无响应。该问题严重影响 Telegram 用户的入门体验，目前处于未合并状态，优先级 **p1**。
    -   **Docker Gateway 端口绑定失败 (#9035)**：`docker compose up -d` 后端口无法访问，显示 `Connection refused`。严重阻碍基于容器的生产环境部署。
    -   **Windows Ctrl+C 强制退出 (#9028)**：导致进程异常退出（code 1073741510）。严重影响 Windows 平台体验。
-   **S2 - 行为异常**：
    -   **Model Cache 只读不写 (#9046)**：`models_cache.json` 文件只读不写，导致 `zeroclaw models refresh` 命令修复无效。
    -   **ZeroCode UI/UX 异常 (#8644, #8646)**：ZeroCode 存在对话顺利完成但无可见输出的问题，且日志详情面板无法展示完整载荷，影响开发调试。
-   **已有修复 PR 的 Bug**：
    -   **凭证泄露检测增强 (#8906)**：扫描链接/图片目标中凭证模式的修复正在审查中。
    -   **SOP AMQP 幂等性 (#9027)**：防止 AMQP 报文被重复调度的修复已提交。
    -   **运行时历史裁剪 (#9007)**：修复工具调用历史因非整轮裁剪导致数据不一致的问题。

## 6. 功能请求与路线图信号

新提出的功能需求与项目既有的路线图高度契合，同时维护者已有计划地开启了下个版本的规划。

-   **v0.8.4 维护周期开启**：核心贡献者 @Audacity88 发起了 **v0.8.4 维护列车 (#8357)** 和 **ZeroCode 巩固与强化 (#9010)** 跟踪器，明确目标日期为 7 月 31 日。标志着工作重心正从 v0.8.3 新特性转移至稳定性、文档和开发者体验优化。
-   **大型功能 PR 接近落地**：以下大型 PR 处于 Open 状态，极有可能进入后续版本：
    -   **Home Assistant 原生集成 (#8994)**：允许 Agent 直接通过 REST API 操控智能家居。
    -   **Hindsight 内存后端 (#8992, #8993, #8995)**：添加了第三方远程内存后端，并优化了相关默认配置。这三者属于堆叠 PR，合并后将是重大的生态扩展。
    -   **Matrix 通道大幅增强 (#8443)**：添加单消息进度草稿功能，是 Matrix 通道的核心体验升级。
-   **开发者体验自动化**：新提案强调自动化配置验证（#8997 警告非法的通道引用）和文档自动生成（#9039 从安装规范生成文档），意图从技术手段解决当前的文档和配置痛点。

## 7. 用户反馈摘要

-   **最强烈的痛点：入门门槛极高**
    -   @t-cc 在 #7758 中直言文档“形同虚设”，导致无法完成任何配置文件编写。结合 Telegram 配置失败 (#8505)、ZeroCode 静默无输出 (#8644) 等问题，新用户的第一印象可能非常负面。项目在“开箱即用”体验上仍需大量投入。
-   **中高阶用户深度参与，但贡献壁垒显现**
    -   高级开发者（如 @Audacity88, @Nillth, @logical-and）正在主导架构级的 RFC、复杂的功能集成以及大规模的代码清理（#8901 移除注释官僚主义）。这说明项目在技术深度上对开发者有很强吸引力，但复杂的代码规范和庞大的 PR 审查积压（45个待审）可能成为潜在的贡献摩擦点。
-   **跨平台体验严重不均衡**
    -   Windows 用户报告了**严重的稳定性问题**（#9028 Ctrl+C 崩溃，#8578 启动失败不退出进程），提示项目在非 Linux 平台上的测试覆盖可能存在明显盲区。

## 8. 待处理积压

以下关键项目长期未得到有效合并或明确回应，正在成为项目健康度的潜在风险。

-   **待合并 PR 积压严重（45个）**：审查资源的短缺正在成为项目的瓶颈。其中大型 PR 风险最高：
    -   **超大 PR 陷入僵局？**：Matrix 通道改进 (#8443)、SOP 通道门控 (#8979) 以及 Hindsight 系列配置 (#8995) 均为 `size:XL` 级别，且长期未合入。维护者需要紧急分配精力进行 Code Review，以避免分支严重发散导致无法合并。
-   **S1 级 Bug 缺乏官方响应**：
    -   #8505 (Telegram 无法配置) 和 #9035 (Docker 网关端口绑定失败) 两个阻塞级 Bug 目前均没有明确的修复 PR 或来自维护者的详细 root cause 分析，这可能打击企业级用户和特定渠道用户的信心。
-   **安全关键路径测试缺失**：
    -   **#7686 (审批门控工具执行顺序)** 是 p1 优先级的安全测试需求，涉及工具调用审批等关键逻辑，目前虽已标记 Accepted 但暂无明确进展。考虑到安全风险，应作为高风险项优先处理。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，收到。作为一名AI智能体与个人AI助手领域的开源项目分析师，现根据您提供的PicoClaw项目数据，为您生成2026年7月14日的项目动态日报。

---

### PicoClaw 项目动态日报 | 2026年7月14日

**分析师摘要：** 今日项目活跃度中等，社区贡献持续，但合并节奏放缓。过去24小时内，Issue和PR数量均有小幅增长，但均处于待处理和讨论阶段，暂无新代码合并或版本发布。值得关注的是，多个关键的旧Issue（如密码学库替换）和PR（如Anthropic缓存支持）仍在等待核心维护者的决策与合并，这可能是项目推进的潜在瓶颈。整体项目健康状况稳定，功能迭代和社区反馈活跃，但需要加快对高优先级/陈旧项的响应速度。

---

### 1. 今日速览
- **活跃度评估：** 中等。社区提报和讨论活跃，但上游合并活动停滞。
- **关键动态：** 过去24小时内新增4个Issue和5个PR，但均为“开放”或“陈旧”状态，没有新版本发布，也没有PR被合并或关闭（除#3253快速关闭外）。这表明项目社区正在积极反馈和贡献，但维护者的审查与合并工作可能积压。
- **主要关注点：** 多个高优先级和重要功能（如加密库替换、Anthropic缓存支持）的相关 Issue/PR 已持续开放多日，需要维护团队重点关注。
- **风险提示：** **`libolm`替换Issue（#3088）** 作为高优先级请求已开放超过一个月，若持续积压，可能成为项目的安全风险点。

### 2. 版本发布
无新版本发布。

### 3. 项目进展
今日无重要PR被合并。唯一合并/关闭的PR是 **#3253（Feat/gateway webhook）**，它被快速关闭，但从描述和标签看是新功能，可能功能尚不完整或有其他问题。这反映出今日项目在主分支的推进速度为**零**。许多有价值的PR（如#3228、#3254）仍在等待审查与合并，项目整体进展受阻于代码审查阶段。

### 4. 社区热点
今日社区讨论的焦点集中在几个开放已久的深度技术议题上：

- **#3088 [Feature] 使用vodozemac替换libolm**
  - **热度：** 👍 2 | 评论 8
  - **链接：** https://github.com/sipeed/picoclaw/issues/3088
  - **分析：** 这是社区呼声最高的诉求之一。`libolm`已被标记为不安全和不再维护，`vodozemac`是官方替代。该Issue已开放超过一个月且被标记为高优先级，反映了用户对通信安全的高度重视以及期望项目尽快摆脱对过期依赖的急切心情。维持者对它的忽视是社区的一个主要痛点。

- **#3229 [Proposal] 实现Anthropic Messages的滚动对话缓存断点**
  - **热度：** 评论 1 (作者为PR #3228的提交者)
  - **链接：** https://github.com/sipeed/picoclaw/issues/3229
  - **分析：** 该Issue与PR #3228密切相关，共同构成了一个旨在解决Anthropic模型高token消耗问题的完整方案。该作者不仅提出了问题，还提交了实现代码（#3228），展现了极高的社区贡献热情。社区的诉求是优化成本，特别是在代理式工作流中，减少重复发送的对话历史。

- **#3230 [BUG] Gemini API通过OpenAI兼容格式调用函数时丢失`thought_signature`**
  - **热度：** 评论 1
  - **链接：** https://github.com/sipeed/picoclaw/issues/3230
  - **分析：** 用户报告了与Google Gemini API集成时的具体兼容性问题。这影响了工具调用功能，表明项目在使用OpenAI兼容层对接其他API时可能存在适配瑕疵。由于AI提供商众多，此类兼容性问题将是用户长期反馈的重点。

### 5. Bug与稳定性
今日报告了一个功能性Bug，暂无严重性崩溃报告。

- **#3230 [FUNCTIONAL BUG] Gemini API via OpenAI格式调用缺少`thought_signature`**
  - **严重程度：** 高（影响核心功能：工具调用）
  - **Fix PR状态：** 无
  - **链接：** https://github.com/sipeed/picoclaw/issues/3230
  - **分析：** 用户在通过Cloudflare AI Gateway使用Gemini时，遇到OpenAI兼容格式下的函数调用错误。这直接阻碍了用户在该场景下的正常使用，是目前最紧急的Bug。

- **#3254 [FIX PR] 修复Agent模型解析时的引用匹配逻辑**
  - **相关Issue：** 无（自行发现并修复的Bug）
  - **严重程度：** 中（可能导致错误地选择模型）
  - **Fix PR状态：** 已提交（#3254，**待合并**）
  - **链接：** https://github.com/sipeed/picoclaw/pull/3254
  - **分析：** 社区的`@fabdelgado`贡献了一个Bug修复，解决了Agent在解析模型配置时可能匹配错误条目的问题。这是一个重要的正确性修复，但是仍然处于等待合并的状态。

### 6. 功能请求与路线图信号
今日需求集中在安全性、兼容性和性能优化上，与社区维护的PR高度相关：

- **安全替换（#3088）**：用 `vodozemac` 替换 `libolm`。高优先级，关乎项目安全基础。
- **Anthropic API增强（#3229 -> #3228）**：实现系统提示词的`cache_control`和对话历史缓存。这将是针对Anthropic用户的一项重大成本和性能改进，很可能成为下一版本的关键特性。
- **API扩展与兼容性（#3231）**：为SearXNG搜索添加BasicAuth支持。这反映了一个小众但实际的使用场景：当用户自建或使用受认证的后端搜索服务时的集成需求。
- **Agent模型解析修复（#3254）**：修复了潜在的逻辑错误。虽然是一个修复，但也为Agent功能的稳定性铺平了道路。

**路线图信号：** `anthropic-messages`提供商的缓存功能是当前最成熟的待集成功能（有Issue提议，有PR实现），且来自同一贡献者，是下一版本最有可能引入的特性。

### 7. 用户反馈摘要
- **痛点与不满：**
  - **安全依赖过时：** 用户在 #3088 中强烈表达了对使用`libolm`的担忧，认为其“不安全”且“无人维护”，希望项目尽快更新。这被视为一个越来越严重的潜在问题。
  - **兼容性问题：** 用户 #3230 在尝试使用Gemini API时遇到阻碍，反馈问题的同时可能对项目在不同AI平台上的稳定性产生疑虑。
- **使用场景与诉求：**
  - **代理与成本优化：** 用户 #3229 深入讨论了代理工作流的成本问题，并提出了非常具体的`cache_control`实现方案，表明存在高级用户正在将项目用于复杂的、高token消耗的场景，并对成本敏感。
  - **自建服务集成：** 用户 #3231 试图给SearXNG配置BasicAuth，体现了用户在自建或受限网络环境中部署项目的实际需求。

### 8. 待处理积压
以下为长期未响应或阻塞性工作项，提醒维护者关注：

- **#3088 [P0 - 最高优先级] [Help Wanted] 替换libolm为vodozemac**
  - **链接：** https://github.com/sipeed/picoclaw/issues/3088
  - **状态：** 开放36天，高优先级，无人认领。
  - **风险：** 安全与健康度风险。作为安全库，此依赖的更新不应被推迟。
- **#3228 [P1 - 高] [PR] 修复Anthropic消息的系统缓存控制**
  - **链接：** https://github.com/sipeed/picoclaw/pull/3228
  - **状态：** 开放8天，有配套Issue #3229，是一个完整的功能实现。
  - **影响：** 阻塞了`anthropic-messages`提供商的关键优化能力。
- **#3192 / #3191 [P2 - 低] [PRs] 基础设施清理（Docker/CI/CD）**
  - **链接：#3192** (https://github.com/sipeed/picoclaw/pull/3192)， **#3191** (https://github.com/sipeed/picoclaw/pull/3191)
  - **状态：** 开放17天，属于低风险的维护性工作。
  - **建议：** 此类“杂务”PR长期不合并，可能会打击社区贡献者的积极性。

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

# ‌QwenPaw 项目动态日报 — 2026‑07‑14

---

## 一、今日速览

过去 24 小时项目处于**高活跃度**（50 Issues 更新、50 PRs 更新），v2.0.0.post1 补丁版发布后持续消化社区反馈。**核心痛点集中在 v2.0.0 回归**：上下文压缩破坏 tool_call/tool_result 配对、Background Offload 导致 API 400 错误、审批路由错误、消息队列缺失等。社区情绪从积极反馈转向回归抱怨，但团队响应迅速：当天合并/关闭 28 个 PRs，包括多个针对 offload 逻辑、权限治理、消息队列修复的关键补丁。项目整体在稳定性和治理能力上仍在快速迭代。

---

## 二、版本发布

### v2.0.0.post1
| 项目 | 内容 |
|------|------|
| 发布摘要 | 修复了 Provider 搜索输入框的浏览器自动填充问题，以及 legacy session 加载错误。 |
| 相关 PR | [#6007](https://github.com/agentscope-ai/QwenPaw/pull/6007)、[#6011](https://github.com/agentscope-ai/QwenPaw/pull/6011) |
| 注意事项 | 该版本未解决上下文压缩配对断裂、offload 机制失效等核心问题，但为后续 hotfix 奠定了基础。 |

> 迁移提醒：从 v1.x 升级后需重新配置 MCP 工具的白名单；若遇到消息队列消失，请关注 #6006 进展。

---

## 三、项目进展

今日合并/关闭的 28 个 PRs 主要围绕以下方向：

### 3.1 核心稳定性修复
| PR | 说明 |
|----|------|
| [#6058](https://github.com/agentscope-ai/QwenPaw/pull/6058) | 展平 offload hint 消息并临时禁用有问题的 offload 机制，阻断了因此引起的 400 BadRequest |
| [#6052](https://github.com/agentscope-ai/QwenPaw/pull/6052) | 修复 Background Tool 完成后产生的孤立 ToolResultBlock 导致 OpenAI API 400 的问题 |
| [#5989](https://github.com/agentscope-ai/QwenPaw/pull/5989) | 多层防御：在上下文压缩、消息发送等多个阶段清理孤立的 tool_result 消息 |
| [#6045](https://github.com/agentscope-ai/QwenPaw/pull/6045) | 修复会话删除后消息队列残留的问题（补全 #6040 未覆盖的真实删除路径） |

### 3.2 治理与权限
| PR | 说明 |
|----|------|
| [#6063](https://github.com/agentscope-ai/QwenPaw/pull/6063) | 将前端 tool-guard 规则桥接到后端 Policy 深度扫描，支持热加载 |
| [#6054](https://github.com/agentscope-ai/QwenPaw/pull/6054) | 放宽无匹配规则时的 fallback 行为，并增加全局沙箱开关 |

### 3.3 运维与诊断
| PR | 说明 |
|----|------|
| [#6053](https://github.com/agentscope-ai/QwenPaw/pull/6053) | `qwenpaw doctor` 健康检查改用 `/api/healthz` 端点，解决一直报告 404 的问题 |
| [#6068](https://github.com/agentscope-ai/QwenPaw/pull/6068) | 迁移滚动历史时保留正确的 session ID，防止会话 ID 错乱 |

### 3.4 性能与依赖
| PR | 说明 |
|----|------|
| [#6062](https://github.com/agentscope-ai/QwenPaw/pull/6062) | 技能初始化时跳过冗余的 manifest 扫描，防止文件描述符耗尽（解决 #3892） |
| [#6060](https://github.com/agentscope-ai/QwenPaw/pull/6060) | 更新 reme-ai 依赖至 0.4.1.0，保持兼容性 |

**项目向前迈进了多少？**  
- 关闭了 3 个关键的 400 BadRequest 复现路径（#5996、#5986、#5960 的根源均被触及）；
- 治理体系（Governance）向动态配置和用户可控迈出一步；
- 诊断工具（doctor）恢复可用性，降低运维困惑。

---

## 四、社区热点

### 4.1 评论最活跃的 Issues

| Issue | 标题 | 评论数 | 核心诉求 |
|-------|------|--------|----------|
| [#5996](https://github.com/agentscope-ai/QwenPaw/issues/5996) | [Bug]: 2.0.0对话时会产生MODEL_EXECUTION_ERROR | 10 | OpenAI formatter 序列化拿不到 tool_calls 导致 400 |
| [#5961](https://github.com/agentscope-ai/QwenPaw/issues/5961) | [Bug]: v2.0.0版本循环执行的问题 | 7 | 搭配 qwen3.7-plus 模型时 agent 反复写入/删除，无法完成简单任务 |
| [#6006](https://github.com/agentscope-ai/QwenPaw/issues/6006) | [Bug]: 消息队列功能没有了！急急急，望修复 | 6 | 升级后消息队列完全消失，用户工作流中断 |
| [#5947](https://github.com/agentscope-ai/QwenPaw/issues/5947) | V2.0.0版本 MCP中禁用了某些子工具的访问,但是agent还是可以调用 | 6 | MCP 拒绝/允许设置无效，权限管控形同虚设 |
| [#6013](https://github.com/agentscope-ai/QwenPaw/issues/6013) | V2.0.0的版本,越来越不稳定了,还不如V1.xxx的版本 | 5 | 用户强烈抱怨稳定性下降，对比腾讯 workbuddy |

### 4.2 用户情绪分析
- **失望型**：#6013 直接表达回归恶化，要求回退 v1.x
- **焦急型**：#6006 喊“急急急”，消息队列是核心功能
- **困惑型**：#5947、#5955 对 UI/UX 变更感到不解
- **建设型**：#5980 列出缺失功能（SSH Offline、Profiles），希望恢复

### 4.3 关注的新 PR
- [#6063](https://github.com/agentscope-ai/QwenPaw/pull/6063)（Governance 桥接）和 [#6062](https://github.com/agentscope-ai/QwenPaw/pull/6062)（性能优化）获得较多隐性关注，社区对治理和性能提升有期待。

---

## 五、Bug 与稳定性

按严重程度排列，标注是否有 fix PR 或正在修复中。

### 🔴 严重（阻塞工作流）

| 编号 | 描述 | 状态 |
|------|------|------|
| [#5996](https://github.com/agentscope-ai/QwenPaw/issues/5996) | OpenAI 400: tool 消息无对应 tool_calls（hint 消息引起） | 已由 #6058/#6052 修复 |
| [#5986](https://github.com/agentscope-ai/QwenPaw/issues/5986) | 上下文压缩拆散 tool_call/tool_result 配对 | 已由 #5989 修复 |
| [#5960](https://github.com/agentscope-ai/QwenPaw/issues/5960) | 同上，跨消息边界拆散 | #5989 覆盖 |
| [#5962](https://github.com/agentscope-ai/QwenPaw/issues/5962) | 微信渠道 session 内也出现 400 | #5989 覆盖 |
| [#6006](https://github.com/agentscope-ai/QwenPaw/issues/6006) | 消息队列完全消失 | [#6045](https://github.com/agentscope-ai/QwenPaw/pull/6045) 已合并，但社区尚未验证 |
| [#6056](https://github.com/agentscope-ai/QwenPaw/issues/6056) | Background offload 立即杀死子进程 | 临时禁用 offload（#6058），长期方案待定 |
| [#5963](https://github.com/agentscope-ai/QwenPaw/issues/5963) | `execute_shell_command` 硬编码 60s 超时 | 尚无 fix PR |
| [#5965](https://github.com/agentscope-ai/QwenPaw/issues/5965) | PyInstaller 打包缺少子模块，Dream 功能崩溃 | [#6024](https://github.com/agentscope-ai/QwenPaw/issues/6024) 关联 |
| [#6012](https://github.com/agentscope-ai/QwenPaw/issues/6012) | Desktop python-runtime 缺少 agentscope 依赖 | 尚无 fix PR |

### 🟡 中等（部分功能受影响）

| 编号 | 描述 | 状态 |
|------|------|------|
| [#6020](https://github.com/agentscope-ai/QwenPaw/issues/6020) | 审批路由错误 + `approval_level: OFF` 失效 | 尚无 fix PR |
| [#5872](https://github.com/agentscope-ai/QwenPaw/issues/5872) | Docker 内 browser_use 因 dbus 失败 | 尚无 fix PR |
| [#6034](https://github.com/agentscope-ai/QwenPaw/issues/6034) | Feishu/微信内部错误、自动添油加醋内容 | 尚无 fix PR |
| [#6049](https://github.com/agentscope-ai/QwenPaw/issues/6049) | 多轮对话后 invalid params, 400 | 尚无 fix PR |
| [#6017](https://github.com/agentscope-ai/QwenPaw/issues/6017) | DeepSeek 400 时整个会话被杀死 | 尚无 fix PR |

### 🟢 轻微（体验影响）

| 编号 | 描述 | 状态 |
|------|------|------|
| [#5955](https://github.com/agentscope-ai/QwenPaw/issues/5955) | WebUI 技能只显示 20 个，超过不加载 | 尚无 fix PR |
| [#5788](https://github.com/agentscope-ai/QwenPaw/issues/5788) | Skills 列表滚动加载失效 | 尚无 fix PR |
| [#5983](https://github.com/agentscope-ai/QwenPaw/issues/5983) | `qwenpaw doctor` 总是报 404 | [#6053](https://github.com/agentscope-ai/QwenPaw/pull/6053) 已修复 |
| [#5984](https://github.com/agentscope-ai/QwenPaw/issues/5984) | ARM 设备上无法关闭 Landlock 审批提示 | 尚无 fix PR |

---

## 六、功能请求与路线图信号

### 6.1 用户提出的新需求

| Issue | 需求 | 是否可能纳入下一版本 |
|-------|------|----------------------|
| [#6048](https://github.com/agentscope-ai/QwenPaw/pull/6048) | 免认证主机白名单支持 CIDR 段 | 低优先级，但已有 WIP PR |
| [#5958](https://github.com/agentscope-ai/QwenPaw/issues/5958) | 复用 AgentScope 的权限系统 | 团队正在推进 Governance 改造，可能纳入 |
| [#5887](https://github.com/agentscope-ai/QwenPaw/issues/5887) | 命令触发的 auto-memory 需附带 session_id | 暂无 PR |
| [#5977](https://github.com/agentscope-ai/QwenPaw/issues/5977) | 插件 HTTP 路由热重载后丢失 | 暂无 PR |

### 6.2 既有 PR 暗示的路线图方向

| PR | 方向 | 状态 |
|----|------|------|
| [#5069](https://github.com/agentscope-ai/QwenPaw/pull/5069) | 视觉模型 fallback（图片/视频转文本） | OPEN，等待 review |
| [#6067](https://github.com/agentscope-ai/QwenPaw/pull/6067) | sensitive files 扩展及全局读取许可 | OPEN，治理增强 |
| [#5927](https://github.com/agentscope-ai/QwenPaw/pull/5927) | 中文 Windows GBK 兼容性 | OPEN，ready-for-human-review |
| [#5953](https://github.com/agentscope-ai/QwenPaw/pull/5953) | 统一 tool result 裁剪中间件 | OPEN，重构核心管道 |
| [#6060](https://github.com/agentscope-ai/QwenPaw/pull/6060) | reme-ai 依赖升级 | 已合并，自动记忆质量提升 |
| [#5935](https://github.com/agentscope-ai/QwenPaw/pull/5935) | ToolResultPruningMiddleware 统一实现 | 已合并 |

> 信号：项目在**治理（Governance）**、**跨平台兼容性（Windows GBK/ARM）**、**稳定性中间件**三个方向持续投入。社区对 v2.0.0 的稳定性回退很敏感，下阶段很可能聚焦于“让 v2 稳定赶上 v1”的目标。

---

## 七、用户反馈摘要

### 7.1 正面反馈（极少）
- 无直接表扬性评论。大多数为问题报告。

### 7.2 负面痛点梳理

| 痛点类型 | 引用 | 代表 Issue |
|----------|------|------------|
| **稳定性倒退** | “越来越不稳定了,还不如V1.xxx的版本” | #6013 |
| **核心功能丢失** | “消息队列功能没有了！急急急” | #6006 |
| **权限管控失效** | “拒绝和允许设置,无效” | #5947 |
| **自动化反常** | “会添油加醋的增加内容” | #6034 |
| **多模型兼容差** | “搭配qwen3.7-plus模型时，智能体总会反反复复的写入、删除” | #5961 |
| **审批流程混乱** | “钉钉发起的请求，审批弹窗显示在电脑端” | #6020 |
| **Docker 环境支持弱** | “browser_use 启动失败 —— dbus 连接错误” | #5872 |

### 7.3 用户期望
- 恢复 v1.x 稳定版的核心体验；
- 提供后端沙箱/权限的 UI 开关（#5984）；
- 改善多轮工具调用的一致性；
- 让 `approval_level: OFF` 真的完全关闭审批（#6020）。

---

## 八、待处理积压

以下 Issues/PRs 已长时间无维护者响应或未分配，提请关注：

### 8.1 长期未响应的重要 Issue

| 编号 | 标题 | 创建时间 | 最近更新 | 重要性 |
|------|------|----------|----------|--------|
| [#5872](https://github.com/agentscope-ai/QwenPaw/issues/5872) | Docker 内 browser_use 启动失败 | 2026-07-09 | 2026-07-13 | 🟠 沙箱关键路径，多用户受影响 |
| [#5788](https://github.com/agentscope-ai/QwenPaw/issues/5788) | Skills 列表只显示 20 条，滚动加载无效 | 2026-07-05 | 2026-07-13 | 🟡 UI 体验问题，等待 triage |
| [#5984](https://github.com/agentscope-ai/QwenPaw/issues/5984) | ARM 设备无法关闭 Landlock 审批 | 2026-07-12 | 2026-07-13 | 🟠 影响嵌入式部署 |
| [#5977](https://github.com/agentscope-ai/QwenPaw/issues/5977) | 插件 HTTP 路由热重载后丢失 | 2026-07-12 | 2026-07-13 | 🟠 插件生态稳定性 |
| [#6055](https://github.com/agentscope-ai/QwenPaw/issues/6055) | 环境变量未传递 + 前端配置未同步 | 2026-07-13 | 2026-07-13 | 🟠 Docker 配置关键路径 |

### 8.2 待合并的 PR（接近 1 周无更新）

| PR | 标题 | 创建 | 标签 | 风险 |
|----|------|------|------|------|
| [#5069](https://github.com/agentscope-ai/QwenPaw/pull/5069) | feat: visual model fallback | 2026-06-10 | OPEN | 功能 PR，需 code review |
| [#5927](https://github.com/agentscope-ai/QwenPaw/pull/5927) | fix: add errors='replace' for GBK | 2026-07-10 | first-time-contributor, ready-for-human-review | 低风险，中文 Windows 兼容 |
| [#5953](https://github.com/agentscope-ai/QwenPaw/pull/5953) | fix: use standard truncation hint for scroll | 2026-07-10 | OPEN | 滚动模式下 tool result 截断，中等风险 |

### 8.3 维护提醒
- **v2.0.0.post1 发布后**，请关注 #6006（消息队列）用户是否验证已修复，若未解决需 hotfix。
- **Dream auto-memory** 相关多 issue（#6024、#5965、#6012）需确认 Python runtime 缺失依赖问题是否有系统级解决方案。
- **安全治理议题**（#5954 权限模式、#6048 CIDR）讨论热度上升，建议尽快指定负责人与社区沟通计划。

---

*以上日报基于 GitHub 公开数据（2026-07-13 00:00 – 2026-07-14 00:00 UTC）生成。数据源：QwenPaw Repository。*

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为 you 生成的 hermes-agent 项目 2026-07-14 动态日报。

---

### hermes-agent 项目动态日报 | 2026-07-14

---

#### 1. 今日速览

截至 2026 年 7 月 14 日，Hermes-Agent 项目在过去 24 小时内表现出极高的社区活跃度与维护响应速度。共处理了 500 条 Issue 更新（其中 388 条已关闭，关闭率高达 **77.6%**），以及 500 条 PR 更新（其中 125 条已合并/关闭）。尽管今日无新版本发布，但大量长期存在的顽固 Bug（特别是桌面端与 OpenAI Codex 提供商）被成功标记为已修复并合入主分支。项目整体健康度优秀，正从密集的功能开发阶段过渡到以稳定性与质量优化为核心的巩固期。

#### 2. 版本发布

*（今日无新版本发布）*

#### 3. 项目进展

过去 24 小时内的 125 个合并/关闭的 PR 和大量 Issue 关闭标志着项目在稳定性上迈出了坚实一步。核心进展如下：

- **桌面应用体验大修**：多个困扰用户的桌面端问题被集中解决并标记为 `implemented-on-main`，包括：**聊天窗口自动滚动对抗用户操作**（[#38272](https://github.com/NousResearch/hermes-agent/issues/38272)）、**长对话中滚轮回弹吸底**（[#37527](https://github.com/NousResearch/hermes-agent/issues/37527)）、**远程网关重连循环**（[#38266](https://github.com/NousResearch/hermes-agent/issues/38266)）以及 **Tailscale 连接失败**（[#38061](https://github.com/NousResearch/hermes-agent/issues/38061)）。
- **OpenAI Codex 提供商修复**：成功合入了针对 Codex 后端的三大严重 Bug 修复，包括 **OAuth 认证导致 TypeError**（[#33415](https://github.com/NousResearch/hermes-agent/issues/33415)）、**返回 null 导致 Slack/Cron 全链路瘫痪**（[#33976](https://github.com/NousResearch/hermes-agent/issues/33976)）以及**上下文条显示 0%**（[#33433](https://github.com/NousResearch/hermes-agent/issues/33433)）。
- **基础设施稳定性提升**：
    - **Docker 部署**：修复了多容器共享数据卷时 `s6-log` 锁死循环的致命 Bug（[#34457](https://github.com/NousResearch/hermes-agent/issues/34457)）。
    - **Cron 调度器**：PR [#38624](https://github.com/NousResearch/hermes-agent/pull/38624) 被合并，解除了任务锁，防止长时间作业阻塞后续调度。
    - **测试**：PR [#13318](https://github.com/NousResearch/hermes-agent/pull/13318) 修正了 Modal 终端测试伪通过的问题。

#### 4. 社区热点

今日讨论最活跃与点赞最高的议题反映了社区对“平台一体化”和“精细化管理”的强烈诉求：

- **最受期待的功能**：Issue [#41222](https://github.com/NousResearch/hermes-agent/issues/41222)（将看板 Kanban 集成到桌面端）以 **12 👍** 高居榜首。用户多次强调在 CLI 与网页端切换的摩擦感，强烈渴望“All-in-One”。
- **UI 与配置管理**：Issue [#37713](https://github.com/NousResearch/hermes-agent/issues/37713)（桌面端支持远程配置文件切换）以 **11 👍** 被关闭，获得了社区高度评价。同时，**Windows 缩放支持**（[#37619](https://github.com/NousResearch/hermes-agent/issues/37619)，7 👍）也被确认修复，解决了桌面端在许多高分辨率屏幕上的可用性问题。
- **有趣的 Bug 讨论**：Issue [#47685](https://github.com/NousResearch/hermes-agent/issues/47685) 因“点击就送”的特点引发了热烈讨论。用户发现 Z.AI 的 GLM-5.2 模型只要系统提示词中出现“Hermes Agent”字符串就会返回 429 错误，这一离奇的提供商行为排查过程在社区中被广泛讨论。

#### 5. Bug 与稳定性

- **严重级别（今日已修复）**：
    - **OpenAI Codex 全面崩溃**：[#33415](https://github.com/NousResearch/hermes-agent/issues/33415)、[#33976](https://github.com/NousResearch/hermes-agent/issues/33976)、[#33433](https://github.com/NousResearch/hermes-agent/issues/33433)，影响所有 OAuth 用户。
    - **Docker 生产环境瘫痪**：[#34457](https://github.com/NousResearch/hermes-agent/issues/34457)，`s6-log` 锁死。
    - **桌面端远程连接与交互**：[#38061](https://github.com/NousResearch/hermes-agent/issues/38061)、[#38266](https://github.com/NousResearch/hermes-agent/issues/38266)、[#38272](https://github.com/NousResearch/hermes-agent/issues/38272)、[#37527](https://github.com/NousResearch/hermes-agent/issues/37527)。

- **严重级别（已有 Fix PR 待合并）**：
    - **ACP 编辑器超时**：PR [#64030](https://github.com/NousResearch/hermes-agent/pull/64030) 修复了编辑审批超时硬编码为 60s 而非读取 `approvals.timeout` 配置的缺陷（P2）。
    - **MCP 工具调用崩溃**：PR [#64034](https://github.com/NousResearch/hermes-agent/pull/64034) 修复了 MCP 工具参数 Schema 传递为空的问题（P2）。
    - **Telegram 轮询崩溃**：PR [#64037](https://github.com/NousResearch/hermes-agent/pull/64037) 修复了回调查询未处理的 `TimedOut` 异常导致整个 Bot 掉线的问题（P2）。
    - **Gemini 推理泄露**：PR [#64036](https://github.com/NousResearch/hermes-agent/pull/64036) 修复了禁用 `show_reasoning` 后仍然显示推理摘要的问题。

- **长期存在的干扰性 Bug**：
    - **Dashboard 粘贴失效**：[#24860](https://github.com/NousResearch/hermes-agent/issues/24860)（P3，自5月13日）。
    - **Claude 模型缓存穿透**：[#56776](https://github.com/NousResearch/hermes-agent/issues/56776)（P3，通过 OpenAI 兼容网关调用时 Cache 命中率 0%）。

#### 6. 功能请求与路线图信号

- **高优先级/下一版本候选**：
    - **持久化会话记忆**：[#8457](https://github.com/NousResearch/hermes-agent/issues/8457) 详细描述了跨会话的长期记忆与自动压缩需求，这是走向“长期 Agent”的核心功能。
    - **Desktop 看板集成**：[#41222](https://github.com/NousResearch/hermes-agent/issues/41222) 是今日点赞最高的功能，预计如果开发资源允许，该功能会被官方正式纳入 Desktop 路线图。
    - **提供商选择器过滤**：[#12655](https://github.com/NousResearch/hermes-agent/issues/12655) 允许用户屏蔽不需要的内置提供商，对于重度自定义用户是刚需。

- **低优先级/等待决策**：
    - **Vaultwarden 秘密管理支持**：[#33126](https://github.com/NousResearch/hermes-agent/issues/33126) 今日被标记为 `not-planned`，建议自我托管用户关注替代方案。
    - **UAIV Google Meet 语音插件**：[#36903](https://github.com/NousResearch/hermes-agent/issues/36903) 同样被标记为 `not-planned`。

- **已提交的 PR 信号**：从今日集中提交的 PR 看，下一个 Patch 版本将着重修复 **ACP 编辑器**、**MCP 工具链** 和 **Telegram 平台** 的稳定性。功能方面，**Matrix 密码支持**（[#64033](https://github.com/NousResearch/hermes-agent/pull/64033)）和 **配置文件同步 CLI**（[#17912](https://github.com/NousResearch/hermes-agent/pull/17912)）是高潜力功能。

#### 7. 用户反馈摘要

- **远程连接配置复杂**：多位用户在 Issue 中反馈了远程桌面网关配置的艰难体验。“测试连接成功，但实际连接失败”这种令人困惑的幻象 Bug（[#38061](https://github.com/NousResearch/hermes-agent/issues/38061)）是典型的反模式，今日已被修复。
- **对桌面端爱恨交织**：用户一方面大力呼吁看板集成（[#41222](https://github.com/NousResearch/hermes-agent/issues/41222)），另一方面对基础的滚动体验严重不满，有用户形容自动滚动“像在打架”（[#38272](https://github.com/NousResearch/hermes-agent/issues/38272)）。基础交互体验（如粘贴 #24860）仍有待打磨。
- **企业级部署特征明显**：多配置文件切换（[#37713](https://github.com/NousResearch/hermes-agent/issues/37713)）、跨重启记忆持久化（[#8457](https://github.com/NousResearch/hermes-agent/issues/8457)）的诉求表明，用户正在认真地将 Hermes Agent 部署到专业的生产工作流中。社区希望看到更成熟的配置管理支持。

#### 8. 待处理积压

以下 Issue 或 PR 长期未获得显著进展或响应，建议维护者团队给予关注：

- **Dashboard 粘贴失效**：[#24860](https://github.com/NousResearch/hermes-agent/issues/24860)（P3，自5月13日）。作为基本交互功能，影响面极广，建议重新评估优先级。
- **Claude 模型跨网关缓存穿透**：[#56776](https://github.com/NousResearch/hermes-agent/issues/56776)（P3，自7月2日）。直接影响使用 OpenAI 兼容网关调用 Claude 的用户的效率和成本。
- **TUI 鼠标支持**：[#4064](https://github.com/NousResearch/hermes-agent/issues/4064)（P3，自3月30日）。长期积压的 UX 改进。
- **配置文件同步 PR**：[#17912](https://github.com/NouRSearch/hermes-agent/pull/17912)。该 PR 规模较大，涉及安全边界，但它是解决多设备配置管理的核心需求，建议维护者组织评审。
- **决策断后**：对于标记为 `not-planned` 的功能，如 [#33126](https://github.com/NousResearch/hermes-agent/issues/33126)（Vaultwarden），建议维护者在 Issue 中提供明确的替代方案指引或社区插件推荐，避免重复提问。

</details>

<details>
<summary><strong>AstrBot</strong> — <a href="https://github.com/AstrBotDevs/AstrBot">AstrBotDevs/AstrBot</a></summary>

# AstrBot 项目动态日报 — 2026-07-14

**数据统计周期**：2026-07-13 00:00 – 2026-07-13 23:59 UTC

---

## 1. 今日速览

过去 24 小时内，项目保持极高的社区活跃度：累计 **22 条 Issue 更新**（其中 14 条为新开或活跃，8 条已关闭），**33 条 PR 更新**（28 条待合并，5 条已合并/关闭）。核心贡献者集中修复了 WebChat 在刷新后的流断连与队列阻塞问题，并针对 Token 圆环显示错误、Dashboard 异常处理等用户体验缺陷提交了多项修复。多位社区成员同时贡献了知识库上传、Provider 配置等领域的修复与增强。项目整体健康度良好，问题响应与修复迭代速度显著加快。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日 **4 个 Pull Request 被合并、1 个被关闭**，涵盖核心稳定性、功能补全与配置健壮性：

- **[#9259 – fix: resume ChatUI streams after refresh](https://github.com/AstrBotDevs/AstrBot/pull/9259)**（已合并，size:XXL）  
  核心改动：将 WebChat 生成流与原始 SSE 生命期解耦，暴露活跃运行快照并提供恢复端点。刷新后能自动恢复最旧的活跃运行、重试瞬断并继续处理队列中的后续消息。**彻底解决刷新后回复丢失与消息积压问题**。

- **[#9256 – fix(webchat): 修复WebChat SSE断开后agent未停止及队列残留问题](https://github.com/AstrBotDevs/AstrBot/pull/9256)**（已合并，size:L）  
  为后台队列引入关闭事件，避免向已关闭队列入队；同时优化消息事件的推送逻辑。与 #9259 协同，消除了因 SSE 断连导致的 agent 永久阻塞。

- **[#9255 – fix: prevent the WebChat token ring from over-reporting context usage](https://github.com/AstrBotDevs/AstrBot/pull/9255)**（已合并，size:S）  
  修正 Token 用量圆环直接使用累计 `token_usage` 导致的百分比虚高（如 deepseek-v4-pro 显示 280%）。改用 `llm_requests` 最后一次调用的 token 状态，反映真实上下文占用。

- **[#4532 – feat: import and export personas](https://github.com/AstrBotDevs/AstrBot/pull/4532)**（已合并，size:L）  
  实现人格设定（Persona）的 JSON 导出/导入功能，对应关闭 issue [#4409](https://github.com/AstrBotDevs/AstrBot/issues/4409)。方便用户分享与迁移人格配置。

- **[#9216 – fix(group_chat_context): use .get() to avoid KeyError when config profile lacks image_caption_prompt](https://github.com/AstrBotDevs/AstrBot/pull/9216)**（已合并，size:XS）  
  修复当旧版配置缺少 `image_caption_prompt` 字段时群聊上下文模块抛出 KeyError 的问题，提升向前兼容性。

以上合并使 **ChatUI 刷新后的体验大幅改善、Token 监控准确、Persona 功能补全、配置兼容性增强**，项目在用户体验与稳定性方面向前迈进了一大步。

## 4. 社区热点

今日讨论最集中的议题源自 **ChatUI 刷新后异常**与 **Token 圆环错误**：

- **刷新导致的消息卡死/丢失**（[#9253](https://github.com/AstrBotDevs/AstrBot/issues/9253)、[#9249](https://github.com/AstrBotDevs/AstrBot/issues/9249)）  
  多位用户反馈：在模型思考时刷新页面后，新发消息被捕获为“follow-up message”排队但永不回复，或回复内容完全丢失。用户表示“最长等待了 20 分钟”仍无响应。这两条 Issue 均在今日关闭，对应修复 PR #9259 与 #9256 已合并。

- **Token 圆环百分比虚高**（[#9248](https://github.com/AstrBotDevs/AstrBot/issues/9248)）  
  用户发现 multi-step agent run 后圆环显示 280%，与实际上下文占用严重不符。根因分析指出 `token_usage` 采用了累加语义而非当前占用。该 Issue 随 PR #9255 合并后关闭。

- **人格设定导出/导入**（[#4409](https://github.com/AstrBotDevs/AstrBot/issues/4409)） 与 **撤回消息不应回复**（[#9142](https://github.com/AstrBotDevs/AstrBot/issues/9142)）  
  虽创建较早，但均在今日关闭，社区长期期待的功能得到满足，反映了项目对用户诉求的积极跟进。

另外，**知识库加载失败**（[#7218](https://github.com/AstrBotDevs/AstrBot/issues/7218)）与 **文件上传报错 `not same nb of vectors`**（[#7589](https://github.com/AstrBotDevs/AstrBot/issues/7589)）在评论区持续有用户附议，属于长期痛点。

## 5. Bug 与稳定性

以下按严重程度排列今日报告的 Bug，并标注修复状态（包含已合并的修复 PR）：

| 严重度 | Issue | 问题描述 | 修复状态 |
|--------|-------|----------|----------|
| 🔴 严重 | [#9253](https://github.com/AstrBotDevs/AstrBot/issues/9253) [#9249](https://github.com/AstrBotDevs/AstrBot/issues/9249) | 模型思考时刷新后消息卡队列/回复丢失 | ✅ 已合并 #9259 #9256 |
| 🔴 严重 | [#9248](https://github.com/AstrBotDevs/AstrBot/issues/9248) | Token 圆环累加虚高（显示 280%） | ✅ 已合并 #9255 |
| 🟡 较高 | [#9254](https://github.com/AstrBotDevs/AstrBot/issues/9254) | `contextLimit` 优先级错误，用户配置被元数据覆盖 | 📌 有 fix PR #9263 (open) |
| 🟡 较高 | [#9268](https://github.com/AstrBotDevs/AstrBot/issues/9268) | 带版本号命名的 Skill 下载失败 | 📌 有 fix PR #9270 (open) |
| 🟡 较高 | [#9269](https://github.com/AstrBotDevs/AstrBot/issues/9269) | Dashboard API 未处理异常返回纯文本，无法调试 | 📌 有 fix PR #9271 (open) |
| 🟡 较高 | [#9262](https://github.com/AstrBotDevs/AstrBot/issues/9262) | 新建 Provider Source 未保存直接删除导致 400 和界面残留 | 📌 有 fix PR #9264 (open) |
| 🟢 中等 | [#9257](https://github.com/AstrBotDevs/AstrBot/issues/9257) | 插话消息显示“思考中…”误导用户以为无效 | ❌ 暂无修复 PR |
| 🟢 中等 | [#7218](https://github.com/AstrBotDevs/AstrBot/issues/7218) [#7589](https://github.com/AstrBotDevs/AstrBot/issues/7589) | 知识库列表不显示 / Markdown/TXT 上传失败 | ❌ 长期未修复，今日有相关 PR #9246、#9245 (open) |

**长期稳定性质疑**：知识库相关问题已存在数月，[#7218](https://github.com/AstrBotDevs/AstrBot/issues/7218) 与 [#7589](https://github.com/AstrBotDevs/AstrBot/issues/7589) 仍为 Open 状态，影响用户正常使用 RAG 功能。

## 6. 功能请求与路线图信号

今日新提交的 Enhancement 多数围绕 **WebUI 细节优化** 与 **核心配置可配置化**，且已有对应 PR 被提交：

- **[上下文压缩阈值可配置化](https://github.com/AstrBotDevs/AstrBot/issues/9252)** → 对应 PR [#9261](https://github.com/AstrBotDevs/AstrBot/pull/9261) (open)，允许用户动态调整压缩触发比例，适配不同模型最大输出能力。
- **[Agent 执行过程中实时更新 Token 圆环](https://github.com/AstrBotDevs/AstrBot/issues/9250)** → 对应 PR [#9260](https://github.com/AstrBotDevs/AstrBot/pull/9260) (open)，使 multi-step agent run 中圆环每轮 LLM 调用后即刷新。
- **[Token 圆环显示生成预留空间](https://github.com/AstrBotDevs/AstrBot/issues/9251)** → 暂无对应 PR，但基于 #9250 与 #9260 可进一步扩展。
- **[支持隐藏 WebUI 侧栏菜单项](https://github.com/AstrBotDevs/AstrBot/issues/9265)** → 暂无对应 PR，期望参考 1Panel 的自定义能力。
- **[插件主动消息保存到对话历史](https://github.com/AstrBotDevs/AstrBot/issues/9240)** → 暂无对应 PR，来自插件作者的切实需求。
- **[为 Text Embeddings Inference (TEI) 添加 rerank provider](https://github.com/AstrBotDevs/AstrBot/issues/9266)** → 暂无对应 PR，HuggingFace TEI 用户的需求。
- **[Discord 适配器完善](https://github.com/AstrBotDevs/AstrBot/issues/9258)** → 提及已有 PR [#9125](https://github.com/AstrBotDevs/AstrBot/pull/9125) 待合并，支持中文斜杠指令与参数。

以上功能请求绝大多数来自同一贡献者 @Fronut 的提交，表明 **WebUI 与核心配置的可观测性、可配置性** 是当前路线图的主要方向，预计下一版本将纳入批量配置改进。

## 7. 用户反馈摘要

从 Issue 描述与评论中可提炼出以下典型用户痛点与诉求：

- **“最长等待了 20 分钟”**（[#9253](https://github.com/AstrBotDevs/AstrBot/issues/9253)）：刷新后消息卡在 follow-up 队列永远得不到回复，必须重启 AstrBot，严重影响使用体验。
- **“user message still there but assistant's reply disappeared”**（[#9249](https://github.com/AstrBotDevs/AstrBot/issues/9249)）：流式关闭时后台日志显示完整输出，但刷新后 ChatUI 只剩用户消息。
- **“圆环显示 280%，与实际上下文占用不符”**（[#9248](https://github.com/AstrBotDevs/AstrBot/issues/9248)）：Token 累积语义误导用户对上下文压力的判断。
- **“插话消息显示思考中…，总觉得没发出去”**（[#9257](https://github.com/AstrBotDevs/AstrBot/issues/9257)）：用户交互中的不必要误导，降低了对插话功能的信任。
- **“WebUI 完全不显示推送消息，LLM 也无法感知”**（[#9240](https://github.com/AstrBotDevs/AstrBot/issues/9240)）：插件开发者希望主动消息也能被记录到对话历史，以实现插件与 LLM 的上下文联动。
- **“Dashboard 看不到任何错误信息，只能看到‘下载失败’”**（[#9268](https://github.com/AstrBotDevs/AstrBot/issues/9268)、[#9269](https://github.com/AstrBotDevs/AstrBot/issues/9269)）：未处理的异常被 Starlette 拦截为纯文本，用户与开发者均无法定位问题。
- **“Knowledge base not found”**（[#7218](https://github.com/AstrBotDevs/AstrBot/issues/7218)）：后台知识库列表空白，但已选配置仍在，实际检索无结果，属于边缘但持续存在的功能性故障。

正面反馈方面，**人格导出/导入功能**（#4409）与 **撤回消息不回 bot**（#9142）的关闭获得了积极关注。此外，社区贡献者 @Fronut、@Last-emo-boy、@lxfight 等人在同一天内提交了 10+ 高质量 PR，体现了社区对项目发展的高度参与。

## 8. 待处理积压

以下为重点关注但尚未解决的长期 Issue 与待合并 PR：

- **知识库相关 Issues**（[#7218](https://github.com/AstrBotDevs/AstrBot/issues/7218)、[#7589](https://github.com/AstrBotDevs/AstrBot/issues/7589)）  
  创建于 3~4 月，至今仍为 Open，涉及知识库列表显示与文件上传失败，直接影响 RAG 功能的可用性。今日虽有相关 PR（如 [#9246](https://github.com/AstrBotDevs/AstrBot/pull/9246)）但尚未合并，建议维护者优先审阅。

- **预设对话批量导入**（[#6321](https://github.com/AstrBotDevs/AstrBot/issues/6321)）  
  3 月提出的 Enhancement，期望允许用户粘贴文本批量添加 Persona 示例对话，降低配置成本。暂无对应 PR，但同类功能（人格导出导入）今日刚合并，可参考实现。

- **Discord 适配器完善 PR**（[#9125](https://github.com/AstrBotDevs/AstrBot/pull/9125)）  
  为 Discord 适配器添加中文斜杠指令与参数支持，提交于 7 月初且尚未合并。对应 Issue [#9258](https://github.com/AstrBotDevs/AstrBot/issues/9258) 今日更新，建议尽快审阅以避免重复工作。

- **Token 圆环显示生成预留空间**（[#9251](https://github.com/AstrBotDevs/AstrBot/issues/9251)）  
  用户提出圆环应扣除模型最大输出预留，以避免上下文溢出。暂无 PR，但概念上可扩展 #9260 的工作，建议标记为后续迭代候选。

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*