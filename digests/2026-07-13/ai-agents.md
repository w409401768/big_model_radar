# OpenClaw 生态日报 2026-07-13

> Issues: 500 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-12 22:37 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，这是根据 OpenClaw 项目实时数据生成的 2026-07-13 项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-07-13

### 1. 今日速览

OpenClaw 项目在过去 24 小时维持了 **极高的活跃度**，Issue 和 PR 的更新数量均达到 500 条级别，呈现出一个大型开源项目在高速迭代期的典型状态——**“一边爆发问题，一边全面扑火；一边重构地基，一边开拓疆域”**。

**核心数据概览：**
- **Issue 动态**：500 条（新开/活跃 297 条，关闭 203 条）
- **PR 动态**：500 条（待合并 348 条，已合并/关闭 152 条）
- **版本发布**：0 个

**项目健康度评估**：黄灯（警惕性乐观）。社区反馈和开发者响应速度均处于极高水平（大量 P0/P1 回归 Bug 被迅速识别并修补）。另一方面，核心 Agent 体验层面出现严重回归（Tool 输出丢失、内存泄漏），且未发布新版本进行止血，暴露出项目在高速扩张期面临的稳定性压力。

---

### 2. 版本发布

本期无新版本发布。

---

### 3. 项目进展

本期虽然没有版本发布，但在架构演化和关键功能推进上取得了实质进展。大量合并/关闭的 PR 集中在**基础设施韧性加固**和**渠道层 Bug 修复**上。

- **【架构演进】云端化里程碑**：`#105719 [MERGED] feat(cloud-workers): gateway inference proxy for worker model turns` 由核心维护者 **@steipete** 完成合并。这是 Cloud Workers 里程碑的重要拼图，实现了 Worker 会话的推理代理能力。
- **【数据安全】备份体系增强**：两项关于备份的重磅 PR 被合并：`#105718 [MERGED] feat(backup): add verified SQLite snapshots` 以及 `#94805 [MERGED] Add SQLite snapshot artifacts`。这为用户提供了官方支持的、可独立验证的 SQLite 快照能力，直接回应了近日频发的数据库损坏问题。
- **【技术债务】配置与内部重构**：`#105709 [MERGED]` 完成了最后六个渠道频道流式配置键的退役，通过 Doctor 迁移清理陈旧的配置项。`#104871 [CLOSED]` 对内部高搅动率的编排表面进行了重构，不改变外部行为，提升了代码可维护性。
- **【渠道韧性】核心渠道 Bug 修复**：`#103562 fix(discord): retry reply session init conflicts` 试图彻底修复昨日爆发的 Discord 消息静默丢失问题。`#104703 fix(slack)` 修复了 Slack 通过 `message_changed` 事件投递附件时丢失的问题。

---

### 4. 社区热点

过去 24 小时的社区讨论焦点集中在严重影响用户体验的 **稳定性和可用性** 问题上。

