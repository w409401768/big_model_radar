# OpenClaw 生态日报 2026-07-10

> Issues: 500 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-09 23:01 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，以下是根据您提供的 GitHub 数据生成的 OpenClaw 项目动态日报（2026-07-10）。

---

## OpenClaw 项目动态日报 | 2026-07-10

### 1️⃣ 今日速览

过去 24 小时内，OpenClaw 项目呈现**极高活跃度**，共记录了 500 条 Issue 更新和 500 条 PR 更新。尽管暂无新版本发布，项目维护者响应迅速，合并/关闭了 171 个 Issue 和 246 个 PR。社区讨论的焦点高度集中于 **Agent 会话状态持久化与消息传递的可靠性**，尤其是子代理任务静默丢失、工具输出渲染异常等问题。同时，项目在基础设施层面正经历重大变革，**SQLite 存储迁移**的推进预示着未来架构的稳定性将大幅提升。

---

### 2️⃣ 版本发布

**无**（过去 24 小时内无新版本发布）。

---

### 3️⃣ 项目进展

今日项目在关键基础设施、多平台兼容性及安全加固方面取得重要进展：

- **🧱 重大基础设施重构：** 核心 PR `#98236` ([link](https://github.com/openclaw/openclaw/pull/98236))（SQLite 存储迁移）持续推进。尽管目前状态仍为“请勿合并”，但它标志着项目正将 **SQLite 确立为会话数据和转录的标准运行时存储**，旨在彻底解决现有 JSON 文件方案的锁冲突与性能瓶颈。
- **📱 多平台 UI/UX 对齐：** 维护者 `@steipete` 今日表现活跃，合并了多项 UI 优化：
    - **WebChat 模型选择器**紧凑化设计 (`#103127`, [link](https://github.com/openclaw/openclaw/pull/103127))
    - **Android 语音电平阈值**与 iOS/macOS 对齐 (`#103130`, [link](https://github.com/openclaw/openclaw/pull/103130))
    - 修复 UI 会话列表在 Gateway 断连后丢失，或显示隐藏 Agent 会话的问题 (`#102485`, [link](https://github.com/openclaw/openclaw/pull/102485); `#103134`, [link](https://github.com/openclaw/openclaw/pull/103134))
- **🛡️ 安全修复：** 合并了针对截断响应中乱码字符的修复 (`#103136`, [link](https://github.com/openclaw/openclaw/pull/103136))，并提交了防止通过配置路径进行原型链污染的安全补丁 (`#102840`, [link](https://github.com/openclaw/openclaw/pull/102840))。
- **🔌 通道稳定性修复：** 修复了 Slack 频道 ID 大小写敏感导致的操作失败 (`#102822`)、Matrix 媒体类型大小写兼容性 (`#102917`) 以及 Discord 论坛线程归档时长继承 (`#103033`) 等问题。

---

### 4️⃣ 社区热点

今日社区讨论最激烈的议题全部围绕 **Agent 执行的可观测性与可靠性**：

- **🔥 最热 Issue：Subagent 完成静默丢失**
    `#44925` ([link](https://github.com/openclaw/openclaw/issues/44925)) 以 **21 条评论**位居榜首。用户 `@IIIyban` 详细描述了子代理在执行过程中因超时等原因静默失败，且**无重试、无通知**的痛点。这反映了用户对 Agent 任务闭环可控性的强烈诉求。
- **🔥 工具输出不可读问题：**
    `#99241` ([link](https://github.com/openclaw/openclaw/issues/99241))（15 条评论）报告了**工具输出被渲染为图片占位符**，导致 Agent 自身无法阅读文本结果的严重缺陷。这直接导致 Agent 在长时间工作流中丧失判断关键证据的能力，是自动化的重大障碍。
- **🔥 生态期望与现实差距：**
    `#50090` ([link](https://github.com/openclaw/openclaw/issues/50090))（15 条评论）作为长期 Issue 再度升温。社区对 **ClawHub 技能生态**的承诺抱有极高期望，但对当前技能分发、安全性审查和治理机制的成熟度表达了不满，认为“承诺与现实之间的鸿沟还很宽”。

---

### 5️⃣ Bug 与稳定性

今日报告的 Bug 呈现高度集中态势，P1 级别问题存量较大，主要攻击方向为 **会话状态机异常** 与 **消息丢失**：

| 严重等级 | 编号 | 摘要 | 当前状态 |
|---|---|---|---|
| ⚠️ P0/Diamond | `#43661` | 会话压缩超时导致消息重发循环 | **✅ 已关闭** |
| 🔴 P1/Diamond | `#44925` | Subagent 完成静默丢失 | 🟡 已有 Fix PR |
| 🔴 P1/Diamond | `#99241` | 工具输出渲染为图片不可读 | 🟡 待复现 |
| 🔴 P1/Diamond | `#48003` | Steer 模式无法中间注入消息 | 🟡 已有 Fix PR |
| 🔴 P1/Diamond | `#49876` | Cron 会话在工具失败时产生幻觉输出 | 🟡 需安全审查 |
| 🔴 P1/Diamond | `#52249` | ACP 父会话在等待子任务时卡死 | 🟡 需产品决策 |
| 🔴 P1/Diamond | `#84569` | WhatsApp 长模型调用导致会话卡死 | 🟡 已有 Fix PR |
| 🔴 P1/Platinum | `#45494` | Cron 在 API 持续故障时慢速超时而非快速失败 | 🟡 待复现 |
| 🟠 P2/Diamond | `#102175` | `room_event` 强制改变消息阶段，破坏 Prompt Cache | 🟡 **已有 Fix PR `#102189`** |
| 🟠 P2/Platinum | `#53408` | 长对话后工具参数静默丢失 | 🟡 待复现 |
| 🟠 P2/Platinum | `#54155` | Gateway 内存泄漏：389MB → 14.7GB (4天) | 🟡 待复现 |

**分析：** 大量 `impact:session-state` 和 `impact:message-loss` 标签的出现，指出当前版本可能存在系统性的会话管理回归问题。好消息是许多 P1 级 Bug 已有关联的 Fix PR 正在等待合并。

---

### 6️⃣ 功能请求与路线图信号

社区需求正在从“功能有无”向“生态成熟度”和“运维可观测性”跃迁：

- **🛠️ 技能生态进阶：**
    - `#50090` ([link](https://github.com/openclaw/openclaw/issues/50090))：要求完善 ClawHub 生态。
    - `#50199` ([link](https://github.com/openclaw/openclaw/issues/50199))：**技能优先级配置**。社区希望 Agent 在面对多个可处理相同任务的技能时，能有智能选择逻辑。
- **📊 运维可观测性：**
    - `#45565` ([link](https://github.com/openclaw/openclaw/issues/45565))：希望能将网关生命周期警告路由到专属频道，减少对话频道噪音。
    - `#50739` ([link](https://github.com/openclaw/openclaw/issues/50739))：请求系统事件具备**优先级/旁路队列模式**，确保在拥堵时告警能直接注入。
    - `#52640` ([link](https://github.com/openclaw/openclaw/issues/52640))：提出为长时间运行的任务建立**持久化任务状态面板**。
- **🧠 记忆与上下文策略优化：**
    - `#45608` ([link](https://github.com/openclaw/openclaw/issues/45608))：建议 `/new` 和每日重置时执行与压缩相同的智能内存刷新。
    - `#90354` ([link](https://github.com/openclaw/openclaw/issues/90354))：提议为预压缩内存刷新加入大小限流和后验证机制。
- **📝 开发者体验：**
    - `#45758` ([link](https://github.com/openclaw/openclaw/issues/45758))：呼声较高的 **YAML 配置格式**支持。

**路线图信号：** 结合 `#98236` (SQLite) 和 `#90259` ([link](https://github.com/openclaw/openclaw/pull/90259))（Reset 上下文延续），可以看出项目正在为下一阶段的 **强健持久化基础** 和 **跨轮次无缝上下文传递** 铺路。

---

### 7️⃣ 用户反馈摘要

从今日的 Issue 讨论中可以提炼出以下用户核心声音：

- **“信任危机”**：用户对 Agent 的不可预测行为感到担忧。无论是 Cron 会话在失败时编造错误输出（`#49876`），还是子代理静默丢失（`#44925`），都影响了用户将关键任务交给 Agent 的信心。**反馈机制的缺失**（无通知、无重试）是放大这种不信任感的直接原因。
- **“跨平台阵痛”**：用户在不同渠道上遇到了差异化的体验问题。WhatsApp 和 Telegram 等平台的消息丢失、卡死问题（`#84569`, `#51628`）反映了通道适配尚未完全成熟，多平台部署的用户体验有待提升。
- **“生态门槛”**：虽然有 ClawHub 这样的平台愿景，但社区用户在开发、发布和安装技能时仍然遇到障碍（`#53628`：环境变量未解释），表明当前技能生态的 **“开发者体验”仍是短板**。
- **社区质量高**：值得肯定的是，社区成员（如 `@IIIyban`, `@aaajiao`）在报告中提供了极其详尽的技术分析和复现步骤，展现了高质量的技术贡献能力。

---

### 8️⃣ 待处理积压

以下为长期未解决或风险较高的关键议题，提请维护者关注：

- **⚠️ 关键安全风险：**
    - `#45740` ([link](https://github.com/openclaw/openclaw/issues/45740))：**gh-issues 技能提示注入漏洞**。自 2026-03-14 开启，至今仍需安全审查。该漏洞可导致恶意 Issue 内容直接污染 Agent 提示，风险极高。
    - `#43996` ([link](https://github.com/openclaw/openclaw/issues/43996))：**Sandbox 容器 NoNewPrivileges 兼容问题**。自 2026-03-12 起影响部分用户部署，需要产品决策。
- **🧊 生态卡点：**
    - `#50090` ([link](https://github.com/openclaw/openclaw/issues/50090))：**ClawHub 社区生态完善**。这是社区呼声最高但进展最慢的议题，是项目实现生态级增长的关键瓶颈。
    - `#53628` ([link](https://github.com/openclaw/openclaw/issues/53628))：**技能安装时环境变量未解析**。自 2026-03-24 起一直待审查，影响技能安装的基础体验。
- **💣 性能炸弹：**
    - `#54155` ([link](https://github.com/openclaw/openclaw/issues/54155))：**Gateway 严重内存泄漏**（4 天内从 389MB 涨至 14.7GB）。虽然已有报告，但仍需精确的实时复现来定位根因。
- **🚧 架构转型风险：**
    - `#98236` ([link](https://github.com/openclaw/openclaw/pull/98236))：**SQLite 存储迁移 PR**。作为“请勿合并”的状态，其体量（XL）和涉及面（几乎所有模块）都表明这是一次高风险重构。一旦准备合并，需要周密的灰度发布和迁移指南。

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告（2026-07-10）

---

## 1. 生态全景

个人 AI 助手 / 自主智能体开源生态处于 **“规模爆发与质量阵痛并行”** 阶段。头部项目（OpenClaw、hermes‑agent）日均处理数百条 Issue/PR，表明采纳者在高速增长，但会话状态异常、工具调用丢失、渠道兼容等回归性 Bug 频繁出现，暴露了基础设施的追赶压力。与此同时，Zeroclaw 和 QwenPaw 分别从 **标准化流程（SOP）** 与 **系统化测试覆盖** 切入，标志着生态正从“原型验证”进入“可运营工程”期。社区对持久化记忆、运维可观测性、安全沙箱的集中诉求，预示下一阶段的核心竞争将围绕 **可靠性、标准接口与细粒度可控** 展开。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 无 | 极高活跃；合并效率高（关闭 171 Issues / 246 PRs），但会话状态类 Bug 堆积 |
| **Zeroclaw** | 30 | 50 | 无（v0.8.3 冲刺） | 极其活跃但审查瓶颈显著（46 条 PR 待合并） |
| **PicoClaw** | 3 | 16（活跃） | 无 | 中等活跃；2 个 Critical Bug 无修复 PR，12 条 PR 积压超 2 周 |
| **QwenPaw** | 35 | 50 | **v2.0.0‑beta.5** | 极高活跃；64% PR 合并率，正从功能扩张转入质量巩固 |
| **hermes‑agent** | 224 | 500 | 无 | 极高迭代活性；Provider/网络兼容性问题大量，社区反馈深刻 |

**说明**：更新数指 24 h 内被创建或更新的 Issue/PR 条数，非存量。

---

## 3. OpenClaw 在生态中的定位

- **核心定位**：以 **会话状态持久化与消息传递可靠性** 为优先的通用 Agent 框架，通过 SQLite 迁移（PR #98236）彻底解决 JSON 文件方案的锁冲突与性能瓶颈。
- **技术路线差异**：相比 Zeroclaw 强调 **SOP 可审计工作流与运行时策略**，OpenClaw 更侧重底层状态机稳定性；相比 QwenPaw（中文渠道、沙箱、v2.0 大版本），OpenClaw 的国际化和平台覆盖更广；相比轻量级 PicoClaw，在功能广度、社区规模和响应效率上明显领先。
- **社区规模**：与 hermes‑agent 同属每日更新 500+ PR 的第一梯队，但 Issue 关闭率（34%）与 PR 合并率（49%）均优于 hermes‑agent，且社区成员提供的高质量复现报告（如 @IIIyban 对子代理丢失的详尽分析）体现了用户群的深厚技术功底。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体需求 / 现象 |
|---|---|---|
| **会话持久化 & 上下文管理** | OpenClaw, Zeroclaw, QwenPaw, hermes‑agent | SQLite 存储迁移、持久化记忆 Tracker、滚动上下文压缩、工具级输出压缩（headroom‑ai）、上下文压缩丢失 Tool Call |
| **渠道标准化与兼容** | 所有项目 | Slack/Matrix 大小写修复、OpenAI 兼容 API 端点、QQ 流式输出、钉钉/飞书静默失败、Weixin/Telegram 适配增强 |
| **运维可观测性** | OpenClaw, Zeroclaw, QwenPaw, hermes‑agent | Gateway 告警路由、实时轮次计数器、Dashboard 崩溃（500）、持久化任务状态面板、事件流未触发 |
| **沙箱与安全** | OpenClaw, QwenPaw, PicoClaw, hermes‑agent | 原型链污染修复、沙箱可关闭需求、write_file 误导覆盖、后台审查误分类、提示注入漏洞（gh‑issues） |
| **Agent 执行可靠性** | OpenClaw, Zeroclaw, PicoClaw, QwenPaw, hermes‑agent | 子代理静默丢失、工具输出渲染为图片、Cron 会话幻觉、批处理参数跳过、防重复误判 |

多个方向已进入 **“有设计方案 / 已有 Fix PR”** 阶段，表明生态正在系统性地解决共性短板。

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Zeroclaw | PicoClaw | QwenPaw | hermes‑agent |
|---|---|---|---|---|---|
| **功能侧重** | 状态持久化、消息可靠性 | 标准化 SOP、运行时策略、ZeroCode | 轻量多通道（QQ/LINE/Matrix/ARM）、工具安全 | 中文生态（钉钉/飞书/沙箱）、v2.0 统一 | 平台/Provider 广度、CLI/Desktop 体验 |
| **目标用户** | 中高级开发者，需稳定持久化 | 商业/审计场景，追求确定性 | 极简个人、边缘计算、IoT 用户 | 中国开发者、企业用户 | 多元个人用户，崇尚自由度与多平台 |
| **技术栈** | Node.js → SQLite | Rust（内存安全） | Go（AWS SDK 等） | Python | Python + 多适配器 |
| **关键竞争点** | 基础设施重构（SQLite） | 标准化流程+可观测仪表盘 | 硬件覆盖（ARM、9Router） | 本地沙箱与中文渠道深度 | 巨大 Provider 兼容矩阵 |
| **当前阶段** | 架构转型期（SQLite 迁移） | v0.8.3 功能注入期 | 维护积压期 | v2.0 Beta 质量加固期 | 广度扩张与并行修复期 |

---

## 6. 社区热度与成熟度分层

### 🔥 快速迭代层（每日 500+ Issue/PR 更新）
- **OpenClaw**、**hermes‑agent**：社区体量最大，反馈最活跃，但系统性回归 bug 较多，需加强回归测试与合并纪律。
- **Zeroclaw**：更新量相对小（30/50），但待合并 PR 占比极高（92%），表明代码贡献热情高但审查成为瓶颈。

### ⚙️ 质量巩固层（合并率 > 60%，测试覆盖增加）
- **QwenPaw**：虽仍处 v2.0 Beta 阶段，但每日合并率达 64%，且主动合并大量测试 PR（200+ 用例），正从“加功能”转向“修 Bug + 测稳定”，是成熟度提升的积极信号。

### 🐢 中等活跃层
- **PicoClaw**：更新量少，2 个 Critical 级 Bug 未有修复 PR，12 条 PR（包括 Bedrock 缓存等高价值功能）积压超 2 周，社区贡献热度可能因等待而冷却。

---

## 7. 值得关注的趋势信号

1. **标准化 API 成为生态入口刚需**  
   Zeroclaw 的 OpenAI 兼容端点（#8550）、hermes‑agent 对 OpenRouter/非 OpenAI 端点的适配压力，都表明用户期望用统一协议接入主流前端（Open WebUI、LobeChat）。Agent 框架应优先对齐 OpenAI API 或推出标准化网关层。

2. **持久化与上下文管理是“能力天花板”**  
   几乎所有项目都在解决“长会话丢失”“工具输出不可读”“压缩破坏结构”等上下文问题。下一代 Agent 竞争的核心将从“能调用几个工具”转向 **“能在 1000+ 轮对话中稳定不丢失状态”**。

3. **渠道碎片化呼唤统一抽象**  
   每个项目都在各自修复 Slack/Matrix/QQ/飞书/微信/Telegram… 未来可能出现跨项目的 **连接器规范**（如 Channel SDK），降低重复劳动。

4. **用户从尝鲜转为“理性部署”——可观察、可控制、可审计**  
   沙箱开关（QwenPaw #5879）、弹窗自定义（#5797）、技能优先级（OpenClaw #50199）、Gateway 告警路由（#45565）大量涌现。用户开始要求 **“给我的 Agent 装个仪表盘”**。

5. **安全信任危机浮现**  
   提示注入（OpenClaw #45740）、工具恶意覆盖（PicoClaw #3226）、原型链污染（#102840）等隐患被持续揭露。Agent 框架需将安全作为 **一等设计约束**，否则难以承载企业关键任务。

### 对 AI 智能体开发者的启示
- 选择框架时优先评估其 **状态持久化方案** 和 **渠道抽象层成熟度**，而非功能数量。
- 关注已启动 **质量巩固（测试覆盖、合并纪律）** 的项目，如 QwenPaw 的转型信号。
- 尽早为应用注入 **可观测性埋点**（事件流、任务面板），这是建立用户信任的底线。
- **标准化接口（OpenAI 兼容）** 可以避免被单一框架锁定，降低集成成本。

---

*报告基于 2026-07-10 各项目 GitHub 社区动态，由 AI 分析师生成。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我根据 Zeroclaw (github.com/zeroclaw-labs/zeroclaw) 提供的数据，为您生成 **2026年7月10日** 的项目动态日报。

---

# Zeroclaw 项目动态日报 | 2026-07-10

## 1. 今日速览

过去24小时内，Zeroclaw 保持了**极其活跃**的开发态势。**30条 Issues** 与 **50条 PRs** 被处理或更新，其中 **46条 PRs** 处于待合并状态，显示出项目正经历一次大规模的功能注入浪潮。项目整体处于 **v0.8.3 里程碑冲刺期**，社区焦点集中在运行时策略、可观测性、标准 API (OpenAI 兼容) 以及全新的 SOP (标准操作流程) 范式上。尽管合并吞吐量暂时受限，但来自社区的代码贡献量与讨论深度均表明项目生态 **健康且高速成长中**。

- **活跃度评估：★★★★☆ (极高)**
- **核心瓶颈：** 46条待合并 PR 表明审查资源可能存在短期瓶颈，但也预示着下一次发布将包含巨量更新。

## 2. 版本发布

**无。**
过去24小时内没有发布新的 Release。从多个 Trackers ( #8070, #8363, #8073 ) 来看，开发焦点全部锁定在 **v0.8.3** 版本的交付上，该版本将重点解决 Gateway / Web UI、配置驱动运行时策略、可观测性 CI 以及 Docker 支持等问题。

## 3. 项目进展

尽管新版本未发布，项目在问题修复和尾部功能打磨上取得了扎实进展：

- **ZeroCode 体验提升**: 贡献者 @wangmiao0668000666 提交的 PR [#8911](https://github.com/zeroclaw-labs/zeroclaw/pull/8911) 已合并，实现了 **ZeroCode 进入代码面板时自动恢复最近会话** 的功能，免去了用户手动选择的繁琐步骤。
- **致命 Bug 清理**: 过去24小时内，**2个高严重性 Bug 被关闭**：
    - **S1 (工作流阻塞):** Issue [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) (多轮对话丢失用户消息) 已关闭。
    - **S0 (数据丢失/安全风险):** Issue [#8094](https://github.com/zeroclaw-labs/zeroclaw/issues/8094) (Anthropic Provider 添加后必须重启才能生效) 已关闭。
- **社区治理推进**: 关于工作流与标签治理的 RFC [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) 持续获得核心开发者的关注，标志着项目在治理规范上的演进。

## 4. 社区热点

过去24小时内，社区讨论聚焦于 **标准 API 兼容性** 与 **本地/企业级部署** 两大核心诉求。

- **最迫切的需求（开放性API）**: Issue [#8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)（增加 OpenAI 兼容端点）虽然评论数不多，但代表了社区最强烈的呼声。用户明确表示现有协议 (WebSocket/Channel) 无法接入 Open WebUI、LobeChat 等主流生态工具，这构成了核心集成壁垒。
- **竞争环境反馈（与Claude Code对标）**: Issue [#8401](https://github.com/zeroclaw-labs/zeroclaw/issues/8401)（TodoWrite 任务跟踪面板）的关闭并不意味着结束。社区在评论中坦言，**因为缺少类似 Claude Code 的任务看板，部分用户已流失**。这为 ZeroCode 的 UI 演进提供了直接的竞争压力信号。
- **前沿范式讨论（SOP）**: PR [#8590](https://github.com/zeroclaw-labs/zeroclaw/pull/8590)（SOP视觉编排）主动要求 Beta 测试者，该 PR 提出了“确定性可审计工作流”的概念，引发了关于 Agent 在严肃商业场景中如何交付的深度讨论，是近期社区内最具幻想影响力的大功能。
- **老牌需求持续发酵**: Issue [#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)（本地优先模式）以 **2个 👍** 保持了用户关注度，社区持续要求减少提示词膨胀并防止系统提示泄露。

## 5. Bug 与稳定性

今天新增/活跃的 Bug 主要集中在 **可观测性** 与 **Provider兼容性** 上。

**按严重程度排序：**

- **S2 (行为降级):**
    - **高优 (Observability):** **新开 Bug** [#8915](https://github.com/zeroclaw-labs/zeroclaw/issues/8915) - `agent_start/agent_end` 事件在通过频道 (Telegram/Discord) 发起的轮次中 **从未触发**。这使得所有依赖事件流的用户功能（如日志追踪、Dashboard）在该路径下完全失效。**目前尚无修复 PR。**
    - **Provider 超时**: Issue [#8762](https://github.com/zeroclaw-labs/zeroclaw/issues/8762) - Anthropic Provider 存在固定的 120 秒总超时，导致长文档合成任务必然失败。
    - **文档错误**: Issue [#8810](https://github.com/zeroclaw-labs/zeroclaw/issues/8810) - Telegram 文档存在严重错误，已被用户明确指正。好在 Fix PR [#8825](https://github.com/zeroclaw-labs/zeroclaw/pull/8825) 已提交等待合并。
- **S3 (次要问题):**
    - **进程管理**: Issue [#8578](https://github.com/zeroclaw-labs/zeroclaw/issues/8578) - ZeroCode 启动失败后不会终止进程，导致必须手动杀掉残留进程。
    - **UI交互**: Issue [#8648](https://github.com/zeroclaw-labs/zeroclaw/issues/8648) - 配置编辑器中存在 `被误编辑。`

**稳定性修复前瞻：**
查看待合并的 PR 池，有两项重要的运行时稳定性修复正在排队中：
- PR [#8838](https://github.com/zeroclaw-labs/zeroclaw/pull/8838) - 修复 **SSE 流式读取的空闲超时**，防止调用本地模型 (如 llama.cpp) 时因服务器返回 Header 后挂起导致客户端卡死。
- PR [#8866](https://github.com/zeroclaw-labs/zeroclaw/pull/8866) - 修复 **Daemon 心跳循环中的 MCP 注册表共享问题**，防止 stdio 模式的 MCP 服务器在静默重启中无限创建，耗尽系统资源。

## 6. 功能请求与路线图信号

综合最近24小时的数据，可以看出 **v0.8.3 的蓝图已经相当清晰**。

- **几乎确认纳入 v0.8.3 的功能：**
    - **网关规范**: 基于 Tracker [#8070](https://github.com/zeroclaw-labs/zeroclaw/issues/8070)，Gateway Web Chat 的多会话支持 ( #7543 )、ZeroCode 的插件目录面板 ( #8907 ) 以及会话归档 ( #8894 ) 均处于活跃开发/接受状态。
    - **配置策略强化**: Tracker [#8363](https://github.com/zeroclaw-labs/zeroclaw/issues/8363) 将推进 MCP 工具的精细权限策略和对 `deferred_loading` 的支持。
    - **可观测性仪表盘**: 新 Feature [#8860](https://github.com/zeroclaw-labs/zeroclaw/issues/8860)（Dashboard 实时 Agent 轮次计数器）已开始跟踪，提升运维可视化能力。

- **尚未被纳入具体版本但呼声极高的信号：**
    - **OpenAI 兼容 API** ( #8550 ) —— 这是**打通生态的关键一战**，建议在 v0.8.3 或 v0.9.0 中降级为实现目标。
    - **持久化记忆** (Tracker [#8891](https://github.com/zeroclaw-labs/zeroclaw/issues/8891) ) —— 作为追赶前沿 Agent 框架的最重要基石，该 Tracker 已开始审计现有代码并设计跨会话记忆子系统。

## 7. 用户反馈摘要

从今天活跃的评论和 Issue 中，我们可以提炼出以下几点核心用户声音：

- **“既然用了 Rust，文档不该是 slop”**: 用户 @cr3a7ure 在 Bug [#8810](https://github.com/zeroclaw-labs/zeroclaw/issues/8810) 中直言不讳，虽然赞赏 Rust 的内存安全和类型系统，但对 Telegram 文档的错误表示不满，认为“如果实现不当，slop 终究是 slop”。**这提醒项目组文档质量的权重必须与代码质量齐平。**
- **“我因为没这个功能投向了 Claude Code”**: Issue [#8401](https://github.com/zeroclaw-labs/zeroclaw/issues/8401) 的关闭并未平息用户的情绪，评论区暴露了竞争痛点。**ZeroCode 在交互细节上的打磨，直接关系到用户留存率。**
- **“本地模型用不起你们的配置”**: Issue [#5287](https://github.com/zeroclaw-labs/zeroclaw/issues/5287) 的持续活跃代表了数量庞大的 **本地优先** 用户群体。他们需要的是一个瘦身版、去耦合、无泄漏的轻量配置模式，而不是为云端模型设计的臃肿配置。
- **“标准 API 是刚需”**: 社区对于 OpenAI 兼容端点的渴求非常直白，“没有它我们就没法集成 Open WebUI”。**这暴露了当前协议栈在企业通用性上的短板。**

## 8. 待处理积压

目前项目最大的积压并非单个 Issue，而是庞大的 **46 条待合并 PR 队列**。此外，以下长期项需特别注意：

- **长期未响应 / 阻塞的 Issue：**
    - **#5287 本地优先模式 (4月4日创建, 已接受)**：尽管获得 `status:accepted`，但至今无对应实现 PR。这是小模型与隐私敏感用户的坚决期待，若持续搁置将打击该用户群体的参与度。
    - **#8871 处理第三方 API 429 限流 (阻塞中)**：这是一个审查意见引发的技术债务，因依赖 `needs-author-action` 而被阻塞。建议核心维护者介入主动解决。

- **等待合并的“老兵” PRs：**
    - **[#7215](https://github.com/zeroclaw-labs/zeroclaw/pull/7215) Quickstart 端口字段 (6月4日创建)**：已濒临停滞，但影响的是 **新用户首次体验流程**（Funeral path for webhooks），理应获得更高的审查优先级。
    - **[#7836](https://github.com/zeroclaw-labs/zeroclaw/pull/7836) 渠道编排器配置错误 (6月17日创建)**：修复了所有渠道中 MCP 工具解析退化为默认 `false` 的 Bug，严重影响了渠道中工具使用的准确性。近一个月未合并，是典型的“重要但不紧急”而被拖垮的案例。

**分析师建议：** 项目维护者可以考虑在未来 2-3 天内组织一次 **“合并冲刺（Merge Fest）”**，优先解决 `bug`、`priority:p1` 以及影响新用户上手的积压 PR，以释放开发团队的创新产能并恢复社区的响应信心。

---
*报告结束*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 开源项目动态日报 | 2026-07-10

---

## 1. 今日速览

项目在过去 24 小时内保持中等活跃度：共 16 个 PR 处于活跃状态，其中 4 个已合并/关闭，3 个 Issue 获得更新。Dependabot 发起的日常依赖更新占 PR 总数的一半，同时两项重要的稳定性修复（工具引导覆盖、LINE 频道 panic）已合并进主线。没有新版本发布。目前 **12 个待合并 PR** 和 **3 个开放 Issue** 中，存在两项严重（Critical）级别的 Bug 尚无修复 PR 关联，功能类 PR 的合并周期也偏长，建议维护者加速积压清扫。

- 活跃 PR：16 | 已合并/关闭：4 | 待合并：12
- 活跃 Issue：3 | 新开：3 | 已关闭：0
- 新版本发布：0

---

## 2. 版本发布

**无。**（项目最近一次发布为 v0.2.9，当前暂无新版本。）

---

## 3. 项目进展（今日合并/关闭的重要 PR）

### ✅ 已合并/关闭（4 项）

| PR | 标题 | 类型 | 影响 |
|---|---|---|---|
| [#3226](https://github.com/sipeed/picoclaw/pull/3226) | fix(tools): stop write_file from coaching destructive overwrite | Bug / UX | **已合并。** 修复 Agent 通过 `write_file` 更新 `MEMORY.md` 时，错误地将已有文件描述为"替换"、引导模型做破坏性覆盖的问题。提升 Agent 自主操作的安全性，是一项关键的工具行为修正。 |
| [#3171](https://github.com/sipeed/picoclaw/pull/3171) | fix(line): add ok checks for sync.Map type assertions in Send | 稳定性 | **已合并。** 为 LINE 频道发送方法中的 `sync.Map` 类型断言添加 `ok` 检查，防止因意外数据类型导致 panic。 |
| [#3213](https://github.com/sipeed/picoclaw/pull/3213) | build(deps): bump aws-sdk-go-v2/config to 1.32.27 | 依赖 | **已合并。** 日常依赖更新。 |
| [#3207](https://github.com/sipeed/picoclaw/pull/3207) | build(deps): bump copilot-sdk/go to 1.0.5 | 依赖 | **已合并。** 日常依赖更新。 |

**项目提升：** 工具安全边界得到加强，LINE 渠道稳定性提升，依赖基线保持健康。

---

## 4. 社区热点

### 🔥 讨论最活跃 / 关注度高的 Items

1.  **[Issue #3201] [Feature] Support streaming output for QQ channel**
    - **链接：** [#3201](https://github.com/sipeed/picoclaw/issues/3201)
    - **热力：** 评论 2 | 发布时间较短
    - **分析：** 作者 @YsLtr 指出 Telegram 和 Pico WebSocket 已经实现了 `StreamingCapable` 接口，而 QQ 渠道是目前主要的缺失版本。**诉求本质是渠道功能一致性。** 随着 QQ 在 AI Bot 场景的流行，这个需求可能会快速升温。

2.  **[Issue #3206] v2→v3 config migration fails with false 'unknown field(s)'**
    - **链接：** [#3206](https://github.com/sipeed/picoclaw/issues/3206)
    - **热力：** 严重程度高，用户情绪中明显受阻（"fresh install" 也无法运行）
    - **分析：** 配置迁移失败是“硬拦截”，直接导致应用无法启动。属于用户上手体验的致命伤，是当前社区最迫切的需求——**不是“我想要什么功能”，而是“我根本用不了”**。

3.  **[Issue #3203] Matrix sync loop has no reconnection logic — silent death**
    - **链接：** [#3203](https://github.com/sipeed/picoclaw/issues/3203)
    - **热力：** 隐蔽性强、影响范围大（Matrix 是重要 Channel）
    - **分析：** @weissfl 报告的网络中断后无法重连问题是典型的“软死”场景。主进程保持存活导致 systemd 的 `Restart=on-failure` 完全失效，本质上构成了一个**资源耗尽&监控盲区**的 bug。

---

## 5. Bug 与稳定性

### 🔴 严重（Critical）

| Issue | 描述 | 状态 | 修复 PR |
|---|---|---|---|
| [#3206](https://github.com/sipeed/picoclaw/issues/3206) | **v2→v3 配置迁移失败**：`config.json` 包含未知字段 `build_info`, `session.dm_scope`，导致即使是全新安装也无法运行 `picoclaw status`。 | OPEN / [stale] | ❌ 暂无 |
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | **Matrix 同步循环无重连逻辑**：网络中断或服务重启后同步永久死亡，进程保持存活，逃避 systemd 重启策略。 | OPEN / [stale] | ❌ 暂无 |

### 🟡 中等（Medium）

| Issue/PR | 描述 | 状态 |
|---|---|---|
| [#3180](https://github.com/sipeed/picoclaw/pull/3180) | CLI 工具调用参数不合法时，整个批次被丢弃而非跳过错误项。 | OPEN / [stale] |
| [#3115](https://github.com/sipeed/picoclaw/pull/3115) | 对文本工具输出中的 `data:image/...;base64,...` 字符串误判为真实媒体附件，导致会话历史损坏。 | OPEN / [stale] |
| [#3202](https://github.com/sipeed/picoclaw/pull/3202) | ID 规范化函数未能正确处理首尾下划线，输出可能不匹配 `^[a-z0-9]` 前缀要求。 | OPEN |

### 🟢 低（Low / Dependencies）

| PR | 描述 | 状态 |
|---|---|---|
| [#3204](https://github.com/sipeed/picoclaw/pull/3204) | 降级 Azure SDK 至冻结基线以通过供应链检查。 | OPEN / [stale] |
| [#3171](https://github.com/sipeed/picoclaw/pull/3171) | LINE 频道 `sync.Map` 类型断言 panic（昨日已合并修复）。 | ✅ 已合并 |

---

## 6. 功能请求与路线图信号

### 📡 可能纳入下一版本的功能

| Item | 功能 | 信号强度 |
|---|---|---|
| [#3163](https://github.com/sipeed/picoclaw/pull/3163) | **AWS Bedrock Converse API 提示缓存**：通过 Cache Points 大幅降低大模型调用成本（写入点 0.1×、命中点 0.01× 输入读数），对生产部署具有极高商业价值。 | ⭐⭐⭐⭐⭐ **高价值** |
| [#3118](https://github.com/sipeed/picoclaw/pull/3118) | **远程 Pico WebSocket Agent 模式**：允许通过 `--remote ws://...` 连接到外部 Pico 中继，打通 Agent 远程调用通道。 | ⭐⭐⭐⭐ |
| [#3201](https://github.com/sipeed/picoclaw/issues/3201) | **QQ 频道流式输出**：用户显性需求，Telegram/WS 已有实现，属于横向补齐功能。 | ⭐⭐⭐⭐ |
| [#3205](https://github.com/sipeed/picoclaw/pull/3205) | **9Router 网关兼容 + Linux ARMv7 构建**：来自边缘计算场景（树莓派）的真实需求，扩展硬件覆盖范围。 | ⭐⭐⭐ |
| [#3222](https://github.com/sipeed/picoclaw/pull/3222) | **DeltaChat 重构**：砍掉 -320 行代码，废弃密码认证和硬编码中继列表，全面拥抱 JSON-RPC 架构。技术债清理的重要一步。 | ⭐⭐⭐ |

### 📊 路线图信号解读
- **成本优化方向**：Bedrock 缓存是一个强烈的信号，表明项目的企业/高级用户正在关注大规模部署的成本控制。
- **通道生态完善**：QQ 流式、9Router 支持、DeltaChat 重构共同指向项目正在丰富 Channel 接入层，保持与 Telegram、Matrix 等渠道的竞争力。
- **交互范式扩展**：远程 WebSocket Agent 模式（#3118）可能开启“PicoClaw as a Service”的新的部署模式。

---

## 7. 用户反馈摘要

| 用户 | 来源 | 原始痛点/诉求 |
|---|---|---|
| @OhYash | [#3206](https://github.com/sipeed/picoclaw/issues/3206) | “全新安装 v0.2.9 运行 `picoclaw status` 直接报未知字段错误、配置迁移失败——项目根本不能用。” |
| @weissfl | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | “Matrix 同步循环在断网后永久死亡，进程不退出。systemd `Restart=on-failure` 完全无效，必须自己写看门狗脚本来保活。非常痛苦。” |
| @sarwonous | [#3205](https://github.com/sipeed/picoclaw/pull/3205) | “在树莓派 3B+ 上运行遇到两个问题：没有 ARM 构建产物，以及 9Router 的响应格式无法解析。希望贡献的代码能帮助到同样想在 ARM 设备上运行的人。” |
| @Alix-007 | [#3180](https://github.com/sipeed/picoclaw/pull/3180) | “当工具调用返回的 JSON 参数非法时，CLI 直接丢弃了整个批次的工具调用，而不是跳过坏的保留好的。我的 Agent 持续对话因此断裂。” |
| @ACMYuechen | [#3226](https://github.com/sipeed/picoclaw/pull/3226) | “`write_file` 把文件存在的场景描述成‘替换’，引导模型产生破坏性覆盖。用户数据的保护措施不足，建议改为‘合并’偏好。” |

**共享情绪关键词：**
- **配置迁移失败** → 上手受阻，挫败感极强。
- **Matrix 静默死亡** → 隐蔽性 Bug，用户需自建 Workaround 监控，信任受损。
- **ARM 构建缺失** → 硬件多元化需求未被满足。
- **Agent 工具行为** → 用户对 Agent 自主写文件的“安全边界”高度敏感。

---

## 8. 待处理积压（需要关注）

以下 Issue / PR 长期未获得有效响应或合并，按紧急度排列：

### 🔴 严重 Bug — 需维护者介入决策

| Item | 创建日期 | 问题 | 现状 |
|---|---|---|---|
| [#3206](https://github.com/sipeed/picoclaw/issues/3206) | 2026-07-02 | **v2→v3 配置迁移失败** | ❌ 无 PR。需确认是 schema 问题还是迁移逻辑漏报。 |
| [#3203](https://github.com/sipeed/picoclaw/issues/3203) | 2026-07-02 | **Matrix 同步无重连** | ❌ 无 PR。建议标记为 P0。 |

### 🔶 待合并 PR — 长时间积压，可能挫伤贡献者积极性

| PR | 创建日期 | 上次更新 | 描述 |
|---|---|---|---|
| [#3118](https://github.com/sipeed/picoclaw/pull/3118) | 2026-06-12 | 2026-07-09 | feat: Add remote Pico WebSocket mode |
| [#3115](https://github.com/sipeed/picoclaw/pull/3115) | 2026-06-12 | 2026-07-09 | fix: Inline data URL media extraction |
| [#3163](https://github.com/sipeed/picoclaw/pull/3163) | 2026-06-23 | 2026-07-09 | feat: Bedrock prompt caching |
| [#3180](https://github.com/sipeed/picoclaw/pull/3180) | 2026-06-26 | 2026-07-09 | fix: CLI tool call arguments |
| [#3204](https://github.com/sipeed/picoclaw/pull/3204) | 2026-07-02 | 2026-07-09 | fix: Azure dependency freeze |
| [#3205](https://github.com/sipeed/picoclaw/pull/3205) | 2026-07-02 | 2026-07-09 | fix: 9router gateway + ARMv7 |
| [#3222](https://github.com/sipeed/picoclaw/pull/3222) | 2026-07-03 | 2026-07-09 | refactor: deltachat cleanup（-320LOC） |

### 💡 观察建议
当前 **12 个待合并 PR** 已跨越 4 个星期（最早可追溯到 6 月 12 日）。虽然 Dependabot 的日常维护运转良好，但高价值的功能 PR（Bedrock 缓存、Remote Agent）和社区原生贡献（9Router 支持、ARMv7 构建）长时间处于停滞状态。建议维护团队在下一版（v0.3.0？）发布前安排一次集中的 Rollup Merge，或至少给予贡献者明确的合并预期和时间表，以避免外部贡献热情冷却。

---

*数据快照时间：2026-07-09 | 报告生成时间：2026-07-10*
*数据来源：github.com/sipeed/picoclaw*

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 **QwenPaw 项目动态日报 (2026-07-10)**。

---

## QwenPaw 项目动态日报 | 2026-07-10

### 1. 今日速览

过去 24 小时内，QwenPaw 项目维持 **极高活跃度**。数据层面共产生 **35 条 Issue 更新**和 **50 条 PR 更新**，其中合并/关闭的 PR 占比高达 **64%**，展现出开发团队强大的交付和回复能力。**v2.0.0-beta.5** 版本正式发布，主要针对 Beta 阶段的滚动上下文（Scroll）机制进行了修复。整体来看，项目正处在 **v2.0 大版本冲刺期与稳定化的并行阶段**，社区反馈（尤其是中文用户对沙箱和渠道功能的诉求）非常强烈，研发侧则在全力推进 Bug 修复与大规模测试覆盖。

---

### 2. 版本发布

- **版本号：** v2.0.0-beta.5
- **变更内容：**
  - `fix(scroll)`: 在 Eviction Index 中为未加标题的被驱逐 Spans 添加标签。
  - `fix(scroll)`: 在 Eviction Index 中使用 Seam Banner 来锚定当前活跃对话轮次。
- **作者：** @niceIrene
- **评估：** 这是一个小步快跑的优化版本，专注于提升 v2.0 上下文管理（滚动）的视觉反馈和数据结构正确性。目前 **未见影响兼容性的破坏性变更**。使用 Beta 版本的用户可直接执行 `pip install --upgrade qwenpaw` 升级。
- **链接：** [v2.0.0-beta.5 Release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0-beta.5)

---

### 3. 项目进展（关键合并/关闭的 PR）

过去 24 小时项目焦点清晰，即 **“扫清核心 Bug、加固测试防线”**。

- **核心逻辑与安全修复：**
  - **[已合并]** #5866：修复了 `rm -rf ${HOME}` 的安全绕过漏洞，对安全模块进行了重要加固。详见：[PR #5866](https://github.com/agentscope-ai/QwenPaw/pull/5866)
  - **[已合并]** #5870：将 `preserve_thinking` 默认值设为 False，解决了部分推理模型（DeepSeek 等）陷入“思维链循环”导致卡死的问题。详见：[PR #5870](https://github.com/agentscope-ai/QwenPaw/pull/5870)
  - **[已合并]** #5841：修复了工具调用（Tool Call）参数中因包含空格 JSON 无法被解析的兼容性问题。详见：[PR #5841](https://github.com/agentscope-ai/QwenPaw/pull/5841)
  - **[已合并]** #5654：修复了钉钉（DingTalk）通道消息发送静默失败的问题。详见：[PR #5654](https://github.com/agentscope-ai/QwenPaw/pull/5654)
  - **[已合并]** #5864：修复了 MCP Driver 审批级别与运行时不一致的问题。详见：[PR #5864](https://github.com/agentscope-ai/QwenPaw/pull/5864)

- **大规模测试建设：**
  - **[已合并]** #5895：完成了 Sprint 4.1 针对 v2.0 Tool-calls API 的集成测试。详见：[PR #5895](https://github.com/agentscope-ai/QwenPaw/pull/5895)
  - **[已合并]** #5810：针对 #5479（大会话崩溃）增加了回归测试。详见：[PR #5810](https://github.com/agentscope-ai/QwenPaw/pull/5810)
  - **[已合并]** #5808 / #5812：对前端 Stores 和 Channels 模块新增了单元测试（200+ 用例）。详见：[PR #5808](https://github.com/agentscope-ai/QwenPaw/pull/5808)

**结论：** 项目已从“功能大跃进”转向 **“质量审计月”**。今日修复的安全和逻辑漏洞等级都很高，大量 Test PR 的合并表明项目正在为 v2.0 稳定版的发布铺平道路。

---

### 4. 社区热点

- **#5879 [Feature] 增加可关闭沙箱的功能**
  - 评论：6
  - **核心诉求：** 用户强烈要求在可信设备上允许关闭沙箱，否则严重限制 Agent 执行 Python 包安装等高级功能。
  - **分析：** 这是目前 **社区呼声最高的功能类 Issue**。用户认为当前沙箱策略过于“一刀切”，希望将安全决策权交还给个人。
  - **链接：** [Issue #5879](https://github.com/agentscope-ai/QwenPaw/issues/5879)

- **#5757 [Bug] 飞书信息不回复情况**
  - 评论：13
  - **核心诉求：** 机器人只能回复第一条消息，后续对话无回应。
  - **分析：** 影响面最大的 Bug 之一。飞书是中国用户最常用的办公协作工具，目前该 Issue 仍为 `OPEN` 状态，需要维护者重点关注。
  - **链接：** [Issue #5757](https://github.com/agentscope-ai/QwenPaw/issues/5757)

- **#5797 [Feature] 定时任务结果弹窗提醒应加开关**
  - 评论：6
  - **核心诉求：** 不要替用户做决定去除弹窗，而是在创建任务时允许用户自定义是否弹窗及停留时间。
  - **分析：** 体现了用户对 **细粒度控制** 的成熟诉求。用户原话为“千问不要因噎废食，有人反对，就都关掉了”。
  - **链接：** [Issue #5797](https://github.com/agentscope-ai/QwenPaw/issues/5797)

- **#5379 [Bug] 通过 Python 命令安装后启动直接报错 Internal Server Error**
  - 评论：10（已关闭）
  - **分析：** 虽然已关闭，但反映出**首次安装体验**是目前影响新用户留存的一大痛点。
  - **链接：** [Issue #5379](https://github.com/agentscope-ai/QwenPaw/issues/5379)

---

### 5. Bug 与稳定性

过去 24 小时内 Bug 报告类型繁多，主要集中在 **上下文管理、沙箱兼容性、渠道连接** 三大块。

| 严重程度 | Issue | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | [#5911](https://github.com/agentscope-ai/QwenPaw/issues/5911) | Windows 沙箱忽略配置的 Shell，强制使用 cmd.exe | **Open** |
| **严重** | [#5910](https://github.com/agentscope-ai/QwenPaw/issues/5910) | Auto Memory Search 产生格式错误的历史记录，导致 OpenAI API 返回 502 | **Open** |
| **严重** | [#5856](https://github.com/agentscope-ai/QwenPaw/issues/5856) | 上下文压缩 (Context Compaction) 丢失 Tool Call 结构，导致 400 错误 | **Open** |
| **严重** | [#5872](https://github.com/agentscope-ai/QwenPaw/issues/5872) | Docker 容器内 browser_use 因 dbus 错误启动失败 | **Open** |
| **严重** | [#5906](https://github.com/agentscope-ai/QwenPaw/issues/5906) | 防重复功能异常触发，导致正常的对话被误判为死循环 | **Open** |
| **高** | [#5896](https://github.com/agentscope-ai/QwenPaw/issues/5896) | v2.0 迭代次数限制计数逻辑错误 | **Open** |
| **高** | [#5898](https://github.com/agentscope-ai/QwenPaw/issues/5898) | OneBot 频道默认开启，导致看门狗无限重启 | **已关闭/已修复** |
| **中** | [#5868](https://github.com/agentscope-ai/QwenPaw/issues/5868) | Matrix 频道 Token 登录失败 | **已关闭/已修复** |
| **中** | [#5858](https://github.com/agentscope-ai/QwenPaw/issues/5858) | Assistant 消息被格式化器静默丢弃，破坏 Tool Use 配对 | **已关闭/已修复** |

**备注：** 值得注意的是，今日封闭的 Bug 修复数量较高（#5328, #5479, #5528, #5566, #5863, #5868, #5893 等瞬间完成修复并合入），说明团队对社区报告的 **响应速度和修复效率极高**。

---

### 6. 功能请求与路线图信号

- **极有可能纳入下一版本：**
  - **#5187**：Windows Desktop GUI Automation (computer_use) 功能，目前已有长达 24 天的持续开发 PR，这是一个巨大的功能亮点。详见：[PR #5187](https://github.com/agentscope-ai/QwenPaw/pull/5187)
  - **#5909**：可配置主题模块，来自 #2291（Help Wanted）的第一个任务已被认领并提交了设计提案。详见：[Issue #5909](https://github.com/agentscope-ai/QwenPaw/issues/5909)
  - **#5692**：记忆搜索 Reranker 功能，正在 PR 中。详见：[PR #5692](https://github.com/agentscope-ai/QwenPaw/pull/5692)

- **社区强烈期待的“开关”功能：**
  - **#5879**：沙箱可关闭。
  - **#5797**：定时任务弹窗自定义。
  - **#5903**：会话分组与导入导出。详见：[Issue #5903](https://github.com/agentscope-ai/QwenPaw/issues/5903)

**路线图信号：** 用户的普遍诉求从“有没有”转向了 **“能不能自定义”**。开发者也在迅速响应这一信号，v2.0 正在从一个“开箱即用”的工具，向 **“高可配置的 Agent 操作系统”** 演进。

---

### 7. 用户反馈摘要

- **正面：**
  - **极高的参与度：** 用户 @guanyanlai-collab 直接在 #5893 中给出了企业微信无法生成二维码的正则修复方案，典型的“用户即开发者”的社区文化。
  - **容忍度高：** 虽然 Bug 多，但用户愿意提供详细复现步骤（如 #5856 描述了压缩丢失数据的完整链路， #5910 给出了自动记忆搜索的包捕获数据），显示出极高的参与热情。

- **负面/痛点：**
  - **沙箱恐惧症：** “沙盒严重限制了 agent 的能力，且无法关闭，连让 agent 安装 python 的库都无法正常完成了”（#5879）。
  - **渠道生态不稳定：** 飞书不回复、OneBot 导致崩溃、Matrix 登录失败，用户在不同渠道间迁移成本很高。
  - **“聪明反被聪明误”：** 上下文压缩、自动记忆搜索、防重复检测等功能出发点是好的，但实现上的 bug 导致大量核心业务流程失败（#5856, #5910）。
  - **早期用户的挫败感：** 有用户报告在 `v1.1.12.post3` 和 `v2.0.0b5` 之间切换时遇到不同的问题集，Beta 版本的体验波动较大。

---

### 8. 待处理积压与提醒

- **#2291 - Help Wanted 任务列表**
  - **状态：** 活跃（64 条评论）。
  - **提醒：** 部分标注为 “Not Started” 的旧任务可能需要检查是否仍然适用，建议维护者 @cuiyuebing 进行一次盘点，剔除过时任务，释放“任务已满”的假象。
  - **链接：** [Issue #2291](https://github.com/agentscope-ai/QwenPaw/issues/2291)

- **#5757 - 飞书不回复**
  - **状态：** Open（13 条评论）。
  - **提醒：** 作为评论数第二多的活跃 Bug（仅次于招聘贴），至今未分配或给出明确排查方向，可能是一个潜在的社区信任危机点。建议优先处理。
  - **链接：** [Issue #5757](https://github.com/agentscope-ai/QwenPaw/issues/5757)

- **#5900 - MCP streamable_http 会话终止后无法自动重连**
  - **状态：** Open。
  - **提醒：** 涉及 v2.0 核心 MCP 生态的稳定性。如果 MCP Server 重启，客户端永久被跳过是非常严重的生产环境问题。详见：[Issue #5900](https://github.com/agentscope-ai/QwenPaw/issues/5900)

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是根据您提供的 hermes-agent GitHub 数据生成的 2026-07-10 项目动态日报。

---

# hermes-agent 项目动态日报 | 2026-07-10

---

## 1. 今日速览

Hermes-Agent 项目在 7月10日展现出极高的迭代活性，社区在 24 小时内贡献了 224 条 Issue 与 500 个 PR 更新。项目当前的核心矛盾集中在**多平台网络适配**（企业代理、Tailscale、Weixin）与 **Provider 兼容性**（OpenRouter、Codex、Ollama）上，但社区大量高赞功能请求（上下文压缩、时间感知）与针对 Windows 及桌面端的集中 Bug 修复表明，项目正处于**广度扩张与稳定性加固并行**的快速发展期，整体健康度良好。

## 2. 版本发布

（无）

## 3. 项目进展

尽管今日无正式版本发布，但从提交的核心 PR 来看，项目在多个维度取得了实质性推进：

- **核心 Agent 稳定性修复**：
  - **PR #61529** ([link](https://github.com/NousResearch/hermes-agent/pull/61529)): 修复了后台自我改进审查（Curator）误分类内存/技能内容的 Bug，通过限制审查子代理的工具集，解决了 **Issue #30220** 中的模式不匹配问题。
  - **PR #61690** ([link](https://github.com/NousResearch/hermes-agent/pull/61690)): 修复了切换模型时 `base_url` 残留导致的凭据串线问题，增强了 Provider 切换的安全性。
  - **PR #61692** ([link](https://github.com/NousResearch/hermes-agent/pull/61692)): 优化了对已知公共端点的本地服务器探测逻辑，减少了 API 调用的无用 404 污染。

- **多平台容错与适配**：
  - **PR #61605** ([link](https://github.com/NousResearch/hermes-agent/pull/61605)): 针对 Weixin 适配器在 iLink 桥断开后陷入无限轮询的问题，增加了累积失败计数限制，提升了网关稳健性。
  - **PR #61687** ([link](https://github.com/NousResearch/hermes-agent/pull/61687)): 新增 **Kindle Scribe** 平台支持，允许签名笔记通过 HTTP 桥接与 Agent 交互，这是网关架构扩展性的有力证明。
  - **PR #61564** ([link](https://github.com/NousResearch/hermes-agent/pull/61564)): 解决了 Windows OpenSSH 下因路径重解析点（Junction）导致 TUI 启动失败的兼容性问题。

- **CLI/TUI 体验优化**：
  - **PR #61541** ([link](https://github.com/NousResearch/hermes-agent/pull/61541)): 修复了 TUI 模式下流式传输尾部文本因 `idle()` 调用被静默丢弃的数据丢失问题。
  - **PR #61488** ([link](https://github.com/NousResearch/hermes-agent/pull/61488)): 将 Telegram/Discord 等平台上的 `/model` 切换命令默认作用域改为会话级别，防止无意的全局配置修改。

## 4. 社区热点

- **最受期待的功能 - 上下文压缩**：
  - **Issue #39691** ([link](https://github.com/NousResearch/hermes-agent/issues/39691))：提议集成 `headroom-ai` 进行工具输出压缩，获得 **13 个 👍**。用户普遍认为现有会话级压缩粒度太粗，对工具调用的输出进行细粒度压缩能极大改善长会话体验。该问题自 6月5日提出以来热度持续走高。

- **最高讨论度的 Bug - OpenRouter 兼容性**：
  - **Issue #60821** ([link](https://github.com/NousResearch/hermes-agent/issues/60821))：由于 `Completions.create()` 接收到非预期的 `system` 参数导致崩溃，24小时内获得 **13 条评论**。这表明第三方非原生 OpenAI 端点（如 OpenRouter、SiliconFlow）的兼容适配依然是高频踩坑区。该 Bug 已被标记为重复且关闭，但社区对其关注度可见一斑。

- **最吸睛的 UX 改进 - Shift+Enter 换行**：
  - **Issue #5346** (已关闭, [link](https://github.com/NousResearch/hermes-agent/issues/5346))：获得 **20 个 👍**，是目前社区呼声最高的纯交互体验提升。该功能已被官方采纳并实现。

- **新硬件集成引发的热议 - Kindle Scribe**：
  - **PR #61687** ([link](https://github.com/NousResearch/hermes-agent/pull/61687))：为 Kindle Scribe 添加平台适配器引来了大量围观。虽然评论不多，但该功能展示了项目在跨场景扩展上的巨大潜力。

## 5. Bug 与稳定性

- **严重/紧急 (P1/P2)**：
  - **`#27038` [P1]**：Codex Responses API 重放长 ID 字段时被拒绝，导致会话恢复功能失效。`comp/agent, provider/openai` ([link](https://github.com/NousResearch/hermes-agent/issues/27038))
  - **`#5454` [P1]**：LLM API 调用无代理支持，企业用户在防火墙后完全无法使用。`comp/agent` ([link](https://github.com/NousResearch/hermes-agent/issues/5454))
  - **`#55130` [P2]**：Dashboard 在仅启用基础密码认证时完全 500 崩溃，无法加载登录页面，严重影响单机部署。`comp/dashboard` ([link](https://github.com/NousResearch/hermes-agent/issues/55130))
  - **`#58646` [P2]**：QQ 机器人适配器因 `connect()` 参数不匹配导致启动失败。`platform/qqbot` ([link](https://github.com/NousResearch/hermes-agent/issues/58646))
  - **`#61487` [P2]**：Z.AI 多密钥池中一个密钥限速后级联标记所有密钥为耗尽，导致服务中断。`provider/zai` ([link](https://github.com/NousResearch/hermes-agent/issues/61487))

- **已有修复关联的 Bug**：
  - **`#30220` [P2]**：后台自改进审查误分类内容。（Fix PR: #61529）
  - **`#44456` [P2]**：Desktop 的 `/compress` 命令失效。（仍在讨论中，`comp/desktop`）
  - **`#39534` [P3]**：Windows Desktop 中文提示被截断。（`platform/windows`）

## 6. 功能请求与路线图信号

结合高赞 Feature Request 与已提交 PR，可以绘制出项目未来的技术演进方向：

- **上下文感知时代即将到来**：
  - **Issue #10421** ([link](https://github.com/NousResearch/hermes-agent/issues/10421)) 要求增加“转轮次实时时间上下文”，累计 **9 个 👍**。
  - **Issue #39691** ([link](https://github.com/NousResearch/hermes-agent/issues/39691)) 要求工具级输出压缩，累计 **13 个 👍**。
  - **PR #61684** ([link](https://github.com/NousResearch/hermes-agent/pull/61684)) 增加了从 Claude Code 等外部来源导入会话的工具，暗示着项目可能为更通用的数据枢纽做准备。

- **统一路由与多租户架构**：
  - **Issue #41190** ([link](https://github.com/NousResearch/hermes-agent/issues/41190)) 呼吁提供一个统一的插件钩子来覆盖 Provider/Model。
  - **PR #61689** ([link](https://github.com/NousResearch/hermes-agent/pull/61689)) 实现了 Matrix 平台按房间分配独立 Profile 的功能，这与统一路由的思路完全契合。

- **网关能力标准化**：
  - **PR #61694** ([link](https://github.com/NousResearch/hermes-agent/pull/61694)) 引入了媒体能力声明机制。这意味着未来不同平台的差异（如能否发送语音、文件）将标准化地暴露给上层应用。

## 7. 用户反馈摘要

- **积极反馈**：
  - `#5346` (Shift+Enter) 的关闭让许多 CLI 用户表示满意。
  - Kindle Scribe 的支持让社区对小众硬件的集成产生了浓厚兴趣，认为项目在“个人 AI 助手”形态上探索得很远。

- **核心痛点**：
  - **网络隔离与服务割裂**：大量反馈集中在网络连通性上。多位用户抱怨在企业网络（`#5454`）、Tailscale（`#38061`）甚至使用微信环境下（`#35713`）体验受损。用户希望在任何网络条件下都能“无缝”使用。
  - **弱模型兼容性**：即便是常见的本地模型（Ollama + Gemma4 `#49297`）或热门商业模型（DeepSeek V4 `#57864`），用户依然频繁遭遇奇特的行为异常，表明 Provider 抽象层的承载压力很大。
  - **桌面端体验落差**：Desktop 无法在 CLI 中恢复会话（`#59224`），Dashboard 跨 Profile 加载失败（`#44147`），用户数据的访问呈现出显著的“割裂感”。

## 8. 待处理积压

以下为长期未获足够回应的关键 Issue，提醒维护者关注：

- **`#5454` [P1]** — Proxy support for LLM API calls。自 4月6日创建以来已搁置 **95 天**，作为 P1 级 Bug 在持续阻塞企业用户。 ([link](https://github.com/NousResearch/hermes-agent/issues/5454))
- **`#27038` [P1]** — Codex Responses API 重放 Bug。核心功能的持久性缺陷，对 Codex 重度用户影响大，开放 **55 天**仍未解决。 ([link](https://github.com/NousResearch/hermes-agent/issues/27038))
- **`#38061` [P2]** — Tailscale 远程网关连接失败。涉及网络基础功能，反馈者众多，但目前缺乏官方指向性回复。 ([link](https://github.com/NousResearch/hermes-agent/issues/38061))
- **`#10421` [P3]** — Turn-level time context。社区诉求稳定且明确（👍 9），几乎可视为下阶段路线图的标准候选功能，但尚无开发组认领。 ([link](https://github.com/NousResearch/hermes-agent/issues/10421))
- **`#39691` [P3]** — headroom-ai 工具输出压缩。社区呼声最高（👍 13），技术上具备可行性，急需项目核心成员介入评估。 ([link](https://github.com/NousResearch/hermes-agent/issues/39691))

---
*报告生成时间：2026-07-10 | 数据来源：GitHub*

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*