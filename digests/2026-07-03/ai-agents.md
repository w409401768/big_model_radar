# OpenClaw 生态日报 2026-07-03

> Issues: 198 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-03 09:29 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于您提供的 OpenClaw 项目 GitHub 数据生成的 2026-07-03 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-07-03

## 1. 今日速览

今日 OpenClaw 项目继续保持极高活跃度，过去 24 小时内有 **198 条 Issues** 和 **500 条 PRs** 更新，显示出社区参与度和项目迭代速度均处于顶峰。然而，**418 条待合并 PR** 的积压量巨大，与 **82 条已处理 PR** 形成对比，可能暗示维护者审查能力出现瓶颈。从 Issue 内容看，**稳定性回归问题（P1 级别）** 和 **消息传递/会话状态丢失** 是当前社区最关切的痛点，尽管有多项修复 PR 在推进，但新问题涌现的速度依然很快。总体而言，项目处于“高活跃度、高风险”的快速发展阶段。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

尽管 PR 积压严重，今日仍有部分关键修复被合并或关闭，推动了项目在稳定性和安全性方面的进步。

- **修复 Gateway 锁文件描述符泄漏**：PR [#99291](https://github.com/openclaw/openclaw/pull/99291) 和 [#98848](https://github.com/openclaw/openclaw/pull/98848) 被合并，解决了 `gateway-lock.ts` 中当 `writeFile` 失败时文件描述符泄漏的问题，避免了潜在的系统资源耗尽风险。
- **修复会话压缩（Compaction）功能**：PR [#99386](https://github.com/openclaw/openclaw/pull/99386) 和 [#99391](https://github.com/openclaw/openclaw/pull/99391) 被关闭，修复了工具调用密集型会话中压缩功能失效、导致 session 上下文爆满的 Bug。这直接回应了社区反馈的稳定性问题。
- **优化 Gateway 诊断**：PR [#99407](https://github.com/openclaw/openclaw/pull/99407) 被合并，优化了诊断流程，避免在 `status` 或 `doctor` 命令中加载过大的日志文件，改善了运维体验。

## 4. 社区热点

今日社区讨论最热烈的 Issues 集中在 **消息泄漏、核心功能回归和平台兼容性** 上，反映出用户对稳定性和数据安全的高度关注。

- **文本泄漏问题（#25592）**：该 Issue 讨论了 Agent 在工具调用之间产生的内部处理文本被错误地路由到用户可见的即时通讯频道，如 Slack 或 iMessage。这是一个严重的 UX 和安全问题，获得了 **33 条评论**，是今日讨论热度最高的话题。
- **Codex 服务器超时回归（#88312）**：这是一个 Bug 回归报告，描述了一个在 `2026.5.27` 版本引入的“Codex 在确认轮次完成前停止”的问题。它有 **19 条评论** 和 5 个 👍，并指出这是对之前一个已修复问题（#84076）的回归，社区对版本质量倒退表现出明显的挫败感。
- **Anthropic 思考签名失效（#92201）**：该问题讨论了嵌入式运行器在重放来自 Anthropic 的流式思考块时，由于签名失效导致的中断。问题的复杂性在于错误信息被通用化，导致恢复逻辑无法工作，引发了 **18 条评论** 的热烈讨论。

## 5. Bug 与稳定性

今日报告的 Bug 涉及范围广，其中 **P1（最高优先级）** 问题突出，尤其是 `session-state`（会话状态）和 `message-loss`（消息丢失）相关复现率高。

| 严重程度 | Issue / PR | 问题描述 | 是否有 Fix PR |
| :--- | :--- | :--- | :--- |
| **严重** | [#88312](https://github.com/openclaw/openclaw/issues/88312) | [回归] Codex 服务器轮次完成停滞，是已修复问题的再回归。 | 状态：OPEN，尚无 Fix PR |
| **严重** | [#92201](https://github.com/openclaw/openclaw/issues/92201) | [P1] 嵌入式运行器中 Anthropic 思考签名失效，导致重放失败且无法恢复。 | 状态：OPEN，尚无 Fix PR |
| **严重** | [#98416](https://github.com/openclaw/openclaw/issues/98416) | [P1] `v2026.6.11` 发布版本遗漏了“重入（reentrancy）”守卫，导致回复会话初始化冲突。 | 状态：OPEN，尚无 Fix PR |
| **严重** | [#98528](https://github.com/openclaw/openclaw/issues/98528) | [回归] `v2026.6.11` 中工具（exec, web_fetch等）首次调用后返回空结果。 | 状态：CLOSED，已有关联 PR |
| **较高** | [#99263](https://github.com/openclaw/openclaw/issues/99263) | [P1] Gateway 在 Node.js 26 上因图片处理导致 `FileHandle` 被 GC 回收而崩溃。 | 状态：OPEN，尚无 Fix PR |
| **较高** | [#98673](https://github.com/openclaw/openclaw/issues/98673) | [P1] `v6.11` 中 `sanitizeContentBlocksImages` 函数错误地将文本工具结果转换为图片块，污染会话历史。 | 状态：OPEN，尚无 Fix PR |
| **较高** | [#98614](https://github.com/openclaw/openclaw/issues/98614) | [回归] `sessions_spawn` 在 `v2026.6.11` 中缺少 `operator.write` 权限，导致操作失败。 | 状态：OPEN，关联 PR[#？] 待确认 |

**稳定性趋势**：数据显示，特别是 `v2026.6.11` 版本发布后，出现了数个与工具执行、会话状态相关的回归问题，建议用户如有顾虑可暂缓升级，或密切关注相关修复的动态。同时，关于 `compaction` 的修复（[#99386](https://github.com/openclaw/openclaw/pull/99386)、[#99391](https://github.com/openclaw/openclaw/pull/99391)）已经合并，预期能缓解部分会话相关的稳定性问题。

## 6. 功能请求与路线图信号

尽管用户对稳定性呼声更高，但仍有结构性的功能请求被提出，预示着后续版本的潜在方向。

- **多智能体协作增强（#35203）**：这是一个详细的 RFC，提出了包括能力画像、共享黑板、分层记忆和 Token 成本治理在内的多个增强点。这反映了社区对于构建更复杂、高效的多 Agent 系统的强烈需求。
- **提供商故障分类和隔离（#47910）**：提议根据故障类型（如认证失败、限流、网络超时）对模型提供商进行分级的故障转移，将被认证阻断的提供商自动隔离。这是一个非常务实的改进，可以显著提升系统的鲁棒性。
- **外部工作区自动发现（#32530）**：希望 OpenClaw 能自动发现并加载来自指定目录的 Agent 配置，减少手动注册的繁琐步骤，这符合用户对更灵活配置管理的期望。

## 7. 用户反馈摘要

从今日的 Issue 讨论中，可以提炼出以下用户声音：

- **对回归问题感到沮丧**：用户在面对“之前能用的，更新后就不能用了”这类回归性 Bug 时表达了明显的困扰，尤其是 #88312 这种反复出现的回归问题，极大地影响了用户对发布质量的信任。
- **渴望透明的错误信息**：用户在 [#73148](https://github.com/openclaw/openclaw/issues/73148)（`Failed to optimize image`）和 [#92201](https://github.com/openclaw/openclaw/issues/92201)（通用错误文本）中反复提出，晦涩难懂的错误信息让他们无法定位和解决问题，期望能有更清晰、更具指导性的错误提示。
- **对数据/消息泄漏高度敏感**：Issues [#25592](https://github.com/openclaw/openclaw/issues/25592)（文本泄漏到频道）和 [#99253](https://github.com/openclaw/openclaw/issues/99253)（AI 伪造用户输入）引发了较多关注，表明用户对 Agent 行为的边界和数据安全性非常在意。
- **高度依赖“小修小补”**：像 [#99439](https://github.com/openclaw/openclaw/issues/99439)（iOS UI 密度）和 [#99237](https://github.com/openclaw/openclaw/issues/99237)（`doctor --fix` 因 `.bashrc` 只读而失败）这类细节问题虽然小，但直接影响日常使用体验，用户乐于提出并期待快速解决。

## 8. 待处理积压

- **核心问题积压**：多个影响重大的 **P1** 级别 Issue（如 `#88312`, `#92201`, `#98416`）仍处于 `OPEN` 状态，且尚无明确的修复 PR。这些问题是目前社区稳定性的最大威胁，亟需维护团队优先评估和介入。
- **长期未响应 Issue**：一些被标记为 `stale` 但仍为 **P2** 或更高严重等级的问题，如 [#73148](https://github.com/openclaw/openclaw/issues/73148)（`Failed to optimize image`），以及 [#55401](https://github.com/openclaw/openclaw/issues/55401)（Per-agent 插件配置覆盖），虽然讨论热度不高，但已持续开放超过两个月，对特定用户群体仍是痛点，建议维护者定期回顾并更新状态。
- **PR 审查瓶颈**：当前有 **418 个待合并 PR**，远超过每日合并/关闭的数量。这是一个需要高度关注的风险信号。为了提高迭代效率，建议项目团队考虑：
    1.  增加活跃的维护者或定期审批人。
    2.  明确 PR 的准入标准，引导贡献者提供更高质量的提交。
    3.  考虑设置自动化流程来处理一些低风险的、格式性或文档性的 PR。

---

---

## 横向生态对比

好的，作为资深技术分析师，现基于您提供的2026-07-03各项目社区动态摘要，为您呈现一份横向对比分析报告。

---

### AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-07-03)

#### 1. 生态全景

当前，个人 AI 助手/自主智能体开源生态正处于 **“规模爆发”与“质量阵痛”** 并存的阶段。头部项目（OpenClaw, hermes-agent）凭借先发优势吸引了海量贡献，But 正面临 PR 审查瓶颈、频繁回归问题和用户信任危机。第二梯队（Zeroclaw, QwenPaw）则在特定的架构创新（如 OIDC、上下文策略）上快速迭代，展现出更强的产品锐度。整体来看，生态正从单一的“跑通对话流程”向 **“高可用、高安全、多模型、多智能体协作”** 的生产力工具转型，用户对部署稳定性、数据安全性和跨平台体验的要求已跃升为首要关注点。

#### 2. 各项目活跃度对比

| 项目 | 今日 Issue 动态 | 今日 PR 动态 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 198 (高活跃) | 500 (瓶颈严重) | 无 | **需关注**：规模最大，但 418 Pending PR 与严重回归问题并存，运维风险高。 |
| **hermes-agent** | 302 (最高) | 500 (最高) | 无 | **需关注**：贡献溢出但社区摩擦大，Dashboard UX 与关键渠道 Bug 亟需解决。 |
| **Zeroclaw** | 33 | 50 | 无 | **健康**：迭代高效，核心修复（WSL2 OOM）与路线图 RFC 双线并行。 |
| **QwenPaw** | 40+ | 40+ | 无 | **健康**：v2.0 Beta 高强度修复期，社区和官方响应迅速，但稳定性仍是痛点。 |
| **PicoClaw** | 1+ | 29 | **v0.3.1** | **需关注**：Release 本身带来了配置迁移阻塞，升级路径断裂，影响用户留存。 |

#### 3. OpenClaw 在生态中的定位

**优势与壁垒**：OpenClaw 是社区的“核心参照”，拥有最大的用户基数和最全面的功能覆盖。其 PR 单日 500 的量级是其他项目的 10 倍以上，这种规模效应构成了巨大的生态粘性。

**技术路线差异**：OpenClaw 走的是 **“大一统”通用网关** 路线，试图解决所有问题，这也导致了其架构臃肿和严重的合并瓶颈。相比之下，**Zeroclaw** 更侧重 **AI-Native 架构（OIDC、OpenAI 兼容）**，追求企业级治理；**PicoClaw** 则走向 **“轻量化连接器”** 路线，聚焦边缘设备和新兴协议。

**社区规模对比**：从数字上看，OpenClaw 是唯一的 **“超级头部”**。但 Zeroclaw 和 QwenPaw 虽然在活动数量上低一个量级，其社区讨论质量（RFC 深度、问题根治能力）和创新活跃度不容小觑，是生态中不可忽视的“潜力挑战者”。

#### 4. 共同关注的技术方向

生态内多个项目不约而同地指向了以下结构性问题：

1.  **模型故障转移与高可用（Multi-Model Fallback）**：
    - **涉及项目**：**PicoClaw** (#3200 模型备用链路)、**QwenPaw** (#5718 自动切换模型)、**OpenClaw** (#47910 提供商故障分类)。
    - **诉求**：用户不再满足于绑定单一 API，要求 Agent 具备 **“弹性”**，在限流或故障时自动切换，这是 Agent 走向生产环境的刚性需求。

2.  **安全与权限精细化（Security & Permission Granularity）**：
    - **涉及项目**：**OpenClaw** (#25592 文本泄漏)、**Zeroclaw** (#8044 指令鉴权)、**PicoClaw** (#3217 角色白名单)、**hermes-agent** (#5528 自定义审批命令)。
    - **诉求**：社区强烈要求 Agent 行为边界可控，从“聊天泄漏”到“操作审批”，**企业级安全治理**正在从可选项变为必选项。

3.  **上下文与记忆机制优化（Context & Memory Optimization）**：
    - **涉及项目**：**OpenClaw** (#99386 会话压缩修复)、**QwenPaw** (#5746 Scroll 策略缺陷)、**hermes-agent** (#47349 可插拔记忆后端)。
    - **诉求**：上下文窗口限制是 Agent 智能的“阿喀琉斯之踵”。用户期待更智能的压缩（而非简单裁剪）和更专业的记忆管理（数据库后端支持），以提升长对话的连贯性。

#### 5. 差异化定位分析

| 维度 | OpenClaw | Zeroclaw | PicoClaw | QwenPaw | hermes-agent |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全功能 Agent 网关与运行时 | AI 原生身份治理与可观测性 | 轻量级多平台连接与嵌入 | 上下文策略与工具链稳定性 | 桌面级 UX 与大规模集成生态 |
| **目标用户** | 重度开发/运维（自建 Pipeline） | 企业架构师（身份/成本/路由） | 个人极客/边缘部署玩家 | 高阶研究员/技术控（追求极致智能） | 内容创作者/终端重度用户 |
| **技术架构** | 单体大库（高槽位、高耦合） | 模块化框架（高迭代、架构清晰） | 插件式连接器（轻量化、聚焦） | 运行时优化（上下文、工具调用） | 客户端+Gateway（功能分层） |
| **社区风格** | “劳动密集型”，管理摩擦大 | “精英密集型”，RFC 驱动 | “功能驱动”，补丁迅速 | “问题驱动”，修复准确度高 | “情绪密集型”，体验诉求强烈 |

#### 6. 社区热度与成熟度

- **第一梯队：超大规模“维护期阵痛”**
  - **OpenClaw & hermes-agent**：日均 Issue/PR 超过 500 条，社区推动力极强。但已进入 **“质量巩固与信任修复”** 阶段。用户对 v2026.6.11 的回归感到沮丧，对 Dashboard 糟糕的 UX 提出抗议。成熟度很高，但维护成本剧增。

- **第二梯队：高速迭代“功能冲刺期”**
  - **Zeroclaw & QwenPaw**：日均 Issue/PR 在 50-100 条之间，项目正处于 **“能力架构搭建”** 的黄金时期。Zeroclaw 忙于 OIDC 和 OpenAI 兼容，QwenPaw 在修复 Scroll 机制。社区反馈诚恳，官方响应积极，项目健康度非常高，是未来半年的增长主力。

- **第三梯队：特定领域“质量巩固期”**
  - **PicoClaw**：活跃度较低，但目标明确（多渠道、嵌入式）。其 v0.3.1 的发布直接带来了迁移阻塞，说明处于 **“快速试错”** 阶段，成熟度尚不足以支撑平滑升级，适合喜欢尝鲜的开发者。

#### 7. 值得关注的趋势信号

1.  **开发者体验压倒功能数量**：多个项目用户因安装卡死（#7066）、启动崩溃（#55658）、文档不符（#5200）而受挫。**“开箱即用”与“稳定运行”** 已超越“功能多寡”，成为留存用户的第一要素。

2.  **Agent 架构从“单体”走向“C/S 分离”**：hermes-agent 的“瘦客户端”诉求 (#38602) 是一个强烈信号。用户希望将重型 Agent 进程运行在服务器，本地只安装轻量 UI。这预示着 **Agent Infrastructure** 的构建将进入一个新阶段。

3.  **数据安全成为准入证，而非加分项**：OpenClaw 的文本泄漏 (#25592)、Zeroclaw 的遥测脱敏 (#8567)、QwenPaw 的密钥日志泄漏 (#5705) 在不同项目同时爆发。**“安全证明能力”** 将是 AI Agent 打入企业市场要跨越的第一道门槛。

4.  **模型中立性与抗锁定**：用户对 Model Fallback 和统一路由的强烈需求，表明社区已深刻意识到对单一模型 API 的依赖性风险。**开源 Agent 框架的正统性，在于帮助用户保持对 LLM 的选择主权。**

5.  **从“聊天”到“任务自动化”的跨越**：Zeroclaw 的目标模式 (#8303)、OpenClaw 的多智能体协作 (#35203)，都指向了一个方向：用户不再需要“聊伴”，而是需要一个能自主执行、有状态、可审计的 **“数字员工”**。

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是根据您提供的 Zeroclaw 项目数据生成的 2026-07-03 项目动态日报。

---

### 2026-07-03 Zeroclaw 项目动态日报

#### 1. 今日速览

项目于 2026-07-03 维持极高强度迭代，24 小时内共处理 33 条 Issue 与 50 条 PR 更新。当日虽无新版本发布，但核心团队展现了对 WSL2 稳定性顽疾的强大攻坚能力（OOM 核心修复补丁合并），同时对 v0.8.3 特性扫尾（统一内存上下文、多渠道/可观测性策略）与面向 v0.9.0 的重大架构 RFC（OIDC、OpenAI 兼容 API）进行了“双线并进”。值得注意的是，ZeroCode TUI 领域集中暴露了 6 个 Bug/FR，表明该零代码交互面正处于密集的品质打磨初期。

#### 2. 版本发布

当日无新版本发布。项目当前处于 v0.8.2 与 v0.8.3 之间的特性积累阶段，社区提交的大规模 PR（如 OpenAI 兼容端点、Telegram 流式模式、Scoped 工具注册表）均已进入合并队列或密集审核期。

#### 3. 项目进展

过去 24 小时内，项目关闭/合并了 9 个 Pull Request，生态走向更加稳固：

- **运行时稳定性修复（高优）**：
  - [[#8633]](https://github.com/zeroclaw-labs/zeroclaw/pull/8633) **(已合并)**：修复 `component supervisor` 在组件异常 `Ok(())` 退出时退避策略重置的问题，根治了 WSL2 环境下频繁的 OOM 崩溃风暴。
  - [[#8599]](https://github.com/zeroclaw-labs/zeroclaw/pull/8599) 与 [[#8488]](https://github.com/zeroclaw-labs/zeroclaw/pull/8488) **(已合并)**：对齐了 `Agent::from_config` 和渠道消息中的工具分发器与系统提示词，消除了特定路径下的工具调用与视感知路由兼容性问题。

- **安全与可观测性加码**：
  - [[#8554]](https://github.com/zeroclaw-labs/zeroclaw/pull/8554) **(已合并)**：为技能 ZIP 提取器增加了漏洞（ZIP 炸弹）的防御。
  - [[#8567]](https://github.com/zeroclaw-labs/zeroclaw/pull/8567) (待合并)：实现运行时 OTel 内容策略，默认禁止传输 LLM/Tool I/O 载荷，堵住遥测侧信道泄漏风险。
  - [[#8640]](https://github.com/zeroclaw-labs/zeroclaw/pull/8640) (待合并)：引入 `ScopedToolRegistry` 组装线，为网关侧工具注册提供审计与隔离边界。

- **渠道与文档打磨**：
  - [[#8656]](https://github.com/zeroclaw-labs/zeroclaw/pull/8656) (待合并)：修复微信频道的 Markdown 表格与格式渲染问题。
  - [[#8610]](https://github.com/zeroclaw-labs/zeroclaw/pull/8610)、[[#8612]](https://github.com/zeroclaw-labs/zeroclaw/pull/8612)、[[#8613]](https://github.com/zeroclaw-labs/zeroclaw/pull/8613) **(已合并)**：新增内存生命周期架构指南、标签规范并完善合并且新鲜度检查机制。

#### 4. 社区热点

当日讨论最热烈的议题反映了社区对平台稳定性与功能扩展性的双重渴求：

- **[[#5542]](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) WSL2 OOM 进入终局**：作为长期占据热点榜的高关注度 Issue，随着修复补丁 #8633 的合并，以及根因拆分为具体跟踪项（#8642），社区与核心团队联合排障的成熟机制得到体现。
- **[[#7141]](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) OIDC 认证 RFC**：7 条评论集中讨论了可插拔认证架构。用户 @singlerider 建立的 Tracker #8289 成为多用户企业部署的有力信号。
- **[[#7462]](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) Windows 平台之痛**：74 个测试失败的现状引发社区强烈共鸣。用户 @NiuBlibing 提出的“CI does not catch this because the Test job only runs on Linux”点出了平台兼容性测试的缺失，呼声极高。
- **[[#8603]](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) OpenAI 兼容适配器**：该 RFC 提出后，用户 @REL-mame 迅速转化为庞大 PR #8486，虽然体量巨大导致审核压力，但社区共建热情可见一斑。

#### 5. Bug 与稳定性

报告期内注入了一批严重影响稳定性的 Bug，需重点盯防：

| 严重度 | 编号 | 问题描述 | Fix PR 状态 |
|---|---|---|---|
| S1 | [[#8631]](https://github.com/zeroclaw-labs/zeroclaw/issues/8631) | Headless SOP 步骤被错误标记为“已完成”，产生虚假审计线索 | **未修复** |
| S1 | [[#8654]](https://github.com/zeroclaw-labs/zeroclaw/issues/8654) | `skill-review` 分叉 Panic 导致进程 `SIGSEGV` (139) | **未修复** |
| S1 | [[#8642]](https://github.com/zeroclaw-labs/zeroclaw/issues/8642) | MCP 工具模式克隆导致 RSS 无限增长（从 #5542 拆分出的根因） | **未修复** |
| S1 | [[#8645]](https://github.com/zeroclaw-labs/zeroclaw/issues/8645) | 环境变量覆写密钥导致 Web 重载横幅显示永久漂移 | **未修复** |
| S1 | [[#8632]](https://github.com/zeroclaw-labs/zeroclaw/issues/8632) | 源码安装带 `embedded-web` 因 API 客户端生成滞后而编译失败 | 修复 PR [[#8643]](https://github.com/zeroclaw-labs/zeroclaw/pull/8643) |
| S2 | [[#8334]](https://github.com/zeroclaw-labs/zeroclaw/issues/8334) | `skills install` 在多 Agent 场景下指向错误的数据目录 | 进行中 |
| S2 | [[#8644]](https://github.com/zeroclaw-labs/zeroclaw/issues/8644) 等 | ZeroCode TUI 集中出现 5 个 UI/UX 瑕疵（配置文本异常、超时无反馈、日志截断等） | **未修复** |

#### 6. 功能请求与路线图信号

该日的 Issue/PR 新增清晰地指向了项目向 AI-Native 框架演进的几个关键维度：

- **AI 原生 API 兼容性**：[[#8603]](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) 提出的 OpenAI Chat Completions 适配器，目标是让 Zeroclaw 无缝对接 LangChain、Open WebUI、Continue.dev。社区成员提交的 [[PR #8486]](https://github.com/zeroclaw-labs/zeroclaw/pull/8486) 证明了该功能的极高呼声。
- **有界自主工作模式**：[[#8303]](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) RFC 的 Goal Mode 旨在让代理执行有预算/暂停/失败兜底的目标驱动任务，是对当前交互式/定时任务的强有力价值扩展。
- **身份与权限架构深化**：OIDC 体系（[[#7141]](https://github.com/zeroclaw-labs/zeroclaw/issues/7141), [[#8289]](https://github.com/zeroclaw-labs/zeroclaw/issues/8289)）持续演进，同时 [[#8044]](https://github.com/zeroclaw-labs/zeroclaw/issues/8044) 要求对 `/model --agent` 这一“全局模型切换”指令进行发送者鉴权，显示安全模型趋于精细。
- **自动化编排增强**：[[#8397]](https://github.com/zeroclaw-labs/zeroclaw/issues/8397) 提议将 Cron 任务内部的 `uses_memory` 标志暴露到 CLI/工具接口中，使自动化任务的上下文注入更加透明。

#### 7. 用户反馈摘要

- **WSL2 用户的绝望感**：长期 OOM 严重阻碍开发流程。[@Themoonshinesontheriver 报告的具体日志显示](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)，进程在内存耗尽时被 OOM Killer 强制结束，极端影响用户体验。
- **Windows 用户被“遗忘”**：[@NiuBlibing 指出](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) CI 仅在 Linux 运行导致 74 个测试未捕获，跨平台的呼声已上升为对项目包容性的质疑。
- **MCP 生态体验受阻**：[@susyabashti 的报告](https://github.com/zeroclaw-labs/zeroclaw/issues/8302) 透露，配置的 MCP 工具虽然在运行中可见，但在管理 UI 中不可见，严重影响了 MCP 生态开发者的调试体验。
- **CI/CD 场景的信任危机**：[@Stalesamy 反馈的 Headless SOP 虚假完成状态](https://github.com/zeroclaw-labs/zeroclaw/issues/8631) 是一个危险的 S2 错误——在自动化接管、无人排障的场景下，它提供的不仅是 Bug，更是虚假的信任感。
- **第三方开发者的积极正反馈**：[@REL-mame（OpenAI 端点贡献者）和 @singlerider（OIDC 推动者+插件验证者，[#8636]）展示了强大的社区共建动力。插件验证报告表示按官方文档走通全流程后发现了潜在迭代点，这本身即是高质量的反馈。

#### 8. 待处理积压

以下长期悬而未决的问题或 PR 建议维护团队重点关注，及时给出明确回应或加速推进：

- **长期悬而未决**：
  - [[#7462]](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) **(Windows 测试失败)**：自 6 月 10 日提出已近一个月，社区要求增加 Windows CI 的呼声极高。建议官方明确回复是否纳入路线图或给出特定延迟说明。
  - [[#7065]](https://github.com/zeroclaw-labs/zeroclaw/issues/7065) **(Agent 评估框架 RFC)**：发布整一个月，对评估 Prompt 质量和模型表现至关重要，目前仍处于无维护者回应的状态，请尽快推动设计决策。

- **可能阻塞生态发展**：
  - [[#8302]](https://github.com/zeroclaw-labs/zeroclaw/issues/8302) **(MCP 工具 UI 不可见)**：虽标记为 `in-progress`，但对于 MCP 生态而言，没有 UI 可视化管理几乎等同于“无法使用”，建议优先合入。
  - [[#8334]](https://github.com/zeroclaw-labs/zeroclaw/issues/8334) **(`skills install` 多 Agent 失效)**：“拉取即可使用”的工作流断裂对多 Agent 部署场景是致命打击，建议尽快修复。

- **待审核的庞然大物**：
  - [[PR #8486]](https://github.com/zeroclaw-labs/zeroclaw/pull/8486) **(OpenAI Chat Completions)**：体量 XL，对维护者是巨大负担。建议维护者引导贡献者将其拆分为功能性积木块（例如：先 `/v1/models`、再 `/v1/chat/completions`、最后 `/v1/auth`），分批合入以确保代码质量。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，以下是根据提供的 GitHub 数据生成的 2026-07-03 PicoClaw 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-07-03

## 1. 今日速览

今日 PicoClaw 项目迎来了显著的活跃度井喷，共计 **29 个 Pull Requests** 更新及 **1 个新版本 Release (v0.3.1)**。社区贡献空前踊跃，尤其是 @AMEOBIUS 集中提交了 4 个涉及多平台断线重连与配置迁移的修复。然而，新版本的发布与用户反馈的配置迁移故障出现了时间差：**v0.3.1 并未包含今日提交的迁移修复**，导致升级路径出现严重阻塞。总体来看，项目进入了密集的 Bug 修复与平台适配期，社区为解决生产环境稳定性问题投入了大量精力，项目健康度良好但需立即响应关键阻断性问题。

## 2. 版本发布

昨日发布了 **v0.3.1** 版本。根据 Changelog，该版本主要合并了 `#2917` (nearai-provider 整合) 和 `#3053` (codex/store-lock-type-assert) 等基础架构改进与 Provider 更新。

- **版本号**：[v0.3.1](https://github.com/sipeed/picoclaw/releases)
- **更新内容**：主要为内部架构重构与依赖更新，未包含破坏性变更说明。
- **迁移注意**：用户反馈显示 v0.3.1 版本仍存在 v2→v3 的配置迁移 Bug（见 #3206）。如果你正在从 v2 版本升级，建议暂缓升级，等待包含 `#3218` 修复的下一个补丁版本。

## 3. 项目进展

过去 24 小时共有 **15 个 PR** 被合并或关闭，核心进展集中在安全增强与依赖维护：

- **安全加固**：
  - `#3160` - 合入了跨站点 Launcher 设置请求防护，阻止了潜在的 CSRF 攻击。
  - `#3161` - 修复了自定义允许规则可能完全绕过 “deny” 列表的安全漏洞。
- **平台扩展**：
  - `#3063` - DeltaChat 网关功能已被合并，PicoClaw 的通信渠道生态进一步扩大。
- **依赖维护**：Dependabot 自动合入了多项前端（Eslint、React-i18next、Shadcn 等）与 Go 后端（AWS SDK、Mautrix）的依赖更新。
- **功能里程碑**：虽然 `#2937` (Agent 协作总线) 和 `#3156` (Token 用量统计) 因长期未跟进而被标记为 Stale 或已关闭，但项目的核心框架已为复杂协作做好了基础准备。

## 4. 社区热点

- **配置迁移阻塞事件（#3206）**：虽然目前尚无用户评论，但作为全天唯一的新 Issue，它直接断送了用户从 v2 升级到 v3 的路径。这大概率会成为社区明日讨论的绝对焦点。@OhYash 的全新安装也遭遇失败，暗示问题在旧版本中普遍存在。
- **@AMEOBIUS 的批量提交**：该贡献者今日连续提交了 4 个 PR（`#3217`, `#3218`, `#3219`, `#3220`），涵盖 Discord 权限控制、配置迁移修复以及 WhatsApp/Matrix 的断线重连。这表明社区中存在着对**连接可靠性**和**企业级权限**的强烈呼声。
- **模型备用链路（#3200）**：由 @lc6464 提出的功能，允许在 WebUI 配置故障切换链路，提升 AI 服务的可用性。这是一个高价值、低侵入的功能，得到了社区的广泛关注。

- [Issue #3206: v2→v3 配置迁移失败](https://github.com/sipeed/picoclaw/issues/3206)
- [PR #3200: 可配置默认备用链路](https://github.com/sipeed/picoclaw/pull/3200)

## 5. Bug 与稳定性

| 严重程度 | 问题描述 | 状态 | 链接 |
| :--- | :--- | :--- | :--- |
| **严重** | **配置迁移完全失败**：运行 picoclaw status 时，v2→v3 迁移解析报 `unknown field(s): build_info, session.dm_scope`。 | 待修复，已有 PR `#3218`。 | [Issue #3206](https://github.com/sipeed/picoclaw/issues/3206) |
| **高危** | **代码回滚**：今日提交了 `#3221` 来回滚之前对 Sandbox FS 的 Windows 路径处理修复，因其导致了 `provider.go` 中的日志导入错误。 | 正在处理。 | [PR #3221](https://github.com/sipeed/picoclaw/pull/3221) |
| **中等** | **WhatsApp 连接静默断开**：WebSocket 在运行 2-3 天后会永久性断开，且不会自动恢复。 | 待合并，已有 PR `#3220`。 | [PR #3220](https://github.com/sipeed/picoclaw/pull/3220) |
| **中等** | **Matrix 同步循环永久死亡**：在发生网络波动或 HomeServer 重启后，同步循环会直接退出且无法自愈。 | 待合并，已有 PR `#3219`。 | [PR #3219](https://github.com/sipeed/picoclaw/pull/3219) |

## 6. 功能请求与路线图信号

- **企业级频道控制**：`#3217` 提议为 Discord 渠道新增角色白名单（allow_roles），允许管理员细粒度控制哪些角色能使用 Bot。这与当前社区对安全性的诉求一致。
- **多模型高可用（Model Fallback）**：`#3200` 提出的模型备用链路，表明用户期望在生产环境上建立一个可靠的多模型网关。这极有可能被纳入下一个小版本。
- **扩展通信协议生态**：`#3193` (Simplex Channel) 以及已合并的 DeltaChat，显示项目正在迅速拥抱去中心化/轻量级通信协议，这是其区别于竞品的重要路线图方向。

## 7. 用户反馈摘要

- **@OhYash (Config Migration)**：反馈显示即使在新安装的环境下，配置迁移也无法运行，导致应用无法启动。这是典型的回归或未兼容场景，直接影响了用户对版本升级的信心。
- **@AMEOBIUS (WhatsApp/Matrix Connectors)**：在 PR 描述中具体描述了长期运行的痛点。他提到 WhatsApp 连接在 2-3 天后就会“永久静默断开”，Matrix 连接在 HomeServer 重启后也“永久死亡”。这反映了核心用户希望 PicoClaw 能作为“永不掉线”的守护进程运行，但目前稳定性还无法满足其期望。
- **@danmobot (Security)**：提交的修复表明用户在执行中发现了正则绕过和跨站请求伪造的风险，说明社区中不乏安全专家在对其进行“渗透测试”。

## 8. 待处理积压

- **Agent 协作总线（#2937）**：由 @afjcjsbx 提出，开启于 2026-05-24，今日有更新但标记为 Stale。该 PR 引入了邮箱、隔离历史记录和权限感知调度等复杂设计。如果项目期望推动多智能体工作流，此 PR 需要维护者明确路线图对齐，否则存在大量代码腐烂风险。
- **OpenAI Compat Seed XML 兼容修复（#3165）**：为兼容火山引擎豆包的 `tool_call` 格式而提的修复，已 Stale 11 天。由于国内开发者使用该模型非常多，建议维护者优先合入。

- [PR #2937: Agent 协作总线](https://github.com/sipeed/picoclaw/pull/2937)
- [PR #3165: 恢复 Seed XML 工具调用](https://github.com/sipeed/picoclaw/pull/3165)

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我将根据您提供的 QwenPaw 项目数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

### QwenPaw 项目动态日报 | 2026-07-03

**分析师点评**: 项目整体处于“高活跃 - 预发布周期”阶段。社区对 v2.0 beta 版本的测试反馈显著增加，暴露出一些关键的稳定性和上下文管理问题，但同时也有大量针对性的修复 PR 快速跟进。项目在向 v2.0 架构迁移的过程中，正经历一个密集的 Bug 修复与功能优化期。

### 1. 今日速览
过去 24 小时，QwenPaw 项目保持高度活跃。Issue 与 PR 的更新量均超过 40 条，表明社区参与度极高。值得关注的是，**Bug 报告（特别是针对 v2.0 beta）占据了主导**，暴露出 `scroll` 上下文策略的核心缺陷和工具调用的稳定性问题。与此同时，**社区贡献者反应迅速**，多个高价值修复 PR 在问题报告当日即被提交，体现了良好的开源协作生态。总体来看，项目当前处于 **“高强度 Bug 修复与功能迭代并行”** 的状态，正为走向稳定版做最后冲刺。

### 2. 版本发布
无新版本发布。

### 3. 项目进展：关键修复与架构演进
今日没有合并/关闭的“重大” PR，但多个已提交的修复 PR 直接瞄准了社区报告的核心痛点，项目正在快速响应并解决 v2.0 版本中的关键问题。

- **`scroll` 上下文策略重大缺陷确认与修复**:
    - **Bug 报告**: `#5746` 报告了 `scroll` 策略可能导致当前任务被错误折叠的问题，影响范围严重。
    - **修复 PR**: `#5747` 和 `#5765` 均在当日提交。特别是 `#5765`，它不仅在 `#5747` 的基础上增加了对当前 `turn` 的保护，还引入了 **“渐进式压力释放”（graduated pressure relief）** 机制，使上下文压缩更加智能，并确保模型在召回失败时能明确感知。这标志着 `scroll` 策略从简单粗暴的裁剪向精细化、智能化的关键演进。
- **工具调用稳定性修复**:
    - **Bug 报告**: `#5717` 报告了 `tool_call.input` 被截断可能导致无限循环执行工具的问题。
    - **修复 PR**: `#5761` 迅速响应，提出在模型请求中**暴露格式错误的 tool-call**，让模型自身进行理解与恢复，而非简单静默丢弃，这能从根本上提高模型对异常情况的处理能力。
- **基础设施与质量保障**:
    - **新功能**: `#5736` (feat(ci): add QwenPaw review bot) 引入了自动化代码审查机器人，有望提升 PR 的审查效率和质量。
    - **新渠道**: `#5762` (feat(channel): add azure_bot channel) 增加了对 Azure Bot Framework 的支持，扩展了在 Teams、Slack 等企业级平台上的应用场景。

### 4. 社区热点：活跃讨论与核心诉求
今日讨论的热点集中在 v2.0 版本的稳定性挑战和长期存在的安全/权限问题上。

1.  **`scroll` 上下文压缩的逻辑缺陷 (Issue `#5746`)**
    - **讨论**: 有 4 条评论，但引起了维护者的高度关注，并迅速衍生出 `#5747` 和 `#5765` 两个修复 PR。用户 `@biaobiaobiao108` 详细描述了整个上下文丢失的过程，为定位问题提供了关键线索。
    - **诉求**: 用户希望 `scroll` 策略能更加智能，**保护正在执行的任务不被错误裁剪**，这是一个非常核心的可用性诉求。

2.  **政策执行（Policy Execution）不生效 (PR `#5506`)**
    - **背景**: 这个由 `@chenzhengcai` 提交的修复 PR 虽然本身评论不多，但其修复的 **“前端策略无法同步到后端”** 以及 **“`off` 值不生效导致审批绕过”** 的 Bug，直接触及权限控制的核心，因此受到广泛关注。该 PR 在今日被合并，意味着这个长期困扰用户的审批流程问题有望得到解决。
    - **诉求**: 用户希望 QwenPaw 的权限控制模型是**可靠且完全遵守用户配置**的，任何绕过行为都是不可接受的。

3.  **密钥安全与日志脱敏 (Issue `#5705`)**
    - **讨论**: 有 6 条评论，显示出社区对安全问题的关注度很高。用户 `@wjt0321` 对现有密钥安全机制进行了深入的代码级审查，并指出了 `dialog` 日志和 `ReMe` 日志中仍可能泄漏 API Key 等敏感信息。
    - **诉求**: 用户需要的是 **“端到端”的密钥安全保障**，不仅仅是存储加密，还包括运行时的日志、缓存等所有环节的脱敏。这是一个对企业级用户至关重要的需求。

### 5. Bug 与稳定性：严重程度评估
今日社区报告的 Bug 集中于 **v2.0 beta** 版本，严重性较高。

| 严重程度 | Bug 描述 | Issue | 状态/修复 PR |
| :--- | :--- | :--- | :--- |
| **严重** | v2.0 `scroll` 上下文策略可能错误折叠当前任务，导致模型“失忆”和回复错乱。 | `#5746` | 已有修复 PR (#5747, #5765) |
| **高** | v2.0 Runtime 中，截断的 `tool_call.input` 会导致模型无限重复执行同一工具。 | `#5717` | 已有修复 PR (#5761) |
| **高** | `#5711` 简要分析了 QwenPaw 的能力短板，包括工具调用效率低、记忆机制缺陷等，虽非具体 Bug，但指明了架构级别的风险。 | `#5711` | 暂无，属于深度分析报告 |
| **中** | 执行重型任务时，项目会无故卡死或中断，原因不明。 | `#5763` | 待诊断 |
| **中** | 计划模式下，同一脚本文件被反复读取，造成资源浪费。 | `#5759` | 待诊断 |
| **低** | Remote SSH 插件卸载不干净，导致对话报错。 | `#5689` | 待修复 |
| **低** | 自动化任务在无干预下莫名终止。 | `#5616` | 待诊断 |

### 6. 功能请求与路线图信号
社区对 QwenPaw 的期望正在从“能用”向“好用”和“深入场景”转变。

- **高度可能纳入下一版本**:
    - **自定义模型协议 (Issue `#5609`)**: 用户希望支持非标准 `/v1/chat/completions` 的 API 接口（如图像生成）。虽然技术上复杂，但需求明确，未来可能会通过“自定义 Provider”或插件机制来满足。
    - **增强 CLI 能力 (Issue `#5737`)**: 企业用户希望有更强大的 CLI 供二次封装。这与 PR `#5736` (添加 PR review bot) 中体现的自动化理念一致，未来可能作为一项基础设施能力进行建设。
    - **自动切换模型 (Issue `#5718`)**: 用户希望模型遇到限额或错误时能自动切换。这是一个提升用户体验的重要功能，可能以“模型回退策略”的形式在未来版本中出现。

- **长期路线图信号**:
    - **Paw 门户（Paw Portal）**: Issue `#5737` 中提到的 CLI 增强需求，指向了用户希望构建一个更易于访问和使用的“通用前端”或“企业门户”的深层诉求。这与项目未来可能发展的 “QwenPaw as a Platform” 方向契合。

### 7. 用户反馈摘要
- **🚨 稳定性是当前最大痛点**: 多位用户（`@vipcys001-bot` 等）报告了任务无故卡死、中断的问题，特别是在执行“偏重型”、“自动化”任务时。这直接影响用户信任，是最需要优先解决的问题。
- **⚙️ “计划模式”效能受关注**: 用户 `@huangreason-blip` 反馈了计划模式中反复读取同一文件的问题，表明用户对 Agent 的“智能”和“效率”有更高期待，不满足于简单的指令执行。
- **🧠 对 Agent 认知能力的批判性思考**: 用户 `@ZhaoX666` 提交的 `#5711` 号 Issue，并非简单提问，而是一份专业的**竞品对比和深度分析报告**，指出了 QwenPaw 在工具调用、记忆、上下文保持等方面的架构短板。这类“高级用户”的反馈极具价值，应被视为产品迭代的核心输入。
- **🛠️ 对企业级功能的渴求**: 从密钥安全、权限控制到 CLI 增强，用户对 QwenPaw 的企业级部署和使用场景表现出浓厚兴趣，这些是项目从个人玩具走向生产力工具的关键。

### 8. 待处理积压
以下为长期未关闭或未得到充分响应的关键议题，提醒维护团队关注。

1.  **系统性解决 Windows GBK 编码问题**
    - Issue: `#4481`
    - 持续时间: 自 2026-05-18
    - 重要性: **高**。影响所有 Windows 用户，建议从系统层面一劳永逸地解决，避免零散补丁。
    - 链接: https://github.com/agentscope-ai/QwenPaw/issues/4481

2.  **Plugin Agent Hook 支持**
    - Issue: `#4613`
    - 持续时间: 自 2026-05-21
    - 重要性: **高**。这是插件系统更深层次扩展能力的基石，能够实现非侵入式的内存、钩子、技能扩展，对构建健康插件生态至关重要。
    - 链接: https://github.com/agentscope-ai/QwenPaw/issues/4613

3.  **支持工作目录功能**
    - Issue: `#4642`
    - 持续时间: 自 2026-05-23
    - 重要性: **中**。请求提供类似 Codex 或 Claude Cowork 的工作目录，改善任务相关的文件管理和用户体验。这是一个明确且呼声较高的需求。
    - 链接: https://github.com/agentscope-ai/QwenPaw/issues/4642

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是为您生成的 hermes-agent 项目动态日报。

---

# Hermes-Agent 项目动态日报 | 2026-07-03

## 1. 今日速览

项目今日活跃度极高，24小时内贡献量达到峰值：共处理 **302 条** Issues 与 **500 条** PRs。Issue 池中开放讨论占主导（267条），讨论激烈。PR 方面，待合并数量庞大（336条），表明有大量工作正在进行或等待审查。社区讨论焦点集中在 **跨平台集成稳定性**（特别是 QQ Bot 和 iMessage）、**Dashboard 用户体验**、以及 **模型兼容性**（Ollama / Copilot）上。没有新版本发布，项目整体处于积极开发与问题修复的“冲刺”阶段。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日虽无正式发版，但通过已合并/关闭的 PR 及关键 Issues 的解决，项目在以下方面取得了实质进展：

- **安全加固**: 一个 P1 级别的安全问题获得修复。`[Security] Terminal session snapshots leak .env secrets to disk in plaintext` (#48441) 已被关闭，补丁通过 PR #57624 (`fix(browser): scope cloud provider credentials per profile`) 进一步解决了浏览器工具中的类似凭证泄露问题。
- **稳定性修复**: 多个高影响 Bug 的修复 PR 提出。`[Bug]: fix(qqbot) ... infinite retry loop` (#52914) 虽未关闭，但已有相关修复思路。直接修复 `[Bug]: Dashboard Chat — Ctrl+V paste broken` (#24860) 和 `[Bug]: Desktop /compress returns error` (#44456) 的 PR 已提交，旨在解决关键的用户界面和命令执行问题。
- **插件与集成优化**: 针对 **Ollama** 的 `[Feature]` (#4505) 提案仍在活跃讨论，目标是利用原生 API 提升效率。同时，今日有多个 PR 旨在添加新 Provider 支持，如 **Kenari** (#57613) 和 **Arabic localization** (#44987)，显示出项目生态的扩张趋势。
- **工具链增强**: PR #57612 (`Hardening fixes for compression, Hindsight, and env snaps`) 合并了一系列通用性加固修复，提升了压缩、Hindsight 记忆及环境快照的健壮性。PR #57595 (`feat(gateway): add /sessions search`) 为 Gateway 用户带来了期待已久的会话搜索功能。

## 4. 社区热点

今日社区讨论和互动最热烈的话题主要集中在用户体验和核心集成上：

- **Dashboard 主题可读性问题** ([#18080](https://github.com/NousResearch/hermes-agent/issues/18080)): 以 **45个 👍** 和 **26条评论** 成为今日最受关注的话题。用户 `@ogermer` 直言现有主题“non-standard”且难以阅读，尤其是衬线字体和低对比度。这反映了社区对**终端产品 UI/UX 质量**的强烈诉求。
- **Ollama 集成优化** ([#4505](https://github.com/NousResearch/hermes-agent/issues/4505)): 虽然只有2个👍，但获得了 **13条评论**，讨论深入。社区不仅仅是提出需求，而是深入比较了“原生 API”与“OpenAI 兼容端点”的技术细节，展示了开发者的专业性，并希望项目能够**优先使用更高效的原生协议**。
- **QQBot 无限重试循环** ([#52914](https://github.com/NousResearch/hermes-agent/issues/52914)): **12条评论** 显示该 Bug 影响范围较广，有明确的复现步骤和错误日志。社区对特定平台（QQ Bot）的**连接稳定性**非常敏感，此问题的快速修复对于维护中国区用户至关重要。
- **桌面客户端轻量化安装** ([#38602](https://github.com/NousResearch/hermes-agent/issues/38602)): 获得了 **37个👍**，是今日呼声最高的功能请求。用户希望将一个重度的 Agent 安装包分离出一个“瘦客户端”，以便远程连接已有的 Agent 实例。这暗示了社区对**灵活的部署架构（C/S模式）**的强烈需求。

## 5. Bug 与稳定性

今日报告的 Bug 范围广泛，涵盖了从安全漏洞到平台兼容性问题。按严重程度排列如下：

| 严重程度 | Issues / PRs | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **P1 (安全)** | [#48441](https://github.com/NousResearch/hermes-agent/issues/48441) | **（已关闭）** Terminal 会话快照将 `.env` 密钥明文写入磁盘。 | **已关闭**，修复 PR #57624 也解决了浏览器工具中的类似问题。 |
| P1 (功能) | [#36934](https://github.com/NousResearch/hermes-agent/issues/36934) | **（已关闭）** `/steer` 命令被高抗注入模型误判为提示注入，导致功能失效。 | **已关闭**，表明该问题已找到解决方案或变通方法。 |
| **P2 (核心功能)** | [#57625](https://github.com/NousResearch/hermes-agent/pull/57625) | **（新提交修复）** 修复 Copilot 集成中，在不同模型间切换（如 Claude 与 GPT）导致的 HTTP 400 错误。 | 待合并 |
| **P2 (平台)** | [#52914](https://github.com/NousResearch/hermes-agent/issues/52914) | QQBot 适配器因 `is_reconnect` 参数缺失陷入无限重试循环。 | 开放中，已有大量讨论 |
| **P2 (用户体验)** | [#24860](https://github.com/NousResearch/hermes-agent/issues/24860) | Dashboard 中 Ctrl+V 粘贴文本和图片失效。 | 开放中，已有修复 PR |
| P2 (稳定性) | [#44456](https://github.com/NousResearch/hermes-agent/issues/44456) | Desktop 端 `/compress` 命令返回错误，无法压缩对话。 | 开放中，已有修复 PR |
| P3 (兼容性) | [#20866](https://github.com/NousResearch/hermes-agent/issues/20866) | 在 Qwen3.6-27B 模型上，辅助任务触发 "System message must be at the beginning" 错误。 | 开放中 |
| P3 (插件) | [#31873](https://github.com/NousResearch/hermes-agent/issues/31873) | 第三方 Web 搜索插件被 `check_web_api_key()` 函数强制禁用。 | 开放中 |
| P3 (MCP) | [#57615](https://github.com/NousResearch/hermes-agent/pull/57615) | **（新提交修复）** MCP 重连计数器在成功重连后未能重置，导致重连愈发困难。 | 待合并 |

## 6. 功能请求与路线图信号

- **部署与架构**:
    - **[Feature]: Desktop Client-Only Installation** (#38602, 👍37): 呼声极高的“瘦客户端”模式，可能指向项目未来支持更灵活的 Server-Client 架构。结合多平台转发问题（#53817），此需求非常迫切。
    - **[Feature]: per-channel model ... overrides for gateway platforms** (#1955, 👍7, 已关闭): 此需求的关闭可能意味着”按渠道/频道配置模型”的基础功能已被合入，为 Gateway 平台的精细化运营铺路。
- **代理功能与插件化**:
    - **[Feature]: Configurable Memory Backends** (#47349, 评论11): 用户希望摆脱硬编码的 `memory.md` 文件，支持更专业的外部后端（如 honcho），这指向 Agent 记忆系统的**模块化与可插拔**趋势。
    - **[Feature]: Unified plugin route selector** (#41190, 评论7): 建议为所有 LLM 调用点提供统一的、插件可接入的路由/模型选择钩子。如果实现，将极大增强插件生态。
    - **[Feature]: configurable approval-locked command patterns** (#5528, 👍12): 用户期望对危险命令（如 `rm -rf`）的审批模式进行自定义配置，而不是硬编码。这是**安全性和灵活性**平衡的重要信号。
- **新功能与集成**:
    - 新 Provider 支持： **Kenari** (#57613) 和 **Camofox cookie import** (#12106) 的 PR 表明项目持续扩展其模型后湍和数据采集能力。
    - **语音/转录优化**: PR #57627 提出的 **TUI draft/refine transcript flow** (转录草稿/润色流程) 是针对语音输入的实用功能增强，旨在改善语音交互体验。

## 7. 用户反馈摘要

- **痛点**:
    - **可读性差**: “The selection of fonts and colours is non-standard... little contrast makes the dashboard hard to read.” (#18080) - 用户对 Dashboard 现有主题的 UX 表示强烈不满。
    - **安装受阻**: “`install blocked for a long time`” (#7066) - 用户在安装过程中卡住，可能与网络或脚本兼容性有关。
    - **更新后无法启动**: “It cannot be started after updating” (#55658) - 有用户在更新后遇到启动崩溃，这类问题对用户体验打击最大。
    - **文档与实际不符**: “documented behavior doesn't match code” (#5200) - 用户发现 `AGENTS.md/SOUL.md` 的描述与实际代码实现不一致，表明文档维护滞后。
- **功能诉求**:
    - **时间感知**: “The Hermes Agent has no built-in awareness of the current time” (#49407) - 用户期望 Agent 能自动感知时间，避免手动查询或猜测。
    - **更好的自定义能力**: “Users cannot mark installation-specific commands as approval-required without patching the source” (#5528) - 用户对无法自定义审批命令规则感到不便，期望开源项目有更高的可配置性。

## 8. 待处理积压

- **重要 Bug 待修复**:
    - `[Bug]: 400 format_error on Qwen3.6-27B` (#20866) - 发布于5月6日，影响特定模型兼容性。至今已有两个月的讨论，但仍在开放中。
    - `[Bug]: install blocked` (#7066) - 发布于4月10日，作为准入门口的问题，近3个月的持续关注仍未解决，可能阻塞新用户加入。
- **功能提案待评估**:
    - `[Feature]: Proper Litellm support` (#8465) - 创建于4月12日，讨论热度不高（4个评论），但 Litellm 作为重要的开源模型网关，该功能对许多自建用户至关重要，长期未关闭也未合并，处于悬而未决状态。
    - `[Feature]: configurable approval-locked command patterns` (#5528) - 获得了12个 👍，代表社区普遍诉求，但缺乏维护者回复和定稿，处于待决策状态。
- **长期开放 PRs**:
    - `feat(browser): support Camofox cookie import (#6109)` (#12106) - 该 PR 已开放了2.5个月，作为浏览器工具链的增强功能，长时间未被合并，可能存在冲突或设计需进一步讨论。

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*