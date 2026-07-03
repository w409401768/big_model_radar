# OpenClaw 生态日报 2026-07-03

> Issues: 197 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-03 09:14 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，这是根据 OpenClaw 项目数据生成的 2026-07-03 项目动态日报。

---

## 2026-07-03 OpenClaw 项目动态日报

### 1. 今日速览

OpenClaw 在今日呈现出极高的社区活跃度，24 小时内共有 **197 条 Issue** 和 **500 条 PR** 获得更新。近期版本（特别是 v2026.5.27 和 v2026.6.11）发布引发了多类严重的回归问题，导致了社区的不满，但同时也激发了大量高质量的贡献，已有多项修复 PR 迅速提交。项目目前处于“高速迭代与质量阵痛”并存的状态，尽管 CI 发布流程暴露出了一些瑕疵，但贡献者社群的响应速度和修复能力极强，项目整体生态健康度依然坚韧。

---

### 2. 版本发布

今日无新版本发布。

---

### 3. 项目进展

项目今日在修复关键缺陷和完善核心功能方面取得了实质性进展。多项重要的社区 Bug 修复已被合并，同时也有若干重大功能特性正在积极推进中。

- **关键 Bug 修复合并（今日关闭/合并）**
  - **会话状态修复**：[#98841](https://github.com/openclaw/openclaw/pull/98841) 修复了会话通过 `/name` 重命名后，在 UI 中仍显示为原始 UUID 的问题。
  - **嵌入搜索引擎兼容性**：[#96724](https://github.com/openclaw/openclaw/pull/96724) 和 [#97095](https://github.com/openclaw/openclaw/pull/97095) 共同修复了 `memory_search` 在解析配置时无法找到通过通用插件生态注册的嵌入提供程序（如 `local`）的问题。
  - **多平台消息异常**：[#98874](https://github.com/openclaw/openclaw/issues/98874)（文本结果被渲染为图片附件）、[#90962](https://github.com/openclaw/openclaw/issues/90962)（Telegram 进度模式被评论覆盖）等问题已解决。
  - **移动端与平台适配**：[#99093](https://github.com/openclaw/openclaw/issues/99093)（iOS Voice Wake 崩溃）、[#99046](https://github.com/openclaw/openclaw/issues/99046)（iOS 18+ 照片权限）、[#87216](https://github.com/openclaw/openclaw/issues/87216)（Android LAN 设置 `ws://` 解析错误）等 Bug 均已关闭。
- **重要功能与适配推进（活跃 PR）**
  - **最新模型支持**：[#99463](https://github.com/openclaw/openclaw/pull/99463) / [#99462](https://github.com/openclaw/openclaw/pull/99462) 快速适配了 Anthropic 最新发布的 `claude-sonnet-5`，支持了 100 万 Token 的上下文窗口。
  - **Signal 渠道增强**：[#98791](https://github.com/openclaw/openclaw/pull/98791) 为 Signal 消息渠道新增了生命周期状态反应，提升用户交互体验。
  - **Codex 运行时升级**：[#98021](https://github.com/openclaw/openclaw/pull/98021) 正在推进对原生 Codex 运行时 “Ultra” 思维链等级的全面支持，这将对高级 Agent 编排产生深远影响。
  - **Node 26 兼容性**：[#99461](https://github.com/openclaw/openclaw/pull/99461) 显式关闭文件句柄以防止 Node.js 26 下的垃圾回收崩溃。

---

### 4. 社区热点

今日社区讨论热度聚焦于 **长期未决的设计缺陷** 与 **高密度的回归问题**。

- **#25592：工具调用间的文本泄露**（[链接](https://github.com/openclaw/openclaw/issues/25592)）
  - **热度**：33 条评论，1 个赞。
  - **诉求分析**：这是一个长期悬而未决的严重 UX/Security 问题。当 Agent 进行多工具调用时，中间的内部处理文本（如错误日志、确认信息）会被直接路由到用户可见的消息频道（如 Slack、iMessage）。社区对此非常在意，认为这违反了 AI Agent 的基本原则——内部处理对用户透明但不是侵入性的。该 Issue 等待产品决策和安全审核已久。
- **#88312：Codex turn-completion 停摆回归**（[链接](https://github.com/openclaw/openclaw/issues/88312)）
  - **热度**：19 条评论，5 个赞。
  - **诉求分析**：用户对“同一个 Bug 修好了又出现”的回归现象感到非常沮丧。这是一个旧病复发的阻塞性问题，导致 Codex Agent 无法完成回合。用户强烈呼唤更严格的回归测试机制。
- **#92201：Anthropic 思考块签名验证失效**（[链接](https://github.com/openclaw/openclaw/issues/92201)）
  - **热度**：18 条评论，1 个赞。
  - **诉求分析**：这是一个高度技术性的 AI 基础设施 Bug。Anthropic 流式传输的“思考块”签名在重放时间歇性失效，且错误处理机制因错误信息被泛化而无法触发。这暴露了系统在处理多供应商复杂 AI 响应时的韧性不足。
- **#98416：v2026.6.11 发布产物缺失关键修复**（[链接](https://github.com/openclaw/openclaw/issues/98416)）
  - **热度**：9 条评论，5 个赞（当前赞数最高的 Issue）。
  - **诉求分析**：用户发现了源代码中的关键修复（重入锁）竟然没有被包含在 npm 发布包中。这击穿了用户对发布流程的信任，引发了关于 CI/CD 质量和发布审查流程的广泛批评。

---

### 5. Bug 与稳定性

今日报告的 Bug 数量众多，且严重性极高，主要集中在 v2026.6.11 版本引入的回归问题和新平台（Node 26）的兼容性崩溃上。

- **严重性：紧急（Critical）**
  - **#99253：安全风险 – Agent 捏造用户输入并自行回答**（[链接](https://github.com/openclaw/openclaw/issues/99253)）。Agent 在响应中生成了不存在的用户对话记录并针对回答，严重威胁用户信任与数据安全性。该项目已由 [#99451](https://github.com/openclaw/openclaw/pull/99451) 尝试修复。
- **严重性：高（High）**
  - **#99263：Gateway 在 Node 26 环境下崩溃**（[链接](https://github.com/openclaw/openclaw/issues/99263)）。`ERR_INVALID_STATE` 致命错误，由 GC 误关文件句柄引发。**PR [#99461](https://github.com/openclaw/openclaw/pull/99461) 已提交。**
  - **#98673：v2026.6.11 文本结果被转换为图片块**（[链接](https://github.com/openclaw/openclaw/issues/98673)）。`sanitizeContentBlocksImages` 函数逻辑错误，导致会话历史中文本结果被污染为图片附件。
  - **#98614：v2026.6.11 `sessions_spawn` 缺少作用域权限**（[链接](https://github.com/openclaw/openclaw/issues/98614)）。导致 Agent 孵化功能失效。**PR [#99452](https://github.com/openclaw/openclaw/pull/99452) 已提交。**
  - **#98416：v2026.6.11 发布产物缺失重入锁**（[链接](https://github.com/openclaw/openclaw/issues/98416)）。源代码有，发布产物无，属于严重 CI 事故。
- **严重性：中（Medium）**
  - **#99237：`doctor --fix` 在只读 `.bashrc` 环境下直接退出码 1**（[链接](https://github.com/openclaw/openclaw/issues/99237)）。阻碍新用户部署。**PR [#99453](https://github.com/openclaw/openclaw/pull/99453) 已提交。**
  - **#99068：Discord 分块发送导致回复通知刷屏**（[链接](https://github.com/openclaw/openclaw/issues/99068)）。`replyToMode: "first"` 时，长消息被分块后每块都带引用回复，造成频道噪音。
  - **#99432：HTTP 429 “过载” 被错误归类为 “速率限制”**（[链接](https://github.com/openclaw/openclaw/issues/99432)）。影响后端容错策略。**已于今日关闭。**

---

### 6. 功能请求与路线图信号

今日社区在功能方面的讨论显示出对 **UI 现代化**、**多智能体治理** 和 **更多模型选择** 的强烈需求。

- **高热度/潜力功能请求：**
  - **多智能体协作增强 [RFC]**（[#35203](https://github.com/openclaw/openclaw/issues/35203)）：提出了能力画像、共享黑板和 Token 成本治理等高级概念，代表了对复杂应用的远景规划。该项目虽列为 P2，但涵盖的内容极为广泛。
  - **UI 质量大更新**（[#75947](https://github.com/openclaw/openclaw/issues/75947)）与 **iOS 控制栏密度优化**（[#99439](https://github.com/openclaw/openclaw/issues/99439)）：用户持续反映当前 UI 难以导航，请求进行系统性重构。对应的修复 PR [#99468](https://github.com/openclaw/openclaw/pull/99468) 今日已提交。
  - **Claude Sonnet-5 的极速适配**：从模型发布到提交 PR（[#99463](https://github.com/openclaw/openclaw/pull/99463)）几乎无延迟，证明了项目组对前沿模型的支持力度。
  - **Signal 渠道增强**（[#98791](https://github.com/openclaw/openclaw/pull/98791)）：由社区贡献者推动，补齐了 Signal 平台与其他平台在用户体验上的差距。
- **可能被纳入下一版本的信号：**
  - **Codex Ultra 思维链**（[#98021](https://github.com/openclaw/openclaw/pull/98021)）正在推进中，表明原生 Codex 运行时仍是项目的核心发力点。
  - **登录会话迁移到 SQLite**（[#98986](https://github.com/openclaw/openclaw/issues/98986)）是一个重要的技术债务清理信号，旨在改善数据持久化性能。

---

### 7. 用户反馈摘要

从今日 Issue 的评论中，可以提炼出以下核心用户声音：

- **对“回归”问题的普遍失望**：“升级到 6.11 时还好好的，第二天早上会话突然全断了。” （[#98672](https://github.com/openclaw/openclaw/issues/98672)）这代表了用户对版本稳定性的严重不满，回归问题正在侵蚀用户的信心。
- **对安全边界的高度恐惧**：“这不仅仅是 UI 渲染的问题……Agent 的回答里出现了一条捏造的用户消息，然后它还自己回答了。” （[#99253](https://github.com/openclaw/openclaw/issues/99253)）。用户对 AI 信任度的下限被击穿，这是今日最严重的负面反馈。
- **新手上手依然困难**：“`Failed to optimize image` 这个错误太不透明了，我根本不知道是 `sharp` 没装。” （[#73148](https://github.com/openclaw/openclaw/issues/73148)）。“`authentication needed` 也不告诉我到底是需要扫码、等待审批还是凭证过期了。” （[#98046](https://github.com/openclaw/openclaw/issues/98046)）。错误信息的模糊性是老生常谈的问题。
- **配置灵活性的刚需**：“我运行两个 Agent，但插件配置是全局的，没法给不同 Agent 不一样的配置。” （[#55401](https://github.com/openclaw/openclaw/issues/55401)）。“沙箱上传文件限制 5MB 竟然是硬编码，也不给个环境变量覆盖。” （[#40880](https://github.com/openclaw/openclaw/issues/40880)）。用户在向更复杂的多 Agent 和多应用场景演进时，急需更高的配置自由度。

---

### 8. 待处理积压

以下积压的 Issue 和 PR 已长期未取得实质性进展，但影响重大，提醒项目维护者重点关注：

- **最老/最严重的待决 Issue：**
  - **#25592：工具间文本泄露**（[链接](https://github.com/openclaw/openclaw/issues/25592)）—— 2026-02-24 开启，33 条评论，至今等待产品决策与安全审核。这是社区公认的 P1 问题，但讨论陷入僵局，急需核心团队定夺方向。
  - **#73148：`sharp` 缺失时的错误提示**（[链接](https://github.com/openclaw/openclaw/issues/73148)）—— 2026-04-28 开启，已标记为 `stale`。作为影响新用户开箱体验的基础问题，应给予更高优先级处理。
  - **#47910：Provider 降级逻辑优化**（[链接](https://github.com/openclaw/openclaw/issues/47910)）—— 2026-03-16 开启。当前将所有失败（认证、限流、超时）一刀切处理的容错逻辑，已被证明会大量浪费性能，建议尽早纳入规划。
- **高风险 / 长期搁置的 PR：**
  - **#79756：启动顺序优化**（[链接](https://github.com/openclaw/openclaw/pull/79756)）—— 2026-05-09 开启，旨在让 Channels 在耗时插件之前启动以降低 Gateway 冷启动时间。目前已搁置两个月，急需更新状态。
  - **#97713：高级代理配置 `NO_PROXY`**（[链接](https://github.com/openclaw/openclaw/pull/97713)）—— 2026-06-29 开启，修复企业代理环境的内部请求路由问题。目前处于等待作者更新的状态，但此问题对使用复杂网络环境的用户至关重要，建议维护组直接接手或推动。
  - **#89113：版本兼容性 – 工具描述符隔离**（[链接](https://github.com/openclaw/openclaw/pull/89113)）—— 2026-06-01 开启，涉及运行时核心兼容性逻辑，目前卡在等待作者授权阶段。

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是根据 2026 年 7 月 3 日 的 GitHub 数据生成的 Zeroclaw 项目动态日报。

---

### Zeroclaw 项目日报 | 2026-07-03

---

### 1. 今日速览

今日项目活跃度处于 **极高** 水平，单日 Issue 和 PR 更新总量达到 **83 条**。团队正围绕 **v0.8.3 版本** 进行密集的攻坚和打磨，重心放在 **运行时稳定性加固**（OOM 崩溃、内存泄漏）、**安全架构**（OIDC 认证、权限控制）以及 **ZeroCode TUI 的用户体验修复** 上。全天共有 **9 个 PR 被关闭/合并**，标志着多个高优 bug 已得到有效解决，代码库演进速度极快。

---

### 2. 版本发布

无新版本发布。

---

### 3. 项目进展

今日项目核心进展在于成功合并/关闭了 9 个 PR，解决了多个关键阻塞问题：

*   **稳定性提升**：
    *   **PR #8633**（已合并）：修复了 WSL2 环境下守护进程组件管理器的重启退避逻辑，解决了 **OOM 重启风暴 (Restart-Storm)** 的根本原因，这是对长期困扰开发者的 `#5542` 问题的重大修复。
    *   **PR #8599 & #8488**（已合并）：解决了 Agent 在不同 Provider（如 OpenAI）和 Channel（如 Slack）间切换时，工具调度器和系统提示（System Prompt）不一致的深层逻辑错误。
*   **安全加固**：
    *   **Issue #8554**（已关闭）：针对技能 ZIP 包提取器进行了安全加固，增加了条目数量、压缩比和解压后大小的上限，防止 ZIP 炸弹攻击。
*   **文档与流程**：
    *   合并了多个文档 PR，包括签署提交规范（PR #8613）、Agent 提示词标签（PR #8612）等，持续优化开发者体验。

---

### 4. 社区热点

今日讨论最热烈的话题反映出社区对 **多平台支持** 和 **企业级安全** 的强烈诉求：

*   **[热点一] Windows 兼容性 (#7462)**：`@NiuBlibing` 报告的 Windows 11 上 74 个测试失败引发了 7 条评论。开发者普遍担忧 Linux-only 的 CI 无法覆盖跨平台场景，这对希望在 Windows 原生环境（非 WSL）下工作的用户构成了显著障碍。
    [查看 Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)
*   **[热点二] OIDC 认证支持 (#7141)**：作为 `#8289` 跟踪器的母议题，该 RFC 获得了 7 条讨论。社区正在深入探讨可插拔认证架构的实现细节，这表明 ZeroClaw 在企业级多用户部署中的身份管理需求非常迫切。
    [查看 Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)
*   **[热点三] WSL2 稳定性 (#5542)**：尽管 `#8633` PR 已修复了重启风暴的问题，但该 Issue 的总评论数最高（7 条）。用户社区对开发环境的稳定性极为敏感，该问题进一步拆分出了内存泄漏追踪议题 `#8642`。
    [查看 Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)

---

### 5. Bug 与稳定性

今日新报告了 **13 个 Issue**，其中崩溃和工作流阻塞问题需要特别关注：

*   **崩溃 / 高严重度 (Crash/SIGSEGV)**：
    *   **#8654**：技能审查（Skill Review）子进程因数组越界导致 `SIGSEGV`，守护进程崩溃。**暂无修复 PR**。
        [查看 Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8654)
    *   **#8642**：MCP/Tool Schema 在代理循环中克隆导致 RSS 内存无限增长，是 `#5542` OOM 问题的另一重根源。**已拆分跟踪，暂无独立修复 PR**。
        [查看 Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8642)
*   **工作流阻塞 (S1 - Workflow Blocked)**：
    *   **#8632**：源码安装启用嵌入式 Web 前端时，因 Rust 编译阶段找不到前端生成的 API 客户端代码而导致构建失败。
        [查看 Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8632)
*   **功能异常 (S2 - Degraded Behavior)**：
    *   **SOP 引擎**：`#8631` 报告无头模式下的确定性 SOP 步骤被错误地标记为完成，导致审计追踪失真。
    *   **配置管理**：`#8645` 报告了环境变量覆写的密钥在重启横幅中显示为“漂移”，造成运维困扰。
    *   **ZeroCode 相关问题**：今日报告了 **6 个** 与 ZeroCode TUI 相关的 Bug，涵盖配置编辑器 (`#8648`)、诊断超时 (`#8647`)、日志详情 (`#8646`)、空输出 (`#8644`) 等，表明该模块正在被重度使用和打磨，但成熟度仍有提升空间。

---

### 6. 功能请求与路线图信号

今日多项 RFC 和 Feature Request 清晰地指向了 v0.8.3 的路线图：

*   **生态兼容性**：
    *   **OpenAI 兼容层**：`#8603` (RFC) 与 `#8486` (PR) 提议增加 OpenAI Chat Completions HTTP 端点。一旦落地，可以无缝接入 Open WebUI、LobeChat、Continue.dev 等主流 LLM 客户端工具。这是扩展 ZeroClaw 生态的关键战略步骤。
*   **自主执行能力**：
    *   **Goal 模式**：`#8303` 提出的有界自主任务执行模式，允许 Agent 持续追求一个目标直到完成。这将是 `zeroclaw cron` 模型的有力补充。
*   **质量保障**：
    *   **Agent 评估框架**：`#7065` 提出的 `zeroclaw eval`，将引入回放和实时两种评估模式，为模型选择、提示词优化提供标准化度量工具。
*   **架构升级**：
    *   **OIDC 统一认证**：`#8289` 跟踪器正在协调可插拔 `AuthProvider` 的落地，标志着安全架构从简单的 API Key 迈向身份即服务 (IDaaS) 集成。

---

### 7. 用户反馈摘要

从今日的社区互动中可以明显感受到真实用户的痛点和场景：

*   **“请给我原生的 Windows 支持”**：`#7462` 的问题反映了相当一部分开发者的真实开发环境。当前仅 Linux CI 的策略让 Windows 用户感到“被边缘化”，修复路径语义和控制台编码是刚需。
*   **“开发环境在 WSL2 里崩了又崩”**：`#5542` 问题的深度排查（用户贡献了详细的 OOM 日志）直接推动了 `#8642` 内存泄漏问题的发现。社区愿意投入时间进行复杂问题的排查，显示出对项目的高容忍度和高期望值。
*   **“ZeroCode 虽然好用，但小毛病太多”**：`@Audacity88` 一次性提交了多个 ZeroCode Bug。这表明 ZeroCode 正处于高强度的“狗粮”测试阶段，用户的期望值在快速提升。日志查看体验（#8646）和配置编辑器（#8648）的小瑕疵是当前体验优化的主要突破口。
*   **“这个 `/model --agent` 命令太危险了”**：`#8044` 对命令权限的担忧来自真实的安全审计需求。在企业环境中，任何用户都能修改 Agent 的底层模型是不可接受的，社区用户明确指出了权限最小化原则。

---

### 8. 待处理积压

以下长期未响应或“等待作者”状态的高价值议题/PR 需要维护者关注：

*   **OpenAI 兼容层 PR (`#8486`)**：这是社区最期待的功能之一，但目前已标记为 `needs-author-action`。该 PR 的技术难度和代码量大，如果作者需要帮助，项目团队或许需要介入协助加速。
    [查看 PR](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)
*   **Doctor 扩展 PR (`#8030`)**：同样标记为 `needs-author-action`，旨在让 `doctor` 命令检测 OpenAI Codex 凭证配置。如果长时间无进展，建议设置 deadline。
    [查看 PR](https://github.com/zeroclaw-labs/zeroclaw/pull/8030)
*   **历史功能/技能 PR (`#6716`, `#6717`, `#6718`)**：这些由 `@JordanTheJet` 在 5 月提交的 PR 已进入 `stale-candidate` 状态。建议维护者评估其与当前 v0.8.3 路线图的兼容性，如果不合适应及时关闭以避免积压。
    [查看 PR #6716](https://github.com/zeroclaw-labs/zeroclaw/pull/6716)
*   **MCP 工具显示 Bug (`#8302`)**：虽然标记为 `status:in-progress`，但该问题已存在超过 10 天，且影响 Web Dashboard 的基本功能，建议加快进度。
    [查看 Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8302)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 PicoClaw 项目数据生成的 2026-07-03 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-07-03

## 1. 今日速览

过去 24 小时内，PicoClaw 项目经历了极高强度的更新。尽管新版本 v0.3.1 发布后曝出了严重的配置迁移回退问题 (#3206)，但社区与维护者迅速响应，当天即提交了修复 PR，项目活跃度处于峰值状态。此外， **WhatsApp** 和 **Matrix** 协议的自动重连机制得到加强，**Delta Chat** 网关成功合并，项目整体在稳定性和功能广度上均迈出了坚实一步。

- **Issues 活跃：** 1 条（新报告）
- **PR 更新：** 29 条（含 15 条已合并/关闭，14 条待处理）
- **版本发布：** 1 个 (v0.3.1)

## 2. 版本发布

**v0.3.1**
- **摘要：** 今日发布了 v0.3.1 小版本迭代。
- **主要变更：** 合并了由社区贡献的 NearAI 提供者支持 (#2917) 以及 Codex 存储类型断言修复 (#3053)。
- **注意事项：** 该版本发布后，用户反馈在 v2→v3 配置迁移时存在兼容性问题（详见下方 Bug 模块）。建议正在使用 v2 配置的用户在升级前关注 #3218 修复的合入状态。

## 3. 项目进展

今日共有 **15 个 PR** 被合并或关闭，以下是关键进展：

- **Delta Chat 网关上线（#3063）**：一个重要的新消息通道集成完成，标志着 PicoClaw 在去中心化/隐私通信协议支持上迈出了重要一步。
- **稳定性大幅度加固：**
  - **WhatsApp 重连（#3220 & #3219）**：为 WhatsApp 和 Matrix 协议引入了带指数退避的自动重连机制。此前这些通道在运行数天后会因网络抖动静默断开且无法恢复，此修复解决了生产环境长期运行的心腹大患。
- **安全漏洞修复：**
  - **Exec 安全绕过（#3161）**：修复了 `custom_allow_patterns` 设置后会完全跳过拒绝模式检查的漏洞，确保了即使配置了允许规则，访问环境变量等敏感操作依然会被有效拦截。
  - **跨站请求伪造（#3160）**：通过校验浏览器来源，阻止了跨站点对启动设置接口的非法写入。

## 4. 社区热点

**#3206 - v2→v3 配置迁移阻断**
- **热门原因：** 该 Issue 报告了从 v2 升级至 v0.3.1 后，`picoclaw status` 等命令完全无法运行，报错 `unknown field(s): build_info, session.dm_scope`。此问题对任何使用旧配置的用户具有毁灭性影响。
- **社区响应：** 该 Issue 提交后，贡献者 **@AMEOBIUS** 迅速分析根本原因（`legacyDiagnosticConfig` 验证模块未同步新增字段），并在同一天提交了修复 PR #3218。这种即时响应的能力体现了项目组的专业度。

**链接：**
- Issue：#3206 (https://github.com/sipeed/picoclaw/issues/3206)
- Fix PR：#3218 (https://github.com/sipeed/picoclaw/pull/3218)

## 5. Bug 与稳定性

当日报告的 Bug 主要集中在基础功能的健壮性上，按严重程度排序如下：

| 严重程度 | 问题描述 | 问题/PR 链接 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | **v2→v3 配置迁移失败**：`build_info` 和 `session.dm_scope` 字段被错误地识别为未知字段，导致应用无法启动。 | #3206 | **已有修复 PR** (#3218) |
| **高** | **WhatsApp 静默断连**：WebSocket 在运行 2-3 天后会进入死锁状态，无法恢复消息接收。 | #3220 (https://github.com/sipeed/picoclaw/pull/3220) | 修复 PR 已提交 |
| **高** | **Matrix 同步循环崩溃**：网络故障或服务器重启后，协程直接退出且无法自愈，失去对外通信能力。 | #3219 (https://github.com/sipeed/picoclaw/pull/3219) | 修复 PR 已提交 |
| **中** | **Exec 拒绝模式绕过**：配置了 `custom_allow_patterns` 后会弱化安全策略。 | #3161 | 已合并 |

## 6. 功能请求与路线图信号

- **Discord 基于角色的访问控制 (RBAC)（#3217）**：新增 `allow_roles` 配置项。允许指定 Discord Guild 角色 ID 来限制机器人的交互权限，无需特权 Intents。这是面向团队协作场景的强需求，有望进入下一个小版本。
- **Simplex 通道支持（#3193）**：新增对高隐私通信协议 Simplex 的支持。虽然尚在待合入状态，但表明项目正在积极拓宽消息源的多样性。
- **Agent 协作总线（#2937）**：该 PR 虽因长期未更新被打上 `[stale]` 标签，但它提案的 Agent 内部门禁、跨 Agent 会话隔离等概念，代表了 PicoClaw 多智能体架构的未来蓝图，仍值得关注。

## 7. 用户反馈摘要

今日用户反馈高度集中在 **配置迁移兼容性** 上。

- **核心痛点：** 用户 @OhYash 描述了即使在全新安装/升级后，立即遭遇应用崩溃的极端体验。这类 Bug 在自动化 CI/CD 部署场景中会造成严重的流程阻断。
- **深层教训：** 这表明在迭代中，对历史配置文件的向前/向后兼容性校验需要与新功能的开发同步进行。`legacyDiagnosticConfig` 这一模块需要更严谨的泛化验证逻辑，以避免未来类似的新增字段导致升级失败。

## 8. 待处理积压

以下两项为悬置时间较长、影响较大的工作项，建议维护团队给予关注优先级评估：

- **PR #2937 - Agent 协作功能（Stale）**：此前最受瞩目的架构级特性，已停滞 40 天。建议核心成员明确该 PR 的设计方向是否仍符合 v3 路线图，决定合并、重构还是暂缓。
  链接：https://github.com/sipeed/picoclaw/pull/2937

- **PR #3165 - OpenAI 兼容 Seed XML 修复（Stale）**：该 PR 旨在恢复火山引擎（Doubao）等 Seed 模型在 OpenAI 兼容接口下的工具调用（Tool Call）功能。如果不修复，使用这些国内主流模型的用户将无法正常使用函数调用功能。
  链接：https://github.com/sipeed/picoclaw/pull/3165

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，这是为您生成的 QwenPaw 项目日报。

---

# QwenPaw 项目日报 | 2026-07-03

## 今日速览
今日项目状态活跃，社区讨论与代码贡献并重。过去24小时内，尽管没有新版本发布，但开发团队在Bug修复和功能迭代上取得了显著进展，合并了大量PR，有效解决了社区反馈的多个关键问题，包括上下文丢失、工具调用异常等。项目正处于从v1到v2的重要转型期，社区对v2.0.0预发布版本的反馈积极且宝贵，帮助项目在稳定性上持续打磨。整体健康度良好，迭代节奏稳健。

## 版本发布
今日无新版本发布。

## 项目进展
今日有多个重要的PR被合并或关闭，主要聚焦于核心运行时稳定性和用户体验优化：

- **核心稳定性增强**:
    - [PR #5755](https://github.com/agentscope-ai/QwenPaw/pull/5755) (已合并): 修复了单个MCP客户端配置错误（如连接字符串拼写错误）导致整个 Agent 配置加载失败的问题。现在系统能对错误配置更具弹性。
    - [PR #5742](https://github.com/agentscope-ai/QwenPaw/pull/5742) (已合并): 在流式响应中，修正了消息时间的显示逻辑，使其展示的是流式传输完成的“最终时间”，而非第一个数据块的“起始时间”，用户感知更准确。
- **前端与UI重构**:
    - [PR #5754](https://github.com/agentscope-ai/QwenPaw/pull/5754) (已合并): 统一了侧边栏和抽屉弹窗中的会话列表组件，通过 `variant` 属性复用逻辑，提升了代码质量并减少了潜在的显示不一致问题。
    - [PR #5753](https://github.com/agentscope-ai/QwenPaw/pull/5753) (已合并): 对技能（Skill）相关UI进行了重构，将市场（Market）页面整合到技能管理页面，并统一了添加技能的入口，简化了用户操作流程。
    - [PR #5744](https://github.com/agentscope-ai/QwenPaw/pull/5744) (已合并): 修复了移动端查看历史会话时列表为空的问题，提升了移动端体验。
- **基础架构调整**:
    - [PR #5732](https://github.com/agentscope-ai/QwenPaw/pull/5732) (已合并): 新增了 `none` 内存后端，允许用户在控制界面直接选择“禁用”记忆系统（ReMeLight），无需手动修改配置文件，提供了更高的灵活性。
    - [PR #5758](https://github.com/agentscope-ai/QwenPaw/pull/5758) (已合并): 更新了官网博客，新增了“开发者日”中关于Runtime模块的讲解会议回放，并优化了Google Analytics的数据埋点。

这些进展表明项目在强化核心稳定性的同时，也在持续进行用户体验和代码架构层面的优化。

## 社区热点
今日社区讨论集中在性能和安全两个关键方向：

1.  **密钥安全机制讨论** ([Issue #5705](https://github.com/agentscope-ai/QwenPaw/issues/5705)): 该issue获得了6条评论，社区的讨论非常深入。发起者对QwenPaw的密钥安全机制进行了源码级的审查，指出虽然LLM Provider的 `api_key` 已有加密存储，但在环境变量回退策略、日志脱敏等方面仍存在覆盖不全的问题，并提出了详细改进方案。这反映了用户对生产环境部署安全性的高要求。

2.  **V2.0.0 预发布版本问题集中反馈** ([Issue #5273](https://github.com/agentscope-ai/QwenPaw/issues/5273)): 作为v2.0.0 Pre-release问题的集中跟踪帖，该issue持续获得关注。社区将各类v2特定的bug、回归问题汇集于此，对于追踪和修复v2版本的初期问题至关重要，是项目健康发展的晴雨表。

## Bug 与稳定性
今日报告的Bug中，有几个问题较为严重，已得到或正在得到修复：

- **关键 Bug**:
    - **[已修复] Scroll 上下文压缩导致任务中断** ([Issue #5746](https://github.com/agentscope-ai/QwenPaw/issues/5746)): 用户在v2.0.0 beta中使用 `scroll` 上下文策略时，发现系统在执行长任务（如 `/heartbeat`）过程中，错误地将正在进行的任务上下文压缩掉，导致模型“失忆”并回复旧消息。这是一个严重的问题，直接破坏了长任务的连续性。**对应PR #5765** 已提交，旨在保护当前活动轮次不被压缩。
    - **[已修复] Runtime 2.0 工具调用异常导致无限循环** ([Issue #5717](https://github.com/agentscope-ai/QwenPaw/issues/5717)): 报告指出，当工具调用的输入参数过长被截断后（如大文件写入），会导致模型反复执行同一个工具，形成死循环。**对应PR #5761** 已提交，解决方案是将异常信息反馈给模型，使其能够感知并自行纠正。

- **中等严重程度**:
    - **[新报告] 计划模式重复读取文件** ([Issue #5759](https://github.com/agentscope-ai/QwenPaw/issues/5759)): 用户反馈在执行单个子任务时，同一脚本文件被反复读取5次，但文件内容未变化，存在严重的性能浪费。目前尚无修复PR。
    - **[新报告] 重任执行卡死与中断** ([Issue #5763](https://github.com/agentscope-ai/QwenPaw/issues/5763)): 用户报告在执行偏重型任务时，系统会经常卡死并无故中断。目前缺乏更多细节，需要维护者进一步跟进。

## 功能请求与路线图信号
今日提交的功能请求清晰地指向了提升平台的自主性和与其他系统的整合能力：

- **[强信号] 自动切换模型** ([Issue #5718](https://github.com/agentscope-ai/QwenPaw/issues/5718)): 用户希望 Agent 在遇到模型配额不足或响应错误时，能自动切换到备选模型，实现“报错->自动重试->成功”的闭环。这反映了社区对Agent高可用性和自愈能力的需求。
- **[强信号] 增强CLI能力** ([Issue #5737](https://github.com/agentscope-ai/QwenPaw/issues/5737)): 用户提出需要更强大的CLI，以便在非图形化场景下操作QwenPaw。例如，在容器化环境或无头服务器上启动并预装Skills。这与 [PR #5734 (Switch Desktop Release to Tauri)](https://github.com/agentscope-ai/QwenPaw/pull/5734) 相辅相成，表明项目正为更广泛的企业级和专业部署场景做准备。
- **[中等信号] 添加自定义模型协议** ([Issue #5609](https://github.com/agentscope-ai/QwenPaw/issues/5609)): 用户希望支持非标准API协议的模型，如仅用于图片生成的模型。这表明社区希望QwenPaw的模型兼容性更广泛，而不仅限于标准的 `/v1/chat/completions` 接口。

## 用户反馈摘要
从今日的讨论和Issue中，可以提炼出以下用户反馈：

- **痛点与期望**:
    - **稳定压倒一切**: 用户对v2.0.0 beta版本中出现的上下文丢失（#5746）和工具调用死循环（#5717）感到困扰，强烈期望核心运行时的稳定性。
    - **安全与自动化**: 生产环境用户对密钥安全（#5705）和任务自动化中断（#5616, #5763）表达了高度关注。他们希望QwenPaw能够更安全、更可靠地运行。
    - **易用性与可扩展性**: 用户希望增加“对话删除”功能（#4113）以及在插件内获取会话ID的能力（#5547），这反映出用户对精细化管理会话内容和开发更复杂插件的需求。
- **满意与肯定**:
    - 社区对于bug响应迅速，从v2.0.0的跟踪Issue（#5273）到针对具体问题的修复PR（如#5746的 #5765， #5717的 #5761），社区协作紧密，用户问题能得到及时关注。

## 待处理积压
- **关键 Issue 跟踪**: [Issue #5273 (QwenPaw v2.0.0 Pre-release Bug & Issue Tracker)](https://github.com/agentscope-ai/QwenPaw/issues/5273) 是v2.0.0版本问题的集中地，维护者应定期检查并分类其中的问题，避免遗漏。
- **长期开放的 PR**: [PR #5525 (Windows Native Sandbox)](https://github.com/agentscope-ai/QwenPaw/pull/5525) 和 [PR #5514 (Chat Input Queue Session ID Migration)](https://github.com/agentscope-ai/QwenPaw/pull/5514) 均处于开放状态超过一周，可能需要进行代码审查或更新，建议维护者关注其进度，以避免分支长期落后于主分支。
- **未定性的严重 Bug**: [Issue #5763](https://github.com/agentscope-ai/QwenPaw/issues/5763) 关于任务执行卡死中断的报告，虽然信息有限，但描述了严重问题。维护者应主动联系报告人以获取更多日志和环境信息，以便定位和修复。

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是基于您提供的 GitHub 数据生成的 hermes-agent 项目动态日报（2026-07-03）。

---

## Hermes-Agent 项目动态日报 | 2026-07-03

### 1. 今日速览
过去 24 小时（截至 2026-07-03），Hermes-Agent 项目呈现**极高强度的社区活跃状态**：共更新 299 条 Issue（其中新开/活跃 264 条，关闭 35 条）和 500 条 PR（其中待合并 333 条，已合并/关闭 167 条）。虽然今日无官方版本发布，但开发与反馈双轨高速运转。项目在 **桌面端功能重构**（Capabilities 页面、MCP 管理）、**模型提供商生态扩展**（Kenari、Ollama 原生适配器）以及 **安全配置加固**（Secret Scope 读取修复）上取得了实质性的代码合并。社区情绪复杂，一方面对新出现的 `dream` 记忆整合技能和新提供商集成表示兴奋，另一方面对 Dashboard 的 UI/UX 及网关平台（QQBot、Photon/iMessage）的稳定性问题表达了强烈不满。

### 2. 版本发布
无。今日未发布新的 Release。

### 3. 项目进展
今日合并/关闭了多项高价值 PR，项目在稳定性、功能拓展和架构清理上均迈出了一大步：

- **安全与架构**：修复了终端快照泄露 `.env` 密钥的问题 (Issue [#48441](https://github.com/NousResearch/hermes-agent/issues/48441)，已关闭)；`/steer` 指令被误判为注入的问题已修复 (Issue [#36934](https://github.com/NousResearch/hermes-agent/issues/36934)，已关闭)。配置层现在能正确通过 Secret Scope 读取环境变量 (PR [#56982](https://github.com/NousResearch/hermes-agent/pull/56982))。
- **网关平台修复**：修复了 SMS 平台因缺少 `import re` 导致的发送崩溃 (PR [#57619](https://github.com/NousResearch/hermes-agent/pull/57619))；重构了网关运行时 delegation 流程，加固了 TUI 网关 worker/websocket 背压和认证重定向 (PR [#57616](https://github.com/NousResearch/hermes-agent/pull/57616))；Kanban 任务流转时不再产生孤儿进程 (PR [#57602](https://github.com/NousResearch/hermes-agent/pull/57602))。
- **桌面端重构**：重新设计了**“能力 (Capabilities)”页面**，将 MCP 管理提升为一等公民，并借此重构了全局共享基元 (PR [#57590](https://github.com/NousResearch/hermes-agent/pull/57590))；修复了 Homebrew/Linuxbrew 下 TUI 启动失败的问题 (PR [#57617](https://github.com/NousResearch/hermes-agent/pull/57617))；适配了 WSLg 窗口控件覆盖层 (PR [#57621](https://github.com/NousResearch/hermes-agent/pull/57621))。
- **模型与智能体核心**：新增印尼 AI 网关 **Kenari** 作为一等提供商 (PR [#57613](https://github.com/NousResearch/hermes-agent/pull/57613))；引入了**原生 Ollama `/api/chat` 适配器** (PR [#55606](https://github.com/NousResearch/hermes-agent/pull/55606))，解决了本地模型 `num_ctx` 和工具调用生效的问题；修复了压缩过程中工具调用参数异常及小型模型在工具调用后产生占位符回复卡死对话的问题 (PR [#57612](https://github.com/NousResearch/hermes-agent/pull/57612), [#57610](https://github.com/NousResearch/hermes-agent/pull/57610))。
- **新增附加值功能**：为内置记忆系统 (MEMORY.md/USER.md) 添加了 `dream` 附加技能，提供确定性的记忆去重和压缩 (PR [#56860](https://github.com/NousResearch/hermes-agent/pull/56860))。

### 4. 社区热点
今日讨论最集中的议题反映了社区对**基础体验和核心可用性**的强烈诉求：

- **Dashboard 主题设计缺陷**：[[OPEN] Issue #18080](https://github.com/NousResearch/hermes-agent/issues/18080) 以 **26 条评论**和 **45 个 👍** 高居榜首。用户直言当前的主题（Midnight, Ember 等）仅仅是对颜色进行了替换，衬线字体在低对比度下“几乎无法阅读”。这折射出用户对基础 UI/UX 质量的普遍不满。
- **Desktop 瘦客户端需求**：[[OPEN] Issue #38602](https://github.com/NousResearch/hermes-agent/issues/38602) 虽评论数中等，但获得了 **37 个 👍**。大量用户强烈希望 Desktop 能作为连接到远程 Hermes 实例的“薄客户端”，而非强制捆绑整个运行时的“厚客户端”。
- **Ollama 技术方案碰撞**：[[OPEN] Issue #4505](https://github.com/NousResearch/hermes-agent/issues/4505) 有 13 条深度评论，社区技术论证非常深入，对比了原生 `/api/chat` 与 OpenAI 兼容端点在流式传输和工具调用上的优劣，且已有对应的 PR [#55606](https://github.com/NousResearch/hermes-agent/pull/55606) 处于开放状态，受到高度关注。
- **QQBot 连接崩溃**：[[OPEN] Issue #52914](https://github.com/NousResearch/hermes-agent/issues/52914) 和 [[OPEN] Issue #53443](https://github.com/NousResearch/hermes-agent/issues/53443) (标为重复) 共产生近 20 条评论。`is_reconnect` 参数缺失导致 QQBot 网关陷入无限重试循环，无法启动，用户反馈非常急切。

### 5. Bug 与稳定性
今日报告的 Bug 按严重程度排列如下：

| 严重程度 | Issue/PR 链接 | 描述 | 状态 |
|---|---|---|---|
| **Critical (P1)** | [#48441](https://github.com/NousResearch/hermes-agent/issues/48441) | **终端快照泄露 .env 明文密钥**：缓存文件可被任意进程读取 | **已关闭 (已修复)** |
| **Critical (P1)** | [#36934](https://github.com/NousResearch/hermes-agent/issues/36934) | `/steer` 指令在高抵抗模型中被误判为 Prompt 注入 | **已关闭 (已修复)** |
| **High (P2)** | [#52914](https://github.com/NousResearch/hermes-agent/issues/52914) | QQBot 无限重试循环，Adapter 接口参数不兼容 | **OPEN，社区呼声极高** |
| **High (P2)** | [#44456](https://github.com/NousResearch/hermes-agent/issues/44456) | Desktop `/compress` 命令完全失效，TUI 命令路由错误 | **OPEN** |
| **Medium (P3)** | [#24860](https://github.com/NousResearch/hermes-agent/issues/24860) | Dashboard Chat 中 Ctrl+V 粘贴失效，且不支持粘贴图片 | **OPEN** |
| **Medium (P3)** | [#57615](https://github.com/NousResearch/hermes-agent/pull/57615) | MCP 重连计数器在成功重连后未重置，导致重连次数累积 (已提 Fix PR) | **OPEN (PR)** |
| **Medium (P3)** | [#20866](https://github.com/NousResearch/hermes-agent/issues/20866) | Qwen3.6-27B 在辅助任务中报 400 错误 (System message must be at the beginning) | **OPEN** |
| **Low (P3)** | [#55416](https://github.com/NousResearch/hermes-agent/issues/55416) | Photon/iMessage: gRPC 流持续 `RST_STREAM code 2`，侧车存活但流死亡 | **OPEN** |

### 6. 功能请求与路线图信号
结合今日活跃的 Issue 和已提交的 PR，以下功能表现出强烈的纳入下一版本的潜力：

- **已进入开发管道 (Very Likely)：**
    - **原生 Ollama 支持**：对应 Issue [#4505](https://github.com/NousResearch/hermes-agent/issues/4505) 和 PR [#55606](https://github.com/NousResearch/hermes-agent/pull/55606)，看来团队已着手解决本地模型的痛点。
    - **Kenari 提供商**：PR [#57613](https://github.com/NousResearch/hermes-agent/pull/57613) 表明项目正在积极吸纳区域化的 AI 网关。
    - **桌面端 Capabilities 重构**：PR [#57590](https://github.com/NousResearch/hermes-agent/pull

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*