- **🥇 长期关注度最高：跨平台桌面端缺失**
    `#75 [OPEN] Linux/Windows Clawdbot Apps`
    链接：[https://github.com/openclaw/openclaw/issues/75](https://github.com/openclaw/openclaw/issues/75)
    以 **110 条评论** 和 **81 个赞** 断层领先。用户对原生 Linux/Windows 客户端的需求极其迫切，这是社区最大的长期痛点。

- **🔥 当日最高热度 Bug：核心 Agent 体验崩溃**
    `#104721 [OPEN] [P0] > All tool results return "(see attached image)" literal string instead of actual output.`
    链接：[https://github.com/openclaw/openclaw/issues/104721](https://github.com/openclaw/openclaw/issues/104721)
    该 Issue 迅速成为复工后的风暴眼。用户表示“This is completely broken”，工具结果被替换为字面量占位符，导致 Agent 完全失明。该问题直接关联到 `#99241`（Tool outputs render as image attachments），构成了一对严重的回归问题。

- **💥 最严重的系统性风险：致命内存泄漏**
    `#91588 [OPEN] [P0] Critical: Gateway Memory Leak — RSS grows from 350MB to 15.5GB`
    链接：[https://github.com/openclaw/openclaw/issues/91588](https://github.com/openclaw/openclaw/issues/91588)
    社区对自部署 Gateway 在 2-3 天内 OOM 崩溃的情况感到焦虑。这是衡量项目 **SRE（站点可靠性工程）** 水平的关键指标。

- **🧠 深度技术讨论：Prompt Cache 跨边界失效**
    `#102175 [OPEN] [P2] [Bug]: embedded prompt cache breaks across room-event, policy, and Responses boundaries`
    链接：[https://github.com/openclaw/openclaw/issues/102175](https://github.com/openclaw/openclaw/issues/102175)
    高级用户 **@baanish** 提供了详细的 Trace 分析，指出 Prompt Cache 在嵌入式会话的多个内部边界（组织策略、队列、恢复）上失效，引发了开发者对 Long-lived Session 深层次技术债务的讨论。

---

### 5. Bug 与稳定性

请注意，下述问题按严重程度排列。今日的报告揭示了 **一个严重的结构性隐患**：P0 级别问题较多，且集中在 Agent 核心工作流和数据持久化上。

| Bug 标题 | 等级 | 摘要 | 关联 Fix PR |
| :--- | :--- | :--- | :--- |
| **> All tool results return "(see attached image)**" (#104721) | **P0** | 回归性 Bug。所有工具结果被替换为文字占位符，Agent 无法读取 stdout/stderr。 | 暂无直接 PR，系统性问题 |
| **Critical: Gateway Memory Leak** (#91588) | **P0** | RSS 从 350MB 涨至 15.5GB，最终 OOM 被 kill，导致 `launchd-handoff` 无限重启。 | 无 |
| **CLI startup preflight corrupts DB** (#101290) | **P0** | CLI 健康检查命令会损坏正在运行 Gateway 的 SQLite 数据库(`database disk image is malformed`)。 | 无 |
| **Second message fails with conflict** (#102020) | **P1** | 会话中第二条消息必然失败，影响所有跨渠道的双轮对话。 | [#103562 fix(discord) (Open)](https://github.com/openclaw/openclaw/pull/103562) |
| **Repeated hard resets on same session** (#63216) | **P1** | 即使配置了高 `reserveTokensFloor`，依然持续硬重置，注入引导上下文。 | 无 |
| **Tool parameters silently dropped** (#53408) | **P1** | 长对话后 write/exec 工具参数被静默丢弃，导致执行空操作。 | 无 |
| **Codex Hook CPU-bound processes** (#91009) | **P1** | Codex 集成导致 CPU 密集型进程激增，阻塞 Gateway RPC。 | 无 |
| **A2A sessions_send duplicate messages** (#39476) | **P1** | 目标 Agent 调用 `sessions_send` 返回时，会导致请求者渠道收到重复消息。 | 无 |
| **State migration leaves SQLite empty** (#94939) | **P1** | 6.x 升级迁移脚本将 JSON 迁移为空 SQLite，导致引用孤儿数据，中断 Bot Framework 推送。 | 无 |

**编者按**：今天 `#104721` 和 `#99241` 描绘了一幅令人不安的画面——如果 Agent 连自己的工具输出都读不了，系统的智能性将瞬间归零。这可能是某个底层渲染机制重大变更的未预见到的影响。

---

### 6. 功能请求与路线图信号

今日的功能请求清晰地指向了三大方向：**安全、跨平台和模型能力**。

- **🛡️ 安全体系全面加固（极高概率并入路线图）**
  - `#10659` [Masked Secrets](https://github.com/openclaw/openclaw/issues/10659): 防止 Agent 看见 API 秘钥，抵御提示注入泄露。
  - `#7707` [Memory Trust Tagging](https://github.com/openclaw/openclaw/issues/7707): 按来源标记记忆，阻止恶意网页/第三方技能污染。
  - `#7722` [Filesystem Sandboxing](https://github.com/openclaw/openclaw/issues/7722): 细粒度文件系统访问控制。
  - `#6615` [Denylist for Exec](https://github.com/openclaw/openclaw/issues/6615): 为审批补充拒绝名单，支持“白名单+黑名单”模式。
  - `#7524` [Group Session Consolidation](https://github.com/openclaw/openclaw/issues/7524): 允许群聊合并到主会话，简化会话管理。

- **💻 跨平台与客户端体验**
  - `#75` (Linux/Windows Apps): 需求长期霸榜。
  - `#10118` [TUI Shift+Enter](https://github.com/openclaw/openclaw/issues/10118): 改善终端写多行提示的体验（**获得 4 个赞，需求明确**）。
  - `#9637` [TUI Accessibility Config](https://github.com/openclaw/openclaw/issues/9637): 为屏幕阅读器禁用 emoji，关注残障用户。

- **🤖 模型与智能能力**
  - `#10687` [Dynamic Model Discovery](https://github.com/openclaw/openclaw/issues/10687): 支持 OpenRouter 等快速迭代的模型目录。
  - `#9986` [Trigger Fallback on Context Length](https://github.com/openclaw/openclaw/issues/9986): 上下文超限时触发 fallback 而不是直接报错。
  - `#9912` [Max Turns Config](https://github.com/openclaw/openclaw/issues/9912): 限制工具调用迭代次数，应对某些模型忽视指令的问题。

---

### 7. 用户反馈摘要

- **😠 负面/痛点**
  - **核心体验崩溃性倒退**：多位用户对工具返回“see attached image”表示极度沮丧 (`#104721`)。有用户直言“This is completely broken”。
  - **数据丢失恐惧**：数据库文件损毁 (`#101290`, `#71689`) 和升级迁移静默失败 (`#94939`) 动摇了用户对数据持久性的信心。
  - **Windows 用户被忽视感**：ACPX 运行时在 Windows 上完全不可用，且错误被吞掉，难以调试 (`#93465`)。
  - **文档与行为不一致**：用户发现 Webhook 的 `sessionKey` 多轮对话功能并未按预期工作 (`#11665`)，这影响了开发者对其自动化工作的信任。

- **😄 正面/认可**
  - **高速迭代与开发者响应**：尽管 Bug 多，但社区看到维护者在疯狂地关闭 Issue 和合并 PR（如 `#104871`, `#67417` 今日关闭）。这种快速反馈构建了宝贵的信任感。
  - **深度技术能力吸引核心玩家**：A2A、ACPX、Codex、Durable 等前沿架构吸引和留住了社区中最高等级的技术用户（如 `#102175` 中的高级溯源分析）。

---

### 8. 待处理积压

以下 Issue/PR 长期未得到妥善解决，暗示了当前系统存在的**结构性盲区**或 **维护者资源瓶颈**，值得项目负责人高度关注。

1. **🥇 最大范围功能缺口**：`#75` [Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)
   - **毒龄**：2026-01-01（197天）
   - **分析**：110 条评论，81 个赞。这是社区的第一大需求，但长期无实质性进展。建议官方给出明确的路线图时间表，要么回应“不做”，要么给出“正在做”的进度。

2. **🔥 最具破坏性的已知问题**：`#91588` [Memory Leak (P0)](https://github.com/openclaw/openclaw/issues/91588) & `#63216` [Hard Reset Loop (P1)](https://github.com/openclaw/openclaw/issues/63216)
   - **毒龄**：2026-06-09 & 2026-04-08
   - **分析**：这两个 P0/P1 级问题直接损害了产品在生产环境中的可用性。维护者需要给出明确修复排期。特别是 `#63216` 从 4 月拖到现在，用户耐心可能接近临界点。

3. **🧩 安全体系的“三座大山”**：`#7707`, `#10659`, `#7722`
   - **毒龄**：均始于 2026-02-03 和 02-06
   - **分析**：这三个安全增强功能（记忆信任、秘钥屏蔽、文件沙箱）代表了构建 Agent 安全基线的关键路径。虽然已有零星 PR 触及，但尚未形成一个系统性的、推动合并的规划。

4. **👻 用户升级路上的一颗“暗雷”**：`#94939` [State Migration Empty (P1)](https://github.com/openclaw/openclaw/issues/94939)
   - **毒龄**：2026-06-19
   - **分析**：这个 Bug 会导致用户在升级到 6.x 后，历史对话记录被“黑洞”吞噬，这会严重阻碍已有用户升级新版本，对版本采用率形成负面影响。

---

## 横向生态对比

好的，作为一名专注于AI智能体与个人AI助手开源生态的资深技术分析师，以下是根据您提供的五个核心项目（OpenClaw、Zeroclaw、PicoClaw、QwenPaw、hermes-agent）在2026年7月13日的社区动态，生成的 **横向对比分析报告**。

---

## 个人AI智能体开源生态横向对比分析报告 (2026-07-13)

**分析师摘要：** 今日的生态全景呈现出 **“分化与成熟”** 并存的态势。头部项目如 OpenClaw 和 Hermes-Agent 在经历高速扩张后的“阵痛期”，社区热度虽极高，但稳定性问题（尤其是回归Bug和内存泄漏）成为普遍挑战。与此同时，以 ZeroClaw 为代表的项目正通过架构重构（Memory 2.0, WASM插件）迈向更成熟的工程化阶段。而 QwenPaw 和 PicoClaw 则分别陷入了 **“大版本阵痛”** 与 **“小步快跑”** 的不同节奏。共同点是，**安全性、跨平台体验和模型兼容性** 已成为多项目社区共同关注的焦点。

### 1. 生态全景

当前AI智能体开源生态正处于 **“从狂热创新到工程化巩固”** 的过渡期。一方面，社区对  Agent 核心能力的探索（如 OpenClaw 的云端化、ZeroClaw 的 Goal Mode）并未停滞；但另一方面，**稳定性、可观测性和安全性** 已成为超越新功能开发的更迫切需求（如 OpenClaw 的P0回归Bug、QwenPaw 的v2.0崩溃）。项目间的分化日益明显：一些项目（如 Hermes-Agent）在大力拓宽模型与平台支持边界，另一些（如 ZeroClaw）则在深挖企业级编排与安全能力。**“开箱即用”的体验崩坏** 是今天最响亮的社区警报，这警示生态早期用户对基础可靠性的容忍度正在降低。

### 2. 各项目活跃度对比

| 项目名称 | Issues 动态 (日) | PR 动态 (日) | 版本发布 | 健康度评估 | 核心主题 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (关闭203) | 500 (合并/关闭152) | 无 | **黄灯** (警惕性乐观) | 架构演进 vs. 稳定性回归 (云端化、内存泄漏、工具失明) |
| **Zeroclaw** | 43 (活跃42) | 50 (合并/关闭2) | 无 | **蓝灯** (积极冲刺) | 功能集成冲刺 (Memory 2.0, SOP, WASM) |
| **PicoClaw** | 5 | 3 (合并2) | 无 | **绿灯** (稳定小步快跑) | 社区贡献驱动 (技能增强、翻译补全) |
| **QwenPaw** | 19 (活跃16) | 10 (合并/关闭3) | 无 | **红灯** (紧急抢修) | v2.0.0 回归Bug修复 (技能瘫痪、API错误、记忆崩溃) |
| **hermes-agent** | 500 (关闭366) | 500 (合并/关闭57) | 无 | **黄灯** (高吞吐修复) | 社区需求大规模实现 (Vertex AI, Brave Search, Windows支持) |

**对比分析：**
- **流量与体量**：OpenClaw 和 Hermes-Agent 的Issue/PR数量级远超其他项目（500级别），反映了其庞大的社区规模和极快的迭代速度。
- **健康度差异**：QwenPaw 因版本重大兼容性问题，健康度最差（红灯）；ZeroClaw 和 PicoClaw 因处于功能密集开发或稳定修复期，显得相对健康。
- **维护效率**：OpenClaw 和 Hermes-Agent 在处理Issue（关闭比例40%-70%+）和PR上效率很高，但海量涌入的反馈也表明其面临“成功带来的烦恼”。PicoClaw 因体量小，处理效率高，健康度稳定。

### 3. OpenClaw 在生态中的定位

- **绝对领先的社区规模与技术影响力**：OpenClaw 的日活跃度（500级Issue/PR）和社区讨论深度（如对A2A、ACPX、Durable等前沿架构的长篇技术分析）表明，它是当前**生态的“参照系”和“基础设施”级项目**。没有任何其他项目达到同等体量和技术复杂性。
- **技术路线的“风险先行者”**：OpenClaw 正在推进的 **Cloud Workers **、**A2A协议** 等架构是其他项目尚未企及的。但这种前沿探索也带来了巨大的稳定性风险，今日报告中出现的 **P0级“工具失明”** 和 **致命内存泄漏** 是其激进策略的直接代价。
- **社区话语权的双刃剑**：其庞大的社区既贡献了高质量的反馈（如对Prompt Cache的深度Trace分析），也在遭遇严重回归时产生巨大的负面声量（用户直言“This is completely broken”）。OpenClaw 的健康度直接影响了整个生态的士气。
- **与ZeroClaw的对比**：如果说 OpenClaw 是在构建“AI智能体的云原生操作系统”，那么 **ZeroClaw** 则更像一个**专注于本地安全与可控编排的“企业级Agent平台”**。ZeroClaw 强化的 WASM 沙箱、SOP审批流、Memory Trust Tagging（OpenClaw也有，但ZeroClaw更聚焦），显示出其对生产环境苛刻要求的前置设计，而非后置修补。

### 4. 共同关注的技术方向

以下是由多个项目的社区反馈共同涌现的行业共识性需求：

1.  **安全体系全面加固（涉及：OpenClaw, ZeroClaw, QwenPaw）**
    - **诉求**：API Key 防泄露（Masked Secrets）、记忆防污染（Memory Trust Tagging）、文件系统细粒度控制（Filesystem Sandboxing）、执行审批的白/黑名单。
    - **信号**：这已从“加分项”变为“基础要求”。QwenPaw 的安全治理模式引发用户抱怨过于严格，而 OpenClaw 和 ZeroClaw 社区则在系统性地构建安全基线。

2.  **跨平台与原生桌面、移动端支持（涉及：OpenClaw, Hermes-Agent, QwenPaw, PicoClaw）**
    - **诉求**：Linux/Windows原生客户端（OpenClaw #75）、Windows非WSL体验（Hermes-Agent）、Android服务稳定性（PicoClaw）、桌面端UI字体缩放（Hermes-Agent）。
    - **信号**：社区对**脱离网页浏览器，获得原生体验**的需求极为强烈。这是项目从“极客玩具”走向“日常工具”的必经之路。OpenClaw 的“长期霸榜”需求即是明证。

3.  **模型提供商兼容性与原生支持（涉及：Hermes-Agent, OpenClaw, ZeroClaw, PicoClaw）**
    - **诉求**：原生支持 Google Vertex AI（已实现）、支持 OpenRouter 等动态模型目录、模型上下文超限时优雅降级、提供方切换时无缝衔接。
    - **信号**：用户正在减少对单一模型提供商的依赖，“模型路由与编排”成为平台层的关键能力。Hermes-Agent 今日合并的 Vertex AI 支持是这一趋势下的直接胜利。

4.  **上下文与记忆管理的可靠性（涉及：OpenClaw, ZeroClaw, QwenPaw）**
    - **诉求**：Prompt Cache 跨边界失效（OpenClaw）、默认上下文预算溢出（ZeroClaw）、上下文压缩导致消息丢弃（QwenPaw v2.0）。
    - **信号**：长对话的**一致性** 和 **内存生命周期管理** 仍是所有项目面临的核心技术债务。这直接关系智能体的“记忆”是否可信。

### 5. 差异化定位分析

| 维度 | **OpenClaw** | **Zeroclaw** | **PicoClaw** | **QwenPaw** | **hermes-agent** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 统一的智能中枢、跨渠道消息传递、云端推理架构 | 自主Agent编排（Goal Mode）、企业级SOP、本地安全优先 | 轻量级个人助手、专注于渠道连接（Matrix等）和易用性 | 桌面/移动个人助手、工具链集成（SSH、Shell）、安全审批 | 多模型聚合、知识检索、社区驱动的“全能”助手 |
| **目标用户** | 高级开发者、技术团队、寻求最大规模自动化与集成的用户 | 企业级开发者、对安全合规、工作流编排有强需求的团队 | 自部署爱好者、注重低功耗和简单可靠性的个人用户 | **开发者**（尤其是Web/桌面开发者），寻求AI增强其现有工作流 | 寻求开箱即用、低门槛，且对模型多样性有追求的个人开发者 |
| **技术架构** | **微服务/云原生** (Cloud Workers, A2A协议, Durable Objects) | **原生+LLM编排** (Memory 2.0, SOP引擎, WASM插件沙箱) | **轻量单体** (Python, 专注于单一进程稳定与渠道对接) | **Electron/桌面优先** (紧密集成TUI/Web UI, 本地工具链) | **Web/API优先** ( 丰富的Provider支持, 功能矩阵覆盖广) |

### 6. 社区热度与成熟度

- **T1 - 极高流量，复杂健康度（OpenClaw, Hermes-Agent）**
  - **状态**：**快速迭代与“救火”并行**。这两个项目是生态的“巨轮”，动辄500级的更新量，但其稳定性问题也最易被放大。OpenClaw 是 **“基建层”** 的标杆，其健康度高度复杂，警报与成就并存。Hermes-Agent 是 **“应用集成层”** 的标杆，通过快速实现社区需求来维持高热度。
- **T2 - 高活跃度，稳定迭代（ZeroClaw）**
  - **状态**：**功能冲刺与架构收尾**。ZeroClaw 处于 v0.8.3 的收尾期，是今天最有“秩序感”的项目。社区讨论深度高，技术方向明确（Memory 2.0, WASM），展现出从原型向成熟产品迈进的工程能力。
- **T3 - 中等活跃度，深度修复 / 早期爆发（QwenPaw, PicoClaw）**
  - **状态**：QwenPaw 是 **“大版本危机”** 典型，活跃度极高但处于“恐慌”修复模式。PicoClaw 则是 **“小而美”** 的代表，活跃度虽低，但社区贡献质量高，项目健康度稳定，是生态中稳固的组成部分。

### 7. 值得关注的趋势信号

1.  **“多平台优先”已成共识，但“体验一致性”是更大挑战**：几乎所有头部项目都在努力拓展平台（Web, Desktop, Mobile）。但企业级用户（如NAS上的Hermes）或移动用户（如PicoClaw的Android）遭遇的路径、权限、稳定问题，揭示了 **“移植不等于适配”**。未来的竞争焦点将从“是否支持”转向“是否好用”。

2.  **安全不再只是“增强”，而是“基线”**：从 OpenClaw 的“三座大山”到 ZeroClaw 的 WASM 沙箱，再到 QwenPaw 被抱怨过于严格的安全治理，这说明 **安全功能已经从“锦上添花”变为“雪中送炭”**。特别是“对Agent进行审计”和“防止提示注入”成为高频词。开发者应默认将安全作为核心架构的一部分，而非后期插件。

3.  **开源项目的“韧性”正在经受考验**：OpenClaw 和 QwenPaw 的严重回归Bug表明，快速迭代的代价可能是**开箱即用体验的剧烈波动**。对于依赖这些项目的技术决策者，**“锁定稳定版本”和“建立测试沙盒”** 将是必要的风险缓解策略。社区对 P0 Bug 的情绪反应（如 Hermes-Agent 中用户指责“criminal behavior”）表明，社区忠诚度与项目稳定性高度相关。

4.  **模型层“路由与抽象”能力，成为平台分化的关键**：Hermes-Agent 对接 Vertex AI，OpenClaw 支持动态模型发现，反映出 Agent 平台正从“使用一个模型”向“管理一群模型”演化。**能否提供透明的成本、延迟、能力路由，将是判断一个智能体平台成熟度的重要指标。**

5.  **“本地优先”与“云端优先”的路线分歧开始凸显**：OpenClaw 在大力推进云端 Workers，而 ZeroClaw 则在强化本地 WASM 插件和 SQLite。这暗示了智能体平台的 **“Locally-executed & Privately-held” (本地执行、私有数据)** vs. **“Centrally-orchestrated & Assistantly-scaled” (中央编排、云端扩展)** 两大终极模式的并存与竞争。对于技术选型者，需根据数据敏感度和计算资源做出选择。

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，以下是根据你提供的 GitHub 数据生成的 Zeroclaw 项目动态日报。

# Zeroclaw 项目动态日报 | 2026-07-13

## 1. 今日速览
项目过去 24 小时活跃度极高，共更新 43 条 Issues 和 50 条 Pull Requests，日均更新量维持在高位。值得注意的是，当前仅 2 个 PR 被合并/关闭、42 条 Issues 仍处于活跃状态，反映出项目正处于**大规模功能集成与密集代码审阅**期，而非简单的热修复阶段。核心贡献者（@Nillth、@JordanTheJet）正主导内存子系统重构、SOP 审批流水线及 WASM 插件等重大特性提交，项目整体处于 **v0.8.3 收尾冲刺** 与 **v0.8.4 规划** 的重要节点。

## 2. 版本发布
无新版本发布。

## 3. 项目进展
今日合并/关闭的 PR 共 2 个（未包含在高评论量 Top 20 列表中，具体合并细节可查阅仓库）。大规模待合并队列（48 个）展现了以下实质性的功能推进：

- **Memory 2.0 架构重构（@Nillth 主导）**
  - [#8897](https://github.com/zeroclaw-labs/zeroclaw/pull/8897) 引入可选的检索缓存装饰器
  - [#8898](https://github.com/zeroclaw-labs/zeroclaw/pull/8898) 修复持久化全局记忆跨会话语义检索
  - [#8900](https://github.com/zeroclaw-labs/zeroclaw/pull/8900) 实现类型化记忆分类与门控事实提取
  - [#8984](https://github.com/zeroclaw-labs/zeroclaw/pull/8984) 在记忆写入和召回边界增加内容扫描层
  - [#8895](https://github.com/zeroclaw-labs/zeroclaw/pull/8895) 实现基于重排序的引擎记忆上下文注入

- **SOP 批准流水线（@Nillth, @singlerider）**
  - [#8848](https://github.com/zeroclaw-labs/zeroclaw/pull/8848) / [#8880](https://github.com/zeroclaw-labs/zeroclaw/pull/8880) / [#8903](https://github.com/zeroclaw-labs/zeroclaw/pull/8903) 构建了准入基座、审批代理（支持群组法定人数）及通道通知的完整链路，标志着 SOP 里程碑迈向 5/5 成熟度。

- **ZeroCode 开发环境加固（@ConYel, @RyanSquared）**
  - [#8796](https://github.com/zeroclaw-labs/zeroclaw/pull/8796) 重构斜杠命令为强类型注册表
  - [#8902](https://github.com/zeroclaw-labs/zeroclaw/pull/8902) 实现 RPC 双向通信，使得 `ask_user` 等服务器主动请求可以正常接收响应

- **开放集成能力（@JordanTheJet, @REL-mame）**
  - [#8852](https://github.com/zeroclaw-labs/zeroclaw/pull/8852) WASM 通道插件首次接入运行时
  - [#8923](https://github.com/zeroclaw-labs/zeroclaw/pull/8923) 为 WASM 通道提供原始 TCP/TLS 网络能力
  - [#8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486) OpenAI Chat Completions 兼容端点，提升与 LangChain 等外部生态的互操作性

- **日常运维修复**
  - [#9003](https://github.com/zeroclaw-labs/zeroclaw/pull/9003) 修复了文档站中仪表盘工作流的链接

## 4. 社区热点

- **[#8681 [Tracker] Goal Mode 实现拆分栈](https://github.com/zeroclaw-labs/zeroclaw/issues/8681) （9 评论）**
  - 作为架构级跟踪器，致力于将已完成开发的 Goal Mode 从功能分支拆分为可审阅的 PR。社区和管理层高度重视执行模型的演进。

- **[#5808 默认 32K 上下文预算溢出（8 评论）](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)**
  - 自 4 月 16 日提出以来持续高热。该 Bug 导致新用户在第一次对话时即强制执行预取修剪（Preemptive Trim），**严重破坏开箱即用的核心体验**。当前仍在讨论最终的修复策略。

- **[#6641 回合级 OTel 可观测性关联（5 评论）](https://github.com/zeroclaw-labs/zeroclaw/issues/6641)**
  - 社区对生产级可观测性需求旺盛。讨论如何将 LLM 调用、工具调用、记忆操作整合在单一的 Trace 下，反映项目从原型向企业级应用过渡的强烈信号。

- **[#8654 skill-review 分支恐慌 SIGSEGV（4 评论）](https://github.com/zeroclaw-labs/zeroclaw/issues/8654)**
  - 严重稳定性 Bug，直接导致整个 Agent 进程因 SIGSEGV 退出。社区对此类导致 Pod 直接退出的 Crash 给了极高的关注度。

## 5. Bug 与稳定性
按严重程度排列：

**严重（S1 - 工作流阻断 / P1 优先级）**
- **#8654** [Bug]: skill-review 分支恐慌导致进程完全崩溃（SIGSEGV）— 高工具密度轮次后触发，偶发性致 Agent 退出。*待修复 PR。*
- **#8563** [Bug]: SOP 在 Web Dashboard 不可用 — Web 端用户无法进行 SOP 操作，严重功能缺失。*待修复 PR。*
- **#8642** [Bug]: MCP/Tool Schema 克隆导致常驻内存无限增长 — 分离自 WSL2 OOM 问题，影响长生命周期实例。*待修复 PR。*
- **#9019** [Bug]: OpenAI Responses Provider 硬编码禁用视觉能力 — 用户图片输入被拒绝。*待修复 PR。*
- **#5808** [Bug]: 默认 32K 上下文预算首次迭代即超 3.3 倍 — 跨季度问题，开箱即用障碍。

**（P2 / 中等风险）**
- **#9016** [Bug]: OpenAI 工具调用因 `reasoning_effort` 参数被拒绝。
- **#9017** [Bug]: `--config-dir` 在 CLI 区域检测中被忽略 — **已有 #9018 修复 PR**，进展良好。

## 6. 功能请求与路线图信号
**新提功能请求（2026-07-12）**
- **[#9022](https://github.com/zeroclaw-labs/zeroclaw/issues/9022) [Feature]: Slack Events API (HTTP) 模式** — 无服务器部署、降低成本。
- **[#9020](https://github.com/zeroclaw-labs/zeroclaw/issues/9020) [Feature]: ZeroCode 添加会话回退与消息分叉工作流** — 从错误的 Provider 或工具轮次中恢复。
- **[#8445](https://github.com/zeroclaw-labs/zeroclaw/issues/8445) [Feature]: Telegram 多消息模式** — 优化当前单消息拼接体验。
- **[#8442](https://github.com/zeroclaw-labs/zeroclaw/issues/8442) [Feature]: Matrix 单消息流式草稿** — 利用 Matrix 编辑能力优化流式渲染。

**路线图前瞻**
- 新增跟踪器 [#9009](https://github.com/zeroclaw-labs/zeroclaw/issues/9009) （Operator UX 上线与自助服务）与 [#9010](https://github.com/zeroclaw-labs/zeroclaw/issues/9010) （ZeroCode 加固与硬化），明确了下一阶段的交付边界。
- **[#8357](https://github.com/zeroclaw-labs/zeroclaw/issues/8357) v0.8.4 维护列车已建立**，目标日期 7 月 31 日。这意味着新功能（如 Memory 重构、ZeroCode Fork、OpenAI 端点）大概率将搭载于该版本。

## 7. 用户反馈摘要

**核心痛点（从 Issue 评论中提取）**
- **开箱即用体验严重受损**：“默认 32k 上下文预算第一次 LLM 迭代就超了 3.3 倍……默认设置完全不可用”（#5808）
- **生产稳定性焦虑**：“后台技能审查分支恐慌直接导致整个 Agent 进程 SIGSEGV，对生产部署是极其严重的打击”（#8654）
- **功能期望落差**：“按照 StageHand 示例配置的 SOP 文件完全不被 Agent 运行时检测到”（#8563）
- **文档与实践鸿沟**：“Cron 文档完全缺失，且找不到让 Cron 跑在特定模型上的方法”（#7762）
- **通道/交互体验摩擦**：“在 Slack 严格提及模式下，用户被迫每次 @提及机器人，非常打断工作流”（#6055）

**积极共建信号**
- 尽管存在上述痛点，用户群体参与了非常高水平的架构设计讨论（Otel Traces、类型化 Memory、运行时双向 RPC），社区技术底蕴深厚，且对项目长期愿景高度认同。
- 维护者（@Audacity88、@JordanTheJet、@Nillth）深度介入复杂问题（#8642、#5808）的根因分离与方案设计，社区与核心团队互动紧密。

## 8. 待处理积压
提醒维护者关注以下长期滞后或停滞的重要项：

- **[#6074 审计：追踪 153 次提交的批量回滚恢复（P2, 风险：High）](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)**
  - 创建于 4 月 24 日，已超 2.5 个月。涉及 **153 个提交** 的历史恢复，目前缺乏明确的 Recovery Plan。

- **[#5808 默认上下文预算崩溃（P1, 风险：High）](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)**
  - 跨季度优先级的核心 P1 问题，当前处于讨论僵局，仍在寻求多方介入的最终修复方案。

- **[#8353 改进错误信息上下文（PR，stale-candidate）](https://github.com/zeroclaw-labs/zeroclaw/pull/8353)**
  - 标记为 `needs-author-action`，预计较长时间无响应，需作者 @Super-Cabbage 推动。

- **[#8963 修复 Telegram 机器人命令数量超限（PR，needs-maintainer-review）](https://github.com/zeroclaw-labs/zeroclaw/pull/8963)**
  - CI 已修复，等待维护者最终审阅。

- **[#8134 session_ttl_hours 实现（Issue，needs-maintainer-review）](https://github.com/zeroclaw-labs/zeroclaw/issues/8134)**
  - 概念明确且社区呼声较高，但长时间未分配具体实现 PR。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

***

# PicoClaw 项目动态日报 | 2026-07-13

## 今日速览

过去 24 小时项目保持中等活跃度，共处理 5 条 Issues 与 3 条 Pull Requests。社区持续关注 Matrix 通道在中断后的“静默死亡”问题，并希望项目优先修复。一条来自社区 fork 的技能系统增强（技能禁用状态 + 定时任务立即执行）已合并入主分支，为即将到来的版本增加了可观测性与用户控制力。此外，Anthropic 提示缓存计费缺失的 Bug 已有人提交修复 PR，等待审核。整体来看，社区贡献质量较高，但 Matrix 长期连接稳定性问题仍悬而未决。

## 版本发布

**无**（过去 24 小时内无新版本发布）

---

## 项目进展

### 技能系统增强已合并
- **PR #3249 (Closed)** — *Skill enable/disable state + cron RunNow*  
  该 PR 来自社区 fork（Ethos P6.6），为核心项目带来了两处重要改进：
  1. **技能禁用持久化**：将技能状态写入 `workspace/skills/.skills-state.json`，技能被禁用后不会在下一轮 `<skills>` 上下文中出现，并且利用文件 mtime 追踪自动触发缓存失效，无需重启。
  2. **定时任务立即执行**：支持 `RunNow` 操作，允许用户或上层 UI 手动触发 cron 任务的即时运行，显著提升了运维灵活性。  
  **链接：** https://github.com/sipeed/picoclaw/pull/3249

### 国际化翻译补全
- **PR #3190 (Closed)** — *fix(i18n): sync missing locale keys*  
  为孟加拉语（bn-in）和捷克语（cs）补充了此前缺失的翻译键（如 `chat.dropImagesActive`、`chat.disableCodeWrap` 等），项目多语言覆盖率进一步提升。  
  **链接：** https://github.com/sipeed/picoclaw/pull/3190

### Anthropic 缓存计量修复进行中
- **PR #3251 (Open)** — *capture prompt cache token usage in Anthropic providers*  
  同时修复了 Anthropic SDK Provider 和 Anthropic Messages API Provider 中缓存相关 token 计数被丢弃的问题。合并后将使运营者能直接查看 Claude 的提示缓存命中率，有助于控制推理成本。  
  **链接：** https://github.com/sipeed/picoclaw/pull/3251

---

## 社区热点

### #3203 — Matrix 同步循环无重连逻辑（最受关注）
- **状态：** OPEN | **评论：** 2 | **👍：** 1  
- **核心问题：** Matrix 通道的 `/sync` 长轮询在遇到网络中断或 HomeServer 重启后会永久死亡，且因主进程未崩溃导致 `systemd Restart=on-failure` 不生效，形成“静默失效”状态。  
- **社区诉求：** 用户明确要求增加自动重连机制，而非依赖外部进程管理。该 issue 是近期 **点赞数最高** 的 Bug 报告，代表了运行在生产环境下的用户对渠道可靠性的强烈需求。  
  **链接：** https://github.com/sipeed/picoclaw/issues/3203

### #3182 — Android 版本服务无法启动
- **状态：** OPEN | **评论：** 3  
- **反馈：** 用户无法在 Android 上启动服务，即使已授予完整权限也无法更改路径设置。虽然带有 `[stale]` 标签，但仍在更新附件截图，表明移动端场景仍有活跃需求。  
  **链接：** https://github.com/sipeed/picoclaw/issues/3182

---

## Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 当前状态 |
|----------|------------|------|----------|
| 🔴 严重 | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Matrix `/sync` 长轮询在断网或服务器重启后永久死亡，无重连逻辑，依赖 systemd 无法恢复。 | **OPEN**，无 fix PR，社区关注度高（1 👍） |
| 🟡 中等 | [#3252](https://github.com/sipeed/picoclaw/issues/3252) | `splitKnownProviderModel` 函数在模型 ID 中含有已知 provider 别名（如 `openai/gpt-4o-mini`）时错误剥离前缀，导致配置解析异常。 | **OPEN**，昨日新上报，无评论 |
| 🟢 较低 | [#3182](https://github.com/sipeed/picoclaw/issues/3182) | Android 版本无法修改默认路径，服务无法正常启动；存在 `[stale]` 标签，长期未解决。 | **OPEN**，无 fix PR |
| ✅ 已修复 | [#3194](https://github.com/sipeed/picoclaw/issues/3194) | 收到加密消息但 crypto 未启用，用户报错日志指向 Matrix 加密处理。 | **CLOSED**（可能因重复或自动关闭） |
| ✅ 修复中 | [#3251](https://github.com/sipeed/picoclaw/pull/3251) | Anthropic 系列 provider 丢失 prompt cache 用量统计，影响成本监控。 | **OPEN (PR)**，等待 Code Review |

---

## 功能请求与路线图信号

### 已确定可进入下版本的功能
- **技能状态控制 + cron RunNow（#3249，已合并）：**  
  允许用户禁用技能（自动从 context 中移除）和手动触发定时任务。预计随 **v0.2.10 或 v0.3.0** 发布，是一个可感知的产品力提升。
- **Anthropic 缓存用量捕获（#3251，PR 待合）：**  
  面向运营者，使提示缓存命中率可视，是大型团队上线 Anthropic 模型的前置条件。

### 用户明确提出的潜在需求
- **ARMv7 / armhf Docker 支持（#3250，已关闭）：**  
  用户请求为玩客云、树莓派 Zero 提供 armhf 架构的 Docker Compose 部署方案。该 Issue 已被关闭，但未在主线看到明确实现，建议维护者主动回复社区计划。  
  **链接：** https://github.com/sipeed/picoclaw/issues/3250
- **Matrix 自动重连机制（#3203）：**  
  虽被归类为 Bug，但本质是属于核心通道的 **容错能力功能缺失**，如若纳入开发计划，将显著提升项目的生产环境稳定性评级。

---

## 用户反馈摘要

### 关键痛点
- **“静默失效”难以排查（#3203）：**  
  用户明确指出 “the main process stays alive, systemd's `Restart=on-failure` does not trigger”，意味着运维人员需要自行编写额外探活脚本，增加了部署复杂度。这是当前用户反馈中最核心的可靠性风险。
- **Android 部署体验断裂（#3182）：**  
  用户展示了截图并强调 has full permission，但依然无法更改路径。这表明 PicoClaw 在 Android 原生文件访问与权限模型适配方面可能存在兼容性缺口，或缺少必要的运行时说明。

### 使用场景暗示
- **ARM 家庭服务器 / NAS 场景（#3250）：**  
  提及玩客云（OneCloud）、树莓派 Zero 等设备，1GB RAM 限制，说明用户倾向于将 PicoClaw 当作低功耗智能网关 7×24 运行。
- **Matrix 作为主力通道（#3203）：**  
  用户详细描述 `/sync` 长轮询流程，表明是以 Matrix 作为生产级消息通道使用，而非测试性质。

---

## 待处理积压

| 编号 | 类型 | 创建于 | 摘要 | 风险说明 |
|------|------|--------|------|----------|
| [#3182](https://github.com/sipeed/picoclaw/issues/3182) | Bug (stale) | 2026-06-26 | Android 版本无法修改路径、启动服务 | 距今已 17 天未取得进展，已被自动标记 stale。若维护方缺乏 Android 测试资源，建议明确回复或关闭。 |
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | Bug | 2026-07-02 | Matrix 同步无重连逻辑 | 距今已 11 天，社区正密切关注（1 👍）。缺乏修复 PR 可能成为竞品对比中的减分项。 |
| [#3252](https://github.com/sipeed/picoclaw/issues/3252) | Bug | 2026-07-12 | 配置前缀解析逻辑缺陷 | 昨日新提交，建议维护者尽快 triage，防止后续用户踩坑扩散。 |

---

**总结：** 社区贡献者正积极补齐企业级部署的最后几块拼图（缓存计量、技能控制），而社区呼声与项目实际开发优先级之间仍有缝隙——Matrix 可靠性问题的高关注度与缺少对应修复 PR 的矛盾值得维护者警惕。

*报告生成时间：2026-07-13，数据窗口截止于 2026-07-12 23:59 UTC。*

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，作为一名AI智能体与个人AI助手领域的开源项目分析师，以下是根据您提供的QwenPaw GitHub数据生成的 **2026-07-13 项目动态日报**。

---

# QwenPaw 项目动态日报 | 2026-07-13

### 1. 今日速览

过去24小时内，QwenPaw 项目活跃度 **极高**，但整体状态偏向 **紧急修复期**。社区共提交了 19 条 Issue（其中 16 条活跃）和 10 个 PR，增量主要集中在 v2.0.0 版本的回归缺陷修复上。**核心挑战在于 v2.0.0 版本引入的多个严重破坏性变更**，包括技能系统瘫痪、上下文压缩导致 API 400 错误、自动记忆模块崩溃以及消息兼容性问题。尽管用户反馈中包含强烈的挫败感，但社区自愈能力强劲，多名贡献者直接提交修复 PR（如 #5987, #5990, #5993），项目维护者也在高优合并关键补丁，展现出了快速的危机响应能力。

### 2. 版本发布

**无。** 过去24小时内无新版本发布。

### 3. 项目进展

过去24小时内共有 3 个 PR 被关闭/合并，主要聚焦于 1.x 到 2.0 的**兼容性修复**和**核心消息链路的稳定性**。

- **兼容性修复已落地：**
  - **[\#5990]** / **[\#5988]** **([first-time-contributor])**: 修复了 `_coerce_block` 函数因遗漏 `file` 类型块导致旧版本 `tool_result` 解析失败的问题。这直接回应了部分用户升级后文件会话解析失败的问题，由贡献者 `@Nioolek` 主导。
  - **[\#5993]** **([first-time-contributor])**: 修复了 v2.0.0 无法读取 v1.x 会话中媒体文件的兼容性问题，解决了旧版图片/文件路径存储格式不匹配导致的加载失败。
- **上下文压缩稳定性修复：**
  - **[\#5987]** **([first-time-contributor])**: 针对 `#5986` 报告的上下文压缩导致 `tool_call`/`tool_result` 配对丢失的问题，提供了紧急修复逻辑（清理孤儿 tool 消息），已合并。
- **评估：** 项目当前处于“被社区推着走”的修复模式。虽然进展很快，但主要精力仍在“补窟窿”，而非推进新功能架构。

### 4. 社区热点

热帖集中在 **v2.0.0 版本的功能退化和稳定性焦虑**。

- **[\#6000]** / **[\#6001]** **技能系统完全瘫痪（Skill Pool Broken）**: 这是本日热度最高、影响面最广的缺陷。用户 `@NicholaLau` 详细描述了“任何新安装的技能在重启后均无法出现在技能池中”。这表明 v2.0.0 的技能发现/加载机制存在根本性缺陷，直接扼杀了项目的扩展生态。尽管帖子反映了严重的挫败感，但目前**尚无任何修复 PR 或维护者指派**。
- **[\#5986]** **上下文压缩致 400 BadRequestError**: 用户 `@tadebao` 报告的关于长会话中消息队列被截断导致 API 错误的帖子，引发了 4 条深度评论。该用户不仅提交了 Issue，还迅速贡献了修复 PR `#5987` / `#5989`，展现了社区极高的技术参与度和自救效率。
- **[\#5952]** **自动记忆失败（Module Not Found）**: 该问题持续发酵，桌面版打包遗漏了关键模块 `_scripts`，导致后台记忆总结任务全面崩溃。**已有 PR \#5997 针对性修复桌面端打包。**

### 5. Bug 与稳定性

Bug 数量激增，以下按严重程度排列。

#### **严重 (Critical)**
- **[\#6001]** / **[\#6000]** **技能系统完全失效**：新技能无法加载，核心扩展点崩塌。**（尚无修复 PR）**
- **[\#5995]** **消息静默丢弃**：Agent 忙碌时，新消息被静默丢弃，无排队或报错，严重破坏交互可靠性。**（尚无修复 PR）**
- **[\#5986]** **上下文压缩导致 `tool_call`/`tool_result` 配对丢失** → 引发 400 API 错误，使长对话链路易崩溃。**已有修复 PR \#5987（已合并）与 \#5989（审查中）。**
- **[\#5998]** **记忆上下文不一致**：Agent 在用户确认新方案后仍按旧方案执行，涉及深层对话逻辑与记忆管理。
- **[\#5952]** / **[\#5978]** **自动记忆与 `/compact` 命令崩溃**：模块导入错误和 session_id 字符校验错误。**已有关键修复 PR \#5997。**

#### **高优先级 (High)**
- **[\#5994]** **安全治理（Governance）Auto 模式过于严格**：每次读写文件/查找均触发审查，严重影响效率。
- **[\#5982]** **Shell 执行每次都要求用户确认**（v2.0.0 回归）：容器化部署环境用户体验降级。
- **[\#5983]** **`qwenpaw doctor` 健康检查接口返回 404**：硬编码的 API 路径与实际不符，诊断工具不可用。
- **[\#5980]** **v2.0.0 丢失 v1.x 核心功能**：SSH Offline，Profiles 等接口返回 404，部分用户面临工作流中断。

#### **中低优先级 (Medium/Low)**
- [\#5977] Plugin 热加载后 HTTP 路由丢失。
- [\#5979] Linux 环境下 Electron CLI 因沙箱限制崩溃。
- [\#5981] Web UI 模型搜索框被用户名自动填充。

### 6. 功能请求与路线图信号

尽管被 Bug 掩没，社区仍提出了对未来的高价值畅想，部分功能已有 PR 实现。

- **高价值需求：**
  - **[\#5999]** **跨频道无缝切换会话**：用户在 Console、飞书、钉钉之间接力同一段对话。这是一个极具前瞻性的企业级需求，涉及 Session 管理层的深度重构。如果纳入路线图，将极大提升 QwenPaw 在跨设备/跨平台场景的竞争力。
- **下一版本可能纳入的 PR：**
  - **[\#5992]** **按 Session 切换模型**：具有极高的实用价值，允许不同对话独立选择模型，已有实现 PR 待审。
  - **[\#5869]** **全局 Slash 命令自动补全**：已在 Review 阶段，将统一 TUI 和 Web UI 的控制交互体验。
  - **[\#5984]** **请求支持永久禁用特定环境的工具审批**：反映了服务器/边缘设备用户对“无值守运行”的刚性需求。

### 7. 用户反馈摘要

- **升级之痛（最大声量）**：用户 `@ausliang`、`@tadebao`、`@jackicy9736` 明确表达了从 v1.x 升级到 v2.0 后的挫败感。旧会话打不开 (#5964)，常用功能接口 404 (#5980)，新技能无法安装 (#6001)。用户认为 v2.0.0 的升级**破坏了既有的工作流**。
- **稳定性焦虑**：用户 `@kukuegg` 和 `@tadebao` 报告在普通对话中频繁出现 `MODEL_EXECUTION_ERROR` 和 400 错误 (#5986, #5996)，这让用户对产品的基本可用性产生了动摇。
- **场景割裂感**：Raspberry Pi 用户 (`@billyoungs`) 无法关闭沙盒确认；Linux 用户 (`@jackphil`) 遭遇 Electron 崩溃；部分用户反馈后台脚本完全无法工作。v2.0.0 在不同部署场景下的表现参差不齐。
- **积极的社区协作**：用户 `@Nioolek`、`Nioolek`、`tadebao` 等贡献者不仅提出问题，还直接提供代码修复，体现了开源社区的韧性。

### 8. 待处理积压

以下问题长期未得到核心团队的公开响应或修复指派，风险较高：

1.  **[P0] 技能系统完全失效**
    - **Issue**: [\#6001] [\#6000]
    - **分析**: 核心系统架构缺陷，直接影响所有第三方开发者。当前无任何分配或修复 PR，属于当前版本最大的 `show-stopper`。
    - **建议**: 需要核心开发者立即介入。

2.  **[P1] 消息静默丢弃**
    - **Issue**: [\#5995]
    - **分析**: 严重影响多轮对话的可靠性，尚未分配负责人。这是一个导致数据丢失的隐蔽 Bug，优先级应该被提升。

3.  **[P1] `MODEL_EXECUTION_ERROR` 消息格式化问题**
    - **Issue**: [\#5996] [\#5985]
    - **分析**: `hint.py` 和后台工具的格式化逻辑存在 bug，导致 OpenAI 兼容接口报错。目前无明确 PR，影响了主流程模型的正常调用。

4.  **[P2] Plugin 热加载路由丢失**
    - **Issue**: [\#5977]
    - **分析**: 影响开发者迭代效率，属于 2.0 新特性的稳定性问题，虽非用户级阻塞项，但应尽快补全测试用例。

---
**分析师观点：**
QwenPaw 目前处于 **v2.0 大版本迭代后的“阵痛期”**。项目热度极高，但产品稳定性经受严峻考验。建议维护团队：
1. **首先确保技能系统和上下文压缩这两个核心模块的稳定**，这是 Agent 扩展和长对话的基础。
2. **考虑在一个补丁版本（v2.0.1）中** 优先合并现有的兼容性修复 PR（#5997, #5993, #5991），并回滚或调整过于激进的安全默认策略（AUTO 模式）。
3. **明确回应 #6001**，这对保护第三方开发者生态至关重要。

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes-Agent 项目动态日报 (2026-07-13)

---

## 1. 今日速览

过去 24 小时项目维持极高活跃度：**Issues 共计更新 500 条**（新开/活跃 134 条，关闭 366 条），**PR 更新 500 条**（待合并 443 条，合并/关闭 57 条）。社区反馈涌入与维护者处理并进，问题净减少 232 条，表明修复效率高于新问题产生率；PR 合并率约 11.4%，大量提交仍处于待审查状态，维护者带宽需重点关注。今日无新版本发布，但多个长期请求（如原生 Vertex AI 支持、Brave Search 后端）已在主分支落地，距离下一个正式发布已不远。

---

## 2. 版本发布

_无新版本发布，本节略。_

---

## 3. 项目进展

尽管过去 24 小时无正式版本发布，但多个 **社区高频请求的功能与 Bug 修复** 已通过 PR 合并至主分支（从 Issue 标签 `sweeper:implemented-on-main` 可见），标志着项目稳健推进。主要进展包括：

- **原生 Google Cloud Vertex AI 提供者**（#13484）与 **支持绕过 OpenRouter 402/限速的 Native Google Provider**（#12639）均已实现，用户现可直接通过 Vertex AI 或 Google AI Studio 使用 Gemini 系列模型，无需依赖第三方路由。
- **Brave Search 作为原生 Web 搜索后端**（#10644）已集成，与现有的 Firecrawl、Tavily 等并列，提供免费层和低延迟选项。
- **Windows 原生支持**（#10359）相关适配已合入，非 WSL 环境的使用体验得到改善，包括文件读写、路径处理等（#17753 等关联修复）。
- **Dashboard 主题改进**（#18080）已实施，针对可读性差、字体/配色不规范的问题进行了优化。
- **微信多账号绑定**（#9756）、**Discord 附件可靠传递**（#11860）、**Mattermost 会话隔离**（#18279）等网关平台增强也已合入。

**新提交的 PR** 则进一步覆盖了多个方向的增量修复与特性：

- `fix(computer_use): normalize bullet app names, surface stale session, re-declare on reconnect`（#63439）修复 CuaDriver 后端中 app 名称带列表标记导致截图失败的问题。
- `fix(tui): stop recovery hanging after gateway restart`（#63437）解决 TUI 在网关断开后自动恢复时挂起。
- `fix(auth): prevent provider auto-detection from disabling credential failover`（#63427）修复认证自动检测覆盖凭据轮替机制。
- `feat(i18n): add Slovak (sk) locale`（#63426）扩展国际化至斯洛伐克语。
- `feat(desktop): preview local paths in completed assistant messages`（#63435）让桌面版可预览助手消息中的本地文件路径。

> 参考：
> - Vertex AI 实现: [#13484](https://github.com/NousResearch/hermes-agent/issues/13484) | [#12639](https://github.com/NousResearch/hermes-agent/issues/12639)
> - Brave Search: [#10644](https://github.com/NousResearch/hermes-agent/issues/10644)
> - Windows 支持: [#10359](https://github.com/NousResearch/hermes-agent/issues/10359)
> - 主题改进: [#18080](https://github.com/NousResearch/hermes-agent/issues/18080)
> - 微信多账号: [#9756](https://github.com/NousResearch/hermes-agent/issues/9756)

---

## 4. 社区热点

讨论热度与反应数最高的 Issues 集中在 **UI/UX、模型提供商兼容性、自动化监控** 三大主题：

| Issue | 标题 | 评论 | 👍 | 状态 |
|-------|------|------|----|------|
| [#18080](https://github.com/NousResearch/hermes-agent/issues/18080) | Improved Themes for Dashboard - currently hard to read | 28 | 50 | ✅ Closed / Implemented |
| [#38240](https://github.com/NousResearch/hermes-agent/issues/38240) | Skills index is stale or degraded (degraded) | 25 | 0 | 🔴 Open |
| [#15895](https://github.com/NousResearch/hermes-agent/issues/15895) | google-gemini-cli causing 429 but gquota ok | 17 | 6 | ✅ Closed / Cannot reproduce |
| [#12639](https://github.com/NousResearch/hermes-agent/issues/12639) | Support for Native Google / Vertex AI Provider | 15 | 10 | ✅ Closed / Implemented |
| [#13484](https://github.com/NousResearch/hermes-agent/issues/13484) | native Google Cloud Vertex AI provider support | 13 | 14 | ✅ Closed / Implemented |
| [#40166](https://github.com/NousResearch/hermes-agent/issues/40166) | Desktop app: add font size / zoom control | 10 | 17 | 🔴 Open |
| [#10644](https://github.com/NousResearch/hermes-agent/issues/10644) | Add Brave Search as a native web search backend | 8 | 23 | ✅ Closed / Implemented |

- **Dashboard 主题** 获得最高点赞（50），反映用户对界面美观与可读性的强烈期望，现已解决。
- **技能索引监控**（#38240）虽由机器人自动发起，但持续 25 条评论暗示该自动检测机制可能存在误报或配置问题，需维护者评估。
- **桌面端字体缩放**（#40166）17 个 👍 且仍开放，是当下 UI 层面最迫切的未被满足需求。
- **Brave Search** 虽仅 8 条评论，但得到 23 个 👍，说明低成本搜索方案是广泛诉求，现已实现。

---

## 5. Bug 与稳定性

### 今日报告的关键 Bug（按严重程度排列）

| 严重度 | Issue | 标题 | 状态 | 是否有修复 PR |
|--------|-------|------|------|---------------|
| **P2** | [#18357](https://github.com/NousResearch/hermes-agent/issues/18357) | [Bug]: Setup SABOTAGES computer integrits - npm global installs hijacked to ~/.hermes/node | 🔴 Open | 未发现 |
| **P2** | [#27178](https://github.com/NousResearch/hermes-agent/issues/27178) | Kanban worker reports 'protocol_violation' when agent ends turn with text response | 🔴 Open | 未发现 |
| **P2** | [#15290](https://github.com/NousResearch/hermes-agent/issues/15290) | Persistent `[Errno 13] Permission denied` on `/opt/data/config.yaml` on NAS Docker | ✅ Closed / Implemented | 已有修复 |
| **P3** | [#38240](https://github.com/NousResearch/hermes-agent/issues/38240) | Skills index is stale or degraded (degraded) | 🔴 Open | 未发现（监控问题） |
| **P3** | [#11860](https://github.com/NousResearch/hermes-agent/issues/11860) | Discord attachments are not reliably passed into agent context | ✅ Closed / Implemented | 已有修复 |
| **P3** | [#18646](https://github.com/NousResearch/hermes-agent/issues/18646) | send_message ignores WhatsApp group target | ✅ Closed / Implemented | 已有修复 |
| **P3** | [#15551](https://github.com/NousResearch/hermes-agent/issues/15551) | Custom Endpoints Don't Execute Commands | ✅ Closed / Implemented | 已有修复 |

- **#18357** 用户指控安装脚本“将 npm 全局安装劫持到 `~/.hermes/node`，破坏其他软件”，措辞激烈，属于安全/系统完整性级别的严重问题，但尚未得到维护者响应。
- **#27178** Kanban worker 协议违规影响自动化工作流稳定性，且无后备机制，需要优先排查。
- **#15290** Docker 权限问题已被修复，但曾是 NAS 用户的核心痛点。
- **#38240** 技能索引降级虽非直接功能故障，但会影响技能市场的可靠性，需确认是监控配置问题还是底层索引生成失败。

### 今日提交的 Bug 修复 PR（快速响应亮点）

- `fix(computer_use): normalize bullet app names`（#63439）针对 CuaDriver 截图缺陷。
- `fix(tui): stop recovery hanging after gateway restart`（#63437）修复 TUI 恢复挂起。
- `fix(kanban): broker detached worker approvals across processes`（#63421）修复 Kanban 分离 worker 审批死锁。
- `fix(kanban): tolerate incomplete completed run history`（#63430）防止 `kanban_show` 因缺少 `ended_at` 崩溃。
- `fix(matrix): drain crypto handlers before DB shutdown`（#63431）修复 Matrix 网关关闭时数据库损坏。
- `fix(auth): prevent provider auto-detection from disabling credential failover`（#63427）修复认证覆盖问题。

这些修复覆盖了桌面端、网关、认证、Kanban 等多个模块，表明维护者在持续打磨稳定性。

---

## 6. 功能请求与路线图信号

### 已确认纳入主分支（下一版本大概率包含）

| 功能 | Issue | 点赞 | 说明 |
|------|-------|------|------|
| 原生 Google / Vertex AI Provider | [#12639](https://github.com/NousResearch/hermes-agent/issues/12639) | 10 | 绕过 OpenRouter，直接使用 Gemini |
| Brave Search 后端 | [#10644](https://github.com/NousResearch/hermes-agent/issues/10644) | 23 | 低成本搜索替代方案 |
| 原生 Windows 支持 | [#10359](https://github.com/NousResearch/hermes-agent/issues/10359) | 8 | 告别 WSL2 依赖 |
| Dashboard 主题改进 | [#18080](https://github.com/NousResearch/hermes-agent/issues/18080) | 50 | 提升可读性 |
| 微信多账号绑定 | [#9756](https://github.com/NousResearch/hermes-agent/issues/9756) | 0（但评论 7） | 家庭/团队场景 |

### 仍开放、呼声高、可能纳入下个版本

- **桌面端字体缩放 / 缩放控制**（[#40166](https://github.com/NousResearch/hermes-agent/issues/40166)，👍 17）：macOS 高分辨率屏幕下无适配，用户期望 `Cmd+Plus` 等原生快捷键生效。
- **Scope-recall 独立内存提供者**（[#42864](https://github.com/NousResearch/hermes-agent/issues/42864)，评论 7）：第三方插件 RFC，请求官方文档化支持。若采纳，可丰富 Hermes 的内存策略生态。
- **TTS 音频回放（WebUI）**（PR [#16717](https://github.com/NousResearch/hermes-agent/pull/16717)）：将 TTS 从 TUI/Discord 扩展到浏览器，增强多媒体交互。虽未合并，但已持续活跃，具备落地潜力。

### 明确不被计划的功能

- **每回合专家切换模型预设**（[#20249](https://github.com/NousResearch/hermes-agent/issues/20249)，标签 `sweeper:not-planned`）被维护者拒绝，理由是设计复杂且可能违背会话连贯性。

> 路线图信号：项目正围绕 **多模型提供商原生接入**、**低门槛搜索**、**平台适配（Windows/微信）** 等方向持续完善，同时关注国际化（斯洛伐克语 PR）与多模态交互（TTS、本地文件预览）。

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的真实用户声音：

- **“The selection of fonts and colours is non-standard […] serif fonts, especially small and light font weight with little contrast makes the dashboard hard to read.”**（#18080）—— Dashboard 主题问题长期影响用户日常使用，现已修复。
- **“Docker 体验太差了。说 10000 用户但 WebUI 是 1000；在容器里 mkdir /root 失败；挂载目录说明不清晰。”**（#14448）—— Docker 部署文档和容器行为对新手不友好，虽已部分修复（#15290），但用户体验提升仍有空间。
- **“Never seen that before - it borders criminal behavior, seriously, computer sabotage.”**（#18357）—— npm 全局安装被劫持激起了用户强烈不满，认为安装脚本“破坏计算机完整”。该问题至今未解决，可能损害项目声誉。
- **“Hermes stops talking to Google gemini model after some prompts. Only Hermes has this problem.”**（#20244）—— 与 Gemini 的兼容性故障影响特定场景，用户对比了 opencode 等其他工具后反馈，已修复。
- **“cannot read local file in windows system (no WSL). However, it can write to the file correctly.”**（#17753）—— Windows 下的文件读取权限或路径处理问题，导致助理无法读取用户文件，已修复。

整体上，用户对 **多平台（Docker、Windows、macOS）的体验一致性** 和 **安装脚本的安全性** 表现出较高敏感度。已修复的反馈多给予正向默认，但未解决的严重问题（#18357）可能引发信任危机。

---

## 8. 待处理积压

以下为长期未获官方响应的 Issue 或 PR，需维护者重点关注：

| 类型 | 编号 | 标题 | 创建时间 | 关注意义 |
|------|------|------|----------|----------|
| 🐛 Bug | [#18357](https://github.com/NousResearch/hermes-agent/issues/18357) | Setup SABOTAGES computer integrits - npm global installs hijacked | 2026-05-01 | 系统完整性安全，用户情绪极端，未有任何官方回复 |
| 🐛 Bug | [#27178](https://github.com/NousResearch/hermes-agent/issues/27178) | Kanban worker protocol_violation when agent ends turn with text | 2026-05-16 | 影响自动化工作流稳定性，没有关闭或标记 |
| 🔧 RFC | [#42864](https://github.com/NousResearch/hermes-agent/issues/42864) | scope-recall standalone memory provider (Show & Tell) | 2026-06-09 | 社区主动贡献的内存插件方案，等待官方指导 |
| 🔧 Feature | [#40166](https://github.com/NousResearch/hermes-agent/issues/40166) | Desktop app: add font size / zoom control | 2026-06-05 | 高点赞（17），高目击者众，维护者未参与 |
| 🔧 PR | [#18555](https://github.com/NousResearch/hermes-agent/pull/18555) | fix(auth): allow Codex CLI auth reuse | 2026-05-01 | 已开放超过 2 个月，涉及企业部署场景的认证兼容性 |
| 🔧 PR | [#20295](https://github.com/NousResearch/hermes-agent/pull/20295) | Fix empty conversation history handling in _handle_runs | 2026-05-05 | 历史遗留 PR，API 行为修复，长期未合并 |
| 🔧 PR | [#20290](https://github.com/NousResearch/hermes-agent/pull/20290) | fix(gateway): guard GatewayConfig.from_dict against non-dict platforms | 2026-05-05 | 小但关键的配置健壮性修复 |

> 建议：对 **#18357** 应立即回应并修复或澄清，避免社区负面发酵；**#27178** 和 **#40166** 是日常使用稳定性与体验的高频痛点，宜分配迭代；**#18555**、**#20295** 等老式 PR 应安排审查或关闭以清理积压。

---

*本报告基于 NousResearch/hermes-agent 公开数据生成，数据截止 2026-07-13 00:00 UTC。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*