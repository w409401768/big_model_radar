# OpenClaw 生态日报 2026-07-07

> Issues: 500 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-06 22:57 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，这是根据您提供的 GitHub 数据生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-07-07

## 1. 今日速览

OpenClaw 今日呈现极高的社区活跃度，24 小时内共更新 500 条 Issue 和 500 条 PR，展现出大型成熟开源项目特有的“自动化繁盛”景象（`clawsweeper` 机器人深度参与）。尽管无新版本发布，但项目在 **多平台客户端开发**（macOS 原生重构、Android/iOS 语音笔记）、**核心通信层稳定性修复**（Discord/Signal/Event-loop）和 **AI 模型生态扩展**（Featherless AI, Claude Sonnet 5）上取得了显著进展。不过，数据也揭示了 **多 Agent 并发脆弱性** 与 **工具结果可见性丢失** 等高优先级痛点亟待解决。目前在途 PR 积压量较大（322 条待合并），维护者带宽可能成为下一阶段瓶颈。

## 2. 版本发布
*无。*

## 3. 项目进展

今日项目在多条战线上高速推进，重点体现在“补课”和“修路”：

- **跨平台客户端补课：**
  - **macOS 原生重构**：PR #101103 正式提交，将原生聊天窗口从简陋的 `NSWindow` 升级为功能完备的原生 Shell，支持侧栏、工具栏选择器、斜杠命令，彻底补齐了 macOS 端的体验短板。
  - **iOS/Android 语音笔记**：PR #100946（iOS）和 #101193（Closed，Android）为用户提供了异步发送语音消息的能力，解决了“只能实时通话，不能录音留言”的痛点。
  - **Android APK 发布**：面对社区对预构建 APK 的长期呼声（#9443），维护者今日立即开启了 PR #101212，标志着 Android 官方分发流程即将落地。

- **关键基础设施修路：**
  - **通信可靠性**：PR #100896 和 #100972 分别修复了 Discord 断线重连期间的静默丢消息问题以及 Signal 回复冲突导致的会话初始化失败，保障了核心 IM 通道的稳定。
  - **性能优化**：PR #89040 通过异步化文件 I/O 和优化 Context 构建，修复了 `embedded_run` 启动阶段长达 14-22 秒的事件循环阻塞，这对高频调用 Agent 的场景影响深远。
  - **ESM 模块兼容性修复**：PR #68936 等也合并了 Windows 守护进程及相关自动化流水线，显示了项目对非主流平台的支持投入。

- **生态扩展**：PR #98254 提交了对 Claude Sonnet 5 的全面支持；PR #101092 和 #101211 则分别引入了 Featherless AI 和 Anvil Voice 作为新的 Provider。

## 4. 社区热点

- **🔥 最热 Issue：Linux/Windows 桌面应用（#75）**
  以 **110 条评论** 和 **81 个赞** 遥遥领先。尽管 macOS 获得了 PR #101103 的史诗级加强，但 Windows 和 Linux 用户依然感到“被冷落”。该项目成为衡量 OpenClaw 全平台野心的核心观察点。

- **🤖 多 Agent 编排的信任危机（#43367）**
  用户 `@waliddafif` 详实报告了并行 `agents add` 导致配置文件覆盖、会话锁失效、子任务变成“孤儿进程”的“集群失败”现象。该 Issue 被标记为 `P1` 且评级为 `diamond lobster`，反映出社区对 **多 Agent 模式下生产级稳定性的迫切需求**。这是一个严重的“路障”型问题。

- **🙈 Agent“失明”事件（#99241 / #96857）**
  有相当多的用户反映，在长会话或 ANSI 输出密集的任务中，工具执行的原始文本输出会被系统错误地替换为一个 `(see attached image)` 占位符。这导致 Agent 在后续决策中完全“失明”，无法读取关键日志。这是当前最阻碍工具使用流程的 **UX 回归** 问题之一。

- **👍 核心诉求得到迅速响应：**
  社区对 **预构建 Android APK（#9443）** 的请求在 24 小时内就得到了 PR #101212 的回应，这种高响应度极大地提振了社区信心，也展示了 OpenClaw 团队对核心用户痛点的重视。

## 5. Bug 与稳定性

本周报告的问题集中在 **回归** 与 **多 Agent 并发** 上，严重程度较高。

| 严重程度 | ID | 标题 | 状态 |
|---|---|---|---|
| 🚨 P1 / Diamond Lobster | **#43367** | 多 Agent 并行编排不稳定（配置覆盖/会话锁失效） | OPEN，有关联 PR |
| 🚨 P1 / Diamond Lobster | **#99241** | 工具输出渲染为图片占位符，Agent 无法读取 | OPEN，`needs-live-repro` |
| 🚨 P1 / Diamond lobster | **#22676** | Signal 守护进程重启时的竞争条件导致孤儿进程 | OPEN，有关联 PR |
| 🚨 P1 / Diamond Lobster | **#38327** | 回归：Google Vertex/Gemini 3.1 报“null/undefined”错误 | OPEN，`needs-maintainer-review` |
| 🚨 P1 / Diamond Lobster | **#98416** | **<已关闭>** v2026.6.11 版本缺少重入保护，会引发回复冲突 | **CLOSED** |
| ⚠️ P2 / Regression | **#38439 / #41201** | Webchat & Control UI 头像接口（/avatar）返回 404 | OPEN |
| ⚠️ P2 | **#40001** | Write 工具缺乏追加(Append)模式，孤立 Cron 会覆盖共享文件 | OPEN |
| ⚠️ P1 | **#40611** | PR #39182（心跳修复）导致心跳阻塞 Telegram 消息处理 | OPEN |

