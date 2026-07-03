# OpenClaw 生态日报 2026-07-03

> Issues: 183 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-03 07:49 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告



---

## 横向生态对比

好的，以下是根据您提供的社区动态摘要（2026-07-03）生成的横向对比分析报告。

---

# AI 智能体开源生态横向对比分析报告（2026-07-03）

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **功能快速迭代与稳定性博弈** 的关键阶段。头部项目如 **QwenPaw** 和 **hermes-agent** 均在24小时内保持极高的 PR/Issue 吞吐量，版本发布节奏明显加快（如 QwenPaw 已推进至 v2.0.0-beta.2）。社区反馈已从基础功能需求转向 **安全性、上下文可靠性、跨平台统一体验** 等更成熟的方向。同时，部分核心参照项目（如 OpenClaw 系列）今日未见公开动态，表明生态内部已出现 **「核心稳定 + 前沿激进」** 的分化态势——上游底座趋向收敛，下游应用与变体加速迭代。

## 2. 各项目活跃度对比

以下数据基于过去24小时内社区动态汇总，OpenClaw / Zeroclaw / PicoClaw 无公开活动记录，标记为“暂无数据”。

| 项目 | Issues（24h） | PRs（24h） | 新版本发布 | 健康度评估 |
|------|--------------|------------|------------|-----------|
| **OpenClaw** | 暂无数据 | 暂无数据 | 无 | 观察期，需进一步确认活跃状态 |
| **Zeroclaw** | 暂无数据 | 暂无数据 | 无 | 同上 |
| **PicoClaw** | 暂无数据 | 暂无数据 | 无 | 同上 |
| **QwenPaw** | 26（新处理） | 42 | v2.0.0-beta.2 | 🟢 高活跃，但 v2.0 系列稳定性问题突出，处于功能扩张与补丁并行期 |
| **hermes-agent** | 306（更新量，其中新开/活跃263） | 500 | 无 | 🟢 极高度活跃，Issue 积压较大但修复响应极快，社区参与密度最高 |

## 3. OpenClaw 在生态中的定位

虽然今日无公开动态，但从项目命名体系（OpenClaw → Zeroclaw / PicoClaw）及行业惯例推断：

- **定位核心参照**：OpenClaw 很可能是该家族的基础框架或核心实现，**Zeroclaw**（侧重零拷贝/轻量）、**PicoClaw**（侧重微型/嵌入式）为其衍生变体。当前缺乏动态可能意味着其已进入稳定维护期。
- **与 QwenPaw / hermes-agent 的差异**：后两者更侧重云/桌面全功能 Agent 平台，与 OpenClaw 系列形成**上游框架 vs. 下游产品** 或 **通用核心 vs. 垂直场景** 的关系。若 OpenClaw 作为底层引擎，其稳定性优势将成为生态健康度的关键锚点。当前无明显社区反馈，亟需更多信息以判断其实际影响力。

## 4. 共同关注的技术方向

以下方向由 **QwenPaw** 和 **hermes-agent** 的项目动态同时涌现，反映行业共性需求：

| 技术方向 | 涉及项目 | 具体诉求与体现 |
|----------|----------|----------------|
| **上下文/会话管理可靠性** | QwenPaw, hermes-agent | QwenPaw 报出 scroll 策略错乱（#5746）、hermes-agent 修复会话压缩后持久化失效（#57508/#57531）。双方用户均对长对话数据不丢失、不被错误截断有强烈需求。 |
| **工具调用/Agent 自循环检测** | QwenPaw, hermes-agent | QwenPaw #5717 工具调用截断导致死循环；QwenPaw #5657 & hermes-agent 无明确对应但 hermes-agent 在 shell 钩子中增加哈希校验（#57562）表明对执行安全与异常终止的重视。 |
| **多通道/多平台统一接入** | QwenPaw, hermes-agent | QwenPaw 合并 Azure Bot 通道（#5762）；hermes-agent 出现 QQ 机器人适配器重连 Bug（#52914/#53443），双方都在努力扩展和稳定非桌面端入口。 |
| **密钥/安全加固** | QwenPaw, hermes-agent | QwenPaw #5705 要求日志脱敏与加密存储（已有 PR #5745）；hermes-agent #57562 增加白名单内容哈希校验。安全已成标配需求。 |
| **记忆系统可配置化** | QwenPaw, hermes-agent | QwenPaw 新增 none 内存后端（#5732），允许一键禁用记忆；hermes-agent #47349 要求可替换记忆后端。用户期望灵活管理长期记忆。 |
| **UI 一致性与阅读体验** | QwenPaw, hermes-agent | QwenPaw 修复移动端会话列表、重构技能页；hermes-agent #18080 主题可读性获45个👍，桌面端 Capabilities 页面重构（#57590）。前端体验进入精细化打磨期。 |

