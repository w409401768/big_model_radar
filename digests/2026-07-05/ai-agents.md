# OpenClaw 生态日报 2026-07-05

> Issues: 500 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-04 22:46 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 | 2026-07-05

---

## 1. 今日速览

OpenClaw 项目在 2026-07-04 展现出极高的维护强度，24 小时内同步更新了 500 条 Issues 与 500 条 PRs。尽管当日无新版本发布，但一系列重量级的 **Policy Doctor（策略医生）** 相关 PR 入库，标志着项目正系统性地从功能扩张阶段向企业级安全治理与自愈能力建设转型。社区的核心讨论仍高度集中在 **Agent 核心循环的可靠性**（消息泄漏、Session 状态丢失、子任务静默失败）与**安全边界加固**上。整体来看，虽然 Bug 歼灭战仍在激烈进行，但通过“策略即代码”和“通道修复攻势”的推进，项目的企业级成熟度正在显著提升。

---

## 2. 版本发布

无。

---

## 3. 项目进展

### 已合并

- **[#100054] fix(gateway): 按 Agent 读取用量缓存**  
  `@NianJiuZst` 修复了 Dashboard 在每次重连时重复读取 `.jsonl` 用量缓存、导致误报内存压力警告的问题。  
  https://github.com/openclaw/openclaw/pull/100054

### 大规模基础设施推进
- **Policy Doctor 自愈框架（`@giodl73-repo`）**  
  今日入库了一组共 6 个关于策略修复的 PR，组成了 `openclaw doctor --fix` 的核心逻辑：
  - `#99686` — 策略分类与修复元数据定义  
  - `#99690` / `#99700` — 自动缩小修复（工具拒绝、不安全网关配置、数据脱敏等）  
  - `#99720` — 通道入口修复（`groupPolicy`、`requireMention` 等）  
  - `#99731` — 网关 HTTP 端点禁止修复  
  - `#99776` — 审查类修复的预览模式  
  这是项目在可运维性上的一个里程碑，大幅降低了企业运维者执行安全合规的成本。  
  https://github.com/openclaw/openclaw/pull/99686

### 核心功能开发中

| PR | 描述 | 解决 Issue | 状态 |
|---|---|---|---|
| `#77127` | Write 工具追加模式 | `#40001` 数据丢失 | 审查中 |
| `#81185` | Exec 工具结果脱敏 | 安全加固 | 待合并 |
| `#100084` | Slack 流式响应自定义身份保留 | `#58737` | 待审查 |
| `#82895` | Slack 交互线程状态保留 | `#82886` | 待审查 |
| `#88992` | 消息工具模式滞留回复恢复 | `#85714` | 等待作者 |
| `#89038` | QQ 频道重连投递修复 | – | 待审查 |
| `#95885` | 防止重复压缩导致的 Session 挂起 | – | 待审查 |
| `#90259` | Session 轮转摘要承继 | – | 待审查 |
| `#100057` | 按 Agent 限定内存扫描范围 | – | 待审查 |
| `#98021` | Codex 运行时 Ultra 思维链支持 | – | 待审查 |
| `#99733` | Google Antigravity 认证桥接 | – | 待审查 |
| `#100029` | Crestodian CLI 循环 MCP 支持 | – | 等待作者 |
| `#100012` | 本地化 Windows netstat 检测 | `#99984` | 待审查 |

**小结：** 项目重心已明确转向 **稳定性**（数据追加、压缩防抖、通道投递可靠性）和 **企业治理**（策略自愈、成本缓存、Agent 级配额）。

---

## 4. 社区热点

### 讨论最热烈 / 反应最多

| Issue | 标题 | 评论数 | 👍 |
|---|---|---|---|
| `#25592` | 工具调用间文本泄漏至消息通道 | 33 | 1 |
| `#44925` | 子 Agent 完成信息静默丢失 | 20 | 1 |
| `#32473` | 控制面板要求 HTTPS（今日关闭） | 17 | 5 |
| `#22676` | Signal 守护进程重启竞态条件 | 17 | 0 |
| `#48003` | 干预模式无法中轮注入消息 | 14 | 3 |
| `#45740` | gh-issues 技能 Prompt 注入 | 14 | 1 |
| `#39604` | 请求开放内网访问 🤖 | 13 | 11 |

### 分析

- **信任危机是核心主题。** `#25592` 和 `#44925` 分别占据了交互层面（我看到不该看的）和系统层面（我看不到我该看的）两个极端。社区对 Agent 在执行过程中的“黑箱”行为感到不安。
- **`#39604`（请求内网权限）** 获得了当日最高的 👍 数量（11），这充分反映了开发者用户群体将其用于自动化内部设施（数据库、本地 API）的强烈意愿。
- **`#44905`（Discord 泄露内部轨迹）** 虽然评论数只有 10，但泄露 `NO_REPLY`、`to=functions` 等内部 JSON 是一个严重的安全事件，引发了广泛隐忧。

**链接汇总：**
- [#25592](https://github.com/openclaw/openclaw/issues/25592)
- [#44925](https://github.com/openclaw/openclaw/issues/44925)
- [#32473](https://github.com/openclaw/openclaw/issues/32473)
- [#39604](https://github.com/openclaw/openclaw/issues/39604)
- [#44905](https://github.com/openclaw/openclaw/issues/44905)

---

## 5. Bug 与稳定性

按严重程度排列，标注是否有修复 PR。

### 🔴 灾难级（Diamond Lobster）

| Issue | 简述 | 危害 | Fix PR |
|---|---|---|---|
| `#25592` | 工具调用间文本泄漏 | 安全、消息丢失 | ❌ |
| `#44925` | 子 Agent 完成静默丢失 | Session 状态、消息丢失 | ❌ |
| `#48003` | Steer 模式无法中轮注入 | Session 状态、消息丢失 | ✅ |
| `#43367` | 多 Agent 编排不稳定 | Session 状态、消息丢失 | ✅ |
| `#40001` | Write 工具缺少追加模式 | 数据丢失 | ✅ (#77127) |
| `#45740` | gh-issues 注入攻击 | 安全 | ❌ |
| `#22676` | Signal 重启竞态条件 | 消息丢失、崩溃循环 | ✅ |
| `#43747` | 内存管理混乱 | Session 状态 | ❌ |
| `#99241` | 工具输出渲染为图片附件 | Agent 不可读 | ❌ |

### 🟠 高风险（Platinum Hermit）

| Issue | 简述 | 危害 |
|---|---|---|
| `#49876` | Cron 会话工具失败时产生幻觉输出 | 安全 / 信任 |
| `#45494` | Cron 遇到 API 错误不快速失败 | 可用性/卡死 |
| `#43661` | 压缩超时导致重复消息发送 | Session 状态、消息丢失 |
| `#43996` | Sandbox 容器 `no-new-privileges` 退出 | 可用性、安全 |
| `#47975` | 子 Agent Session 残留导致主 Session 无响应 | 可用性 |
| `#44905` | Discord 泄露内部工具调用轨迹 | 安全、消息丢失 |
| `#49603` | 孤儿锁在 Gateway 重启时未清理 | 消息丢失、崩溃循环 |

### 回归 / 待关注

- **`#38327`** — Google Vertex 模型 `Cannot convert undefined or null to object`（回归）
- **`#45765`** — `OPENCLAW_HOME` 设置为 `~/.openclaw` 时产生嵌套目录（回归）
- **`#45314`** — 提前中止时响应模板变量未填充
- **`#46252`** — 成本 Dashboard 遗漏 `.jsonl.reset.` 归档文件，严重少报消耗
- **`#50490`** — 飞书群聊 `/activation mention` 模式切换无效（回归）

**总结：** 今日 Bug 的显著特征是 **Session 层可靠性**和**数据边界安全**的问题占主导。好消息是多个致命的 Diamond Lobster 和 Platinum Hermit 都有配套的 Fix PR 在同步推进。

---

## 6. 功能请求与路线图信号

### 社区强需求

| Issue | 描述 | 点赞数 | 纳入下一版本可能性 |
|---|---|---|---|
| `#39604` | 内网访问控制（`allowPrivateNetwork`） | 11 | **高**（企业刚需） |
| `#42840` | Control UI 添加 MathJax/LaTeX 支持 | 8 | **中**（社区呼声高） |
| `#20786` | Telegram Business Bot 支持 | 6 | **中**（渠道扩展） |
| `#7722` | 文件系统沙箱配置 | 4 | **高**（安全加固核心） |
| `#22358` | 子 Agent 执行后 Hook | – | **高**（可观测性基础设施） |
| `#42475` | 按 Agent 成本预算 | – | **高**（运维刚需） |
| `#50739` | 系统事件旁路队列模式 | – | **高**（告警可靠性） |
| `#22438` | 分层 Bootstrap 加载 | – | **中**（性能优化） |
| `#40418` | Session 重置时自动保留/合成记忆 | – | **中**（用户体验提升） |

### 路线图分析（基于当前 PR 动态）

- **短期（下个 Release）：** 核心数据安全（Append Mode `#77127`）、通道稳定性（Slack/Discord/QQ 修复集锦）、Policy Doctor 初版。
- **中期（Q3）：** 安全边界加固（Sandbox `#7722`、内网控制 `#39604`）、成本治理（`#42475`）、核心 Agent 可靠性重构（Session State）。
- **长期：** 分布式运行时（`#42026`）、Codex Ultra 推理（`#98021`）、多 Agent 协作增强（`#35203`）。

---

## 7. 用户反馈摘要

### 核心痛点

1.  **信任赤字：**  
   > "Subagent task orchestration has multiple failure modes where *results are silently lost*" — `#44925`  
   > "Cron sessions deliver hallucinated output instead of failing cleanly" — `#49876`  
   用户不敢完全放手让 Agent 独立执行任务，害怕后台悄悄“假性完成”。

2.  **安全焦虑：**  
   用户对 `#25592`（文本泄漏）、`#44905`（Discord 内部轨迹暴露）、`#45740`（Issue Body 注入）感到不安。缺乏内网访问控制（`#39604`）也阻碍了 Agent 在更敏感的生产网络中的应用。

3.  **部署摩擦：**  
   - 控制面板 HTTPS 要求（`#32473`）阻止了 VPS 用户的快速上手。  
   - Sandbox 容器启动失败（`#43996`）让首次体验直接中断。  
   - `OPENCLAW_HOME` 嵌套目录（`#45765`）导致配置混乱。

### 使用场景特征

- **多 Agent 编排** 正成为主流用例，但 `#43367` 报告的同时添加 Agent 会导致配置覆盖，暴露了 CLI 在并发场景下的脆弱性。
- **Cron / 自动化** 用户群体庞大，他们期望严格的失败模式（快速失败而非幻觉/超时），这反映了从“实验”到“生产”的转变压力。

### 社区成熟度

- 用户普遍提供**高度详细的可重现步骤**（`source-repro`），配合技术分析甚至截图（`proof: 📸 screenshot`）。
- 多个 RFC 帖子（`#42026`、`#48874`、`#35203`）拥有深度讨论，显示社区中具备架构设计能力的高级用户已十分活跃。

---

## 8. 待处理积压

### 最需关注的灾难级问题（无修复 PR，长期开放）

| Issue | 开放时间 | 评论数 | 描述 | 风险等级 |
|---|---|---|---|---|
| `#25592` | 2026-02-24 | 33 | 工具调用间文本泄漏 | 🔴 极度严重 |
| `#44925` | 2026-03-13 | 20 | 子 Agent 完成信息丢失 | 🔴 极度严重 |
| `#22676` | 2026-02-21 | 17 | Signal 守护进程重启竞态条件 | 🔴 极度严重 |
| `#45740` | 2026-03-14 | 14 | gh-issues 技能 Prompt 注入 | 🔴 安全红线 |
| `#7722` | 2026-02-03 | 9 | 文件系统沙箱配置（最老的高优 Feature） | 🔴 安全红线 |

### 堵塞 / 待审核的 PR

| PR | 创建时间 | 描述 | 阻塞原因 |
|---|---|---|---|
| `#51762` | 2026-03-21 | 修复默认 Agent 配置未在所有路径生效 | `status: 📣 needs proof` |
| `#100102` | 2026-07-04 | 修复 Debian 安装脚本 `pacman` 命令冲突 | `status: 📣 needs proof` |
| `#99776` | 2026-07-04 | Policy Doctor 审查类网关修复预览 | `status: ⏳ waiting on author` |

**建议：** `#25592` 和 `#44925` 已开放超过 4 个月，讨论度极高但无 Fix PR，建议维护者集中资源分配安全审查，或至少发布正式的架构决策（ADR）以安抚社区。`#51762` 作为一项配置修复悬而未决已达 3 个半月，建议尽快纳入小版本修复。

---

## 横向生态对比

好的，以下是根据您提供的五份项目日报，经过系统化提炼与对比后生成的横向分析报告。报告聚焦于业界关心的架构选择、社区成熟度与共同痛点，旨在为技术决策者和开发者提供参考视角。

---

## 个人 AI 智能体开源生态横向对比分析报告 | 2026-07-05

### 1. 生态全景

个人 AI 助手与自主智能体开源生态正经历从“功能堆叠”到“生产成熟度”的剧烈转型。当前，项目普遍面临着信任赤字——内部轨迹泄漏、子任务静默失败、状态丢失等“黑箱”行为已成为社区首要焦虑点，促使安全治理、数据边界与可观测性成为各项目的优先投入方向。同时，长期记忆与多 Agent 协作等基础设施级需求从少数项目蔓延至整个生态，标志着行业已开始为复杂的持久化交互场景做准备。此外，Provider 兼容性、部署摩擦和成本治理等问题正要求项目在灵活性与标准化之间做出更成熟的平衡。

---

### 2. 各项目活跃度对比

| 项目 | 24h Issues 更新 | 24h PRs 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500（含已有活动） | 500（含已有活动） | 无 | **高强度维护**；重心从功能转向企业治理，Bug 歼灭与安全加固并行，库稳定性快速提升 |
| **Hermes-Agent** | 239（新开 209 / 关闭 30） | 500（合并 132 / 待合 368） | 无 | **极高活跃度**，社区参与踊跃，关键修复大量合入；但存量 PR 积压严重，审查需加速 |
| **Zeroclaw** | 50（全部新活动） | 50（仅合并 2） | 无（v0.8.3 冲刺） | **高提交但审查瓶颈**；新功能如 Goal Mode 体量大，缺乏及时合并将引发分支分歧 |
| **QwenPaw** | 10（活跃 8 / 关闭 2） | 3（全待合并） | 无 | **中低活跃**，正处于 2.0 质量攻坚；核心功能记忆与上下文存在严重回归，修复待合入 |
| **PicoClaw** | 4（更新） | 7（合并 1 / 待合 6） | 无 | **偏低**；多 Agent 路由 Bug 已修复，但社区贡献长期无审核，Android 崩溃问题未回应 |

*注：OpenClaw 和 Hermes-Agent 的绝对数字远超其他项目，反映其社区规模与维护团队响应能力已处于生态头部。*

---

### 3. OpenClaw 在生态中的定位

OpenClaw 是当前生态中**维护最密集、企业治理最积极**的项目，以其每日 500+ Issue/PR 的处理量稳居第一阵营。与其主要竞品 Hermes-Agent 相比，OpenClaw 的技术路线更强调 **“策略即代码”与自愈能力**：Policy Doctor 框架能让运维者以代码方式定义安全基线并自动修复违规配置，这直接瞄准了中大型组织的合规需求。同时，其对短信（Signal）、IM（Slack/Discord/QQ/Telegram）等通道的全覆盖及通道级修复优先级，使其在渠道可靠性上极具竞争力。

相较 Zeroclaw 的流程驱动（SOP/目标模式）和 QwenPaw 的模型强绑定（与 Qwen 深度集成），OpenClaw 更偏向 **通用 Agent 运行时 + 企业安全治理**，定位更接近企业级内部 Copilot 基座。社区规模庞大，贡献者多样化，但内部沟通成本也更高——“信任赤字 ”（如 #25592 文本泄漏、#44925 子 Agent 静默丢失）成为长期热点，暴露了其核心循环在高并发下的设计下沉不足。

---

### 4. 共同关注的技术方向

以下是至少出现在 3 个活跃项目中的关键技术趋势：

- **长期记忆与会话持久化**  
  OpenClaw（#90259 摘要继承、#40418 记忆合成）、QwenPaw（#5775/PR#5777 自动记忆状态管理）、Hermes（#8457 持久会话+RAG）、Zeroclaw（#8685 SQLite 目标存储）。各项目均在构建超越单轮对话的持久化机制，但实现路径各异（滚动压缩、自动记忆、目标存储），表明该领域尚无标准答案，是下一阶段竞争焦点。

- **Provider 兼容性与容错降级**  
  Hermes (#58502/58451/58374)、QwenPaw (PR#5597 LLM fallback)、Zeroclaw (#8675 参数格式校验)、OpenClaw (#99733 认证桥接)。模型接口碎片化（非标准 OpenAI 兼容、工具调用差异、数字类型边界）迫使项目投入大量精力到 Provider 适配层，直接关系到用户体验的“即插即用”程度。

- **安全边界与数据泄漏防护**  
  OpenClaw (#25592 文本泄漏、#7722 沙箱配置)、Hermes (GHSA-visual sandbox escape、#25083 不可变技能)、Zeroclaw (#8424 .ignore 文件保护)、PicoClaw (Matrix 加密库替换 #3088)。社区对 Agent 内部数据可见性（不该看的和该看不到的）高度敏感，正推动从网络边界防御延伸到运行时数据访问控制。

- **多 Agent/多步骤编排可靠性**  
  OpenClaw (#44925 子 Agent 静默丢失、#43367 配置覆盖)、Zeroclaw (#8687 Goal Mode 委托边界)、Hermes (#14853 多实例 Discord 协作)、PicoClaw (#3224 路由清除修复)。编排不再是简单 fork-join，如何在失败、丢消息、并发写等场景下保持状态一致性，是共同面对的工程难题。

---

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes-Agent | Zeroclaw | QwenPaw | PicoClaw |
|---|---|---|---|---|---|
| **功能侧重** | 企业治理、通道可靠、策略自愈 | Provider 广度、社区创新、视觉管道 | 可视化流程（SOP）、多步目标（Goal Mode） | 与 Qwen 模型深度集成、对话记忆 | 多平台客户端（Android/Mac/CLI） |
| **目标用户** | 企业运维、安全合规团队 | 开发者、自托管爱好者、多模型用户 | 工作流设计师、自动化工程师 | Qwen 模型用户、阿里云生态 | 个人移动用户、跨平台使用者 |
| **核心语言/存储** | Go（推测） + 高性能网关 | Python + 插件化 | Rust + SQLite | Python + 阿里云 | Go（推测） + 轻量化 |
| **社区特征** | 高贡献量大，Issue 可复现率高，信任讨论深刻 | 最庞杂，PR 体量巨大，但审查滞后 | 核心团队快速迭代，外部贡献受审查带宽限制 | 反馈密集，但活跃度偏低 | 维护乏力，贡献滞留，Android 响应缺失 |
| **创新前沿** | Policy Doctor 自愈框架 | Context Governor、语音唤醒、kanban 生命周期钩子 | 目标模式持久化、SOP 可视化编辑 | Auto-memory 状态管理、LLM fallback UI | 多 Agent 路由清除、Agent 独立配置 |

---

### 6. 社区热度与成熟度

根据 Issue/PR 处理量、社区讨论深度及版本迭代质量，可以将五个项目分为三个梯队：

- **第一梯队：快速迭代与技术领先**  
  **Hermes-Agent** 与 **OpenClaw** 保持极高的社区热度，每日均有数百量级的交互，且合并速度领先（Hermes 合入 132 个 PR，OpenClaw 有 6 个 Policy Doctor PR 等大型合入）。两者已具备企业级雏形，但 Hermes 更偏社区功能多元化，OpenClaw 更偏系统治理收敛。

- **第二梯队：创新活跃但存在阻塞**  
  **Zeroclaw** 提交质量高（Goal Mode、SOP 编辑器均为重量级功能），但审查能力远落后于提交速度，大量 `size:XL` 和 `risk:high` 的 PR 积压，若不尽快组织集中合并冲刺，将面临严重的合并冲突与迭代降速。

- **第三梯队：质量巩固与合规维护**  
  **QwenPaw** 与 **PicoClaw** 活跃度处于低位，且集中于 Bug 修复与技术债务清理。QwenPaw 2.0 处于功能补完期，社区期待高但现存回归严重；PicoClaw 则面临 Android 完全不可用的极端投诉，社区贡献长期无人审查，健康度堪忧。

---

### 7. 值得关注的趋势信号

- **“可信执行”已成为最低期望**：社区不再容忍 Agent 在后台静默产生幻觉输出或丢消息（OpenClaw #49876、Zeroclaw #8695）。开发者对子任务回执的完整性、失败快速通知提出了刚性要求，这推动项目在 Core Loop 层面引入持久化事务日志或多阶段确认。

- **多 Agent 协作从构想走向真实工作负载**：OpenClaw 的 #43367 并发冲突、Hermes 的 #14853 频道历史隔离、Zeroclaw 的委托边界 #8688，都在试图解答“如何让多个 Agent 安全地共享信息且不产生冲突”。这一趋势将带动访问控制列表、活动拓扑和编排 DAG 等基础设施需求的增长。

- **社区贡献者的“审查饥渴”正在成为项目瓶颈**：Zeroclaw（48 个 PR 待合）和 PicoClaw（4 个 PR 停滞 8 天）的案例显示，高增长项目若无法匹配维护者审查带宽，将导致贡献者流失和分支分歧扩大。预计下半年会看到更多项目引入自动合并机器人或分层维护制度。

- **模型接口碎片化催生 Provider 中间层竞争**：Hermes、QwenPaw、Zeroclaw 均投入 PR 解决整数类型、空 `tool_choice`、`num_ctx` 固化和认证细节等 Provider 兼容性问题。这预示着未来可能出现独立的“Provider 网关中间件”或标准化规范（如 Model Context Protocol 的演进竞争），以降低每个项目重复适配的成本。

- **安全左移：从“按需审计”到“设计时防护”**：OpenClaw 的 Policy Doctor、Zeroclaw 的 .ignore 文件机制、Hermes 的不可变技能，共同指向一个方向：**安全策略不再作为事后检查，而是嵌入 Agent 配置链和技能执行前置校验**。这将是企业推广 Agent 自主化的重要前提。

---

**结语**：今日的生态图景显示，个人 AI 智能体正越过“能跑就行”的早期阶段，进入以可靠性、安全性、可运维性为核心的成熟度竞赛。头部项目在治理流程和工程实践上已逐步拉开差距，而新兴项目若不能在审查效率和核心循环稳定性上做出突破，将很难维持用户信任与社区动力。对于技术选型者而言，建议优先评估项目在多步编排失败模式下的可观察性策略，以及 Provider 故障时的降级明晰程度——这些将直接决定生产环境的真实可用性。

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是为您生成的 Zeroclaw 项目动态日报。

---

# Zeroclaw 项目动态日报 | 2026-07-05

## 今日速览

项目目前处于 **v0.8.3 开发冲刺的高峰期**，社区贡献和代码提交异常活跃。过去 24 小时内，共处理了 **50 条 Issue 和 50 条 PR**，其中包含大量由核心贡献者（@vrurg, @singlerider, @Audacity88）提交的 **大型功能 PR**，尤其是“目标模式”的全面落地。**需要注意的是，尽管提交量巨大，但当日仅合并/关闭了 2 个 PR，其余 48 个 PR 仍处于待审查状态**，代码审查带宽已成为制约项目推进速度的核心瓶颈。在稳定性方面，Provider 和 Runtime 依然存在多个 S1 级别的阻塞性 Bug，但团队响应修复速度极快。

## 版本发布
无新版本发布。

## 项目进展

> 尽管今日合并数量极少（仅 2 个），但提交的巨型 PR 标志着项目在架构和功能上迈出了巨大一步。

- **目标模式 (Goal Mode) 全线推进**： @vrurg 提交了一整套由跟踪器 #8681 协调的 PR 链，将 Zeroclaw 从单轮对话推向多步骤长期任务执行：
    - **#8687**: 添加 Rust 侧目标控制器与验证器。
    - **#8685**: 添加基于 SQLite 的持久化目标任务存储与恢复机制。
    - **#8689**: 实现 `/goal` 命令在终端渠道的受理。
    - **#8688**: 添加受信目标工具及委托边界，确保 Agent 在框架内安全执行。
- **SOP 可视化编辑器落地**： @singlerider 提交了巨型 PR **#8590**，带来了直观的 SOP 可视化创作工具、渠道汇合 (channel fan-in) 机制以及全面的测试覆盖，显著降低了 SOP 的使用门槛。
- **Git 渠道扩展**： PR **#8611** 为 Git 锻造渠道新增了 Gitea/Forgejo 支持，增强了自托管场景的兼容性。
- **快速修复**： 针对昨日报告的 `skill-review` 导致守护进程 SIGSEGV 的严重 Bug，PR **#8680** 已被迅速提交，目前待合并。

## 社区热点

- **治理与流程讨论**： **#6808** (RFC: Work Lanes) 以 13 条评论持续火热。社区对如何自动化标签、清理看板、优化工作流非常关心，这表明贡献者队伍正在扩大，对规范化协作的需求日益迫切。
- **安全权限诉求强烈**： **#8424** (RFC: .ignore File Mechanism) 获得 7 条评论。用户普遍对 AI Agent 能够随意读取工作区内的敏感文件（凭证、配置、.env）感到不安，希望引入类 `.gitignore` 的防御机制。
- **目标模式透明度高**： **#8681** (Goal Mode 跟踪器) 尽管是技术协调 Issue，但获得了核心粉丝的高度关注，评论集中在功能拆解策略和 API 设计上。

## Bug 与稳定性

**严重等级 S1（工作流阻塞）：**
- **#8675**: [Provider] 原生工具调用参数格式错误未经校验直接发送给 Provider，导致 Provider 400 错误和无响应。*当前无 Fix PR，影响所有使用 OpenAI 兼容格式的 Provider*。
- **#8654**: [Runtime] 技能审查 (skill-review) 分支因切片越界导致 panic (SIGSEGV)，使 Agent 进程崩溃。*已有 Fix PR #8680 待合并*。
- **#7862**: [Provider] OpenAI 兼容 Provider 在工具列表为空时仍发送 `tool_choice`，被 vLLM 等严格 Provider 拒绝。*状态：开放*。

**中等等级 S2（功能降级）：**
- **#8695**: [Cron] `uses_memory` 配置无效，定时任务仍错误加载记忆上下文。*已有 Fix PR #8676 待合并*。
- **#8678**: [SOP] `advance_step` 缺少运行状态守卫，驾驶员可绕过审批关卡直接推进流程，存在审批完整性风险。
- **#8615**: [Provider] 兼容 Provider 无条件剥离 `<think>` 标签，导致回复内容被静默截断，用户难以察觉。
- **#8664**: [ZeroCode] 代码块复制功能错误包含了 Markdown 围栏（```），影响开发者日常使用。

**已修复/关闭的 Bug：** 团队清理了 #8193 (MCP 工具不同步)、#6361 (上下文压缩工具丢失) 等多个旧版顽固 Bug，展现了强大的排查能力。

## 功能请求与路线图信号

- **核心路线图（高确定性）**：
    - **目标模式** 全线即将合入 (#8687, #8685, #8689, #8688)。
    - **SOP 增强序列**：除了编辑器 (#8590)，社区提出了增强路由规则（#8719）和增加更多文档示例（#8587）的需求，极有可能被纳入 v0.8.4 计划。
    - **可观测性**：Turn 级 OTel 追踪 (#6641)、结构化登录事件 (#8622) 等正在稳步推进。

- **社区呼声较强的新需求**：
    - **#8424**: **工作区文件保护机制**.ignore。这是在当前 Agent 自主性增强下，用户对数据安全的最强诉求，建议提升优先级。
    - **#7497**: **OCI 注册表作为插件分发机制**。这是 WASM 插件生态的架构级改进，虽然当前优先级为 P3，但长期看是构建真正 Plugin Marketplace 的基石。
    - **#8720**: 为特定模型 (Bedrock Nova 2 Lite) 的配置文件增加开关以禁用缓存功能。这反映了模型碎片化带来的配置灵活性挑战。

## 用户反馈摘要

- **痛点直击**：
    1.  **工具链体验割裂**：MCP 工具在 TUI 中不可见 (#8193) 和 ZeroCode 日志详情无法展开 (#8646) 的反馈表明，用户对客户端界面的一致性和信息完整性要求极高。
    2.  **配置变更非即时生效**：Memory 嵌入不刷新 Provider 配置 (#8359)、Cron 忽略内存开关 (#8695) 等问题，显示出动态配置生效机制的缺失，导致用户产生挫败感。
    3.  **文档与实现脱节**：SOP 审计功能在文档中大力宣传但实际从未写入 (#6689) 的发现，引发了用户对文档可靠性的质疑。
- **正面评价**：
    - 社区角色对 RFC 治理模式高度认可，愿意花费精力撰写详细的 RFC（如 #8424 和 #6808），说明项目治理透明，用户参与度高。
    - @Audacity88, @vrurg, @singlerider 等核心开发者在 Issue 中的快速响应和详细解释，让用户感觉“被听见”，维护了社区的高信任度。

## 待处理积压

- **悬而未决的代码审查瓶颈（最高优先级）**：当前共有 **48 个 PR** 处于待合并状态，其中包含多达 6 个 `size:XL` 和超 10 个 `risk:high` 的巨型 PR。这是项目当前面临的最大风险。如果合并速度跟不上提交速度，大规模的代码分叉将导致严重的合并冲突和发布延期。**建议维护者团队安排一次针对 v0.8.3 特性分支的集中合并冲刺。**
- **长期未推进的 Accepted 功能**：
    - **#4832**：禁用 LeakDetector 高熵令牌编辑。功能虽小，但影响所有用户日常使用。自 3 月 `status:accepted` 以来无实质进展。
    - **#6808**：工作流治理 RFC。自 5 月提出，虽一直在更新，但缺乏最终的落地执行计划。
- **稳定性回归信号**：Provider 相关的 Bug（#8675, #8615, #7862）和 Runtime 的恐慌（#8654）在短时间内密集爆发，建议在 v0.8.3 发布前，组织一次针对“Provider 消息序列化”和“Agent 主循环”的专项回归测试。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-07-05

**分析师评估：** 数据驱动，客观专业，突出项目健康度。

---

## 1. 今日速览

过去 24 小时内，PicoClaw 项目活跃度处于**中等水平**，共更新 4 个 Issues 和 7 个 PRs，无新版本发布。项目取得了一项重要的正向进展：一个破坏多 Agent 会话管理的核心 Bug 被成功修复并合入主线（#3224），显著提升了 Agent 路由系统的健壮性。但在另一方面，一项针对 Windows 路径的测试因引入编译错误被迫回滚（#3221），提示跨平台兼容性测试需要更严格的 CI 审核。社区层面，Android 平台完全不可用（#3182）以及 Matrix 加密库替换的高优诉求（#3088）依然是悬而未决的痛点。此外，多项高质量的社区维护 PR 陷入停滞状态，建议维护者加快审核节奏。

---

## 2. 版本发布

**无变化。**

---

## 3. 项目进展

### ✅ 已合并 / 已关闭（重要）

- **Agent 会话修复（高优 Bug 修复）**
  **[#3224 fix(agent): clear routed agent session](https://github.com/sipeed/picoclaw/pull/3224)**
  这是今日最有价值的合并。修复了一个在多个 Agent 同时启用时，用户向非默认 Agent 发送 `/clear` 后错误清除了默认 Agent 会话上下文的严重逻辑错误。该修复直接提升了多 Agent 工作流场景的可用性。

- **编译紧急回滚**
  **[#3221 Revert "test: cover sandbox fs Windows path handling"](https://github.com/sipeed/picoclaw/pull/3221)**
  由于之前合入的 Windows 沙箱路径测试在 `pkg/providers/openai_compat/provider.go` 中引入了 `log` 导入错误，导致主线代码无法编译。该回滚保证了主线代码的稳定，但也意味着跨平台测试覆盖暂时退步。

### 🔄 正在活跃推动（待合并 / 开放中）

- **Agent 差异化配置功能（新功能）**
  **[#3225 Support agent-specific runtime overrides](https://github.com/sipeed/picoclaw/pull/3225)**
  该 PR 允许用户在配置中为每个 Agent 独立覆盖 `max_tokens`、汇总阈值等运行时参数。这是社区长期呼吁的灵活性提升，代码已通过本地编译测试，具有较高的合并优先级。

---

## 4. 社区热点

- **最强呼声：安全合规与功能进化**
  **[#3088 [Feature] use vodozemac instead of libolm](https://github.com/sipeed/picoclaw/issues/3088)**
  **指标：** 👍 2 | 💬 4 | 标签: `priority: high`, `help wanted`, `stale`
  **分析：** 这是目前项目标签中优先级最高的议题。libolm 已被宣告不安全且不再维护，社区强烈要求迁移至官方替代品 Vodozemac。虽然该 Issue 因长期未推进变为 `stale`，但昨日仍有新评论刷新，说明用户始终在关注。这是项目在 Matrix 通道安全合规上必须正视的技术债务。

- **最紧急投诉：Android 平台完全阻塞**
  **[#3182 [BUG] Android version](https://github.com/sipeed/picoclaw/issues/3182)**
  **指标：** 💬 2
  **分析：** 用户 @Monessem 反馈在已授予全部权限的情况下，服务仍无法启动，且路径配置选项失效。这是当前直接影响用户使用的最高危 Bug，尽管评论数不高，但代表了移动端用户基数的核心痛点。

- **争议与反思：测试回滚**
  **[#3221 Revert "test: cover sandbox fs Windows path handling"](https://github.com/sipeed/picoclaw/pull/3221)**
  社区对此次回滚保持关注，因为暴露出项目在合并跨平台改动时缺乏充分的集成测试环境验证。

---

## 5. Bug 与稳定性（按严重程度排列）

| 严重程度 | Issue / PR | 描述 | 是否有 Fix PR |
|---|---|---|---|
| **严重 - 阻塞** | [#3182](https://github.com/sipeed/picoclaw/issues/3182) | Android 用户完全无法启动服务，App 崩溃。 | ❌ 无 (等待官方复现) |
| **严重 - 功能性** | [#3194](https://github.com/sipeed/picoclaw/issues/3194) | 未启用 E2EE 加密时，收到加密 Matrix 消息导致异常处理流程。 | ❌ 无 (需要判断是否为使用问题或 Bug) |
| **中等 - 已修复** | [#3224](https://github.com/sipeed/picoclaw/pull/3224) | 多 Agent 路由下 `/clear` 命令错乱 | ✅ 已合并主线 |
| **低 - 已回滚** | [#3221](https://github.com/sipeed/picoclaw/pull/3221) | Windows 路径测试导致编译错误 | ✅ 已回滚（修复稳定性） |
| **低 - 已关闭** | [#3150](https://github.com/sipeed/picoclaw/issues/3150) | 模型“失忆”Bug（可能因热加载或上下文溢出，长期未复现被标记为 Stale 后自动关闭） | 🔒 已关闭 (Stale) |

---

## 6. 功能请求与路线图信号

### 🔜 极有可能纳入下一版本
- **Agent 运行时参数覆盖**（PR #3225）：用户可对每个 Agent 单独设置 `max_tokens`、汇总阈值。该 PR 代码已就绪，只要通过 Review 即可合入。
- **国际化翻译同步**（PR #3190）：补充了 `bn-in`（印度语）和 `cs`（捷克语）的缺失键值，提升项目本地化完整性。

### 🗺️ 路线图上必须重视的信号
- **Vodozemac 加密库替换**（Issue #3088）：该项目不应继续留在 `stale` 状态。涉及 Matrix 模块的深度重构与编译选项调整，建议维护者尽快指定负责人或明确 Roadmap 时间线。
- **Docker 基础镜像安全升级**（PR #3192）：将 Alpine 从 3.21 升级至 3.23，属于常规安全维护，应尽快合入。

---

## 7. 用户反馈摘要

**痛点与不满：**
- **移动端体验极度恶化**：Android 用户 @Monessem 通过 Issue #3182 展示了完整的崩溃日志和截图，表示应用完全无法进入主界面。这可能是由于新版对 Android 沙箱或存储权限的处理出现了回归。
- **加密功能边界模糊**：用户 @Damian-o2 在 Issue #3194 中遇到 “crypto is not enabled” 的报错，但服务端却推送了加密消息。这暴露了 Matrix 通道在加密配置开启/关闭切换时，缺乏对异常数据的容错处理。
- **社区贡献反馈延迟**：贡献者 @chengzhichao-xydt 在一天内集中提交了 4 个高质量 PR（#3189 ~ #3192），全部是低风险、高价值的代码维护优化，但至今 8 天无人审核进入 `stale` 状态。这反映出当前维护者审查带宽可能存在瓶颈，有挫伤社区积极性的风险。

**满意与认可：**
- 开发组对 Agent 上下文的修复（#3224）非常及时，解决了多 Agent 重度用户的核心困惑。
- 用户对 Agent 个性化配置的开放表示欢迎（#3225），认为这是项目走向成熟的重要一步。

---

## 8. 待处理积压（提醒维护者关注）

以下为长期未响应或停滞的重要议题与 PR，建议项目维护团队优先介入：

1. **[安全 Debt - 严重超期]** **[#3088] 使用 Vodozemac 取代 libolm**
    - 创建 26 天，持续 `stale`。项目在 Matrix 安全合规性的最大隐患，必须打破停滞。
    - **链接：** https://github.com/sipeed/picoclaw/issues/3088

2. **[平台支持 - 紧急]** **[#3182] Android 版本 Bug**
    - 创建 9 天，无官方回复。移动端是 AI 助手的重要场景，请尽快复现问题或与用户沟通。
    - **链接：** https://github.com/sipeed/picoclaw/issues/3182

3. **[功能异常 - 待确认]** **[#3194] 收到加密消息但 crypto 未启用**
    - 创建 8 天，评论数 1。需要维护者确认是否是已知 Bug 还是配置使用问题。
    - **链接：** https://github.com/sipeed/picoclaw/issues/3194

4. **[社区维护 - 积压堵塞]** **[#3189] ~ [#3192] 四项维护性 PR**
    - 全部由 @chengzhichao-xydt 提交，停滞 8 天。内容涉及：
      - [#3189](https://github.com/sipeed/picoclaw/pull/3189): LINE 通道 `resp.Body.Close` 错误处理优化
      - [#3190](https://github.com/sipeed/picoclaw/pull/3190): 多语言翻译同步
      - [#3191](https://github.com/sipeed/picoclaw/pull/3191): `.gitignore` 配置清理
      - [#3192](https://github.com/sipeed/picoclaw/pull/3192): Docker 基础镜像升级至 Alpine 3.23
    - **建议：** 此类低风险、标准化的维护性 PR 应设立定期审查机制，避免社区贡献石沉大海。

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 **2026-07-05 QwenPaw 项目动态日报**。

---

## QwenPaw 项目日报 — 2026-07-05

### 1. 今日速览

过去 24 小时内，项目保持中等活跃度，社区围绕 **稳定性** 和 **2.0 版本质量** 反馈集中。共产生 **10 条 Issue 更新**（其中新开/活跃 8 条，已关闭 2 条），**3 条 PR 更新**（全部处于待合并状态），无新版本发布。多个关于 **记忆模块异常**、**上下文丢失**、**渠道兼容性** 的 bug 被详细报告，表明 2.0 版本在复杂场景下仍有待打磨。积极信号是两项关键功能（LLM 故障切换、记忆状态管理）的 PR 已进入审查，项目正针对社区痛点进行修补。

---

### 2. 版本发布

无（当日无新 Release）。

---

### 3. 项目进展

当日**无 PR 被合并**，但三项重大功能/修复 PR 处于开放待合并阶段，代表了项目近期的开发重心：

- **[PR #5777] feat(memory): add auto-memory turn state management**  
  专门针对 #5775 报告的记忆调度失效问题，在 middleware 中引入基于会话的自动记忆状态管理，避免因每次请求重建 Agent 导致状态丢失。[@jinliyl](https://github.com/jinliyl)

- **[PR #5598] feat(console): add LLM fallback configuration UI for agent and global models page**  
  与 #5597 配套，在控制台 Models 设置页添加了 LLM 故障切换的开启/关闭、候选模型列表编排、拖拽排序等 UI。[@yaozy2020](https://github.com/yaozy2020)

- **[PR #5597] feat(backend): per-agent and global LLM model fallback with safe retry boundaries**  
  为 LLM 调用实现模型级故障切换机制：当主模型重试耗尽后自动轮换至备用模型列表，避免因单点模型故障导致服务中断。[@yaozy2020](https://github.com/yaozy2020)  

这三项 PR 如果合并，将显著提升项目的 **记忆稳定性** 和 **LLM 调用容错能力**，特别是 #5597/#5598 构成的 fallback 机制是社区长期呼唤的功能。

---

### 4. 社区热点

| Issue/PR | 类型 | 评论数 | 热度原因 |
|----------|------|--------|----------|
| [#2865](https://github.com/agentscope-ai/QwenPaw/issues/2865) | 功能请求 | 4 (最高) | 讨论自定义 Agent 名称与头像，用户对个性化交互有强烈需求，自 4 月提出以来持续获得关注 |
| [#5775](https://github.com/agentscope-ai/QwenPaw/issues/5775) | bug | 2 | Auto-memory 功能完全不触发，影响 2.0b3 用户的记忆持久化，是本次更新中最影响核心使用的 bug |
| [#5770](https://github.com/agentscope-ai/QwenPaw/issues/5770) | 讨论 | 2 | 用户表达对 2.0 正式版的期待与鼓励，反映社区对项目方向的支持 |

- **#2865 诉求分析**：用户希望能在聊天界面显示自定义 Agent 名称，并通过 URL 设置自定义头像，而非仅使用系统预设。这指向 **个性化 Agent 交互** 的普遍需求，是提升沉浸感的关键特性。
- **#5775 诉求分析**：用户 `howyoungchen` 详细描述了 `auto_memory_interval > 1` 时记忆永不触发的根因——`MemoryMiddleware` 状态在每次请求重建 Agent 后丢失。该问题直接导致 2.0 的“大记忆”功能不可用，是优先级极高的回归。

---

### 5. Bug 与稳定性

当日共报告 **7 个 Bug**（含 1 个已关闭），按严重程度排列如下：

| # | 标题 | 严重性 | 影响版本 | 症状概要 | 是否有关联 PR |
|---|------|--------|----------|----------|--------------|
| [#5778](https://github.com/agentscope-ai/QwenPaw/issues/5778) | scroll 压缩后上下文丢失，后续回复完全跑偏 | 🔴 **严重** | 2.0 | scroll 压缩策略把关键决策、讨论信息压缩成模糊标题，模型“失忆”且回复牛头不对马嘴；thinking 模式额外引发 API 400 | 无 |
| [#5775](https://github.com/agentscope-ai/QwenPaw/issues/5775) | Auto-memory interval never triggers | 🔴 **严重** | 2.0b3 | 由于 MemoryMiddleware 状态跨请求重建而丢失，`auto_memory_interval` 永远不生效 | [PR#5777](https://github.com/agentscope-ai/QwenPaw/pull/5777)（待合并） |
| [#5776](https://github.com/agentscope-ai/QwenPaw/issues/5776) | stale pinned first user message treated as active task | 🟠 **较高** | 2.0b3 | 在长期 QQ/IM 会话中，旧消息（如6月28日）被当作当前任务，导致 AI 执行过时指令 | 无 |
| [#5773](https://github.com/agentscope-ai/QwenPaw/issues/5773) | 记忆搜索导致 OpenCode 渠道报错 | 🟠 **较高** | 1.1.12 | 开启 `auto_memory_search` 后 OCG provider 所有请求失败，关闭后正常，仅影响 OCG | 无 |
| [#5774](https://github.com/agentscope-ai/QwenPaw/issues/5774) | Google 渠道 Gemini 模型报错 | 🟠 **较高** | 1.1.12post2 | GoogleGemini 格式端点调用失败，附带 traceback | 无 |
| [#5771](https://github.com/agentscope-ai/QwenPaw/issues/5771) | model_factory.py 调试日志误用 WARNING 级别 | 🟢 **较低** | 不限 | assistant 消息块的调试日志使用 `WARNING` 级别导致日志刷屏，影响日志可读性 | 无 |
| [#5772](https://github.com/agentscope-ai/QwenPaw/issues/5772) | _is_bad_request_or_media_error() 误判 HTTP 400 | 🟢 **已关闭** | 1.1.10 | 当 LM Studio 切换模型时，所有 400 被当作多模态拒绝，导致能力缓存被错误标记（可能已通过其他方式解决或确认非 bug） | 已关闭 |

**备注**：#5772 已 Closed，但关闭原因未说明；其余 bug 均无已合并的修复。**#5778 和 #5775 是 2.0 版本最应优先解决的稳定性问题**。

---

### 6. 功能请求与路线图信号

- **[#2865](https://github.com/agentscope-ai/QwenPaw/issues/2865) (自定义 Agent 名称/头像)**：已开放 3 个月，至今未进入开发排期。考虑到社区评论持续活跃，建议将其纳入下一阶段规划。
- **[PR #5597 / #5598 (LLM 故障切换)](https://github.com/agentscope-ai/QwenPaw/pull/5597)**：后端+控制台全链路实现，是 2.0 恢复力提升的关键特性。如通过评审，预计将包含在 2.0 正式版或后续小版本中。
- **[PR #5777 (记忆状态管理)](https://github.com/agentscope-ai/QwenPaw/pull/5777)**：直接对应 #5775，属于“修复即功能”的补丁，大概率会在 2.0b4 或 RC 阶段合并。
- **[#5770](https://github.com/agentscope-ai/QwenPaw/issues/5770) (对 2.0 正式版的期待)**：虽非具体功能，但代表社区对项目方向的积极预期，可视为整体满意度的信号。

**路线图信号总结**：短期焦点是 **记忆可靠性修复 + LLM 故障切换**，长期看 **Agent 个性化交互** 可能成为下一个社区驱动的重点方向。

---

### 7. 用户反馈摘要

从当日 Issues 评论中提炼出的真实用户声音：

- **记忆功能是 2.0 的最大痛点**：“QwenPaw 2.0 默认的 scroll 压缩策略会导致严重的上下文丢失……模型忘记了原本在做什么任务，像换了一个人。”（#5778 @elain0205）
- **Auto-memory 完全不可用带来的挫折**：“Auto-memory does not persist conversation memory to the workspace `memory/` directory when `auto_memory_interval > 1`.”（#5775 @howyoungchen）
- **长对话中的“鬼打墙”**：“A message from June 28 saying ‘create a test task in DeskQuill’ was still pinned in context on July 3.”（#5776 @howyoungchen）
- **渠道兼容性令人头疼**：“开启 auto_memory_search 后 OCG 所有请求失败，关闭后恢复正常。该问题仅影响 OCG。”（#5773 @Cederys）；“GoogleGemini 格式端点报错。”（#5774 @no-teasy）
- **日志质量细节问题**：“model_factory.py 中 assistant 消息块调试日志误用 WARNING 级别导致日志刷屏。”（#5771 @elain0205）
- **积极声音**：“希望 V2.0 的正式版推出之后，能够惊艳所有人！还是非常期待的💪”（#5770 @vipcys001-bot）

总结：**用户对 2.0 的核心功能（记忆、上下文管理）要求严苛，当前稳定性和兼容性尚未满足预期**；同时用户也在积极探索多提供商切换、长会话等真实场景，对项目改进方向有较高期待。

---

### 8. 待处理积压

- **[#2865](https://github.com/agentscope-ai/QwenPaw/issues/2865) （打开，4月3日创建，已存活93天）**  
  用户请求支持自定义 Agent 名称和头像。该 Issue 已有 4 条评论且长期未标记 milestone/label，可能已被遗漏。建议项目维护者回应社区预期或将其纳入 Backlog。

- **[PR #5597](https://github.com/agentscope-ai/QwenPaw/pull/5597) / [#5598](https://github.com/agentscope-ai/QwenPaw/pull/5598) （打开，6月29日创建，已活跃 6天）**  
  两项 PR 构成完整 fallback 特性，但尚无人 Review。持续未合并可能导致特性延迟至 2.0 之后，建议尽快安排审查。

- **[#5775](https://github.com/agentscope-ai/QwenPaw/issues/5775) （打开，7月4日创建）**  
  虽非长期积压，但因其影响面广（记忆模块核心功能），且已有修复性 PR [#5777](https://github.com/agentscope-ai/QwenPaw/pull/5777) 提交，强烈建议优先合并 PR 并发布补丁版本。

---

**报告总结**：QwenPaw 2.0 正处于功能完善与质量攻坚的并行阶段。社区反馈热情但紧迫，建议优先解决 **scroll 上下文丢失（#5778）** 和 **auto-memory 不触发（#5775）** 两个严重问题，并推动 LLM fallback PR 的 Review，为正式版发布扫清障碍。

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 | 2026-07-05

---

## 1. 今日速览

过去 24 小时项目保持极高活跃度，共处理 **239 条 Issue**（新开/活跃 209，关闭 30）和 **500 条 PR**（待合并 368，已合并/关闭 132）。今日无新版本发布。整体健康度良好，社区参与踊跃；焦点集中在 **QQBot 网关重连故障、视觉工具安全与统一解析、以及多项 Provider 边界兼容性修复**。合并的修复 PR 数量较多，尤其是视觉子系统经历了一轮集中的安全加固和功能补齐，代码库向前迈出坚实一步。

---

## 2. 版本发布

*（无新版发布，本栏目省略。）*

---

## 3. 项目进展

今日合入/关闭的 PR 覆盖 Provider 兼容性、视觉管道、安全修复、文档等多个方向，下面是其中最关键的几项：

- **Provider 边界修复四合一（#58502）** — 包含 Anthropic 辅助任务凭据池回退、OpenRouter 工具调用 404 的快速降级、Poolside 整数 finish_reason/tool_call.id 类型转换、Codex app-server 文本恢复。已合并到 main。
- **视觉工具统一解析器 + 沙箱逃逸修复（#57890）** — 解决视觉图像源读取路径不一致问题，同时修复高危身份验证绕过漏洞（GHSA‑gpxw‑6wxv‑w3qq），所有图像读取统一经过终端后端，杜绝沙箱逃逸。
- **视觉支持 base64 data: URL（#30197）** — `vision_analyze` 现在可以接受 agent 内联生成的 base64 图片，无需先写入磁盘。
- **支持 SVG/BMP/TIFF 自动转 PNG（#52688）** — 避免 Anthropic API 因不支持的媒体类型返回 400 错误。
- **OpenRouter 工具调用 404 降级（#58451）** — 当端点不支持 tool use 时，直接归类为 `model_not_found` 并触发模型回退，避免重试浪费。
- **Poolside 整数类型兼容（#58374）** — 使 Poolside（Laguna）成为一等 Provider，可以正常在 CLI/TUI 中显示并用于流式对话。
- **Codex app-server 文本恢复（#58433）** — 当切换截止时间到达但尚未收到 `turn/completed` 时，接受已有的 assistant 消息作为终态，避免静默丢失回复。

此外还有 `fix(qqbot): accept is_reconnect`（#58537）、`fix(auxiliary): Anthropic pool 无可用条目时回退 token 解析器`（#58474）、`fix(skill-manager): 误报白名单未生效`（#58011）等 PR 已合并或待合入。

---

## 4. 社区热点

以下几则 Issue/PR 在今日引发了最多讨论或共鸣：

- **#52914 [Bug] QQBot 适配器缺少 is_reconnect 参数导致无限重连** — 15 条评论，4 👍。用户升级后网关无法启动，社区积极报告复现步骤，已有修复 PR #58537 获得 maintainer 快速响应。
- **#8457 [Feature] 持久会话记忆 + 跨会话搜索 + 自动压缩** — 12 条评论，需求性强。社区希望 Agent 能在网关重启后保留上下文，并支持跨对话搜索，代表了对长期记忆能力的迫切渴求。
- **#22930 [Feature] 小模型（2B-14B）离线运行指南** — 8 条评论。用户因 64k 最小上下文限制而无法使用本地小模型，反映出个人/边缘部署场景下的实际痛点，社区在讨论如何降低资源门槛。
- **#14853 [Feature] 多 Agent Discord 频道协作** — 7 条评论，6 👍。在共享频道中运行的多个 Hermes 实例无法看到彼此的对话历史，导致协作断裂；该需求获得较高赞同，表明社区对**多智能体协同**有明确使用预期。

**趋势洞察**：近期讨论的热点集中在**连接稳定性**（QQ/Telegram/WhatsApp）、**长期记忆**（RAG/持久会话）和**多实例协作**上，反映出 Hermes 正从单会话代理人向持久协作基础设施演进。

---

## 5. Bug 与稳定性

以下按严重程度罗列今日活跃的 Bug 报告，标注是否有修复 PR（FIX PR）。

### P2（中高严重度）

| Issue | 问题描述 | 状态 | FIX PR |
|-------|----------|------|--------|
| #52914 | QQBot.connect() 缺少 `is_reconnect` 参数 → 无限重连 | OPEN | #58537 ✅ |
| #42961 | `terminal.cwd` 配置在 local 后端下被忽略，始终使用进程 cwd | OPEN | 无 |
| #17199 | deepseek provider 模型名标准化 + base_url 覆盖破坏自定义端点（如火山引擎 ARK） | OPEN | 无 |
| #28823 | WhatsApp 引用回复的 `quotedMessageId` 未传递给 agent → 回复上下文丢失 | OPEN | 无 |
| #57928 | Telegram 中 `/steer` 等斜杠命令附加文件时附件被静默丢弃 | OPEN | 无 |
| #58437 | MoA 安静模式下 `_collect_stream` 不收集 `delta.tool_calls` → aggregator 工具调用导致崩溃 | OPEN | 无 |
| #44799 | Codex OAuth 凭据在冷却窗口期内刷新令牌过期，无法恢复凭据链 | OPEN | 无 |
| #12058 | OpenAI Codex OAuth 在 CLI 可用但 Telegram 网关提示无凭据（已关闭，由其他修复解决） | CLOSED | 关联 PR 合入 |
| #48534 | Anthropic Max OAuth 因 User-Agent 被封锁导致 token exchange 404（已关闭） | CLOSED | 通过 User-Agent 调整解决 |

### P3（一般严重度）

| Issue | 问题描述 | 状态 | FIX PR |
|-------|----------|------|--------|
| #43900 | Ollama 本地模型静默使用 `num_ctx=4096`，即使 GGUF 元数据支持更大窗口 | OPEN | 无 |
| #44562 | 前端 `tapClientLookup` 数组越界导致 GUI 崩溃/白屏 | OPEN | 无 |
| #18449 | TUI 快速调整终端窗口大小时出现字符残影 | OPEN | 无 |
| #58458 | Windows 上 `hermes update` 因 matrix 依赖 `python-olm` 需要 make 而失败 | OPEN | 无 |
| #44490 | 同 provider 内切换模型（opencode-go）生成空 `api_key` → 401 | OPEN | 无 |
| #33195 | `/model` 选择器自动发现 GitHub Copilot（基于 gh auth token），无需用户显式配置 | OPEN | 无 |
| #46742 | Ubuntu 26.04 桌面构建失败（已关闭，可能环境特有） | CLOSED | 无 |

### 🔒 安全修复

- **GHSA‑gpxw‑6wxv‑w3qq（视觉沙箱逃逸）** — 通过 #57890 修复，统一图像解析路径并强制经过终端后端，已合入 main。

---

## 6. 功能请求与路线图信号

今日提出的或已有 PR 对应的重要增强需求：

- **持久会话 & RAG** — #8457（持久记忆+搜索+压缩）、#844（知识库 RAG 系统）、#624（自动会话标题生成）。这三者构成了完整的记忆方案，社区呼声高，可能被纳入下一版路线图。
- **多 Agent 协作** — #14853（Discord 频道多实例历史注入+级联预防）。结合今日的 kanban 生命周期钩子 PR（#58541），团队似乎正在构建更丰富的多 agent 编排能力。
- **智能推理开销路由** — #13663（`reasoning_effort` 根据任务复杂度自适应调整），4 👍，可显著降低长流程中 token 浪费。
- **技能保护** — #25083（不可变/保护技能）+ 今日 #58540 PR（选择性的技能写入许可），两者方向一致，有望在下一版本集成。
- **OAuth HTTPS 回调** — #29299（MCP OAuth 需要 HTTPS 回调 URL），企业级部署的硬需求。
- **今日开放的功能性 PR**（大多为 feature 标签）：
  - #58493 — Context Governor：工具调用上下文压缩与摘要
  - #58542 — 插件配置与状态桥接（RFC）
  - #58541 — Kanban 生命周期钩子扩展
  - #58539 — “Hey Hermes”语音唤醒词
  - #58532 — 可安装 PWA 仪表板 + 移动端修复
  - #58043 — Mistral、Cohere 等 Provider 自动发现注册

这些 PR 表明项目正在主动捕捉社区呼声，并通过具体实现推进路线图。

---

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中，可以提炼出以下真实用户痛点：

- **QQBot 升级后完全无法连接**：用户 fishlikeX 报告即使回滚提交也无法恢复，社区多人复现并提供了详细日志。团队响应迅速，当天即开出修复 PR。
- **Ollama 用户对上下文限制困惑**：“模型明明支持 131k，但响应在 4k 被截断，感觉被静默欺骗。” — 多次尝试后才意识到是 `num_ctx` 未传递。
- **自定义 API 端点的配置挫折**：用户 yalding8 表示“Volcengine ARK 完全按照 OpenAI 兼容 API 配置，但 Hermes 强制标准化模型名，使得所有请求都 404”。
- **多 Agent 运维者的协作困境**：用户 kaishi00 详细描述了三个 Discord 实例无法共享上下文、产生无限循环的现实场景，呼吁增加历史注入和防级联机制。
- **Telegram 文件附件丢失**：YdocYNj 表示“用户明确说‘见附件’，但 agent 根本没有收到文件，非常影响体验”。
- **前端健壮性**：Huangwenboiiii 报告 GUI 在工具返回意外数据时白屏，称“这是生产环境不可接受的”。

这些反馈指向**配置透明性、网关健壮性、多实例协作**三个提升方向。好消息是大部分痛点已有对应 Issue 或修复 PR 在推进。

---

## 8. 待处理积压

以下 Issue/PR 长期未响应或虽重要但缺少分配，提请维护者关注：

| 项目 | 创建时间 | 更新 | 重要性信号 | 备注 |
|------|----------|------|------------|------|
| #844 RAG 知识库系统 | 2026-03-10 | 2026-07-04 | 4 👍，7 评论 | 核心功能缺失，至今无 PR |
| #624 自动会话标题 | 2026-03-07 | 2026-07-04 | 4 评论 | 小功能，易实现，但长期搁置 |
| #8457 持久会话记忆 | 2026-04-12 | 2026-07-04 | 12 评论，高活跃 | 与 #844 一起构成记忆体系，建议规划 |
| #14853 多 Agent Discord 协作 | 2026-04-24 | 2026-07-04 | 6 👍，7 评论 | 使用场景明确，社区支持度较高 |
| #17199 deepseek 自定义端点 | 2026-04-29 | 2026-07-04 | 5 评论 | 影响所有非标准 OpenAI 兼容 Provider |
| #42961 terminal.cwd 配置无效 | 2026-06-09 | 2026-07-04 | 7 评论 | 配置项形同虚设，影响用户脚本工作目录 |
| #43900 Ollama num_ctx 不生效 | 2026-06-11 | 2026-07-04 | 7 评论 | 广泛影响本地模型用户，但尚未分配 |
| #25083 不可变技能 | 2026-05-13 | 2026-07-04 | 6 评论 | 有安全含义，今日已有相关 PR #58540 |
| #29299 HTTPS OAuth 回调 | 2026-05-20 | 2026-07-04 | 6 评论 | 企业集成刚需 |
| #58458 Windows matrix 刷新失败 | 2026-07-04 | 2026-07-04 | 3 评论 | 平台兼容性，新开但影响 Windows 用户 |
| #58437 MoA 安静模式崩溃 | 2026-07-04 | 2026-07-04 | 3 评论 | 刚报告，需尽快确认是否影响广泛使用 |

另外，待合并 PR 当前积压 **368 条**，虽然部分可能为草稿或早期审查，但仍建议关注审查轮转效率，避免社区贡献者等待过久。

---

*本日报基于 hermes-agent 公开 GitHub 数据（NousResearch/hermes-agent）生成，数据截止 2026-07-05。所有链接可直接跳转至对应 Issue/PR。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*