**关键修复进展：** 针对 Discord (#100896) 和 Signal (#100972) 的消息丢失问题已有具体的修复 PR 正在审查队列中，进展良好。

## 6. 功能请求与路线图信号

- **强信号 (Ready for Implementation / 高热度)：**
  - **Agent 级资源隔离：** #63829（按 Agent 隔离 Memory Wiki）和 #42475（按 Agent 成本预算）是当前呼声极高的功能，表明社区正在将 OpenClaw 从单一助手向**多租户/多职能团队平台**迁移。
  - **上下文窗口优化：** #22438（分层 Bootstrap 文件加载）和 #14785（减少工具 Schema Token 开销）反映了用户在 **LLM 成本压力下** 对 Token 精细控制的强烈需求，这是亟需产品决策的功能。

- **弱信号 / 未来方向 (Long-term / Speculative)：**
  - **架构演进：** #42026（分离控制平面与 Agent 计算平面 RFC）虽然讨论热度一般，但代表了项目走向**分布式、微服务化**的技术远见。
  - **安全强化：** #12678（基于能力的权限许可系统）、#13583（前置强制执行 Hook）和 #20935（Agent 内存审计日志）构成了一个完整的企业级安全栈诉求，尽管缺乏实时进度，但这是向企业级迈进必不可少的基础设施。
  - **云原生部署：** #13597（AWS 部署指南）的出现表明开源社区的自运维需求正在增长。

## 7. 用户反馈摘要

- **深度痛点：**
  - **“操作很可怕，不可靠”**：这正是 #43367 用户对多 Agent 并发的原话。用户在实际批量任务中发现，除了少数子任务外，大多变成了孤独进程，使得并发功能“难以在生产中使用”。
  - **“Agent 完全无法读取输出”**：来自 #99241 的反馈。针对终端工具（如检查日志、运行部署脚本）的输出，Agent 只能看到一个图片占位符，完全失去了对运行结果的理解能力，这是一个致命的交互流程断裂。
  - **“数据无声丢失”**：来自 #40001。用户指出 `write` 工具缺乏追加模式，导致多个隔离的 Cron 会话重复覆盖同一个 `memory.md` 文件，造成“无声的数据丢失”。

- **满意之处：**
  - 社区对 **修复速度** 高度认可（例如 #98416 在报告后迅速闭合）。
  - **飞书、Telegram、Slack**等渠道的集成深度得到认可，用户正在针对这些平台提交细粒度的改进请求（如 #33413 Slack 工具级进度提示）。

## 8. 待处理积压

以下 Issue/PR 长期缺乏进展或响应，值得维护者重点关注：

- **严重 Bug 无人推进：**
  - **#39847** (P1，Echo Contamination / 回波污染)：直接在回复中带出 LLM 内部上下文，可能导致敏感信息泄露给 Discord 用户。3 月提出，无进展。
  - **#41744** (P1，Feishu 图片丢失)：飞书场景下读取本地图片后最终回复丢失媒体，标记为 `stale`。

- **高潜功能请求待决策：**
  - **#14785** (减少工具 Schema Token 开销)：这能直接节省用户约 3500 Token/会话的成本，但因涉及架构变动，`needs-product-decision` 标签滞留。
  - **#42026** (分布式运行时 RFC)：开创性的架构变革，仅 7 条讨论，需要项目核心团队介入引导社区讨论。

- **合并瓶颈预警：**
  目前有 **322 条 PR 处于待合并状态**。虽然 `clawsweeper` 机器人能处理大量自动化合并，但大量冠以 `needs-maintainer-review` 和 `waiting on author` 的 PR（如 #101117、#101126）表明，**人工审核资源**是当前最紧缺的资源。维护者需要关注这三十二多个等待人工审核的 PR，避免社区贡献者热情消退。

---

## 横向生态对比

# 开源 AI 智能体生态横向分析报告 (2026-07-07)

本报告基于 **OpenClaw、Zeroclaw、PicoClaw、QwenPaw、hermes-agent** 五项目的单日社区动态，从活跃度、技术方向、社区成熟度与趋势信号等维度进行横向对比，为技术决策和开发者选型提供参考。

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于从“功能可用”向“生产可靠”跨越的关键阶段。各项目在**多 Agent 编排、平台通信集成、工具调用透明度和成本优化**上集中发力，暴露出大量并发稳定性、上下文管理和审核效率等真实“深水区”问题。同时，本地化即时通讯（QQ、飞书、Zalo）接入和记忆/上下文精细化管理的需求快速上升，反映社区正从单用户实验走向多团队、多平台的复杂部署场景。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度 |
|------|--------------|-----------|---------|--------|
| **OpenClaw** | 500 | 500 | 无 | **高活跃**，但 322 条 PR 待合并，人工审核承压 |
| **Zeroclaw** | 50 (47新开+3关闭) | 50 (40待合+10合/关) | 无 | **高活跃**，40 条待合并，3 个 S1 阻塞未解 |
| **PicoClaw** | 4 | 5 | 无 | **稳定**，小步快跑，无显著积压 |
| **QwenPaw** | 34 | 50 | v1.1.12.post3 | **良好**，补丁响应迅速，2.0 预发布推进中 |
| **hermes-agent** | **综合>789（未细分）** | 355 条待合并 | 无 | **过热**，功能迭代快但质量回退风险高 |

- OpenClaw 和 hermes-agent 的 PR 积压最为严重（分别 322 和 355 条），表明社区贡献涌入但维护者带宽不足，可能成为下一阶段增长瓶颈。
- QwenPaw 通过即时发布补丁（`v1.1.12.post3`）锁死上游依赖，展现了成熟的 LTS 支撑能力。

---

## 3. OpenClaw 在生态中的定位

OpenClaw 凭借 **500+ 日更新量**稳居生态核心参照位置，社区规模远超同类。其优势体现在：

- **全平台覆盖**：macOS 原生 Shell 重构（#101103）、iOS/Android 语音笔记、Android APK 发布启动，移动与桌面端同时补齐。
- **Provider 生态最广**：Featherless AI、Claude Sonnet 5、Anvil Voice 等新 Provider 一次性加入。
- **自动化基础设施**：`clawsweeper` 机器人批量处理 Issue/PR，维持极高吞吐。

但 OpenClaw 也暴露了与规模伴生的典型问题：  
  - **多 Agent 并发脆弱性**（#43367，配置文件覆盖、会话锁失效）—— 该问题在生态中被多次提及，但 OpenClaw 用户反馈最具体。  
  - **工具输出可见性丢失**（#99241，Agent“失明”）—— 同样出现在 Zeroclaw 和 QwenPaw 的工具渲染问题上，属于生态共性。

与 Zeroclaw 相比，OpenClaw 更侧重“一站式助手操作系统”，而 Zeroclaw 走 Rust 高性能 + 终端原生路径；与 hermes-agent 相比，OpenClaw 的渠道和提供者覆盖更宽，但 hermes-agent 在桌面端 MCP 集成和插件机制上更为深入。

---

## 4. 共同关注的技术方向

以下方向至少出现在 3 个项目的活跃讨论中，代表当前生态的核心着力点：

| 技术方向 | 涉及项目 | 典型诉求 |
|---------|---------|---------|
| **多 Agent 编排与自主性** | OpenClaw, Zeroclaw, QwenPaw, hermes-agent | 并发配置覆盖、目标模式、子 Agent 注册、角色预设 |
| **即时通讯/社交平台集成** | OpenClaw, Zeroclaw, QwenPaw, hermes-agent | QQ/飞书/Zalo/Signal/Telegram 稳定性及新通道 |
| **工具调用可靠性与透明性** | OpenClaw, Zeroclaw, PicoClaw, QwenPaw, hermes-agent | 工具输出被替换、MCP 工具缺失、序列化丢失、渲染崩溃、重复循环 |
| **上下文与成本优化** | OpenClaw, PicoClaw, QwenPaw, hermes-agent | 分层加载、滚动缓存断点、压缩崩溃、session 负载限制 |
| **记忆系统精细化** | OpenClaw, QwenPaw, hermes-agent | 按 Agent 隔离、自动记忆间隔、重排序、网关内存丢失 |

**解读**：工具可见性与上下文管理已成为制约长时间 Agent 任务的核心瓶颈，而多 Agent 编排的稳定性则决定了项目能否从“单会话助手”升级为“多职能团队平台”。

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Zeroclaw | PicoClaw | QwenPaw | hermes-agent |
|------|----------|----------|----------|---------|-------------|
| **目标用户** | 个人/小团队，追求功能全面 | 开发者/DevOps，偏好终端与自动化 | 个人开发者，注重 API 成本 | 企业团队，多组织协作 | 桌面中心用户，插件生态 |
| **核心架构** | Python/JS，全栈 Web+桌面 | Rust，TUI 优先，SOP 工作流 | 轻量 CLI，围绕 Provider 优化 | Python，高度集成飞书/钉钉/Zalo | 桌面+网关分离，MCP 连接器 |
| **关键差异化** | 最大 Provider 生态；自动化工具体系 | 高性能，结构化 Goal Mode | Anthropic 极致缓存优化 | 中国企业 IM 适配；定时任务和 Coding 模式 | 桌面侧栏和插件扩展；MCP 目录 |
| **当前最大挑战** | 多 Agent 并发脆弱；审核积压 | S1 级 Telegram 配置阻塞；合并队列积压 | Provider 兼容性（Gemini 网关） | 上下文压缩稳定；多用户账户缺失 | 回归测试不足；355 条 PR 待处理 |

- **OpenClaw** 与 **hermes-agent** 在功能广度上最接近，但 hermes-agent 的稳定性代价更大。
- **Zeroclaw** 是唯一采用 Rust 并在 TUI 和 SOP 上发力的项目，定位极客开发者。
- **PicoClaw** 则定位“小而美”，在 Anthropic 单点深度上超过其他项目，适合重度 Claude 用户。

---

## 6. 社区热度与成熟度

### 快速迭代 / 创新层
- **OpenClaw**、**Zeroclaw**、**hermes-agent**  
  三者日更新量均为“极高”，频繁引入新功能（Goal Mode、macOS Shell 原生、桌面 MCP 连接器等）。但合并积压和 Bug 开放在三者中均突出，处于“高速但松散”的阶段。

### 质量巩固 / 稳定发布层  
- **QwenPaw**、**PicoClaw**  
  QwenPaw 以 LTS 补丁快速响应兼容性问题，并借助自动 Review Bot 提升审核效率，版本节奏可控。PicoClaw 以小范围修复+演进提案形式推进，社区健康度最佳。

### 成熟度关键信号
- **QwenPaw** 拥有明确的版本分支（1.x LTS + 2.0 预发布）和自动化 CI 机器人，体现项目管理成熟。
- **OpenClaw** 虽然活跃，但 `needs-maintainer-review` 标签大量堆积，社区对审核效率的抱怨开始出现。
- **hermes-agent** 的多个 P1/P2 Bug（网关内存丢失、桌面回归）长期未关闭，表明测试回退流程不足。

---

## 7. 值得关注的趋势信号

对 AI 智能体开发者与团队选型具参考价值：

1. **工具输出标准化成为刚需**  
   OpenClaw (#99241)、Zeroclaw (#8193)、PicoClaw (#3227) 不约而同遭遇 Agent“无法读取工具结果”的问题。未来项目应设计**结构化工具输出协议**，确保 LLM 稳定消费。

2. **多 Agent 可靠编排仍缺生产级方案**  
   OpenClaw (#43367) 的并发配置覆盖、孤儿进程引发广泛讨论。当前生态缺乏事务性保障机制，开发者投入前需评估稳定性风险。

3. **本地化 IM 驱动区域增长**  
   飞书 (QwenPaw #5757)、QQ (Zeroclaw #2503, hermes-agent #52914)、Zalo (QwenPaw #5168) 在多个项目中成为 Top 诉求。融入区域市场是获取用户的关键路径。

4. **成本意识催生智能缓存**  
   Anthropic prompt caching 已从“支持”进化到“滚动断点”(PicoClaw #3229)。“Token 精细控制”（OpenClaw #14785）同样在高票待处理。成本优化将成为 Provider 核心竞争点。

5. **记忆系统从存储走向智能检索**  
   自动记忆的重排序（QwenPaw PR #5669/#5692）、按 Agent 隔离（OpenClaw #63829）表明社区已不满足于简单存取，正向**相关性排名**与**目标导向记忆**演进。

6. **社区治理瓶颈可能引发贡献者流失**  
   三个最活跃项目待合并 PR 均超 40 条（Zeroclaw 40，OpenClaw 322，hermes 355）。如果审核速度长期跟不上提交速度，将挫伤外部贡献积极性，项目需引入更多维护者或改进自动化审查。

---

**总结**：个人 AI 智能体生态正经历从“单点功能”向“生产级平台”的转变。OpenClaw 虽为生态体量最大的参照项目，但头部项目在稳定性、并发处理和质量控制上均面临共性痛点；Zeroclaw 和 PicoClaw 在特定领域（高性能、极致成本）表现出差异化优势，而 QwenPaw 则在企业集成和版本管理上相对成熟。开发者在选型时应重点关注**工具可观察性、多 Agent 可靠性、成本控制策略和社区维护响应效率**这四个关键维度。

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报 | 2026-07-07

---

## 1. 今日速览

过去 24 小时项目活跃度极高：共产生 **50 条 Issue 更新**（新开/活跃 47 条，关闭 3 条）及 **50 条 PR 更新**（待合并 40 条，合并/关闭 10 条）。虽然当日无新版本发布，但内部进度显著——一个长期困扰用户的 **S1 级关键缺陷（MCP Tools 在 TUI 中不可见）** 已被关闭，社区稳定性获得重大提振。核心特性 **"目标模式"（Goal Mode）** 的 PR 栈（#8687, #8688, #8689）持续演进，标志项目正从对话式 Agent 向结构化自主行为体转型。**主要隐忧**在于 PR 合并队列严重积压（40 个待合并），且仍有 3 个 S1 级工作流阻塞 Bug 悬而未决。

---

## 2. 版本发布

（当日无新版本发布，无版本说明。）

---

## 3. 项目进展

### 🔨 关键 Bug 修复
- **MCP 工具同步危机解除**：S1 级 Issue **#8193**（MCP Tools 在 TUI 中缺失，网关可见但终端不可见）正式关闭。该问题共引发 16 条讨论，修复后 @CedricConday 随即提交了回归防护测试 **PR #8775**，确保该场景不会复发。
- **CI 门禁补强**：Issue **#8753** 暴露 CI 脚本 `rust_quality_gate.sh` 因缺少 `--workspace` 参数，成员 crate 的测试目标被遗漏，断裂代码可直接合入 `master`。@IftekharUddin 提交修复 **PR #8776**，使本地 Clippy 与 CI 保持一致。同时 @Project516 提交 **PR #8781**，移除 18 条陈旧的 CVE 忽略记录，修复 Security CI 门禁故障。

### 🧩 核心功能推进：目标模式（Goal Mode）
@vrurg 主导的庞大特性栈迎来集中更新：
- **PR #8687**：运行时目标控制器（Controller）与验证器（Verifier），含重启恢复与成本归因。
- **PR #8688**：受信目标工具（`goal_start` / `goal_objective` / `goal_resume`）及委托边界，仅对持有作用域准入上下文的调用者注册。
- **PR #8689**：通道端 `/goal` 命令准入体系（start / objective / status / budget / pause / resume / cancel / help），通过共享命令目录与可信控制面接入。
- **PR #8746**（依赖 #8689）：修复活跃目标自恢复死循环。

以上 PR 标志着 Tracker **#8681**（Goal-mode 实现拆分栈）的核心拼图已完成，正在等待合并审核。

### 💻 ZeroCode TUI 优化
- **PR #8779**：修复流式文本未能累积时，最终助手回复被静默丢弃的问题，以 daemon 回传的 `TurnComplete.content` 作为 fallback。
- **PR #8777**：修复代码块复制按钮将 Markdown 围栏（反引号 + 语言标记）一并复制到剪贴板的问题，提升终端开发体验。
- **PR #8774**：新增 `Ctrl+W` 删除前一个单词的快捷键，通过 keymap registry 注册为 `DeletePreviousWord`。
- **PR #8773**：修复 ACP 协议下 `ask_user` / `poll` 间歇性失败（目标会话不匹配导致被错误 `cancel`）。
- **PR #8655**：@ConYel 对 ZeroCode 聊天面板进行重大重构，将 ACP 面板统一为 `code.rs`，共享会话记录落于 `transcript.rs`，合并「完整聊天」与「仅代码」两种模式。

### ⚙️ 运行时与 SOP 稳定性
- **PR #8771**：修复 SOP 步骤 `when` 条件为假时的路由错误——此前会错误地完结运行，现在正确落至线性下一步。解锁多阶段 SOP（自循环步骤 + 终审步骤）支持。
- **PR #8639**：@tidux 提交 TodoWrite 追踪器实现（RPC + ACP + 持久化），为 ZeroCode 带来类似 Claude Code 的实时任务看板能力。

---

## 4. 社区热点

| 排名 | Issue / PR | 类型 | 评论数 | 热度分析 |
|---|---|---|---|---|
| 1 | **[#8193] bug(zerocode): MCP tools/tool_search missing from TUI sessions** | S1 Bug → **已关闭** | 16 | 用户长期受困于网关与 TUI 间 MCP 工具不一致的硬阻塞。Issue 文档质量极高，包含 #8045 参照、多用户复现路径与 Gateway/RT 通道差异分析。关闭消息获得社区广泛关注。 |
| 2 | **[#6808] RFC: Work Lanes, Board Automation, and Label Cleanup** | 内部治理 RFC | 13 | 社区维护者在推动看板自动化与标签规范化方面的持续讨论。虽非用户直接痛点，但关系项目长期协作效率。 |
| 3 | **[#2503] [Feature]: where is napcat channel** | 功能请求 | 9 | 一个「老生常谈」的需求。用户 @irunmyway 代表了一大批期望将 ZeroClaw 接入 QQ 生态（OneBot / NapCat）的社群。该 Issue 自 3 月 2 日开放至今已达 4 个月，未产生实质进展。呼声与实现之间存在明显缺口。 |
| 4 | **[#8603] RFC: OpenAI Chat Completions compatibility adapter** | RFC | 3 | 社区希望 ZeroClaw 暴露 OpenAI 兼容接口，以直接接入 Open WebUI / LobeChat 等第三方前端。这反映了用户「融入既有 AI 基础设施」而非「重建封闭入口」的强烈偏好。 |
| 5 | **[#8780] [Feature]: Realtime speech-to-speech channel (Gemini Live)** | 新功能 (今日提交) | 0 | @metalmon 再次推进语音交互边界——提出模型原生主导的语音-语音通道（ASR/TTS/Function-calling 全由模型侧持有），ZeroClaw 退居工具/审批/记忆层。与 #7943 和 #7944 构成了完整的实时语音矩阵。 |

---

## 5. Bug 与稳定性

### 🔴 严重（S1 - 工作流阻塞）

| ID | 标题 | 状态 | 组件 | 风险等级 | 备注 |
|---|---|---|---|---|---|
| **#8505** | Telegram channel cannot be configured | **开放中** | runtime/daemon | High | 用户按 Quickstart 配置后，`zeroclaw channels doctor` 和 Bot 均无响应。核心配置流存在健壮性问题，预估影响面广。 |
| **#8675** | Malformed native tool-call arguments → provider 400 → empty reply | **开放中** | provider | Medium | 原生 Tool Call 的 `function.arguments` 未经 JSON 校验直接回传给 Watson Wire Format 的 Provider，触发 400 错误且**静默返回空回复**，用户完全无感知。 | 
| **#8753** | rust_quality_gate.sh misses member-crate test targets | **开放中** | CI | High | 缺少 `--workspace` 导致编译故障的可坏代码可绕过 CI 进入 `master`，破坏发布基线。已有修复 PR #8776，等待合并。 |

### 🟡 中等（S2 - 降级行为 / 误报）

| ID | 标题 | 状态 | 组件 | 备注 |
|---|---|---|---|---|
| **#8193** | MCP tools/tool_search missing from TUI sessions | 已关闭 | zerocode/tui, runtime | 已修复。S1 提升至已关闭。 |
| **#8631** | Headless deterministic SOP steps recorded Completed without executing | 已关闭 | runtime/daemon (SOP engine) | 已修复。S2「虚假绿标」审计陷阱，具有隐蔽性。 |
| **#7870** | Agent runtime options can leak from first configured provider | 开放中（Tracker） | agent, runtime | 配置顺序可能导致错误 Provider 获取错位选项，跟踪中。 |

### 🛠️ 修复 PR 排队中
这些 PR 今日已提交/更新，正在等待审核合并：
- **PR #8773**：修复 ACP 协议下 `ask_user` 间歇性取消。
- **PR #8771**：修复 SOP `when` 条件路由错误。
- **PR #8746**：修复 Goal 自恢复死循环。
- **PR #8776**：CI `--workspace` 修复。
- **PR #8781**：安全 CI `cargo-deny` 陈旧的 advisory 移除。

---

## 6. 功能请求与路线图信号

### 📌 大概率纳入 v0.9.0 / v0.8.4

| 特性 | 入口 | 简介 | 当前状态 |
|---|---|---|---|
| **目标模式（Goal Mode）** | #8681（Tracker）、#8687、#8688、#8689 | 运行时控制器+受信工具+通道命令准入，实现长期自主任务。 | 功能已完成，PR 栈等待合并。 |
| **TodoWrite 追踪器** | PR #8639 | 实时只读任务看板，源码风格的任务规划/执行追踪。 | 功能 + RPC + 持久化已就绪。 |
| **ZeroCode 面板重构** | PR #8655 | 合并 Code 与 Chat 面板为统一的 ACP 体验。 | 重大重构，已通过 CI，需要深度 Review。 |

### 🗣️ 社区高呼声但待维护者投入

| 需求 | 入口 | 用户诉求摘要 | 沉寂时长 |
|---|---|---|---|
| **OneBot/NapCat 通道** | #2503 | 连接 QQ 生态，国内刚需。 | 4 个月 |
| **OpenAI 兼容 API** | #8603 | 接入 Open WebUI / LobeChat 等第三方前端 | 5 天（呼声高但时间短） |
| **文件编码自动检测** | #7521 / #8602 | `file_read` 对 cp1251/Shift-JIS 静默乱码 | 近 1 个月 |
| **Per-Chat 模型切换** | #8600 | 用户从 Moltis 迁移，期望前缀式模型选择 | 6 天 |
| **Telegram 通道配置修复** | #8505 | 配置后 Bot 不响应 | 8 天（阻塞） |

### 🔭 前沿探索：语音交互
- **#8780**（今日新开）：实时语音-语音通道（Gemini Live 驱动，模型天然处理 VAD、Barge-in、Function-calling）。
- **#7943**：通用 VoiceHost 通道（WS 客户端，委托 ASR/TTS/播放）。
- **#7944**：物理语音卫星设备（ESP32/手机/PWA + 审批按键）。
- 以上三条形成了从物理设备到云端模型的完整语音链路，为 ZeroClaw 的下一个交互范式铺路。

---

## 7. 用户反馈摘要

### 😠 真实痛点

> "The bot does not answer on TG. The agent replies in CLI."
> **— @AIWintermuteAI**, [#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505)

> "Several OpenAI-wire-format providers re-serialize assistant `tool_calls[].function.arguments` verbatim without validating it's well-formed JSON... leading to provider 400 errors and **empty replies** with no user-facing error."
> **— @metalmon**, [#8675](https://github.com/zeroclaw-labs/zeroclaw/issues/8675)

> "In moltis, provider is a model provider... then the full set of supported models are available... But in Zeroclaw, I have to pick a single model per agent. Can't easily switch..."
> **— @vvuk**, [#8600](https://github.com/zeroclaw-labs/zeroclaw/issues/8600)

> "When a `deterministic = true` SOP is started with no human gate, the steps are recorded as **Completed without executing** the script in the cooldown window — creating a false-green audit trail."
> **— @Stalesamy**, [#8631](https://github.com/zeroclaw-labs/zeroclaw/issues/8631)

### 😊 满意与肯定
- 用户对项目灵敏度高度赞许：几乎每个 Bug 报告都能获得核心维护者的 "Status: accepted" 标签且快速排期。
- 迁移用户（@vvuk, #8600）表示「大多数功能都是存在的」，整体表示认可。
- 终端用户体验改进（PR #8777 修复 Markdown 围栏、PR #8774 Ctrl+W 快捷键）是用户直接通过 PR 参与反馈的正面案例。

### 💡 建议方向用户画像
- 报告 Issues 的社区成员多是**高技术水平用户**：他们提供详细的 Cargo 构建路径、Rust 恐慌栈、Provider Wireshark 级别的请求体分析，并有能力提交修复 PR。
- 用户表达了「希望 ZeroClaw 成为 Agent 基础设施核心，而非孤立的聊天机器人」的诉求，体现于对 OpenAI 兼容层、语音、任务追踪等特的支持需求。

---

## 8. 待处理积压

> 以下为长期未获响应或进度延迟的重要项目，提请维护者关注。

| ID | 标题 | 类型 | 创建日期 | 最后活跃 | 评论 | 停滞原因分析 |
|---|---|---|---|---|---|---|
| **#2503** | [Feature]: where is napcat channel | 功能请求 | 2026-03-02 | 2026-07-06 | 9 | 实现 OneBot/NapCat 需要对 Channel 层进行较大改动，且涉及 QQ 协议适配的法律合规风险？需维护者官方表态。 |
| **#6808** | RFC: Work Lanes, Board Automation, and Label Cleanup | 治理 RFC | 2026-05-20 | 2026-07-06 | 13 | 虽持续活跃（更新标签），但迟迟未进入实施阶段。看板自动化直接影响维护效率，建议设立截止日。 |
| **#8398** | RFC: Plugin permission, config, and secrets model | 架构 RFC | 2026-06-27 | 2026-07-06 | 1 | 标记为 `needs-maintainer-review` 且 `status:blocked`。从 `all-or-nothing` 的 `PluginPermission` 到细粒度权限，是插件生态扩展的前置条件。 |
| **#6311** | inject agent alias into system prompt on init | 功能请求 | 2026-05-03 | 2026-07-06 | 1 | 作为 V3 多智能体工作（#6266）的部件，系统提示词缺失 "You are agent 'xxx'" 会影响 Agent 的自我认知与行为一致性。 |
| **#6810** | Add a user-facing feature and support matrix | 文档 | 2026-05-20 | 2026-07-06 | 1 | 已有第 3839 号 Issue 的 roadmap 基础，但 Features Matrix 迟迟未落地。缺乏功能矩阵增加了新用户的入门成本。 |

---

**报告总结**：ZeroClaw 在 2026 年 7 月 7 日保持极高开发强度和社区活跃度。项目在稳定性（MCP 工具同步修复）、核心能力（目标模式 PR 栈就绪）和终端体验（ZeroCode TUI 一系列优化）上齐头并进。需要警惕的是合并队列的审核瓶颈及 S1 级 Telegram 配置 Bug 的持续影响。用户功能请求（OneBot、OpenAI 兼容层、文件编码、语音）清晰指向了**平台化**与**全球化**的发展需求。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 PicoClaw 项目动态日报（2026-07-07）。

---

# PicoClaw 项目动态日报 | 2026-07-07

## 1. 今日速览
过去 24 小时内，PicoClaw 项目呈**非常高**的活跃度，社区处理了 4 个 Issue 和 5 个 Pull Request。核心主线是 **Anthropic provider 的 prompt caching 功能链式修复**，从问题报告（#2191）、修复提交（#3228）到演进提案（#3229）在一天内密集完成，显著提升了该 provider 的性能上限。此外，工具系统（Tooling）可靠性也获得重大提升，包括 `tool_use` 历史序列化 Bug 修复（#3227 已合并）和 `write_file` 覆写逻辑优化（#3226）。同时，新的 Bug 报告（Gemini 兼容性 #3230）和功能请求（SearXNG 认证 #3231）表明用户群正在向更复杂的生产环境迁移。

## 2. 版本发布
无。过去 24 小时内无新版本发布。

## 3. 项目进展

**已合并/关闭：**
- **[#3227] [CLOSED] fix(providers): resolve tool_use name/args from Function on reloaded history**
  - **摘要：** 作者 @AayushGupta16 修复了一个影响所有 Provider 的深层会话恢复 Bug。此前 `ToolCall.Name` 和 `ToolCall.Arguments` 因被标记为 `json:"-"` 运行时字段，导致会话历史序列化并重载后工具调用信息完全丢失。
  - **影响：** 该修复直接提升了 Agent 长时间运行和状态恢复的可靠性，属于数据完整性修复。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3227)

- **[#2191] [CLOSED] [BUG] anthropic_messages provider ignores SystemParts**
  - **摘要：** 该长期存在的 Bug 引发了今日的密集修复流程。随着 #3228 的提交，此 Issue 被关闭。它代表了社区闭环解决复杂问题的高效协作能力。
  - [Issue 链接](https://github.com/sipeed/picoclaw/issues/2191)

**核心推进中（已提交待合并）：**
- **[#3228] [OPEN] fix(anthropic-messages): send SystemParts as system blocks with cache_control**
  - **进展：** 实现了对 `SystemParts` 内容的块级 `cache_control` 支持，使得 Anthropic prompt caching 功能在该 provider 上成为可能。这是一个直接的性能提升补丁，也是今日项目进展的里程碑。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3228)
- **[#3226] [OPEN] fix(tools): stop write_file from coaching destructive overwrite**
  - **进展：** 优化了 `write_file` 工具的系统提示，避免模型默认采取破坏性覆写操作，提升了 Agent 文件操作的安全性和智能性。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3226)

## 4. 社区热点
- **最热焦点：Anthropic Caching 生态全链路讨论**
  - **核心分析：** 由 Issue #2191（Bug）、PR #3228（修复）和 Issue #3229（演进提案）构成的讨论链是今日绝对热点。
  - **[#3229] Proposal: rolling conversation cache breakpoints for anthropic-messages**
  - **作者：** @AayushGupta16
  - **诉求：** 在修复了静态系统提示缓存后，作者立刻提出更激进的“滚动缓存断点”方案。在 Agentic 工作负载中，对话历史是主要 Token 消耗源，该提案允许在长对话的高成本切换点设置缓存。
  - **分析：** 这直接反映了重度用户对控制 Anthropic API 成本的**极度敏感**和**深度技术把控能力**。用户已不满足于基础功能可用，而是在追求极致的性能和成本优化。
  - [Issue 链接](https://github.com/sipeed/picoclaw/issues/3229)

- **持续关注：[#3118] Add remote Pico WebSocket mode**
  - **作者：** @jp39
  - **分析：** 虽然已开放近一个月，但仍在活跃更新。该 PR 代表了 PicoClaw 从简单 CLI 工具向分布式 Agent 后端架构演进的关键步骤，显示了社区对架构扩展的浓厚兴趣。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3118)

## 5. Bug 与稳定性
- **[#3230] 高严重性：Function call is missing thought_signature (Gemini API)**
  - **状态：** 新报告（2026-07-06），暂无修复 PR。
  - **描述：** 在通过 OpenAI 兼容格式（如 Cloudflare AI Gateway）调用 Gemini 进行工具调用时，返回 `missing thought_signature` 错误。这会直接导致 Agent 工具调用执行失败。
  - **影响面：** 使用中转方式调用 Gemini 模型的用户。
  - [Issue 链接](https://github.com/sipeed/picoclaw/issues/3230)

- **[#3227] 严重性：高（已修复）**
  - 工具调用历史序列化 Bug。今日已通过合并 PR #3227 修复。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3227)

- **[#3115] 中严重性：Session 历史损坏**
  - **状态：** 修复 PR 已存在（开放近一个月），待合并。
  - **描述：** `data:image/...;base64,...` 字符串在通用工具输出中被错误解析为媒体附件，导致会话历史损坏。虽然不直接导致崩溃，但属于“无痛血条”式长期损害，影响用户信任度。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3115)

## 6. 功能请求与路线图信号
- **高概率纳入下版本：**
  - **[#3229] Rolling conversation cache breakpoints:** 作为 #3228 的自然演进，该特性对于运行复杂任务链的用户价值极高。项目组今日已展现对 Anthropic Caching 生态的投入，纳入路线图优先级很高。
  - [Issue 链接](https://github.com/sipeed/picoclaw/issues/3229)

- **生态系统集成信号（潜在需求）：**
  - **[#3231] SearXNG Basic Auth 支持：** 用户需要在自部署的 SearXNG 实例上使用 Basic Auth 认证。这表明社区存在大量**私有化和企业级部署**需求，需要更细粒度的网络访问控制兼容性。
  - **[#3230] Gemini OpenAI Compat 修复：** 表明用户已进入“多模型、多后端”的混合部署阶段，对 Provider 间接口的细节兼容性要求极高。

## 7. 用户反馈摘要
- **核心痛点：API 成本与兼容性**
  - **Anthropic 成本敏感：** 用户 @AayushGupta16 的修复和提案（#3228, #3229）强烈表明，在重度 Agent 场景下，当前版本因缺乏深度 Caching 功能导致的 Token 开销是难以容忍的。
  - **网关兼容性摩擦：** 用户 @VictorSu000 在 Cloudflare AI Gateway 遇到 Gemini 兼容性 Bug（#3230），体现了当用户将 PicoClaw 接入自有中间件基础设施时的摩擦感。

- **对 Agent 自主性的精确控制需求**
  - 用户 @ACMYuechen 修复 `write_file` 行为（#3226），揭示了社区对 Agent 的要求：**不仅是功能上“可用”，更要求行为上“可控”和“可预测”**，不希望模型被语料误导执行不合理的操作。

## 8. 待处理积压
- **[PR #3118] Remote Pico WebSocket mode** (开放: 2026-06-12)
  - **提醒：** 已开放 25 天。作为重要的架构级功能，建议核心维护者尽快安排深度 Code Review，以避免大分支长期发散导致合并成本剧增。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3118)

- **[PR #3115] Fix inline data URL media extraction** (开放: 2026-06-12)
  - **提醒：** 已开放 25 天。虽然属于“静默数据损坏”类 Bug，但对长期用户的体验伤害较大。修复代码逻辑相对独立，建议优先合并。
  - [PR 链接](https://github.com/sipeed/picoclaw/pull/3115)

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，以下是为 QwenPaw 项目生成的 2026-07-07 项目动态日报。

---

# QwenPaw 项目日报 - 2026-07-07

## 今日速览

项目社区今日保持高度活跃，过去24小时内共有34条Issue更新和50条PR更新，并发布了v1.1.12.post3补丁版本。新版本紧急修复了因上游依赖（ACP）变更导致的1.x版本启动崩溃问题，体现了对长期支持版本的快速响应。近期社区焦点集中于流式输出性能、渠道（飞书、钉钉）稳定性及2.0.0预发布版本的Bug修复，同时社区贡献者在单元测试覆盖和新的功能特性（如记忆管理与重排序）方面贡献了大量PR。项目健康度良好，但需关注上下文压缩等关键功能的稳定性问题。

## 版本发布

### v1.1.12.post3 补丁版本
- **链接**: [Releases - v1.1.12.post3](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.12.post3)
- **更新内容**: 此补丁版本是v1.1.12系列的小版本更新，核心目的是解决1.1.12系列与`agent-client-protocol` (ACP) 库的兼容性问题。由于ACP库的新版本引入了breaking change，导致QwenPaw在导入时出现`ImportError`（对应Issue #5816）。
- **修复**: 将`agent-client-protocol`依赖锁定在`>=0.9.0,<0.11.0`范围，避免后续ACP的自动升级再次引发兼容性问题。
- **迁移注意事项**: 对于仍在使用1.x系列版本的用户，执行`pip install --upgrade qwenpaw==1.1.12.post3`即可解决因ACP版本升级导致的启动崩溃。

## 项目进展

今日项目在功能开发、Bug修复和代码质量方面均有显著推进，多项重要PR被合并或取得进展：

1.  **兼容性与稳定性修复**:
    - **PR #5818** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5818)): 此PR被合并，发布了v1.1.12.post3补丁，紧急修复了ACP兼容性问题，保障了1.x用户的稳定性。
    - **PR #5768** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5768)): **已合并**。修复了后端API返回的时间日期字符串缺少时区信息的问题，解决了前端可能因时区解析错误导致的时间显示异常。
    - **PR #5524** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5524)): **已合并**。由社区贡献者提交，将`spawn_subagent`工具注册到Runtime 2.0中，并完成了端到端测试，强化了子Agent管理功能。

2.  **新功能与增强**:
    - **PR #5210** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5210)): **已合并**。新增了 `qwenpaw cron update` CLI命令，允许用户直接修改已有定时任务配置，替代了原先“删除后重建”的繁琐流程。这是一个社区贡献的PR，解决了长久以来的用户痛点。

3.  **基础设施与测试**:
    - **PR #5736** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5736)): **已合并**。CI流程新增了自动化代码审查机器人（QwenPaw review bot），这将有助于提升PR审查效率和代码质量。
    - **PR #5807, #5808, #5809, #5810** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5807), [链接](https://github.com/agentscope-ai/QwenPaw/pull/5808), [链接](https://github.com/agentscope-ai/QwenPaw/pull/5809), [链接](https://github.com/agentscope-ai/QwenPaw/pull/5810)): 今日有多项针对Backend（inbox模块）和Console（hooks, stores, API模块）的单元测试PR被提交，旨在提升核心模块的测试覆盖率，这是项目走向成熟的重要标志。

## 社区热点

1.  **#5757 飞书渠道不回复问题** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5757))
    - **活跃度**: 今日新增3条评论，共11条评论，热度最高。
    - **诉求分析**: 用户报告在飞书渠道中，Agent只在首次回复，后续消息无响应。该问题影响docker用户和官方平台用户，指向渠道处理机制的共性问题。用户焦急等待回复，社区关注度高。

2.  **#5401 Console前端因大型对话渲染崩溃** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5401))
    - **活跃度**: 8条评论，持续活跃。
    - **诉求分析**: 这是一个影响用户体验的严重Bug。当对话历史中包含大量工具调用时，Console前端会白屏崩溃。这暴露了前后端数据格式不匹配的问题，表明前端渲染组件对`tool_use`/`tool_result`类型的消息处理存在缺陷。该Bug在2.0.0中也可能存在，是社区排查的热点。

3.  **#5273 QwenPaw v2.0.0 预发布版本Bug跟踪** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5273))
    - **活跃度**: 5条评论，持续作为v2.0.0的集中反馈入口。
    - **诉求分析**: 社区对即将到来的v2.0.0大版本充满期待，同时也积极在此tracker下反馈各种预发布版中的问题。该项目是社区和开发团队沟通v2.0.0稳定性与功能细节的桥梁。

## Bug 与稳定性

- **严重**:
    - **#5816 ACP导入错误导致程序崩溃**: **已由PR #5818在v1.1.12.post3中修复。** (Issues: 链接, PR: 链接) 这是阻止性Bug，已通过发布热修复版本解决。
    - **#5401 Console无法渲染含大量工具调用的会话**: **待修复。** (Issues: 链接) 影响核心功能，导致前端白屏。已有社区讨论和根因分析，暂无关联的Fix PR。

- **高**:
    - **#5757 飞书渠道机器人不回复**: **待修复。** (Issues: 链接) 影响特定渠道的正常使用，复现率高，社区反馈强烈。
    - **#5725 Console流式输出过程中浏览器卡顿**: **待修复。** (Issues: 链接) 影响核心交互体验，用户在对比DeepSeek后期望优化。
    - **#5782 Google Gemini embedding兼容性问题**: **已关闭，修复待确认。** (Issues: 链接) 使用OpenAI兼容端点时导致向量搜索静默降级为用户无感知的Bug。
    - **#5710 上下文压缩无保护锚点，关键消息被截断**: **待修复。** (Issues: 链接) 可能导致Agent在压缩后“失忆”，严重危害对话连续性和任务执行。
    - **#5789 上下文压缩因JSON Schema校验失败崩溃**: **待修复。** (Issues: 链接) 上下文压缩功能在高负载或特定模型下直接崩溃，严重影响稳定性。
    - **#5775 Auto-memory间隔不生效**: **待修复。** (Issues: 链接) 影响v2.0.0核心的自动记忆功能，导致记忆无法持久化。
    - **#5773 OCG渠道因记忆搜索报错**: **待修复。** (Issues: 链接) 特定模型提供商与记忆功能的兼容性问题，导致请求完全失败。
    - **#5779 Cron任务状态API时区错误**: **待修复。** (Issues: 链接) 影响定时任务状态显示的准确性。
    - **#5787 移动端WebUI页面底部被截断**: **已关闭，修复待确认。** (Issues: 链接) 影响移动端用户体验。

- **中**:
    - **#5784 前端压缩阈值显示错误**: **已有PR #5822。** (Issues: 链接, PR: 链接) UI显示值与实际行为不符，会造成用户困惑。社区贡献者已提交修复。
    - **#5790 Console加载动画不消失**: **待修复。** (Issues: 链接) 轻度影响用户体验。
    - **#5776 IM会话中陈旧消息被当作当前任务**: **已有PR #5765。** (Issues: 链接, PR: 链接) 影响长对话处理，可能导致Agent执行错误指令。
    - **#5771 model_factory.py日志级别误用导致刷屏**: **待修复。** (Issues: 链接) 影响开发和生产环境的日志可观测性。
    - **#5769 /api路径重复导致404错误**: **已关闭。** (Issues: 链接) 影响v2.0.0b2版本，已修复。

## 功能请求与路线图信号

1.  **多用户账户管理 (#5780)** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5780)): 团队协作场景的核心需求，希望支持多用户、权限分级。目前QwenPaw缺乏此功能，限制了其在企业团队中的使用。此项功能呼声较高。

2.  **Zalo Bot渠道支持 (#5168)** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5168)): 来自越南社区的强烈需求，希望QwenPaw能接入越南流行的通讯软件Zalo，以拓展其在东南亚的应用场景。

3.  **Console功能增强**: 多个Issues提出了Console的优化建议：
    - **#5797**: 定时任务弹窗提醒应提供用户开关。
    - **#5793**: 聊天时间戳增加“常驻显示”选项。
    - **#5795**: 微信渠道新消息到达时，Web Console自动刷新。
    - **#5785**: Coding模式下支持选择隐藏文件夹。
    - **#5821**: `rejects_media`能力细化到媒体类型层面，避免一刀切。

4.  **记忆与上下文管理增强**:
    - **#5316**: 提议为每日记忆搜索增加“近因感知”排序，以提升记忆检索的相关性。虽然该Issue已关闭，但其核心思路已体现在PR #5669和#5692中，这两个PR正在为记忆搜索添加重排序（reranker）支持，**是社区贡献和官方关注的重点方向**。这表明围绕“记忆”功能的增强是当前项目路线图的一个强信号。

5.  **已有PR对应的功能请求**:
    - **PR #5820** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5820)) 和 **PR #5815** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5815)): 这两个PR分别针对自动记忆搜索的token估算和状态管理进行了重构和增强，表明官方正在积极优化v2.0.0的自动记忆功能。它们与上述#5775等Bug修复紧密关联，是v2.0.0稳定化的关键步骤。
    - **PR #5805** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/5805)): 为桌面版Tauri应用添加DevTools入口，以方便高级用户进行性能分析和调试。

## 用户反馈摘要

从今日活跃的Issues中，可以提炼出以下真实用户声音：

- **“飞书渠道第一个消息回复，之后无反应。”** (#5757) - 这是当前最迫切的用户痛点，影响生产级使用，用户情绪较为急切。
- **“流式输出过程中浏览器卡顿，回答完毕恢复。同样场景DeepSeek网页版不卡。”** (#5725) - 用户对前端性能提出了高标准要求，并与竞品进行了直接对比。
- **“移动端WebUI所有页面底部内容被截断，按钮不可见。”** (#5787) - 移动端用户的直接负面体验，表明响应式设计有待完善。
- **“上下文压缩后Agent忘记自己在飞书群聊，做出不符合群聊规范的回复。”** (#5710) - 用户对压缩机制的副作用感到困扰，期望能更智能地保留关键上下文。
- **“定时任务弹窗功能，不应该一刀切关闭，应该让我自己选择开不开。”** (#5797) - 用户希望拥有更多主动控制权，而非被动接受开发者决策。
- **“云端部署的QwenPaw没有添加团队成员的设置，难以实施按用户的策略。”** (#5780) - 有团队使用需求的用户明确指出了项目在协作能力上的短板。
- **“离线使用Coding模式，无法预览文件内容，因为需要在线下载资源。”** (#5781) - 对离线/内网部署场景的支持提出了明确需求。

## 待处理积压

以下是值得重点关注但尚未有明确解决办法或回复的Issues/PRs：

1.  **#5401 Console大型会话渲染崩溃** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5401)): 作为破坏前端核心功能的严重Bug，已存在多日，虽经社区分析根因，但仍在等待官方或社区的修复PR。此问题在新发布的v1.1.12.post3中也未提及，需项目组优先评估。

2.  **#5775 Auto-memory间隔不生效** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5775)): 作为v2.0.0-b3的Bug，直接影响了自动记忆这一核心特性。虽然今日有PR #5815和#5820在优化相关模块，但此特定Issue直至截稿时仍为`OPEN`状态，提醒维护者在新PR中就此类问题进行验证。

3.  **#5773 OCG渠道因记忆搜索报错** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5773)): 使用特定渠道（OCG）的用户被一功能（auto_memory）阻塞所有请求，该问题影响面虽不及大型渠道，但对用户体验伤害极大。

4.  **#5725 Console流式输出过程中浏览器卡顿** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/5725)): 作为影响核心交互体验的性能问题，用户反馈明确且易于复现，建议开发团队在Console性能优化路线图中予以优先考虑。

5.  **#5710 上下文压缩与 #5789 压缩崩溃**: 这两个关于上下文压缩的Bug都指向了该功能的薄弱环节，建议项目组集中资源进行重审和加固。

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我已根据您提供的 hermes-agent 项目数据，为您生成了2026年7月7日的项目动态日报。

***

### Hermes-Agent 项目日报- 2026年7月7日

---

#### 1. 今日速览

项目在 **24小时内处理了超过789条 Issue 和 PR**，社区活跃度极高，接近“过热”状态。虽然今日无版本发布，但**团队在修复高频Bug（尤其是QQ机器人适配器问题）和优化核心功能（如代理上下文管理、桌面端体验）上投入了大量精力**。值得注意的是，待合并的PR数量（355条）远高于已关闭/合并的数量（145条），表明维护团队的审核与合并速度可能成为项目发展的瓶颈。同时，多个严重的P1/P2级Bug（如网关内存丢失、桌面端功能回归）仍在开放中，项目稳定性面临挑战。

---

#### 2. 版本发布

今日无新版本发布。

---

#### 3. 项目进展

尽管待合并PR积压严重，但今日仍有一些关键PR被提出，展示了项目在以下方面的推进：

*   **核心代理与上下文管理**：
    *   **[PR #59876]** 为 `context_references` 中的 `Future.result()` 增加了超时机制，防止URL获取挂起导致代理无限阻塞。
    *   **[PR #59870]** 修复了上下文压缩（Compression）功能，现在在会话恢复时能正确保留网关来源信息，防止会话路由出错。
    *   **[PR #55640]** 限制了 `session_search` 返回的上下文负载大小，解决了因注入过多历史会话导致的“上下文膨胀”和性能问题。

*   **桌面端（Desktop）与用户界面**：
    *   **[PR #59872]** 将MCP（Model Context Protocol）工具目录作为“连接器”（Connectors）在桌面端呈现，提升了易用性和集成体验。
    *   **[PR #59868]** 修复了桌面端通过 `Ctrl+C` 退出时的异常处理，改善了用户体验。

*   **网关与插件生态**：
    *   **[PR #59869]** 修复了Slack适配器在多配置文件模式下，套接字模式应用令牌（App Token）作用域不正确的Bug。
    *   **[PR #59867]** 提升了Photon（iMessage）插件，修复了回复消息上下文丢失的问题。
    *   **[PR #59846]** 扩展了NeMo Relay插件的版本兼容性，并支持动态插件激活。
    *   **[PR #59874]** 为网关新增了模糊技能建议功能，当用户输入错误命令时，会提供相似技能提示，改善了交互体验。

*   **开发者体验与诊断工具**：
    *   **[PR #59875]** 改进了 `hermes doctor` 诊断命令，增加了对 `npm` 全局安装包的检测，使其在无法通过 `which` 命令找到时依然能正确判断agent-browser的安装状态。

---

#### 4. 社区热点

今日讨论最热烈的Issue反映了用户对于**基础连接稳定性**和**平台扩展性**的强烈诉求：

1.  **QQBot适配器连接崩溃（#52914，#53443，#58646）**
    *   **链接**: [#52914](https://github.com/NousResearch/hermes-agent/issues/52914), [#53443](https://github.com/NousResearch/hermes-agent/issues/53443), [#58646](https://github.com/NousResearch/hermes-agent/issues/58646)
    *   **热度**: 总计 **28条评论**。
    *   **分析**: **QQ机器人适配器的连接问题已成为过去一周社区最大的痛点**。核心Bug（`is_reconnect`参数缺失）引发了无限重试和连接失败。虽然已有修复PR（#59870）提出，但多个重复Issue的出现表明该问题影响广泛，用户反馈非常急切。这反映出中国用户群体在项目中的重要性，以及单一平台Bug对社区情绪的显著影响。

2.  **Rocket Chat平台支持（#3725）**
    *   **链接**: [#3725](https://github.com/NousResearch/hermes-agent/issues/3725)
    *   **热度**: **14条评论**, 13个👍。
    *   **分析**: 对于添加 **Rocket Chat** 作为新消息通道的支持请求已持续3个月，至今仍热度不减。这表明用户对除Discord、Slack等主流平台之外的**企业级或开源替代品**有明确需求，社区渴望更大的平台多样性。

3.  **网关RBAC权限模型（#527）**
    *   **链接**: [#527](https://github.com/NousResearch/hermes-agent/issues/527)
    *   **热度**: **11条评论**, 6个👍。
    *   **分析**: 这是一个长期存在的功能请求，旨在引入细粒度的**角色访问控制**。讨论热度表明，随着项目向生产环境部署迈进，用户尤其是团队用户，对于**安全性和权限管理**的需求日益迫切。

---

#### 5. Bug 与稳定性 - *按影响范围排序*

| 严重程度 | Issue标题 | 摘要 | 状态 | 修复关联 |
| :--- | :--- | :--- | :--- | :--- |
| **P1** | Gateway Memory Loss — INSERT omits `active` column (#51646) | 网关消息写入数据库时 `active` 字段为NULL，导致代理在所有网关平台上零历史记录记忆。 | **Open** | 待确认 |
| **P2** | QQBot连接无限重试 (#52914, #53443, #58646) | `QQAdapter.connect()` 缺少参数导致持续崩溃和重试。 | **Open** | 有修复PR [#59870](https://github.com/NousResearch/hermes-agent/pull/59870) |
| **P2** | Desktop `/compress` 命令错误 (#44456) | TUI界面中 `compress` 命令被错误地当作未知命令处理，功能失效。 | **Open** | 待确认 |
| **P2** | Ollama模型上下文限制 (#43900) | 使用Ollama时，模型上下文被固定为4096 token，导致长文本被截断和生成错误。 | **Open** | 待确认 |
| **P2** | Projects范式破坏Desktop侧边栏工作流 (#53004) | 新版本重构的项目功能导致无法在侧边栏创建和选择会话文件夹。 | **Open** | 待确认 |
| **P2** | Desktop模型选择器只显示部分模型 (#59702) | 配置文件中的自定义提供者（`custom_providers`）条目在桌面端下拉菜单中缺失。 | **Open** | 待确认 |
| **P2** | MoA静默模式崩溃 (#58437) | 在安静模式下，`_collect_stream` 函数未收集工具调用消息，导致聚合器崩溃。 | **Open** | 待确认 |
| **P2** | Desktop配置文件删除失败 (#47368) | 删除配置文件的UI操作失效，文件被删除后会重新出现。 | **Open** | 待确认 |
| **P3** | Intel Mac上无法运行 (#37505, #42928) | 官方macOS DMG安装包仅支持`arm64`，在Intel Mac上无法启动。 | **Closed** | 由Issue [#42928](https://github.com/NousResearch/hermes-agent/issues/42928) 跟踪 |

**Bug修复进展**: 今日修复主要集中在**各种偶发性和边缘情况**，如对代理无响应、桌面端非正常退出等进行了加固。但核心的P1/P2级Bug（如内存丢失、重构回归）仍未关闭。

---

#### 6. 功能请求与路线图信号

*   **高热度、可能纳入下版本的功能**:
    *   **Claude订阅集成 (#25267)**: 此请求获得 **41个👍**，是社区最强烈的呼声之一。用户希望在不额外支付API费用的前提下，使用Claude模型。一旦技术方案（如Codex集成）达成，该功能将极大提升用户覆盖。
    *   **RBAC权限模型 (#527)**: 与安全性高度相关，是项目从个人工具走向企业级协作的必经之路。已有多个相关讨论，可能性较高。
    *   **Google Cloud语音服务 (#57120)**: 请求整合Google Chirp 3和ADC认证的TTS/STT。考虑到Google Cloud的超大用户基础，这是一个低频但高价值的集成。

*   **已出现对应PR的功能**:
    *   **子代理（Subagent）角色预设 (#56010)**: `[Feature]: 子代理角色预设 (PR #56010)` 已提交，与Issue #56010相对应，表明项目正在推进更精细化的代理编排能力。
    *   **Slack频道历史记录工具 (#54535)**: 一个只读的Slack历史查看工具，与`[Feature]`相关，丰富了网关平台能力。
    *   **桌面端MCP连接器 (#59872)**: 对应的PR已提出，说明将MCP工具标准化为桌面端“连接器”是大概率事件。

---

#### 7. 用户反馈摘要

*   **核心痛点 (高频)**: “**QQBot又用不了了**”和“**Desktop更新后X功能坏了**”是本周最常见的用户抱怨。这表明**回归测试**和**多平台兼容性测试**存在短板，用户的升级体验受到影响。
*   **性能与成本**: 用户在[#41490](https://github.com/NousResearch/hermes-agent/issues/41490)中抱怨“**代理陷入了重复调用同一工具的循环**”，而[#13332](https://github.com/NousResearch/hermes-agent/issues/13332)则提出“**过多的工具schema浪费了大量token**”。这反映出用户对**推理成本**和**执行效率**的高度敏感。
*   **不满意的地方**: 有用户反映**配置文件中 `terminal.cwd` 等设置被忽略 (#42961)**，以及**配置文件删除功能无效 (#47368)**。这些问题虽然不大，但累积起来损害了用户对软件稳定性的信任。
*   **满意与期待**: 对有明确场景的功能（如“**保持工具在本地运行，但远程连接Hermes Agent**”（#18715））期待值极高，获得了19个👍。用户希望项目能解决更复杂的分布式部署需求。

---

#### 8. 待处理积压

以下Issue/PR自创建以来长期未获得维护者或团队的明确回应，或处于停滞状态，提请维护者关注。

| 类型 | 标题 | 创建时间 | 链接 | 提醒理由 |
| :--- | :--- | :--- | :--- | :--- |
| **Issue** | Dashboard反向代理 `--allowed-hosts` 标志 (#34390) | 2026-05-29 | [链接](https://github.com/NousResearch/hermes-agent/issues/34390) | 已开放超过1个月，无 Assignee，但这是一个对生产部署安全至关重要的功能。 |
| **Issue** | 渐进式加载架构提议 (#16493) | 2026-04-27 | [链接](https://github.com/NousResearch/hermes-agent/issues/16493) | 这是一个架构级别的长期优化建议，得到社区讨论但无官方回应。 |
| **Issue** | Claude订阅集成 (#25267) | 2026-05-13 | [链接](https://github.com/NousResearch/hermes-agent/issues/25267) | 社区呼声最高（41 👍），但官方路线图中尚无明确信号，用户感到被忽视。 |
| **PR** | Zulip集成 (#3335) | 2026-03-27 | [链接](https://github.com/NousResearch/hermes-agent/pull/3335) | 一个3个月前的、功能完整的PR，至今仍在Open状态，未获审核。这会打击外部贡献者的积极性。 |

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*