## 5. 差异化定位分析

| 维度 | QwenPaw | hermes-agent | OpenClaw 系列（推测） |
|------|---------|-------------|----------------------|
| **功能侧重** | Agent 工具链与平台化，强化通道扩展（Azure Bot 等）与上下文策略（scroll/scroll） | 个人桌面 AI 助手为核心，CLI 与网关并重，社区包罗万象（Telegram, QQ, iMessage等） | 底层核心能力守护，轻量变体面向边缘/嵌入式 |
| **目标用户** | 平台集成者、功能型 Agent 开发者 | 桌面深度用户、多服务串联爱好者和开发者 | 框架使用者、硬件集成商（PicoClaw） |
| **技术架构** | v2.0 正在重构，社区反馈集中在上下文和工具调用机制 | 社区 PR 非常多，架构演进快（Capabilities 页面集成 MCP），依赖网状扩展 | 推测为模块化核心，衍生产品专注于资源受限场景 |
| **版本稳定性心智** | v1.1.x 稳定但有内存泄漏，v2.0.0-beta 激进但问题多 | 无正式版本发布，持续滚动开发，用户对更新频率高容忍但也抱怨回归 | 如果长期无动态，可能强调稳定、变更少 |
| **社区主导** | AgentScope-AI 组织驱动，外部贡献者高质量参与 | NousResearch 组织，社区参与规模极大（24h 500 PR） | 暂无明显外部贡献信号 |

## 6.

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>



</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>



</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，以下是为您生成的 **QwenPaw 开源项目日报 (2026-07-03)**。

***

# QwenPaw 项目动态日报 2026-07-03

**数据快照：** 过去24小时 (截至2026-07-03) 项目活跃度极高，共处理26个 Issues 和42个 PR。 v2.0.0 新版本迭代加速，但伴随的稳定性问题和社区反馈也显著增加。

---

## 1. 今日速览

- **版本迭代加速：** 项目在24小时内发布了 `v2.0.0-beta.2`，并已合并 `v2.0.0b3` 的版本号更新，显示团队正全力推进 2.0 系列的开发与修复工作。
- **稳定性成焦点：** `v1.1.12.post2` 版本报告了**内存泄漏**问题，且 `v2.0.0-beta.2` 被反馈存在**上下文压缩**逻辑缺陷和**工具调用格式**异常，稳定性是当前社区和开发者的共同关注重点。
- **生态与社区活跃：** 社区提出了**密钥安全改进**、**增强 CLI**、**自动切换模型**等多个高质量增强建议，并贡献了如**Azure Bot 通道**、**Windows 原生沙箱**等新特性 PR，外部贡献活跃度保持在高位。
- **关键问题修复进行中：** 针对**滚动上下文错乱**和**工具调用无限循环**这两个关键 Bug，已有社区成员提交了修复 PR，并正在审查中。

---

## 2. 版本发布

### [v2.0.0-beta.2](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0-beta.2)
- **发布时间：** 2026-07-02
- **说明：** 这是 QwenPaw 2.0.0 的第二个早期测试版，正在积极开发中，可能包含破坏性变更和不稳定因素。
- **主要变更：**
    - `feat(cli): add cron up` - 新增 CLI 的 `cron up` 功能，加强后台任务管理能力。
- **注意事项：**
    - ⚠️ 此版本不适合生产环境。
    - ⚠️ 更新的安装验证流程（Release Duty）已自动触发并通过。
    - **已知风险：** 根据社区反馈，此版本的默认 `scroll` 上下文策略可能导致上下文错乱（Issue #5746）和工具调用截断问题（Issue #5717）。

---

## 3. 项目进展

过去24小时内，项目在稳定新功能和优化架构方面取得显著进展，多个关键 PR 被合并或处于审查后期。

