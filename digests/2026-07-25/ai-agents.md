# OpenClaw 生态日报 2026-07-25

> Issues: 450 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-24 22:52 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)
- [AstrBot](https://github.com/AstrBotDevs/AstrBot)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-07-25

## 1. 今日速览

过去 24 小时，OpenClaw 项目保持极高的社区活跃度：**450 条 Issue 更新**（新开/活跃 344 条，关闭 106 条）与 **500 条 PR 更新**（待合并 180 条，已合并/关闭 320 条）。当日无正式版本发布，但维护者与贡献者围绕大量 P0/P1 级 Bug 和功能性重构展开密集讨论与修复。核心技术债务仍集中在**会话持久化、多代理协调、跨渠道消息投递**等领域，多个标记为“clawsweeper-recovery-stuck”的卡死问题正被集中排查。整体呈现“高频迭代、质量攻坚”的状态。

## 2. 版本发布

当日无新版本发布。

## 3. 项目进展

今日共有 **320 个 PR 被合并或关闭**，重要变更包括：

- **供应链安全加固**  
  - PR [#113307](https://github.com/openclaw/openclaw/pull/113307) 合入了安装脚本执行前的哈希校验逻辑，防止下载失败或篡改后仍执行 Bash。  
  - PR [#113428](https://github.com/openclaw/openclaw/pull/113428) 将 `brace-expansion` 锁定至修补版本，清除生产依赖审计中的 GHSA 告警。

- **Bug 修复闭环**  
  - Issue [#98528](https://github.com/openclaw/openclaw/issues/98528)（v2026.6.11 回归：工具调用首轮后返回空结果）今日关闭，对应修复已合并。  
  - Issue [#110950](https://github.com/openclaw/openclaw/issues/110950)（“万物皆 Cron”统一自动化提案）关闭，推测该概念已被内部路线图采纳或现有设计覆盖。

- **大型架构重构进入审查**  
  - 多槽记忆架构 PR [#88504](https://github.com/openclaw/openclaw/pull/88504)（XL）开放审查，若合并将彻底改写记忆层设计。  
  - 插件 SDK 实时语音会话 PR [#112820](https://github.com/openclaw/openclaw/pull/112820)（XL）进入维护者测试阶段，预示媒体能力扩展。

以上进展表明项目在维持功能迭代的同时，持续强化安全基线、修复回归缺陷，并为下一版本储备架构级改进。

## 4. 社区热点

当日讨论热度最高的 Issues 集中反映了用户的深层痛点：

- **跨频道会话初始化冲突**：[#102020](https://github.com/openclaw/openclaw/issues/102020)（评论 16）——全新会话中第二条消息即失败，报错“回复会话初始化冲突”，影响 Signal 和 Discord，社区强烈要求统一状态机。  
- **Anthropic thinking 块签名错误导致工具线程坏死**：[#94228](https://github.com/openclaw/openclaw/issues/94228)（评论 14，👍 2）——长链路工具调用后历史 thinking 块的 signature 校验失败，永久 400 错误，被标为 Platinum Hermit 级别。  
- **Compaction 超时无中间进度复用**：[#92043](https://github.com/openclaw/openclaw/issues/92043)（评论 13，👍 3）——180 秒压缩窗口为整体壁钟计时，合法慢压缩每次失败且无法恢复，用户呼吁引入增量 checkpoint。

PR 方面虽未公开评论数，但 [#112820](https://github.com/openclaw/openclaw/pull/112820) 和 [#112678](https://github.com/openclaw/openclaw/pull/112678)（隐式 main 代理重构）在维护者与贡献者之间反复互动，暗示架构层面的热烈讨论。

## 5. Bug 与稳定性

按严重程度排列的当日主要 Bug（已附修复 PR 状态）：

| 严重程度 | Issue | 摘要 | 修复 PR |
|---------|-------|------|--------|
| **P0** | [#90378](https://github.com/openclaw/openclaw/issues/90378) | 升级 5.28→6.1 时 Cron 存储静默迁移 SQLite，新任务默认 announce 模式导致渠道报错 | 有 linked PR |
| **P1** | [#94228](https://github.com/openclaw/openclaw/issues/94228) | Anthropic 原生路径 thinking 块签名无效致工具线程永久 400 | 有 linked PR |
| **P1** | [#92043](https://github.com/openclaw/openclaw/issues/92043) | Compaction 超时无中间进度，慢压缩反复失败 | 有 linked PR |
| **P1** | [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex 路径引发长延迟、钩子超时与启动中止 | 无 fix（待决策） |
| **P1** | [#47975](https://github.com/openclaw/openclaw/issues/47975) | 子代理会话持久不结束，主会话无响应 | 无 fix |
| **P1** | [#45224](https://github.com/openclaw/openclaw/issues/45224) | Playwright 断言未捕获致 Gateway 进程崩溃 | 无 fix |
| **Regression** | [#111519](https://github.com/openclaw/openclaw/issues/111519) | v2026.7.2-beta.3 中 Telegram DM 回退，源回复丢失 | 无 fix |
| **Regression** | [#98528](https://github.com/openclaw/openclaw/issues/98528) | v2026.6.11 工具调用首轮后空结果（今日已关闭，修复完成） | 已合并 |
| **Regression** | [#112906](https://github.com/openclaw/openclaw/issues/112906) | v2026.7.1 富消息模式下 `` 渲染破裂 | 无 fix |

此外，多个 P1 议题带有 `clawsweeper-recovery-stuck` 标签，表明会话恢复流程存在系统性卡死，维护者正集中分析根因。

## 6. 功能请求与路线图信号

当日高频功能请求中，以下方向最可能进入下一版本：

- **动态模型发现**：[#10687](https://github.com/openclaw/openclaw/issues/10687) 要求为 OpenRouter 等提供全动态模型列表，处于 needs-product-decision，预计与多槽记忆架构协同落地。  
- **YAML 配置文件支持**：[#45758](https://github.com/openclaw/openclaw/issues/45758)（👍 2）呼声稳定，属于低风险 UX 改进。  
- **插件 SDK 实时语音**：PR [#112820](https://github.com/openclaw/openclaw/pull/112820) 将允许插件通过 Gateway 管理 Realtime 语音会话，若合并将开启丰富的第三方交互场景。  
- **Everything is a Cron**：[#110950](https://github.com/openclaw/openclaw/issues/110950) 关闭暗示该统一自动化概念已被内部采纳，或成为未来版本的设计基础。  
- **Skill 权限清单标准**：[#12219](https://github.com/openclaw/openclaw/issues/12219) 提出 `skill.yaml` 声明，目前 needs-security-review，若纳入将大幅提升技能生态透明度。

值得关注的是，大规模 PR [#88504](https://github.com/openclaw/openclaw/pull/88504) 如果通过，将重构整个记忆层，这是路线图上最重要的进化之一。

## 7. 用户反馈摘要

从当天 Issues 评论中提炼的核心用户声音：

- **“升级迁移很透明吗？不。**” [#90378](https://github.com/openclaw/openclaw/issues/90378) 反映 SQLite 迁移未经告知，导致 Cron 任务默认行为改变，通道报错。用户认为升级流程缺乏前置沟通与回退预览。  
- **“Telegram 在退化”**：Telegram 相关 Bug 频发——论坛主题黑盒 ([#91564](https://github.com/openclaw/openclaw/issues/91564))、DM 来源丢失 ([#111519](https://github.com/openclaw/openclaw/issues/111519))、会话 JSON 损坏致频道卡死 ([#43549](https://github.com/openclaw/openclaw/issues/43549))。用户对渠道稳定性信心下降。  
- **“长会话一碰就碎”**：Anthropic 用户遭遇 thinking 块签名错误 ([#94228](https://github.com/openclaw/openclaw/issues/94228))；OpenAI 用户因前缀缓存被动态注入持续打碎而抱怨成本飙升 ([#95610](https://github.com/openclaw/openclaw/issues/95610))。社区期望更健壮的长期会话保护。  
- **“Subagent 一多，主 Agent 就废”**：[#47975](https://github.com/openclaw/openclaw/issues/47975) 指出子代理会话残留导致主界面无法接收新消息，用户被迫手动清理。  
- **“给我更多控制”**：文件沙箱 ([#7722](https://github.com/openclaw/openclaw/issues/7722))、每模型超时 ([#8724](https://github.com/openclaw/openclaw/issues/8724))、YAML 配置 ([#45758](https://github.com/openclaw/openclaw/issues/45758))、屏蔽子代理广播 ([#8299](https://github.com/openclaw/openclaw/issues/8299)) 等诉求持续获得 👍，社区追求“可配置的稳健性”。

## 8. 待处理积压

以下重要议题已停留数月，缺乏维护者响应或产品决策，需优先关注：

- **Filesystem 沙箱配置**：[#7722](https://github.com/openclaw/openclaw/issues/7722)（2026-02-03，P2，needs-security-review）——文件访问白名单请求，搁置近 6 个月，安全影响显著。  
- **Skill 权限清单标准**：[#12219](https://github.com/openclaw/openclaw/issues/12219)（2026-02-09，P2，needs-security-review）——Skill 权限声明规范，对生态安全至关重要。  
- **测试回退链命令**：[#6599](https://github.com/openclaw/openclaw/issues/6599)（2026-02-01，P3，needs-product-decision）——提供 `test-fallback` 命令验证模型回退配置，一直未决策。  
- **Cron 作业在 API 故障时静默超时**：[#45494](https://github.com/openclaw/openclaw/issues/45494)（2026-03-13，P1，needs-maintainer-review）——当 LLM 返回 HTTP 500 时，Cron 任务不快速失败而是耗尽超时窗口，目前无对应修复 PR。  
- **嵌入运行器因工具参数超时断开**：[#53540](https://github.com/openclaw/openclaw/issues/53540)（2026-03-24，P1，needs-live-repro）——大参数工具调用生成耗时超过请求超时，导致“网络断开”，该场景尚无用例复现。

建议维护团队在下一路线图循环中优先评估这些长期挂起项，避免社区贡献动力流失。

---

## 横向生态对比

## 横向对比分析报告：个人 AI 助手 / 自主智能体开源生态

### 1. 生态全景

当前个人 AI 助手开源生态正处于 **“功能堆叠期”向“架构成熟期”过渡**的关键阶段。多项目同时面临三大共性挑战：**稳定性回归**（v2.0 升级断裂、Cron 静默失败）、**安全体系补课**（Shell 沙箱绕过、MQTT 证书跳过）以及**多代理/子会话治理**（会话残留、budget 竞争）。与此同时，对插件标准化、跨渠道一致性、自动化工作流的底层需求高度一致，说明行业正从单一聊天机器人向可编程 Agent 平台演进。整体呈现“大项目攻坚、中型项目扩张、小项目深耕”的差异化格局，社区贡献意愿强烈但维护者带宽普遍吃紧。

---

### 2. 各项目活跃度对比

| 项目 | GitHub | Issue 日活跃 | PR 日活跃 | 当日 Release | 健康度评估 |
|------|--------|-------------|-----------|-------------|-----------|
| **OpenClaw** | openclaw/openclaw | 450（新开/活跃 344，关闭 106） | 500（待合 180，合/关 320） | 无 | 核心参照，极高迭代速率，但技术债务重，质量攻坚；多 P0/P1 未闭环 |
| **Zeroclaw** | zeroclaw-labs/zeroclaw | 47（活跃 39，关闭 8） | 50（待合 40，关闭 10） | 无 | 修复响应迅捷，但 S0 级安全漏洞（#9247）及重要功能缺陷（#9340）仍悬空 |
| **PicoClaw** | sipeed/picoclaw | 有限（主要活动：1 个新 Bug + 积压旧 issue） | 合并 6 个，待合 1 个（#3261） | 无 | 维护活跃，集中清除积压 PR，安全/优化主线清晰；新 Bug 待响应 |
| **QwenPaw** | agentscope-ai/qwenpaw | 48（新开/活跃 26，关闭 22） | 36（待合 23，合/关 13） | v2.0.1 + v2.0.1-beta.3 | 平台化推进迅速，但 v2.0 功能回归与性能延迟削弱社区信心；MCP 稳定性存疑 |
| **AstrBot** | AstrBotDevs/AstrBot | 17（新 9，关 8） | 22（合/关 13，待合 9） | 无 | 社区协作高效，Bug 修复合并快；WebUI 阻塞仍未彻底解决，插件隔离架构待决策 |

---

### 3. OpenClaw 在生态中的定位

OpenClaw 属于 **全能型个人 AI 助手标杆项目**，在生态中处于绝对核心地位：

- **社区规模领先**：日活跃 Issue/PR 数量是第二梯队（Zeroclaw/QwenPaw）的 **10 倍**，贡献者网络与讨论深度远超同类。
- **技术路线差异**：强调**多槽记忆架构（#88504）**、**插件 SDK 实时语音（#112820）** 以及“万物皆 Cron”统一自动化概念，覆盖多代理协调、跨渠道投递、会话持久化等完整链路。相较之下，Zeroclaw 更侧重安全与 SOP，QwenPaw 聚焦 PawApp 平台生态，AstrBot 轻量快速。
- **优势**：功能最全面、集成度最高、路线图宏大；大型重构（记忆层、插件系统）将带来指数级能力跃迁。
- **短板**：回归 Bug 频发（如 #98528、#111519）、长会话场景脆弱（#94228）、升级迁移透明性差（#90378），社区开始出现“可配置的稳健性”诉求。

---

### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 / 表现 |
|---------|--------|--------------|
| **多代理/子会话治理** | OpenClaw、Zeroclaw、QwenPaw | OpenClaw 子代理不结束（#47975）；Zeroclaw `shared_budget` 竞态恐慌（#9192）与执行树预算所有权 RFC（#9323）；QwenPaw 多模型并行请求（#6455） |
| **跨渠道消息稳定性** | OpenClaw、Zeroclaw、PicoClaw、AstrBot | OpenClaw Signal/Discord 初始化冲突（#102020）；Zeroclaw Discord 打字指示器卡死（#9198）；PicoClaw Discord 400 错误修复；AstrBot QQ @提及、Telegram 长文等多平台兼容问题 |
| **自动化工作流（Cron）** | OpenClaw、Zeroclaw、QwenPaw、AstrBot | OpenClaw 统一 Cron 概念（#110950）；Zeroclaw Cron 输出静默丢弃（#9340，S1）；QwenPaw 定时任务覆盖用户会话（#6401）；AstrBot 重试链路检查点丢失 |
| **安全与沙箱** | OpenClaw、Zeroclaw、PicoClaw、AstrBot | OpenClaw 供应链哈希校验（#113307）；Zeroclaw Shell 符号链接绕过（#9247，S0）；PicoClaw MQTT 强制 TLS（#3246）；AstrBot 屏蔽词绕过修复（#9232） |
| **插件生态标准化与隔离** | OpenClaw、Zeroclaw、QwenPaw、AstrBot | OpenClaw 插件 SDK + 实时语音；Zeroclaw “一切皆插件” RFC（#6489）；QwenPaw PawApp 平台；AstrBot 隔离架构 RFC（#3210） |
| **长会话 / 上下文管理** | OpenClaw、PicoClaw、QwenPaw、AstrBot | OpenClaw compaction 超时（#92043）；PicoClaw 历史显示不全（#2796）；QwenPaw 2s 固定延迟（#6307）；AstrBot 引用 GIF 污染历史（#9295） |

这些共性需求表明：**多代理协调、安全沙箱、插件隔离、长期记忆**是制约 Agent 走向实用的四大核心瓶颈。

---

### 5. 差异化定位分析

| 维度 | OpenClaw | Zeroclaw | PicoClaw | QwenPaw | AstrBot |
|------|----------|----------|----------|---------|---------|
| **功能侧重** | 全能个人助手，多 Agent 编排，记忆层重构，语音扩展 | 企业级安全，SOP 标准操作，认证与审计 | 轻量化，性能优化，国际化，代码质量 | 平台化 App 生态，PawApp SDK，桌面 GUI 自动化 | 跨平台消息机器人，插件扩展，社群管理 |
| **目标用户** | AI Agent 开发者、高级用户 | 安全敏感企业、自动化运维 | 资源受限环境、OP/边缘场景、贡献者新手 | AI 应用创作者、内容制作、开发者 | 机器人运营者、个人与社群助手 |
| **技术架构关键差异** | 多槽记忆、插件 Gateway、统一 Cron 触发 | 执行树 + 沙箱 + 可验证意图链 + 认证 | seahorse 模块化、O(n²)→线性优化 | AgentScope 原生、PawApp 运行时、内置看板 | 插件隔离架构（RFC）、消息队列式适配层 |

---

### 6. 社区热度与成熟度

**第一梯队（极高热度，质量攻坚期）：**  
- **OpenClaw** — 日活跃量级 450+/500+，但多个 P0/P1 回归未解；社区讨论深、贡献密度高，但维护者负重前行。

**第二梯队（高活跃，快速迭代→安全成熟过渡）：**  
- **Zeroclaw** — 日活 47/50，v0.9.0 认证里程碑前夜，社区安全研究活跃，修复速度获认可。  
- **QwenPaw** — 日活 48/36，v2.0 系列发布后生态扩张，但版本断裂引发信任危机；平台化与稳定性需平衡。

**第三梯队（中等活跃，协作高效）：**  
- **AstrBot** — 日活 17/22，贡献协作紧密，24h 内合关 13 PR 8 Issue；长期卡点集中在 WebUI 与插件隔离。

**第四梯队（较小规模，专注深耕）：**  
- **PicoClaw** — 日活指标低，但合并力度大（6 PR/日积压清理），安全加固与性能优化导向清晰；社区虽小但健康。

---

### 7. 值得关注的趋势信号

1. **安全不再是加分项，而是准入门槛**：Zeroclaw 的 S0 Shell 绕过、PicoClaw 的 MQTT 强制 TLS、OpenClaw 的供应链校验均说明社区已将安全防御前移至设计阶段。Agent 开发者应默认遵循“Fail Secure”原则。

2. **插件平台化成为主流架构选择**：QwenPaw PawApp、AstrBot 隔离架构 RFC、Zeroclaw “一切皆插件”、OpenClaw 插件 SDK 共同指向一个趋势：未来的 Agent 能力将通过 **标准化运行时 + 权限声明** 来安全扩展。skill.yaml 类清单标准（如 OpenClaw #12219）将加速生态互操作。

3. **多代理资源治理是最棘手工程难题**：子代理残留、budget 竞争、协调者超载等问题在三个项目中集中爆发。Zeroclaw #9323 提出“执行树迭代预算所有权”，OpenClaw 子代理残留、QwenPaw 多模型并行均显示现有方案存在设计空白，为下一轮架构创新提供了切入点。

4. **Cron 自动化信任机制面临重建**：Cron 任务“假成功”（Zeroclaw #9340）和时间任务覆盖历史（QwenPaw #6401）暴露了自动化隐式假设的风险。未来需要**可观测性**（执行可追溯输出）、**可干预**（增量 checkpoint）和**可回滚**（升级预览）三位一体的机制。

5. **跨渠道消息抽象层仍未成熟**：Signal/Discord/Telegram/QQ 各渠道的行为差异导致社区反复修复初始化冲突、格式兼容、状态机不一致。统一会话状态机（如 OpenClaw #102020 所呼吁）将是下一阶段平台必争之地。

6. **长期记忆 / 上下文压缩成为效率瓶颈**：OpenClaw compaction 超时、PicoClaw 历史记录截断、QwenPaw 固定延迟均指向同一问题——现有压缩策略既损失信息又增加延迟。增量 checkpoint 与按需解压成为社区共识方向。

上述趋势对 AI 智能体开发者的直接启示是：**以安全为底线、以可观测性为基线、以插件隔离为架构、以多代理治理为核心挑战，优先构建可测试、可回退、可审计的系统。**

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# 🐾 Zeroclaw 项目动态日报 | 2026-07-25

> AI Agent / Personal AI Assistant 开源项目分析

---

## 1. 今日速览

过去 24 小时，Zeroclaw 社区保持**极高活跃度**。共计 **47 条 Issue 更新**（39 条活跃，8 条关闭），**50 条 PR 更新**（40 条待合并，10 条关闭）。项目未发布新版本，但大量工作围绕安全加固（Shell 工具工作区边界绕过 #9247、可验证意图链验证 #9328）、核心稳定性修复（配置系统点号键名丢失 #9240、Cron 输出静默丢弃 #9340）以及大型架构 RFC（执行树迭代预算所有权 #9323、AI 辅助 PR 预审 #9330）展开。v0.9.0 安全与认证里程碑（Tracker #7432）正密集推进，项目健康度总体向好，但安全风险暴露和自动化功能缺陷是当日主要负面信号。

---

## 2. 版本发布

> 无新版本发布。

---

## 3. 项目进展

今日共关闭/合并 10 个 PR，对应一系列重要 Bug 修复的收尾，夯实了 v0.9.0 的底层基础：

#### 🔧 配置系统大幅完善
- **修复 `config set` 无法为非 `providers.*` 动态 Map 段创建别名**（#8834 🔒）。此前在 `risk_profiles`、`peer_groups`、`channels.telegram.*` 等路径下执行 `config set` 会误报未知属性。**【已关闭】**
- **修复 `save_dirty` 在键名包含点号时静默丢失写入**（#9240 🔒）。模型 ID 如 `gpt-4.1`、`claude-3.5-sonnet` 等配置写入将被完全吞掉。**【已关闭】**

#### 🔧 工具执行与运行修复
- **修复 Shell 工具在 `autonomy level = "full"` 时完全被拒绝执行**（#6434 🔒）。这是一个阻断级别的 S1 回归。**【已关闭】**
- **修复 Delegate 工具跨代理 API Key 泄漏**（#7623 🔒）。在 `requires_openai_auth` 的子代理场景中，`resolve_brain` 错误传递了协调者的 API Key。**【已关闭】**
- **修复 Landlock 沙箱导致 ZeroClaw 守护进程自身受限**（#9204 🔒）。沙箱策略在保护外部的同时锁死了自身 SQLite 内存访问。**【已关闭】**

#### 🔧 用户体验修复
- **修复 Telegram 别名在守护进程重载后被静默丢弃**（#9236 🔒）。
- **修复 ACP 控制台思绪输出被截断为碎片化单词**（#9116 🔒）。

**小结：** 项目在 Bug 修复上响应极快，昨日报告的配置系统痛点几乎全部收尾。但新涌现的 S1 级严重缺陷（Cron 输出、Windows 崩溃）仍悬而未决。

---

## 4. 社区热点

#### 🔥 治理与长期架构讨论
- **#6808 — RFC 工作流、看板自动化与标签清理 (🗨️ 14 条评论)**
  讨论如何通过自动化和标签治理减轻维护者负担，是项目治理层面最受关注的话题。
  [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)
- **#6489 — [RFC] “一切皆插件”统一插件目录 (🗨️ 4 条评论)**
  长期架构方向提案，将现有"集成"（通道、AI Provider、内置工具）与"Wasm 插件"概念统一为单一插件注册表。技术影响力极大，持续获得深度讨论。
  [#6489](https://github.com/zeroclaw-labs/zeroclaw/issues/6489)

#### 🔥 今日新晋焦点
- **#9323 — RFC: 执行树迭代预算所有权 (今日创建)**
  直指当前 `shared_budget` 形同虚设（生产环境均为 `None`）的核心运行时缺陷。若被接受，将彻底改变多代理工具循环的资源边界行为。**极可能被纳入 v0.9.0/v0.10.0 规划。**
  [#9323](https://github.com/zeroclaw-labs/zeroclaw/issues/9323)
- **#9330 — RFC: AI 辅助 PR 预审与再审 (今日创建)**
  提出利用现有 CI 结果的 AI 初评，同时保持按风险级别的人工最终审批权。反映了大规模开源社区平衡代码质量与审查速度的切实需求。
  [#9330](https://github.com/zeroclaw-labs/zeroclaw/issues/9330)
- **#9340 — [Bug] CLI 创建的 Cron 任务无法传递输出 (今日创建, S1)**
  用户 `@AngryPacifist` 报告，Cron 任务 `delivery.mode` 硬编码为 `"none"`，任务看似运行成功实则输出静默丢弃。因触达了自动化核心信任机制，迅速引发社区关注。
  [#9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340)

---

## 5. Bug 与稳定性

按严重等级排列，标注修复进展：

| 严重程度 | Issue | 描述 | 状态 | 关联 Fix PR |
|---|---|---|---|---|
| **S0 (数据泄露/安全风险)** | #9247 | Shell 工具不强制执行工作区边界，可通过 symlink 读写外部文件 | **OPEN** (无关联 PR) |
| **S1 (工作流阻塞)** | #9340 | CLI 创建的 Cron 任务 `delivery.mode` 硬编码为 `"none"` | **OPEN** (无关联 PR) |
| **S1** | #9290 | Windows 桌面安装器缺失 `TaskDialogIndirect` API 无法启动 | **OPEN** (无关联 PR) |
| **S1** | #9192 | `shared_budget` 的 TOCTOU 条件竞争导致 `AtomicUsize` 环绕 panic | **OPEN** (无关联 PR) |
| **S1** | #6434 | Shell 工具在 `full` 自治等级下完全被拒绝 | **CLOSED** ✅ | 已合并修复 |
| **S1** | #9204 | Landlock 沙箱锁死守护进程 (SQLite 内存访问) | **CLOSED** ✅ | 已合并修复 |
| **S2 (功能降级)** | #9328 | `vi_verify` 未验证凭证链即执行约束检查 | **OPEN** (无关联 PR) |
| **S2** | #9198 | Discord 打字指示器在守护进程重载后永久卡死 | **OPEN** (无关联 PR) |
| **S2** | #9285 | `nested set_prop` 将无效值误报为路径错误 | **OPEN** (无关联 PR) |

#### 🛡️ 安全特报
`#9247`（Shell 工具符号链接绕过）是本日最严重的威胁：攻击者只需在工作区内创建一个指向 `/etc/passwd` 的符号链接，即可通过 Shell 工具读取系统敏感文件。目前**暂无修复 PR**，社区应予以最高优先级关注。

---

## 6. 功能请求与路线图信号

| 类型 | 标题 | 链接 | 备注 |
|---|---|---|---|
| **RFC (高优先级)** | 执行树迭代预算所有权 #9323 | [#9323](https://github.com/zeroclaw-labs/zeroclaw/issues/9323) | 核心运行时架构补全，预计是 v0.9.x 目标 |
| **RFC** | AI 辅助 PR 预审 #9330 | [#9330](https://github.com/zeroclaw-labs/zeroclaw/issues/9330) | 开发者体验创新，若落地将加速 PR 流程 |
| **Feature (PR 已就绪)** | 支持 data-wrapped OpenAI 兼容响应 #9335 | [#9335](https://github.com/zeroclaw-labs/zeroclaw/issues/9335) | 兼容特定返回格式为 `{data: {...}}` 的推理端点 |
| **Feature (PR 已就绪)** | 添加 Crusoe Managed Inference Provider #9338 | [#9338](https://github.com/zeroclaw-labs/zeroclaw/pull/9338) | 遵循 NEAR AI 模板，8 文件标准接入 |
| **Tracker** | v0.9.0 Auth / Security / Breaking Changes #7432 | [#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432) | 当前最大工作集，包含大量待办 |
| **Tracker** | SOP 里程碑 5/5 完成 #8288 | [#8288](https://github.com/zeroclaw-labs/zeroclaw/issues/8288) | 目标 13 个 SOP 能力全部验证通过 |

**路线图信号解读：** 项目的短期重心非常明确——**v0.9.0 的安全性与认证重构**（#7432）和 **SOP 标准操作程序能力收尾**（#8288）。同时，社区贡献者在丰富 Provider 生态方面持续发力（#9338 Crusoe），并积极探索运行时资源边界（#9323）和开发者效率工具（#9330）等中远期方向。

---

## 7. 用户反馈摘要

从 Issues 评论中提炼出的用户痛点与诉求：

#### ✅ 积极反馈
- **响应速度认可：** 昨日曝出的配置系统类 Bug（#8834 别名写入、#9240 点号键名、#9236 Telegram 别名丢失）全部在 24 小时内完成修复关闭，体现了维护团队对稳定性问题的极高响应优先级。
- **安全社区参与积极：** 安全研究员 `@vshanbha` 和 `@AngryPacifist` 分别提交了 Shell 工作区绕过和 VI 链缺失验证的高质量安全报告，显示出外部安全审计力量对项目的深入参与。

#### ❌ 核心痛点
- **Windows 开箱体验断裂：** 用户 `@newcomm` 反馈 Windows 安装器启动失败。鉴于项目提供了 `v0.8.3` 的 Windows 分发包，此问题构成新用户准入门槛，严重性较高。
- **自动化信任危机：** 用户 `@AngryPacifist` 指出 Cron 任务的设计缺陷（DeliveryConfig 默认为空），导致 **“假成功”现象**：任务记录为 ok，但用户无法获取任何输出。这很可能导致用户信任自动化流水线的结果，造成业务决策失误。
- **配置系统复杂性：** 用户 `@yanchenko` 提交的 #8834 和 #9240 表明，动态 Map 路径下的属性设置机制仍对普通用户不友好，错误提示含糊（“Unknown property”掩盖了真实的类型/值错误）。

---

## 8. 待处理积压

以下为需要维护者高度关注、但尚未得到有效驱动的关键项目：

#### ⚠️ 安全风险（无 Fix PR）
- **#9247 Shell 工作区边界绕过（S0）** — 已提交安全报告，存在明确可利用路径，零修复 PR 状态令人揪心。
- **#9328 可验证意图链路缺失（S2）** — 虽非高危，但涉及核心验证模型的理论完备性，长尾搁置可能影响后续审计合规。

#### ⚠️ 严重功能缺陷（无 Fix PR）
- **#9340 Cron 输出丢失（S1）** — 新开，对自动化场景打击极大。
- **#9290 Windows 安装器崩溃（S1）** — 跨平台兼容性硬伤。
- **#9192 Shared Budget 并发 Panic（S1）** — `SopEngine` panic 可能导致生产环境守护进程崩溃。

#### ⚠️ 大量高质量 PR 等待作者行动（Needs Author Action）
- **vrurg Goal 系列大重构**（5 个关联 PR：#8746, #8996, #8689, #8688, #8687）—— 涉及 Goal 命令准入、控制器/验证器、重载时状态保持等核心功能，目前已全部标记 `needs-author-action`，处于协作瓶颈。
- **wangmiao0668000666 安全加固系列**（#8741 浏览器快照路径检查, #8713 file_download SSRF 检查）—— 同为高质量安全修复，拖延越久风险敞口越大。
- **metalmon ACP/MCP 资源二进制交换**（#9195, #9196）—— 重构后需 rebase 至最新 master，涉及 ACP 与 MCP 核心协议能力对齐。

#### ⏳ 长期搁置架构
- **#6489 “一切皆插件” RFC**（自 2026-05-06 起） — 虽标记 accepted，但自 6 月以来缺乏实质推进。随着 v0.9.0 临近，若该架构不纳入本轮，则需考虑推迟至 v0.10.0。
- **#6808 工作流看板自动化**（自 2026-05-20 起） — 治理层面的长期讨论，Rev. 22，正等待具体实施计划的形成。

---

> **总结：** Zeroclaw 今日在 Bug 修复上成果斐然（配置系统、工具执行、沙箱），展现了成熟项目的响应力。然而，Shell 边界安全漏洞（#9247）、Cron 功能缺陷（#9340）和 Windows 兼容性崩塌（#9290）构成了当前最大的三层风险。社区对运行时资源边界（#9323）和流程自动化（#9330）的密集提案，标志着项目正从功能堆叠期转向架构优化与安全成熟期前夕。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，现在根据您提供的数据，为您生成 **PicoClaw 项目动态日报 (2026-07-25)**。

---

## **PicoClaw 项目动态日报 | 2026-07-25**

**分析师评价：** 项目维护活跃度较高，社区贡献持续涌入。过去 24 小时内，项目维护者集中合并了多份历史积压的 PR，尤其是针对 **代码质量、性能优化和安全加固** 方面进行了显著改进。同时，一个新报告的 **CPU 占用 Bug** 和一项 **国际化（繁体中文）** 贡献值得关注。

### **1. 今日速览**

- **维护活跃，代码整合加速：** 项目在 24 小时内密集合并了 6 个 Pull Requests，表现出积极的代码整合态度。
- **性能与安全优化成为主线：** 从合并的 PR 来看，项目团队或社区贡献者正致力于重构底层代码以减少内存分配，并修复了一个重要的 MQTT 安全漏洞。
- **社区贡献多元化：** 贡献者不仅提交了 Bug 修复，还提供了多种本地化支持（捷克语、繁体中文）和性能优化，体现了社区生态的健康发展。
- **新 Bug 报告待响应：** 出现了一起关于 Web 前端 CPU 占用过高的问题，尚未有维护者介入，需要关注。

### **2. 版本发布**

- 过去 24 小时无新版本发布。

### **3. 项目进展**

今日项目通过合并 6 个 Pull Requests，在 **代码健壮性、性能、安全及国际化** 方面取得实质性进展。

- **安全加固（高优先级）：** PR [#3246](https://github.com/sipeed/picoclaw/pull/3246) 被合并。该 PR 修复了三个安全问题：强制启用 MQTT 的 TLS 证书验证（修复了之前硬编码跳过验证的漏洞）、为 OAuth 流程添加超时控制、限制搜索读操作的边界。这是今日最重要的变化，显著提升了项目的安全基线。
- **性能优化（中优先级）：** 三个来自同一贡献者的 PR 被合并，针对 `seahorse` 和 `skills` 模块进行了深度优化：
    - `skills` 模块：PR [#3245](https://github.com/sipeed/picoclaw/pull/3245) 优化了 XML 转义逻辑，减少内存分配。
    - `seahorse` 模块：PR [#3243](https://github.com/sipeed/picoclaw/pull/3243) 和 PR [#3244](https://github.com/sipeed/picoclaw/pull/3244) 将字符串拼接操作从 O(n²) 优化为线性复杂度，并减少了摘要生成过程中的内存分配。这些优化将有利于处理长对话的效率和系统资源占用。
- **Discord 频道体验修复：** PR [#323](https://github.com/sipeed/picoclaw/pull/323)（合并日期稍早，但属于近期进展）被正式标记为已关闭。该 PR 修复了 Discord 频道因消息长度超限导致 400 错误的问题，并优化了机器人的状态指示，提升了渠道的稳定性。
- **国际化支持进展：**
    - 捷克语翻译：PR [#3247](https://github.com/sipeed/picoclaw/pull/3247) 合并，补全了 v0.3.1 中缺失的捷克语代码换行选项。
    - 繁体中文（台湾）翻译：PR [#3261](https://github.com/sipeed/picoclaw/pull/3261) 仍 **待合并**，该 PR 为 WebUI 和文档引入了台语用词，对繁体中文使用者社区的友好度有重要意义。

### **4. 社区热点**

- **PR #3261: 添加繁体中文（台湾）翻译**
  - **热度分析：** 尽管未合并，但作为一项国际化贡献，通常能吸引特定语言背景的社区成员关注。背后的诉求是提升项目在全球范围内的易用性，尤其是在大中华区的覆盖。
  - **链接：** [https://github.com/sipeed/picoclaw/pull/3261](https://github.com/sipeed/picoclaw/pull/3261)

- **Issue #2796: 历史记录显示不全**
  - **热度分析：** 获得 7 条评论，属于过去几周内讨论最热烈的问题。用户明确指出当前消息压缩机制影响了用户界面的历史回看，这是一个影响日常使用体验的痛点，已关闭但仍值得关注其解决方案是否彻底。
  - **用户诉求：** 用户期望历史记录能完整展示所有交互，压缩和摘要应仅作用于大模型的上下文，而不应影响用户从 UI 查看完整对话的能力。
  - **链接：** [https://github.com/sipeed/picoclaw/issues/2796](https://github.com/sipeed/picoclaw/issues/2796)

- **Issue #3292: 输入框选中时CPU占用高**
  - **热度分析：** 新鲜出炉的 Bug，暂无评论，但报告的立即生效非常强烈。这通常会引起开发者的重视，因为直接关系到最基础的用户交互体验。
  - **用户诉求：** 用户在使用 Firefox 浏览器打开 Web 界面时，一旦聚焦聊天输入框，CPU 占用就会飙升。这暗示可能存在前端渲染或事件处理的性能问题。
  - **链接：** [https://github.com/sipeed/picoclaw/issues/3292](https://github.com/sipeed/picoclaw/issues/3292)

### **5. Bug 与稳定性**

| 严重程度 | Issue ID | 标题 | 状态 | 分析 |
| :--- | :--- | :--- | :--- | :--- |
| **中** | [#3292](https://github.com/sipeed/picoclaw/issues/3292) | CPU usage too high when focus on input box | **新开，未分配** | 严重影响 Web 端用户的基础输入体验，疑似前端性能问题，需要核心团队尽快定位。 |
| **低** | [#2796](https://github.com/sipeed/picoclaw/issues/2796) | History recording display issue | **已关闭** | 尽管已关闭，但该问题反映了消息压缩机制对用户可见层的影响，是潜在的回溯或修复验证点。 |
| **已修复** | [#3246](https://github.com/sipeed/picoclaw/pull/3246) | Security and robustness hardening | **已合并** | MQTT 跳过证书验证是一个严重安全风险，已通过此 PR 修复。 |

### **6. 功能请求与路线图信号**

- **核心运维与基础设施优化（高采纳率信号）：** 从今日合并的 PR 看，核心团队对 `corporatepiyush` 提交的 **性能优化** 和 **安全加固** 类 PR 采纳率极高。这表明优化代码质量、性能和安全性是目前的重要方向，可能成为下一个版本的亮点。
- **国际化（i18n）持续推进：** 多个语言翻译的提交和合并表明项目正在积极建设国际化生态，降低非英语用户的使用门槛。新贡献者可以从翻译入手。
    - 待合并 PR：[#3261 - zh-TW locale](https://github.com/sipeed/picoclaw/pull/3261)
    - 已合并 PR：[#3247 - Czech translations](https://github.com/sipeed/picoclaw/pull/3247)
- **渠道功能增强：** 虽然 [Issue #3201](https://github.com/sipeed/picoclaw/issues/3201) (QQ 频道流式输出) 已关闭，但它反映了用户对即时反馈体验的普遍诉求。未来可能在其他未支持流式输出的渠道（如 Discord）上推进类似功能。

### **7. 用户反馈摘要**

- **正面反馈（间接）：** 社区贡献者（如 `corporatepiyush`）持续投入大量的优化性代码，表明项目的代码库具备良好的可维护性和潜在吸引力。
- **负面痛点：**
    - **UI 性能问题：** 用户 `@Acdfmwaopuio` 报告了严重的 Web 前端性能问题（Issue #3292），聚焦输入框就导致 CPU 飙升，直接降低了核心聊天体验。
    - **历史记录体验不佳：** 用户 `@EverestSnow` 对消息压缩算法影响用户界面表示困扰（Issue #2796），认为压缩应该对用户透明。
    - **渠道功能差异：** 用户 `@YsLtr` 反馈 QQ 频道缺少流式输出支持（Issue #3201），导致体验落后于 Telegram 和 WebSocket 渠道。

### **8. 待处理积压**

- **高关注度 PR 待合并：**
  - **[PR #3261](https://github.com/sipeed/picoclaw/pull/3261): Add zh-TW locale and Traditional Chinese translations.** 该 PR 已存在多日且标记为 `stale`，建议维护者尽快审核或合并，以保持社区贡献者的积极性，并完善国际化工作。
- **新 Bug 待处理：**
  - **[Issue #3292](https://github.com/sipeed/picoclaw/issues/3292): CPU usage too high when focus on input box.** 这是直接影响用户体验的质量问题，建议优先分配资源进行复现和排查。

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

**QwenPaw 项目动态日报 (2026-07-25)**  
*数据覆盖：2026-07-24 ~ 2026-07-25*

---

### 1. 今日速览

过去 24 小时项目社区保持高度活跃：共跟进 **48 条 Issue**（新开/活跃 26，关闭 22）和 **36 条 PR**（待合并 23，已合/关 13）。**v2.0.1 正式版**发布，引入 PawApp 插件平台及内置看板应用；同时 **v2.0.1-beta.3** 带来了控制台性能优化。用户对 v2.0 系列的功能缺失（#5980）和性能回归（#6307）讨论最为集中，功能请求涵盖 RAG、多模型协作、桌面自动化等方向，表明项目正从聊天工具向全能 Agent 平台演进，但稳定性和兼容性仍需加强。

---

### 2. 版本发布

#### v2.0.1  
- **新增内容**  
  - **PawApp 平台 & SDK**：提供插件构建丰富交互 UI 的能力，伴随内置看板（Kanban）应用用于项目管理（PR #6150）。  
  - 版本号正式 bump 至 v2.0.1（PR #6404）。  
- **破坏性变更 / 迁移注意**  
  未明确说明，但 #5980 等用户报告显示 v2.0 系列部分旧功能（SSH Offline、配置 Profile 404）不兼容，建议升级后核对相关配置。  

#### v2.0.1-beta.3  
- 修复/优化：稳定对话选项记忆（memo），减少 SSE 重新解析（PR #6393）。  
- 版本号同步更新（PR #6404）。  

> 两个版本均已发布，beta 版可视为向正式版的过渡，正式版用户如遇稳定性问题可尝试降级或参考社区 Issue 反馈。

---

### 3. 项目进展

今日有 **13 个 PR 被合并/关闭**，重要合并包括：

- **#6118 – Zalo Bot 频道**（已合并）  
  新增越南 Zalo 社交平台集成，采用长轮询无需公网 Webhook，扩展渠道生态。  
- **#5698 – 工具 `run_tool_batch` 适配 AgentScope 2.0**（已合并）  
  完成核心工具批量执行功能的迁移，并添加控制流原语支撑复杂工作流。  
- **#6396 – 侧边栏 Inbox 抖动动画**（已合并）  
  新审批到达时菜单抖动并色标提醒，提升通知可见性。  

此外，多个重量级 PR 处于审核中（见功能请求部分），项目在平台化、多 Agent、桌面自动化等方向的路线图清晰。

---

### 4. 社区热点

| 议题 | 评论数 | 核心诉求 |
|------|--------|----------|
| [#5980 – v2.0.0 Missing features: SSH Offline, Profiles 404](https://github.com/agentscope-ai/QwenPaw/issues/5980) | **7** | v1.x 功能在 v2.0 完全不可用（404），工作流受阻 |
| [#6307 – v2.0 固定 ~2s 对话延迟](https://github.com/agentscope-ai/QwenPaw/issues/6307) | **7** | 架构变化导致每轮对话额外加 2s 开销，独立于模型推理 |

**分析**  
升级用户反馈最为激烈，问题集中在功能兼容性和性能。前者需要官方确认是否计划补回或提供替代方案；后者若为框架级开销则需优化请求流水线。这两个 Issue 最能反映当前社区对 v2.0 的总体满意度的瓶颈。

---

### 5. Bug 与稳定性

按严重程度排列，部分标注是否有修复 PR：

| 严重等级 | Issue | 描述 | 已有修复 PR |
|----------|-------|------|-------------|
| **严重 - 数据丢失/功能不可用** | [#6401](https://github.com/agentscope-ai/QwenPaw/issues/6401) 定时任务覆盖用户会话历史（**已关闭**，需验证修复有效性） | – |
| | [#5980](https://github.com/agentscope-ai/QwenPaw/issues/5980) SSH Offline、Profiles 404，核心特性缺失 | 未 |
| | [#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405) Docker 版 MCP Tool not found 持续报错 | 未 |
| | [#6407](https://github.com/agentscope-ai/QwenPaw/issues/6407) ReAct Agent 上下文 `tool_result` 混入 `role:assistant`，导致 OpenAI API 400 | 未 |
| **高 - 性能/稳定回归** | [#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) 2s 固定对话延迟（回归） | 未 |
| **中 - 功能异常** | [#2999](https://github.com/agentscope-ai/QwenPaw/issues/2999) MCP 重复注册导致 `list_tools()` 被外部取消（长期未修） | 未 |
| | [#6258](https://github.com/agentscope-ai/QwenPaw/issues/6258) OpenAI 最大输出 token 配置不生效 | 未 |
| | [#6458](https://github.com/agentscope-ai/QwenPaw/issues/6458) 定时任务安全检查默认关闭（可绕过） | 未 |
| **低 - 体验/UI** | [#6341](https://github.com/agentscope-ai/QwenPaw/issues/6341) 删除频道后新建 agent 默认仍指向已删频道 | 未 |
| | [#6457](https://github.com/agentscope-ai/QwenPaw/issues/6457) 任务模式历史记录中出现非预期对话 | 未 |

今日提交的修复 PR 主要面向局部场景：  
- [#6409 fix(local-models): 过滤非对象 tool_call JSON](https://github.com/agentscope-ai/QwenPaw/pull/6409)  
- [#6410 fix(providers): Gemini 空 schema 带 title 的分支处理](https://github.com/agentscope-ai/QwenPaw/pull/6410)  
- [#6412 fix(shell): Windows PowerShell 保留多行命令](https://github.com/agentscope-ai/QwenPaw/pull/6412)  

但上述高严重级别的 Bug 仍缺少绑定修复，维护者需优先响应。

---

### 6. 功能请求与路线图信号

今日涌现大量高质量功能提案，社区对项目定位的期望远超聊天层面：

**呼声强烈的新功能**  
- **内置 RAG 知识库**：[#6432](https://github.com/agentscope-ai/QwenPaw/issues/6432)  
- **/undo 重新编辑上一条对话**：[#6408](https://github.com/agentscope-ai/QwenPaw/issues/6408)  
- **一个 Agent 使用多个模型并行跑**：[#6455](https://github.com/agentscope-ai/QwenPaw/issues/6455)  
- **Agent 级 Token 统计**：[#6392](https://github.com/agentscope-ai/QwenPaw/issues/6392)  
- **体验细节**：选中文字“复制”菜单、中文文件名保持、多模态提示优化（#6454 #6453 #6452）

**系列设计提案**  
用户 @Hazemaen 提交了十几条 feature，包括画图、翻译、笔记、OCR、并行 Sub-Agent、MCP 一键安装、多用户支持等，全部标注 `Close-and-review-later`。这表明官方有意向但当前排期靠后，可视为长期路线图的一部分。

**正在审核的 PR 信号**  
- [#6397 – 集成 Codex/Qoder 等第三方 Agent](https://github.com/agentscope-ai/QwenPaw/pull/6397)  
- [#6424 – 原生桌面 GUI 自动化 (Windows/macOS)](https://github.com/agentscope-ai/QwenPaw/pull/6424)  
- [#6276 – 统一浏览器控制 SDK](https://github.com/agentscope-ai/QwenPaw/pull/6276)  
- [#6284 – 视频创作 App（PawApp Creator）](https://github.com/agentscope-ai/QwenPaw/pull/6284)  
- [#6323 – Scroll 分阶段 compaction 与持久任务连续性](https://github.com/agentscope-ai/QwenPaw/pull/6323)  

综合来看，QwenPaw 下一阶段重点将在 **平台化（App/PawApp）、多 Agent 协作、原生自动化与上下文管理** 上。

---

### 7. 用户反馈摘要

- **升级阵痛明显**：多位用户反映 v2.0 砍掉了 v1.x 的关键功能（#5980 “critical for my workflow”），且新引入的固定延迟严重影响日常使用（#6307 “independent of model latency”）。  
- **数据安全担忧**：定时任务覆盖历史记录（#6401）导致用户会话丢失，引发信任警觉。  
- **MCP 稳定性成瓶颈**：Tool not found（#6405）和长期未修的注册取消问题（#2999）使得 MCP 集成不可靠，降低生态可用性。  
- **体验细节差距**：对比 Cherry Studio、ChatGPT 等竞品，用户对无法撤回消息（#6408）、无法一键复制选中文字（#6454）、文件中文名被替换（#6453）等细节感到不便。  
- **积极的一面**：用户对项目抱有很高期望，希望 QwenPaw 成为“All-in-One”个人助手，主动提出大量新特性并愿意贡献 PR（#6446 #6447 等均勾选贡献意向）。

---

### 8. 待处理积压

| 类别 | 标识 | 描述 | 积压时间 |
|------|------|------|----------|
| **长期 Bug** | [#2999](https://github.com/agentscope-ai/QwenPaw/issues/2999) | MCP 重复注册导致 CancelledError，影响 MCP 稳定性 | 自 2026-04-06（>3 月） |
| **严重功能回归** | [#5980](https://github.com/agentscope-ai/QwenPaw/issues/5980) | v2.0 SSH Offline、Profiles 404，核心功能缺失 | 自 2026-07-12（13 天） |
| **PR 等待 Review** | [#5692](https://github.com/agentscope-ai/QwenPaw/pull/5692) | 记忆搜索添加 reranker 后端（配合 #6399 UI） | 自 2026-07-01（24 天） |
| **长期 feature 等待决策** | [#2999 系列 → 多条 Close-and-review-later](https://github.com/agentscope-ai/QwenPaw/issues?q=label%3AClose-and-review-later+) | Hazemaen 等多用户提交的平台级功能提案 | 今日批量关闭/打标，建议维护者按优先级梳理纳入规划 |

> 建议项目团队尽快为 #5980、#6307 分配负责人，并评估是否在 v2.0.2 中回归受影响的功能，以稳定社区信心。

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>AstrBot</strong> — <a href="https://github.com/AstrBotDevs/AstrBot">AstrBotDevs/AstrBot</a></summary>

好的，AstrBot 项目分析师已就位。以下为根据您提供的 GitHub 数据生成的 2026-07-25 项目动态日报。

---

## AstrBot 项目日报 - 2026-07-25

### 1. 今日速览

项目整体处于 **极高活跃度** 状态。过去24小时内，社区贡献力度强劲，共关闭/合并了 **13** 个 PR 和 **8** 个 Issue，显示出核心团队与社区协作的效率和响应能力。同时，新提出的 **9** 个 Issue 和 **9** 个待合并 PR 表明项目仍在快速迭代和解决用户反馈。尽管今日无新版本发布，但在 **Bug 修复**（如 Checkpoint 丢失、屏蔽词绕过、平台兼容性）和 **功能完善**（如上下文压缩、指令组重构）方面取得了显著进展。需重点关注的是 **WebUI 加载失败** 和 **插件与核心隔离架构** 等长期或关键性问题。

### 2. 版本发布

无。

---

### 3. 项目进展

过去24小时，项目通过合并修复与特性 PR，在稳定性和功能体验上迈进了一步。以下是部分重要合并/关闭的 PR：

- **修复 LLM 请求失败后的重试问题** ([PR #9359](https://github.com/AstrBotDevs/AstrBot/pull/9359))：解决了当上游模型返回异常时，点击重试按钮提示 `Linked checkpoint not found` 的问题。现在失败后会正确保留历史记录和检查点，允许用户重试。
- **修复 QQ 官方平台 @提及 在主送消息中失效** ([PR #9362](https://github.com/AstrBotDevs/AstrBot/pull/9362))：解决了 `send_message_to_user` 工具在 QQ 官方平台无法正确渲染 @提及 的问题，现已能正常产生真正的 @提及。
- **修复屏蔽词可通过引用绕过** ([PR #9232](https://github.com/AstrBotDevs/AstrBot/pull/9232))：增强了内容安全检查机制，现在会检测被引用消息中的文本，修补了安全策略的漏洞。
- **修复 Tavily 搜索参数冲突** ([PR #9234](https://github.com/AstrBotDevs/AstrBot/pull/9234))：当同时提供 `time_range` 和 `start_date/end_date` 时，Tavily API 会返回 400 错误。此修复优先使用明确的日期参数，解决了冲突。
- **修复嵌入批处理结果顺序** ([PR #9241](https://github.com/AstrBotDevs/AstrBot/pull/9241))：修复了并发批量请求导致嵌入结果顺序错乱的问题，确保数据一致性。
- **防止 AI 人格编辑器意外关闭** ([PR #9238](https://github.com/AstrBotDevs/AstrBot/pull/9238))：解决了点击编辑器外部区域会丢失未保存编辑进度的问题，优化了用户体验。
- **兼容 Spark Lite 模型** ([PR #9243](https://github.com/AstrBotDevs/AstrBot/pull/9243))：为讯飞星火 Lite 模型添加了 OpenAI 兼容适配，移除了该模型不支持的功能调用字段。
- **其他合并项**：还包括 FAISS 懒加载修复 ([#9350](https://github.com/AstrBotDevs/AstrBot/pull/9350))、Dashboard CPU 统计修复 ([#9367](https://github.com/AstrBotDevs/AstrBot/pull/9367))、插件配置保存状态提示 ([#9327](https://github.com/AstrBotDevs/AstrBot/pull/9327)) 等，体现了项目在性能优化和细节打磨上的持续工作。

---

### 4. 社区热点

- **【架构提案】插件与核心隔离架构** ([Issues #3210](https://github.com/AstrBotDevs/AstrBot/issues/3210))：该 RFC 已有 **10条评论** 和 **15个 👍**，是社区最关注的核心议题。讨论围绕如何解决插件依赖冲突和安全问题，参考了成熟的沙箱模型。这反映了随着插件生态壮大，社区对系统稳定性和安全性的诉求日益强烈。

- **【高关注度 Bug】WebUI 加载失败** ([Issues #9297](https://github.com/AstrBotDevs/AstrBot/issues/9297))：有 **7条评论**，多位用户报告了白屏和 `MIME type` 错误问题。尽管开发者提供了建议，但问题仍未完全解决，成为影响新用户上手的首要痛点。

- **【功能请求】Telegram 平台长文转图片优化** ([Issues #9353](https://github.com/AstrBotDevs/AstrBot/issues/9353))：用户建议使用 Telegraph 代替 t2i 模块，以解决图片压缩导致文字模糊的问题。此提议引发了关于跨平台信息呈现方式的讨论，反映了用户对高质量交互体验的追求。

---

### 5. Bug 与稳定性

**严重**

- **FAISS 向量索引维度不匹配** ([Issues #9375](https://github.com/AstrBotDevs/AstrBot/issues/9375))：配置使用自动维度 (`embedding_dimensions: 0`) 时，FAISS 未能正确获取 `qwen3-embedding-8b` 等模型的维度（4096），导致 `AssertionError`。此问题直接影响知识库检索功能，暂无关联修复 PR。
- **群聊空提及等待器截获他人消息** ([Issues #9377](https://github.com/AstrBotDevs/AstrBot/issues/9377))：`session_waiter` 仅以群会话作为标识，导致同群其他成员的消息被错误截获。此问题严重干扰群聊体验，已有对应的修复 [PR #9378](https://github.com/AstrBotDevs/AstrBot/pull/9378) 待合并。

**中等**

- **WebUI 加载失败** ([Issues #9297](https://github.com/AstrBotDevs/AstrBot/issues/9297))：核心问题定位在 WebUI 静态文件 `dist` 目录缺失或 MIME 类型错误，是影响面最广的 Bug 之一，持续引发社区讨论。
- **引用 GIF 污染会话历史** ([Issues #9295](https://github.com/AstrBotDevs/AstrBot/issues/9295))：引用动态 GIF 图会导致部分不支持该格式的多模态模型持续报错。已有修复 [PR #9335](https://github.com/AstrBotDevs/AstrBot/pull/9335) 待合并，通过在上下文清理器中过滤不支持的 MIME 类型来解决。

**轻微**

- **QQ 官方机器人回复首位字符被随机截断** ([Issues #9368](https://github.com/AstrBotDevs/AstrBot/issues/9368))、**WebUI 套娃滚动条** ([Issues #9361](https://github.com/AstrBotDevs/AstrBot/issues/9361))、**网页搜索自动关闭** ([Issues #9372](https://github.com/AstrBotDevs/AstrBot/issues/9372)) 等，均为影响特定场景或 UI 体验的轻微问题，尚无对应修复。

---

### 6. 功能请求与路线图信号

- **Telegram 长文支持 Telegraph** ([Issues #9353](https://github.com/AstrBotDevs/AstrBot/issues/9353))：用户提议使用 Telegraph 发布长文，以绕过图片压缩问题。该建议直接关联到消息平台适配层的体验优化，可能会被纳入后续的平台功能迭代计划。
- **插件独立 Logger** ([Issues #9186](https://github.com/AstrBotDevs/AstrBot/issues/9186))：请求为插件提供独立 Logger，以便插件作者控制自身日志等级。这是社区对开发友好性提出的明确信号，能有效降低插件开发和调试的噪音。
- **QQ 平台“正在输入中……”状态** ([Issues #9363](https://github.com/AstrBotDevs/AstrBot/issues/9363))：提升用户等待回复的耐心，属于体验优化类需求，实现起来相对独立，可能被社区开发者快速实现。

---

### 7. 用户反馈摘要

- **正面反馈**：用户在插件提交 ([Issues #9373](https://github.com/AstrBotDevs/AstrBot/issues/9373)) 中主动分享新插件，社区对开发 `session_waiter` 修复 ([PR #9378](https://github.com/AstrBotDevs/AstrBot/pull/9378)) 的讨论显示出用户对平台机制的深入理解，表明社区开发者技术能力强且乐于贡献。
- **负面/痛点反馈**：
    - **安装体验不顺**：多个用户在 WebUI 加载失败 ([Issues #9297](https://github.com/AstrBotDevs/AstrBot/issues/9297)) 中反映即使按照开发者提供的方案也难以解决问题，表明文档或部署流程存在盲区。
    - **功能不稳定**：用户对“网页搜索自动关闭” ([Issues #9372](https://github.com/AstrBotDevs/AstrBot/issues/9372)) 和“上游模型异常后重试失败” ([Issues #9358](https://github.com/AstrBotDevs/AstrBot/issues/9358)) 等现象表示困扰，这些偶发性问题影响了用户对机器人稳定性的信心。
    - **基础功能缺陷**：QQ群聊中的空提及问题 ([Issues #9377](https://github.com/AstrBotDevs/AstrBot/issues/9377)) 和引用GIF崩溃 ([Issues #9295](https://github.com/AstrBotDevs/AstrBot/issues/9295)) 触及了核心消息处理逻辑，尽管已有修复 PR，但用户暴露出的问题场景值得在后续测试中加强覆盖。

---

### 8. 待处理积压

- **[RFC] AstrBot Plugin and Core Isolation Architecture** ([Issues #3210](https://github.com/AstrBotDevs/AstrBot/issues/3210))：创建于近一年前的核心架构提案，虽然昨日仍有更新，但进展缓慢。该项目对插件生态的未来发展至关重要，建议维护者积极跟进，明确采纳时间线或结论。
- **[Bug] WebUI加载失败** ([Issues #9297](https://github.com/AstrBotDevs/AstrBot/issues/9297))：自 7月15日 提出以来，已持续近10天，且用户反馈热情高、问题尚未彻底解决。作为影响新用户的第一印象阻塞性问题，应优先彻底修复并更新相关文档。
- **[Bug] 引用 GIF 会污染会话历史** ([Issues #9295](https://github.com/AstrBotDevs/AstrBot/issues/9295))：尽管已有修复 [PR #9335](https://github.com/AstrBotDevs/AstrBot/pull/9335)，但该 PR 自 7月20日 提出后尚未合并。此问题影响多模态模型体验，建议加快审核与合并流程。

</details>

---
*本日报由 [Big Model Radar](https://github.com/huajiao1998/big_model_radar) 自动生成。*