- **[🚀 已合并] 核心健壮性提升：**
    - [#5755 - fix(config): make agent resilient to invalid MCP client config](https://github.com/agentscope-ai/QwenPaw/pull/5755) - 修复了因单个 MCP 客户端配置错误（如参数拼写错误）导致整个 `AgentProfileConfig` 验证失败的问题。这使得核心配置模块更加健壮。
    - [#5742 - fix: show stream completion time instead of first-chunk time](https://github.com/agentscope-ai/QwenPaw/pull/5742) - 修复了流式输出计时问题，现在展示的是消息完成时间而非首次响应时间。
- **[🚀 已合并] 用户体验优化：**
    - [#5744 - fix(console): mobile chat history panel shows empty session list](https://github.com/agentscope-ai/QwenPaw/pull/5744) - 修复了移动端浏览器中，历史会话列表为空的问题。
    - [#5753 - refactor(skill): skill-related UI](https://github.com/agentscope-ai/QwenPaw/pull/5753) - 重构了技能相关的前端 UI，将市场功能集成到技能页面，统一了添加操作入口。
- **[🚀 已合并] 新生态与能力扩展：**
    - [#5762 - feat(channel): add azure_bot channel (New)](https://github.com/agentscope-ai/QwenPaw/pull/5762) - 新增 Azure Bot 通道支持，可连接 Teams、Slack、Telegram 等多种平台。这是一个重大的通道扩展。
    - [#5732 - feat: add 'none' memory backend to disable memory system](https://github.com/agentscope-ai/QwenPaw/pull/5732) - 新增 `none` 内存后端，允许用户通过 UI 界面完全禁用记忆系统，无需手动修改配置文件，降低了用户使用门槛。
- **[🔄 关键修复 PRs 评审中]：**
    - [#5747 - Protect active turn from scroll context eviction](https://github.com/agentscope-ai/QwenPaw/pull/5747) - 针对 #5746 Bug 的修复，防止 `scroll` 上下文策略折叠当前正在执行的任务。
    - [#5761 - fix(agents): surface malformed tool-call input to model](https://github.com/agentscope-ai/QwenPaw/pull/5761) - 针对 #5717 Bug 的修复，将格式错误的工具调用信息暴露给模型，而非简单丢弃，避免模型陷入死循环。

---

## 4. 社区热点

- **[#5746 - [Bug]: 2.0 beta：scroll 上下文压缩可能错误折叠当前任务](https://github.com/agentscope-ai/QwenPaw/issues/5746)**
    - **热度：** 评论 3，状态 OPEN。
    - **分析：** 用户详细描述了在执行 `/heartbeat` 复杂任务时，因 `scroll` 上下文压缩导致模型“失忆”，转而回复旧消息的严重问题。此问题直接关系到 2.0 新版本的核心稳定性，引发了广泛关注。**用户的诉求是对 `scroll` 策略的可靠性和透明性提出质疑。**

- **[#5717 - [Bug]: Runtime 2.0 malformed tool-call 导致无限循环](https://github.com/agentscope-ai/QwenPaw/issues/5717)**
    - **热度：** 评论 2，状态 OPEN。
    - **分析：** 用户复现了因大文件工具调用参数被截断，导致模型反复执行同一个工具调用的问题。这触及了 Agent 核心逻辑中的循环检测缺失问题，是高危 Bug。**用户的深层需求是 Agent 需要拥有执行超时和循环自检能力。**

**总结：** 社区热点高度集中在 `v2.0.0-beta` 版本的稳定性问题上，特别是`上下文管理`和`工具调用`这两个 Agent 核心环节。用户不仅是报告问题，更是在通过详细的分析和复现步骤，**推动项目在核心架构层面建立更完善的容错和恢复机制**。

---

## 5. Bug 与稳定性

### 严重
- **[#5720 - 内存泄漏 (v1.1.12.post2)](https://github.com/agentscope-ai/QwenPaw/issues/5720)**：用户报告进程内存从150MB持续增长至580MB后被杀进程，导致配置损坏。`[分析：这是稳定版本存在的高危问题，可能影响所有用户]`
    - **状态：** OPEN，无关联修复 PR。
- **[#5746 - 上下文压缩逻辑错误 (v2.0.0-beta.2)](https://github.com/agentscope-ai/QwenPaw/issues/5746)**：`scroll`策略折叠了当前活动任务，导致回复错乱。
    - **状态：** OPEN，已有修复 PR [#5747](https://github.com/agentscope-ai/QwenPaw/pull/5747) 正在审查。
- **[#5717 - 工具调用格式错误导致死循环 (Runtime 2.0)](https://github.com/agentscope-ai/QwenPaw/issues/5717)**：截断的工具调用参数未被正确处理，导致模型无限重复执行。
    - **状态：** OPEN，已有修复 PR [#5761](https://github.com/agentscope-ai/QwenPaw/pull/5761) 正在审查。
- **[#5725 - 流式输出时浏览器卡顿 (v1.1.12.post2)](https://github.com/agentscope-ai/QwenPaw/issues/5725)**：用户在服务端部署时，前端浏览器在流式响应期间卡顿，回答完毕才恢复。可能影响所有 Web UI 用户。
    - **状态：** OPEN，无关联修复 PR。

### 中等
- **[#5759 - 计划模式反复读取文件 (v1.1.12.post1)](https://github.com/agentscope-ai/QwenPaw/issues/5759)**：同一文件在单次任务执行中被多次重复读取，造成资源浪费。
    - **状态:** OPEN。
- **[#5757 - 飞书通道不回复](https://github.com/agentscope-ai/QwenPaw/issues/5757)**：第一条消息正常回复，后续消息无响应。
    - **状态:** OPEN。

### 轻微
- **[#5744 - 移动端历史会话列表为空 (已修复)](https://github.com/agentscope-ai/QwenPaw/pull/5744)**：该问题已在 PR #5744 中修复并合并。
- **[#5183 - 宠物功能在 Wayland 下无法使用](https://github.com/agentscope-ai/QwenPaw/issues/5183)**：Linux 用户反馈的桌面端特性兼容性问题。

---

## 6. 功能请求与路线图信号

- **[#5705 - 密钥脱敏与安全存储](https://github.com/agentscope-ai/QwenPaw/issues/5705)**：提出加密密钥存储、环境变量回退和日志脱敏的需求。**高优先级，已有 PR [#5745](https://github.com/agentscope-ai/QwenPaw/pull/5745) 针对日志脱敏进行安全加固。**
- **[#5737 - 增强 CLI 能力](https://github.com/agentscope-ai/QwenPaw/issues/5737)**：用户希望通过 CLI 进行预装 SKILL 等操作，以便于业务二次包装。直接对应到新发布的 CLI `cron up` 功能，表明团队正在此方向投入。
- **[#5718 - 自动切换模型](https://github.com/agentscope-ai/QwenPaw/issues/5718)**：用户期望 Agent 在遇到模型限额或错误时能自动切换到备用模型。结合 [#5726 - 视觉降级功能 PR](https://github.com/agentscope-ai/QwenPaw/pull/5726)，表明团队正在探索模型层面的容错与切换机制。
- **[#5657 - 循环检测机制](https://github.com/agentscope-ai/QwenPaw/issues/5657)**：用户提出 Agent 在工作流中容易陷入死循环的问题，建议实现循环检测机制。这与 #5717 的 Bug 直接相关，是 Agent 框架成熟度的重要标志。
- **[#5756 / #4437 - 对话记录选择性引用/删除](https://github.com/agentscope-ai/QwenPaw/issues/5756)**: 用户多次提出需要精细化操作历史对话（选中、部分引用、删除），这是提升对话界面易用性的核心需求。
- **[#5762 - Azure Bot 通道（已实现）](https://github.com/agentscope-ai/QwenPaw/pull/5762)**：来自社区的 PR，用于支持 Azure Bot 框架的所有连接平台，扩展了企业的集成能力。

---

## 7. 用户反馈摘要

- **痛点：** 用户普遍反映“任务出现问题时，缺乏自动恢复和容错机制”，不得不手动干预（如 #5718 要求自动切换模型， #5717 报告的工具调用循环）。
- **挫败感：** 1.1.12.post2 版本的内存泄漏问题（#5720）导致用户数据丢失，需要重新配置，严重影响了使用体验和信任度。
- **诉求明确：** 社区非常希望 Agent 具备更强的“自我修复”和“异常感知”能力，例如要求实现“循环检测”（#5657）和“计划模式中避免重复读取文件”（#5759），体现了用户对 Agent 智能化程度的更高期待。
- **正面反馈：** 用户通过提交高质量的 Feature Request（如 #5705 安全改进）和快速跟进的 Bug 报告，表现出对项目的高度参与和专业度。许多用户开始尝试 v2.0.0 版本并提供了宝贵反馈，说明社区对新架构有很强的探索意愿。

---

## 8. 待处理积压

- **⚠️ 高优先级需关注：**
    - [#5720 - (Bug) 内存泄漏反馈](https://github.com/agentscope-ai/QwenPaw/issues/5720): 影响所有 v1.1.12.post2 用户的稳定性，目前无关联 PR，建议优先排查 `_consume_queue` 等异步任务泄漏可能性。
    - [#5725 - (Bug) 流式输出时浏览器卡顿](https://github.com/agentscope-ai/QwenPaw/issues/5725): 影响所有 Web UI 端用户的实时体验，可能与前端渲染性能或 WebSocket 数据传输有关，建议进行性能 Profiling。

- **⌛ 长期需求待回应：**
    - [#5657 - (Feature) Loop Detection Mechanism](https://github.com/

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是为您生成的 hermes-agent 项目动态日报。

---

# hermes-agent 项目动态日报 (2026-07-03)

## 今日速览

今日项目活跃度极高。过去24小时内，Issues 更新量达到306条，其中新开/活跃263条，PR 更新量更是高达500条，表明社区反馈踊跃且项目组响应迅速。虽然今日无新版本发布，但多个高优先级 Bug 被修复并合并，尤其是在状态持久化、会话压缩和安全性方面。PR 方面，关于桌面端统一“Capabilities”页面和 MCP 管理的 PR (#57590) 是今日最重大的功能推进，预示着 UI/UX 层面的重构。整体来看，项目处于高强度迭代与问题修复并行的状态，项目健康度良好，但 Issue 积压量仍需关注。

## 版本发布

无

## 项目进展

今日有多个重要 PR 被合并或推进，主要集中在 Bug 修复与功能增强，项目在稳定性和功能性上均有所前进。

- **核心稳定性修复**：多个高优先级 (P1) Bug 得到解决。例如，修复了会话压缩轮转后，压缩的转录数据未持久化到 SQLite 数据库的问题 (`#57508`, `#57531`, `#57574`)。这些修复确保长会话在经过压缩后，历史记录不会在重启后丢失，是重要的数据完整性改进。
- **代理与网关修复**：PR `#57585` 修复了 `opencode-go` 因基础 URL 缺少 `/v1` 后缀而导致的 404 错误，提升了跨模型兼容性。PR `#57577` 修复了 Telegram 网关中，语音消息无法作为对 `clarify` 提示的响应的问题。
- **安全加固**：PR `#57562` 为 shell 钩子（shell-hooks）的白名单机制增加了内容哈希校验，防止脚本内容被篡改后仍能被自动批准，增强了安全性。
- **UI/UX 改进**：PR `#57583` 修复了模型选择列表未按字母排序的问题，提升了 CLI 工具的用户体验。
- **重大功能构建进行中**：PR `#57590` (仍在开放中) 提议将桌面端的“技能与工具”页面重构为统一的“能力 (Capabilities)”页面，并将 MCP 作为一级公民集成。这代表了桌面端 UI 的重大演进方向。

## 社区热点

今日社区讨论最活跃的议题主要集中在以下方面：

1.  **主题与 UI 可读性**：Issue `#18080` [Feature]: Improved Themes for Dashboard - currently hard to read 以 **26条评论** 和 **45个👍** 成为今日最热议题。用户普遍反映当前的界面主题在字体选择和对比度上不符合标准，尤其是衬线字体在小字号下导致可读性极差。这表明社区对桌面端 UI 质量的提升有强烈诉求，与今日的 `#57590` Capabilities 页面 PR 形成了呼应。

2.  **QQ 机器人适配器 Bug**：Issue `#52914` [Bug]: fix(qqbot): QQBot adapter.connect() missing is_reconnect parameter... 获得了 **12条评论**。该 Bug 导致 QQBot 网关陷入无限重试循环，严重影响使用了中文聊天平台的用户群体。此后又出现了相似的 Issue `#53443`，表明该问题具有普遍性且用户关注度很高。维护者需尽快推动相关修复 PR 的合并。

## Bug 与稳定性

今日报告的 Bug 中，严重程度较高的问题如下：

| 严重程度 | Issue ID | 标题 | 描述 | 是否有修复 PR |
| :--- | :--- | :--- | :--- | :--- |
| P2 (高) | `#55658` | [Bug]It cannot be started after updating | 用户报告更新后桌面端应用无法启动，属于严重的阻断性问题。 | 暂无 |
| P2 (高) | `#52914` / `#53443` | [Bug]: fix(qqbot): QQAdapter.connect() missing is_reconnect parameter | QQBot 网关无限重试，无法连接，对中文用户影响较大。 | 无明确修复 PR |
| P3 (中) | `#55416` | Photon iMessage: persistent RST_STREAM code 2... | iMessage 通道的 gRPC 流持续被服务器以内部错误终止，服务处于不可用状态。 | 无 |
| P3 (中) | `#44456` | Desktop /compress returns "not a quick/plugin/skill command: compress" | 内置的 `/compress` 命令在桌面端失效，被错误地识别为非内置命令。PR `#57530` 已提供修复方案。 | `#57530` (Open) |
| P3 (中) | `#42082` | fix(auxiliary): pass explicit_base_url... in fallback chain | 回退链中的参数名不匹配，导致配置了自定义 `base_url` 的代理在回退时失效。 | 暂无 |
| P3 (中) | `#49858` | Photon iMessage: sidecar death causes silent reconnect death spiral | iMessage sidecar 进程崩溃后不会自动重启，导致通道永久死亡，需要手动干预。 | 暂无 |

## 功能请求与路线图信号

今日用户提出的功能请求呈现出对“可配置性”和“集成体验”的更高要求。

1.  **桌面端独立客户端**：Issue `#38602` 提议将 Hermes Desktop 部署为仅连接远程后端的“瘦客户端”。该需求获得 **37个👍**，表明用户对架构灵活性有强烈需求，希望分离计算与展示层。

2.  **可配置记忆后端**：Issue `#47349` 要求将固定的 `MEMORY.md` 文件变为可配置的“规则”，并允许禁用或替换记忆后端（如使用 Honcho 等外部服务）。这是对当前硬编码记忆系统的一次重要改进提议。

3.  **统一的路由选择器插件**：Issue `#41190` 提出了一个核心架构层面的需求：提供一个统一的、插件可访问的钩子，用于在每次 LLM 调用时覆盖“提供商/模型”选择。这旨在解决当前路由逻辑分散在各处（配置文件、启发式逻辑等）的问题。

这些信号与今日开放的 PR `#57590` (Capabilities 页面) 结合来看，项目正在向更模块化、更灵活、UI 更现代化的方向演进。

## 用户反馈摘要

- **痛点：QQBot 连接问题**：用户 `@fishlikeX` 和 `@crayontomas` 都遇到了 QQ 机器人适配器因参数缺失而无法启动的问题，只能回滚到旧版本。这是目前社区反馈最集中的技术问题。
- **痛点：桌面端模型选择不全**：用户 `@Chris-IdahoAIStrategies` 指出，Windows 版桌面端在连接远程 Linux 网关时，无法在模型选择器中看到 MoA/BeastMode 等预设，而 Telegram 端则可以正常选择。这暴露了桌面端与网关之间的功能同步问题。
- **使用场景：CLI vs 网关插件不一致**：用户 `@niklaserlewein` 反馈，在 CLI 中安装并可见的 TickTick 技能，在 Telegram 会话中却无法使用，提示“Skill not found”。这反映了不同平台间插件加载和作用域管理的割裂问题。
- **好评：修复安装问题**：用户 `@ericdong2012` 创建的 Issue `#7066` 反映了安装脚本在特定网络环境下卡住的问题，此类问题虽无今日更新，但属于社区普遍关注的基础体验问题。

## 待处理积压

- **长期未响应的核心 Bug `#4505`**：Issue `#4505` 关于优化 Ollama 集成的建议，创建于4月1日，更新于7月3日，但官方未置评。虽然已有相关 PR (`#55606`) 提出，但该 Issue 本身仍然开放，表明原生 Ollama API 的支持仍未被正式采用或解决。
- **持续存在的文档/代码不一致 `#5200`**：Issue `#5200` 指出关于上下文文件（AGENTS.md/SOUL.md）的文档与实际代码行为不符。该问题创建于4月5日，虽有关注但进展缓慢，可能持续误导新用户。
- **安装问题 `#7066`**：此 Issue 关于安装脚本卡住的问题，虽然可能涉及特定网络环境，但长时间未解决会影响新用户的第一印象和项目推广。

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*