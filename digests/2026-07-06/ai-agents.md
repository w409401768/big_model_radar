# OpenClaw 生态日报 2026-07-06

> Issues: 500 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-05 22:52 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 (2026-07-06)

> *数据统计时段：2026-07-05 00:00 UTC — 2026-07-05 23:59 UTC*

---

## 1. 今日速览

- **极高活跃度**：过去 24 小时内，项目完成了 500 条 Issue 和 500 条 PR 的更新，其中 131 个 PR 已被合并/关闭，49 个 Issue 被关闭，维护和交付效率位于高位。
- **新版本**：发布 `v2026.7.1-beta.2`，主要带来 OpenAI GPT-5.6 模型支持和外部 Harness 挂载能力。
- **核心贡献者活跃**：@steipete 主导提交了 10 项小型可靠性修复（#100483）及多项 UI 功能增强 PR，项目正在从“功能扩张期”转入“稳定性加固期”。
- **隐患仍然突出**：会话 OOM、内存泄漏、安全性回归（提词注入、文件越权）等 P0/P1 级别 Bug 仍集中在最前列，修复 PR 整体有待推进合入。

---

## 2. 版本发布

### v2026.7.1-beta.2

- **OpenAI GPT-5.6 支持**：OpenClaw 正式在目录、能力检测和运行时选择路径中识别 GPT-5.6 模型家族。这也意味着 `gpt-5-nano` 等模型将被正确路由。
  - 关联 PR: [#98333](https://github.com/openclaw/openclaw/pull/98333) @steipete-oai
- **外部 Harness 挂载**：新增 `openclaw attach` 命令，支持为正在运行的 Gateway 会话动态挂载外部 harness 进程，对调试和生产监控形态有利。

> **迁移注意事项**：暂无明确 breaking changes，但使用旧版 Cron 逻辑（`payload.kind=agentTurn`）的用户需注意 [#63918](https://github.com/openclaw/openclaw/issues/63918) 中 “thinking” 参数兼容性问题。建议升级后全面回归 Cron 任务路径。

---

## 3. 项目进展

| 维度 | 核心进展 |
|------|----------|
| **核心修复合并** | `#97052 @harjothkhara` 关闭：修复 Gateway 启动时插件媒体目录因携带 video/audio 模态导致会话注册表失败的 Bug，对多媒体交互场景至关重要。 |
| **跨平台加固** | @steipete 的 `#100483（10项可靠性修复合辑）` 进入预合并阶段，覆盖 LSP、Docker、Android、iOS 等边界场景。 |
| **UI 功能推进** | 三项大型 UI 功能 PR 提交并进入审核：`#100434`（GitHub Issue/PR 悬停预览）、`#100386`（Codex 极简侧栏）、`#100432`（对比成本分析），标志着 Control UI 从基础交互走向运营级能力。 |
| **本地模型生态** | `#100482 @TurboTheTurtle`：Ollama 流式断连时自动降级到后备模型，而非永久卡住。 |
| **Cron 稳定性** | `#99724`：修复 hot reload 下 on-exit watch 被重复触发/中断的竞争条件。 |
| **Channel 增强** | `#96864` 等 Signal 频道系列 PR（上下文溯源、提及属性暴露）正推进多人群聊消息精确路由能力。 |

> 以上 PR 均处于 Open 状态待合入，预计将在未来 1–2 个 alpha/beta 版本中陆续合并。

---

## 4. 社区热点

| 议题 | 热度指标 | 核心诉求 |
|------|----------|----------|
| [#98416](https://github.com/openclaw/openclaw/issues/98416) 正式发布版丢失重入守卫 | 16 评论 / 5 👍 | 用户 @yaaboo-gif 发现 `v2026.6.11` 未包含关键 `reentrant: true` 修复，导致回复会话初始化阶段并发冲突。社区对“发布版本质控失败”表达了强烈不满。 |
| [#96857](https://github.com/openclaw/openclaw/issues/96857) 工具文本输出退化为图片占位符 | 9 评论 / 3 👍 | 用户 @cael-dandelion-cult 报告普通工具输出（`stdout`）被替换为 `(see attached image)`，导致 Agent 对自身工具输出“失明”。触及 AI Agent 可解释性底线。 |
| [#58450](https://github.com/openclaw/openclaw/issues/58450) Agent 承诺后续操作但实际未执行 | 15 评论 / 3 👍 | Agent 对用户说“我去检查项目记忆稍后回来”，但未真正启动任何后台子进程，本质上等同于“虚假承诺” —— 用户对 Agent 信任度高度敏感。 |
| [#50090](https://github.com/openclaw/openclaw/issues/50090) ClawHub 技能生态长期搁置 | 15 评论 / 2 👍 | 用户 @ocdlmv1 直言“承诺与现实的鸿沟很宽”。社区对技能市场安全审核和开发者体验有极高期待，但目前处于产品决策停滞状态。 |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) AgentDir 引导文件完全失效 | 14 评论 / 5 👍 | 安全高度敏感的 P1 问题，配置引导文件（SOUL.md 等）被静默忽略。至今无对应修复 PR，社区反馈强烈。 |

---

## 5. Bug 与稳定性（按严重程度排列）

### P0 — 发布阻断

| Issue | 关键问题 | 点评 |
|-------|----------|------|
| [#48920](https://github.com/openclaw/openclaw/issues/48920) | **文档领先于发布**：`IsolatedSessions` 文档中存在但实际版本不存在，直接导致用户配置报错。 | 属于发布流程断裂，影响用户信任，需紧急统一。 |

### P1 — 严重（会话/数据丢失/安全/崩溃）

| Issue | 影响面 | 是否有 Fix PR |
|-------|--------|---------------|
| [#98416](https://github.com/openclaw/openclaw/issues/98416) 正式版缺少重入守卫 | 回复会话初始化冲突，会话损坏 | **尚无**（已标记为 `fix-shape-clear, needs-maintainer-review`） |
| [#55334](https://github.com/openclaw/openclaw/issues/55334) sessions.json 无限增长导致 OOM | 内存占用 50–100MB/分钟，直至 OOM | **尚无**（待产品决策） |
| [#54155](https://github.com/openclaw/openclaw/issues/54155) Gateway 内存泄漏 | 4 天从 389MB 膨胀到 14.7GB | **尚无**（需 live-repro） |
| [#64810](https://github.com/openclaw/openclaw/issues/64810) 心跳吞掉 Telegram 进行中回复 | Telegram 用户视角丢消息 | **尚无** |
| [#69118](https://github.com/openclaw/openclaw/issues/69118) Claude CLI 群组会话每轮重置 | 群聊场景完全不可用 | **尚无** |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) gh-issues 技能注入（RCE 风险） | 第三方 Issue 正文可直接注入 Agent 提示 | **尚无**（标记 `needs-security-review`） |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) AgentDir 配置引导文件无效 | 安全配置不生效 | **尚无** |
| [#54531](https://github.com/openclaw/openclaw/issues/54531) 回复未能返回源消息频道 | 消息滞留 Gateway UI 不抵达用户 | **尚无** |
| [#49876](https://github.com/openclaw/openclaw/issues/49876) Cron 在工具失败时依然产生幻觉输出 | 虚假数据流向用户 | **尚无** |
| [#45224](https://github.com/openclaw/openclaw/issues/45224) Playwright 未捕获断言导致整个 Gateway 进程退出 | 进程级 Crash | **尚无** |
| [#45494](https://github.com/openclaw/openclaw/issues/45494) Cron 在 LLM API 故障时不会快速失败 | 每个请求等足 180s 超时 | **尚无** |

### P2/P3 — 值得关注

| Issue | 问题 |
|-------|------|
| [#51429](https://github.com/openclaw/openclaw/issues/51429) | 硬编码用户 `wangtao` 的工作区路径到代码库并发布，社区形象影响恶劣。 |
| [#63918](https://github.com/openclaw/openclaw/issues/63918) | Cron 向 GPT-5-nano 发送不支持的 `thinking=none`。 |
| [#50490](https://github.com/openclaw/openclaw/issues/50490) | 飞书群聊 `/activation mention` 切换无效回归。 |
| [#96857](https://github.com/openclaw/openclaw/issues/96857) | 工具文本输出退化为 `(see attached image)` 占位符。 |
| [#53486](https://github.com/openclaw/openclaw/issues/53486) | 飞书卡片 JSON 渲染回归为纯文本。 |
| [#48949](https://github.com/openclaw/openclaw/issues/48949) | 飞书在 HTTP 代理环境下 `tenant_access_token` 完全无法解析。 |

---

## 6. 功能请求与路线图信号

### 高频呼声——有望纳入近期路线图

- **安全防御体系**：
  - `#7707`（Memory Trust Tagging by Source）：防止第三方技能污染 Agent 记忆。
  - `#7722`（Filesystem Sandboxing Config）：让 `tools.fileAccess` 真正生效。与 #7707 并列为生产部署核心安全功能。
  - `#50090`（ClawHub 技能安全审核机制）：社区技能生态的前提条件。
- **群聊/频道增强**：
  - `#47677`（Telegram Reaction Triggers）：将 Reaction 变为一等触发源。
  - `#50093`（WhatsApp Messages Backfill）：重连后补偿丢失消息。
  - `#54531`（强制回复源频道）：解决消息滞留不送达的问题。
- **成本与运营**：
  - `#33975`（Fallback Approval Mode + Model Attribution）：模型回退时通知用户并显示使用模型。
  - `#45565`（Lifecycle Warnings 路由到专有频道）：避免系统告警淹没对话。
  - `#50739`（System Event Priority Queue）：高优先级绕过拥塞队列直插会话流。

### 基于近期 PR 的技术方向判断

| PR | 方向 | 下个版本可能性 |
|----|------|--------------|
| `#100434` GitHub Issue/PR 悬停预览 | Control UI 深度集成 GitHub 工作流 | **高** |
| `#100432` 对比成本分析面板 | 模型运营可见性 | **高** |
| `#100386` Codex 风格侧栏 | UI 现代化重构 | **高** |
| `#96863 / #96862 / #96864` 源角色属性 + 提及上下文 | 多参与者频道消息元数据基础设施 | **中高**（影响内存、工具链架构） |
| `#100481` 精简 Skill Workshop Prompt 段 | Token 成本优化，提示契约化 | **高**（无兼容风险） |
| `#88881` Lean 模式裁剪媒体工具 | 本地小模型可用性提升 | **中**（等待作者更新） |

---

## 7. 用户反馈摘要

### 高频痛点

1.  **“我配置的东西不生效”**：
    - 用户是配置驱动的，但 `#29387`（AgentDir 文件静默忽略）、`#53628`（XDG_CONFIG_HOME 不解析）、`#57901`（compaction.model 配置被无视）让技术用户反复踩坑。
    - 用户 @tuna-chin（#29387）直接提问：“是不是 developer 搞错了目录优先级的逻辑？”

2.  **“数据丢了 / Agent 乱说”**：
    - `#98416` 中用户发现正式版缺少关键 reentrancy patch，表示“刚升级就回退”。
    - `#96857` 中用户惊讶于正常 `stdout` 被替代为“see attached image”——用户质疑是否自己的对话被非预期截断。
    - `#50093` 和 `#54531` 表明频繁断连的生产环境下消息丢包是严重的信任断层。

3.  **安全性关注**：
    - #45740 用户指出 gh-issues `body` 直接注入 sub-agent 提示，被定性为“untrusted data → arbitrary code execution”。用户 @zients 在摘要结尾用表情或语气表达了担忧。
    - #51396 和 #57326 涉及 token-auth / CLI dispatch 被绕过，存在越权可能。

### 满意度亮点

- 用户对新模型（GPT-5.6）的即时支持表示欢迎。
- @steipete 的连续 PR 获得隐性的社区信任（没有直接赞扬评论但多个 PR 被迅速打上“ready for maintainer look”标签）。
- `#100482`（Ollama 回退修复）获取到真实用户场景的直接反馈，社区贡献者和最终用户之间的互动在提速。

---

## 8. 待处理积压

### 🔴 高危安全/架构 Issue——长期未关闭

| Issue | 提出时间 | 标签 | 当前状态 |
|-------|----------|------|----------|
| [#50090](https://github.com/openclaw/openclaw/issues/50090) ClawHub 安全审核 | 2026-03-19 | **impact:security, needs-product-decision** | 3个月无实质推进，技能生态停滞 |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) AgentDir 引导文件失效 | 2026-02-28 | **P1, impact:security** | 有 `fix-shape-clear` 标记但无 Fix PR，P1 空转 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) Memory Trust Tagging | 2026-02-03 | **P2, impact:security** | 5个月无进展，评级过低 |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) Filesystem Sandboxing | 2026-02-03 | **P2, impact:security** | 同 #7707，社区用户 @LumenLantern 反复呼吁 |

### 🟡 长期未合入但价值显著的 PR

| PR | 提出日期 | 阻塞原因 |
|----|----------|----------|
| [#89419](https://github.com/openclaw/openclaw/pull/89419) `fix(config): allow explicit main agent bindings` | 2026-06-02 | P1，标注 **needs-real-behavior-proof**，维护者未回应。 |
| [#89454](https://github.com/openclaw/openclaw/pull/89454) `fix(feishu): resolve exec/keychain appSecret SecretRefs` | 2026-06-02 | P1，飞书渠道 blocker，已就绪但未合并。 |
| [#90450](https://github.com/openclaw/openclaw/pull/90450) `fix(agents): preserve streamed assistant text when Claude CLI result event is empty` | 2026-06-04 | P1，等待作者更新（status: waiting on author）。 |

### 🟠 需立即关注

- **`#48920`（P0, 文档领先发布）**：这是一个流程问题——即使有 `IsolatedSessions` 的开发分支文档，正式版发布前必须同步降级或标记为 unstable。目前社区用户被误导配置后报错，流程需改进。

---

*本报告由 OpenClaw 社区数据驱动生成，所有链接基于 2026-07-05 快照；项目动态频繁，请以 GitHub 实时页面为准。*

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告
**数据快照：2026-07-06**

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正在从 **“功能扩张期”** 全面转向 **“稳定性加固与运营能力构建期”**。各项目普遍保持极高社区活跃度，但分化明显：头部项目（hermes-agent、OpenClaw）着力于平台级可靠性与多智能体编排，中间层（ZeroClaw）陷入“高产但低效消化”的瓶颈期，而细分项目（QwenPaw、PicoClaw）专注于特定市场（飞书/中国企业、嵌入式/轻量级）的深度打磨。**安全防御体系的系统化构建和记忆子系统的架构升级**是贯穿全生态的两条主线，且社区对“配置即契约”的可靠性和“开箱即用”的体验要求达到了前所未有的高度。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭数 | 新版本 | 健康度评估 | 核心阶段 |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 条 | 500 条 | 131 PR / 49 Issues | **v2026.7.1-beta.2** | 产出极高，但严重 Bug 积压 | 稳定性加固期 |
| **ZeroClaw** | 23 条 | 50 条 | 7 PR | 无 | **PR 审查瓶颈严重**，贡献者疲劳风险高 | 高审查压力期 |
| **PicoClaw** | 2 条 | 5 条 | 1 PR | 无 | 健康聚焦，社区驱动闭环优秀 | 精细修复期 |
| **QwenPaw** | 12 条(新) | 5 条(新) | 0 | 无 (v1.1.12.post2) | 管道健康，维护响应积极 | 功能与修复并行期 |
| **hermes-agent** | 326 条 | 500 条 | 138 PR | 无 | **整体执行力最强**，稳定性领先 | 生态打磨与质量巩固期 |

---

## 3. OpenClaw 在生态中的定位

**角色：生态中的“标准通用参照系”与“边界探索者”**

- **核心优势：**
  - **广度最大：** 功能覆盖最全（多频道、ClawHub 技能市场、Control UI 运营面板、External Harness），是社区定义个人 AI 网关平台功能边界的基准项目。
  - **社区规模：** 绝对活跃度指标（Issue/PR 总量）居生态之首，贡献者梯队清晰（@steipete 等高产核心贡献者）。
  - **版本迭代激进：** 比所有竞品更快适配 GPT-5.6、外部 Harness 等前沿特性。

- **与同类对比的关键差异：**
  - **vs. hermes-agent：** Hermes 更聚焦于“内核稳定性与执行精度”（DeepSeek 修复、MCP 重连），Bug 修复效率更高，用户信任度更稳健。OpenClaw 功能更丰富但 Bug 债更重（P0 文档领先、P1 丢消息/OOM 等长期悬而未决）。
  - **vs. ZeroClaw：** ZeroClaw 在架构设计上更前瞻（轻量化内核 RFC、WASM 插件、SOP 控制平面），但执行卡在 PR 审查环节；OpenClaw 在执行力上显著领先。
  - **vs. QwenPaw / PicoClaw：** OpenClaw 是通用型平台，而 QwenPaw 深耕中国企业 IM 生态（飞书/通义千问），PicoClaw 专注嵌入式/去中心化场景（Vodozemac、DeltaChat），三者目标用户群重叠度有限。

- **结论：** OpenClaw 是社区 **“功能参照物”**，但若持续无法解决 P0/P1 缺陷的积压，可能导致核心用户向 hermes-agent 等稳定性更强项目迁移。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/表现 |
|---|---|---|
| **🧠 记忆系统架构升级** | **OpenClaw** (#7707 Memory Trust Tagging)、**PicoClaw** (#3226 MEMORY.md 误覆盖修复)、**QwenPaw** (#5777 自动记忆轮次管理)、**hermes-agent** (#47349 可配置记忆后端) | 社区普遍共识：平面文件 `MEMORY.md` 机制已触及天花板，需要结构化、可溯源、持久化的记忆服务。 |
| **🔒 安全防御体系系统化** | **OpenClaw** (#7707/#7722 沙箱/信任标签，#45740 注入 RCE)、**ZeroClaw** (#8727 空 Token 拒绝、#8690 越权鉴权、#8741 路径越权)、**PicoClaw** (#3088 加密库替换) | 从单点漏洞修复转向体系化防御：文件沙箱、提示注入免疫、MCP 鉴权、可信数据溯源。 |
| **⚙️ 多智能体/子任务编排** | **OpenClaw** (AgentDir、Delegation)、**hermes-agent** (#5012/#25386 delegate_task 参数传递、子运行时标准化)、**ZeroClaw** (SOP 控制平面 RFC)、**QwenPaw** (Cron 任务扩展) | 从“单 Agent 对话”走向“工作流引擎”。`delegate_task`、SOP、Cron 组合成为标准能力。 |
| **🌐 工具调用/MCP 可靠性** | **ZeroClaw** (#8731 僵尸进程、#8560 挂起)、**hermes-agent** (#59222 MCP 重连预算/沉降恢复)、**OpenClaw** (#45224 Playwright 导致整个进程退出) | 工具执行不再是“尽力而为”，要求进程级隔离、重连弹性与超时熔断。 |
| **💰 成本与运营可见性** | **hermes-agent** (#18304 成本统计彻底失效)、**OpenClaw** (#100432 对比成本分析面板 PR)、**ZeroClaw** (OTel RFX #8462) | 社区对多模型花费追踪的需求从“锦上添花”变为“生产部署必要条件”。 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | **通用智能体网关 + 技能生态** | 高级开发者、平台运营者 | 重量级单体网关 + ClawHub 市场 + Control UI |
| **ZeroClaw** | **运行时架构与安全** | 系统架构师、DevOps | 强调声明式配置、WASM 沙箱插件、SOP 工作流引擎、OpenAI 适配器网关 |
| **PicoClaw** | **轻量级/嵌入式智能体** | 极客、嵌入式开发者、去中心化支持者 | 小体积核心，优先加密免中心化（Vodozemac + DeltaChat） |
| **QwenPaw** | **中国企业生态集成** | 中国开发者、企业团队 | 深度绑定 Qwen 模型生态 + 飞书/企业微信 IM 集成 |
| **hermes-agent** | **稳定可靠的执行内核** | 生产环境开发者、多模型团队 | 高吞吐 MCP 框架 + 深度多模型路由 + 最精细的稳定性格子 |

---

## 6. 社区热度与成熟度分层

**第一梯队：成熟期（质量巩固 + 高执行力）**
- **hermes-agent：** 社区活跃度最高（500 PR），且维持了最高的合并效率（138 合并/关闭），核心维护者 @teknium1 主导关键修复，总体健康度最优，是当前生态中“最像可投产产品”的项目。
- **QwenPaw：** 虽总量不及 Hermes，但维护响应速度极快（Bug 报出当天即有修复 PR），社区参与质量高（源码级 Debug），在中国市场已形成黏性。

**第二梯队：功能扩展与债务积累并行期**
- **OpenClaw：** 绝对活跃度领先，但 Bug 修复速度跟不上 Bug 产生速度。若不能在未来 1-2 个版本解决 P0/P1 积压，用户信心可能发生拐点。当前处于“高产出、高争议”的焦灼状态。
- **ZeroClaw：** 架构设计最前瞻，但 **43 条 PR 积压** 是项目目前最大的系统性风险。若审查流程不加速，高活跃的社区贡献可能迅速冷却。

**第三梯队：深耕细分市场期**
- **PicoClaw：** 规模最小，但社区协作质量极高（#3150→#3226 的高效联动诊断），在去中心化和轻量级场景下潜力可期。

---

## 7. 值得关注的趋势信号

1. **“记忆即服务”将取代“文件即记忆”：** PicoClaw 的 `MEMORY.md` 误覆盖修复和 hermes-agent 的可配置后端诉求表明，Agent 记忆正在从“一个文本文件”升级为“一个结构化子系统”。未来 3-6 个月内，主流项目将推出内置的向量化/关系化记忆服务 API。

2. **MCP 从“可用”走向“高可用”：** Hermes-Agent 的 MCP 重连预算/沉降恢复机制和 ZeroClaw 的僵尸进程报告，共同指向了工具调用层需要“熔断器”、“重连预算”、“进程隔离”等生产级能力。**“MCP 可运维性”将成为项目下阶段的核心竞争点。**

3. **安全审查不再是“选修课”：** 四个主流项目（OpenClaw、ZeroClaw、PicoClaw、Hermes）在今日快照中均有安全相关严重 Issue 或修复 PR。社区对提示注入（#45740）、鉴权绕越（#8690）、文件越权（#7722）的容忍度已降至冰点。**没有安全体系的个人 AI 智能体将无法进入企业场景。**

4. **“配置即契约”的可靠性要求：** OpenClaw 的 AgentDir 失效（#29387）、ZeroClaw 的模板自带 Bug（#8718）、Hermes 的 `api_key_env` 配置忽略（#44666）——用户反复强调：**“我配置了，就必须生效”**。配置系统的测试覆盖率和防御性编程将是开发者体验的核心壁垒。

5. **中国市场的独特分化：** QwenPaw 与飞书的深度绑定，以及 OpenClaw/ZeroClaw 对飞书/Bocha 的适配，说明中国用户对国内 IM 和企业软件的集成有极强刚需。**“Qwen + Feishu”** 组合正在形成生态护城河，海外项目难以直接渗透。

6. **运营级能力（成本/告警/路由）走到台前：** OpenClaw 提交的成本对比面板（#100432）和生命周期告警路由（#45565），以及 Hermes 成本追踪 BUG（#18304）的高热度，标志社区需求已从“能不能跑”进入“跑得贵不贵、好不好管”。**Agent Ops（AIOps）** 正在成为一个独立的技术栈方向。

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 | 2026-07-06

---

## 1. 今日速览

项目在24小时内迎来 **23条 Issues 更新** 和 **50条 PR 更新**，活跃度处于极高水位，表明社区正密集提交反馈、贡献代码，同时核心维护团队也在积极推动 Bug 修复与特性落地。开发重心显著集中于运行时稳定性（僵尸进程、Agent 挂起）、安全加固（鉴权绕越、敏感环境变量泄露）以及 Gateway 协议标准化（OpenAI 适配器）。**但需高度警惕的是，当前 PR 合并效率严重滞后——50条活跃 PR 中仅 7 条被合并/关闭，43 条处于待合并状态，这构成了社区贡献流程的主要瓶颈，可能导致贡献者热情消退。** 同日无新版本发布，项目处于大量成果等待集结发布前的“高审查压力期”。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

### ✅ 今日合并/关闭的 PR
- **[Security] `fix(gateway): reject empty bearer token in require_auth`** ([#8727](https://github.com/zeroclaw-labs/zeroclaw/pull/8727))  
  合并了防御性安全检查：在 Gateway 鉴权逻辑中增加对空 Bearer Token 的显式拒绝，防止后续绕过。

### ✅ 今日关闭的重要 Issue（部分）
- **RFC: Runtime Policy for OTel LLM and Tool Content** ([#8462](https://github.com/zeroclaw-labs/zeroclaw/issues/8462)) — 已关闭/接受，结构化可观测性策略覆盖 LLM 与工具内容的管控方案定稿。
- **Feature: Surface relationship memory as user-facing workflows** ([#8251](https://github.com/zeroclaw-labs/zeroclaw/issues/8251)) — 关闭，关系型知识图谱的记忆功能完成了面向用户工作流的转型文档化。
- **Bug: Reload banner shows persistent drift for ZEROCLAW_* env-overridden secrets** ([#8645](https://github.com/zeroclaw-labs/zeroclaw/issues/8645)) — 已关闭，环境变量密钥覆盖导致的刷新生效状态漂移问题已被修复。
- **Feature: Surface security-audit-skipped skills** ([#7861](https://github.com/zeroclaw-labs/zeroclaw/issues/7861)) — 已关闭，现在 `zeroclaw skills list` 可以查询被安全审计跳过的技能目录。
- **Feature: add bounded SKILL.md reflection for skill creation** ([#7879](https://github.com/zeroclaw-labs/zeroclaw/issues/7879)) — 已关闭/接受，新增从已执行 Agent 任务自动生成 SKILL.md 的能力。

### 🚧 被阻塞的高价值 PR（待合并）
尽管以上成果已落地，但仍有大量重量级 PR 处于待合并状态，拖累项目整体推进速度：

- **`refactor(zerocode)`: 统合 Code 面板、Rails 与 Prompt Drafts** ([#8655](https://github.com/zeroclaw-labs/zeroclaw/pull/8655)) — 重构大型 ZeroCode 交互界面。
- **`feat(matrix)`: 新增单消息进度草稿模式** ([#8443](https://github.com/zeroclaw-labs/zeroclaw/pull/8443)) — 让 Matrix 渠道支持工具执行进度流式渲染。
- **`feat(skills)`: 默认采用紧凑注入模式** ([#8313](https://github.com/zeroclaw-labs/zeroclaw/pull/8313)) — 优化技能加载性能，默认实现按需读取。
- **`fix(channels)`: 为 /model --agent 命令增加发送者鉴权** ([#8690](https://github.com/zeroclaw-labs/zeroclaw/pull/8690)) — 修复越权设置全局 Agent 模型的严重安全问题。
- **`fix(runtime)`: 强制在 Provider 分发前确保首条用户轮次不变量** ([#8696](https://github.com/zeroclaw-labs/zeroclaw/pull/8696)) — 修复对话上下文截断可能引发的 Provider 调用崩溃。

---

## 4. 社区热点

### 🏛 架构之争：轻量化内核边界
**[RFC] Prefer a lighter ZeroClaw core through external integrations** ([#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165))  
获得 8 条评论，是今日讨论最为热烈的议题。社区各方围绕“哪些集成应被移出核心交由 Skills/MCP/插件托管”展开了密集辩论，这直接关联到项目未来 3-6 个月的架构走向。该 RFC 的高关注度也间接反映出用户对当前核心膨胀的忧虑。

### 💥 稳定性恐慌：僵尸进程与 Agent 挂起
- **[Bug] Stdio-based MCP servers accumulating as zombie processes** ([#8731](https://github.com/zeroclaw-labs/zeroclaw/issues/8731)) — P1 严重度，运行时 Daemon 无法回收终止的 MCP 子进程，长期运行后导致系统资源耗尽。
- **[Bug] browser_open hangs the agent turn** ([#8560](https://github.com/zeroclaw-labs/zeroclaw/issues/8560)) — P1 严重度，无头环境或启动器前台挂起时，Agent 回合被无限阻塞。

这两个 P1 Bug 直击用户核心使用场景（Agent 自动化和工具调用），引发了大量同感留言和复现信息。目前两者均尚无修复 PR 提交，风险持续积累。

### 🔗 生态呼声：OpenAI API 兼容适配器
**[RFC] OpenAI Chat Completions compatibility adapter** ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603))  
作为一个刚提出的 RFC，快速收获社区正面讨论。用户期待通过该适配器直接接入 Open WebUI、LobeChat 等主流客户端，这将是 ZeroClaw 从“独立客户端”走向“通用后端引擎”的关键一步。

---

## 5. Bug 与稳定性

按严重等级排列，突出标注是否有修复 PR 跟进。

| 严重等级 | Issue / PR | 摘要 | 修复 PR 状态 |
|---|---|---|---|
| **🔴 P1 - S2** | [#8731](https://github.com/zeroclaw-labs/zeroclaw/issues/8731) | MCP 僵尸进程累积，无有效回收机制 | ❌ 无修复 PR |
| **🔴 P1 - S1** | [#8560](https://github.com/zeroclaw-labs/zeroclaw/issues/8560) | `browser_open` 在无头环境造成 Agent 挂起 | ❌ 无修复 PR |
| **🔴 P1 - S2** | [#8718](https://github.com/zeroclaw-labs/zeroclaw/issues/8718) | `config init` 模板自带 BUG，导致 `local_whisper` 转录静默失败，影响所有新用户 | ❌ 无修复 PR |
| **🟡 P2 - S2** | [#8733](https://github.com/zeroclaw-labs/zeroclaw/issues/8733) | `models.dev` 目录仅解析模型 ID，丢弃视觉能力等特性标识，导致模型能力检测异常 | ❌ 无修复 PR |
| **🟡 P2 - S2** | [#8722](https://github.com/zeroclaw-labs/zeroclaw/issues/8722) | 高熵检测器将合法的生成文件名误判为 Token 并和谐 | ❌ 无修复 PR |
| **🟡 P2** | [#8720](https://github.com/zeroclaw-labs/zeroclaw/issues/8720) | Bedrock Nova 2 Lite 模型无法关闭 `cachePoint` 功能，随机报错 | ❌ 无修复 PR |
| **✅ 已修复** | [#8645](https://github.com/zeroclaw-labs/zeroclaw/issues/8645) | 环境变量密钥覆盖导致刷新 Banner 漂移 | 已关闭 |
| **✅ 已修复** | [#8727](https://github.com/zeroclaw-labs/zeroclaw/pull/8727) | 空 Bearer Token 鉴权绕越 | 已合并 |
| **⏳ 待合入** | [#8739](https://github.com/zeroclaw-labs/zeroclaw/pull/8739) | 错误上下文丢失（`map_err` 吞噬原始错误） | PR 待合并 |
| **⏳ 待合入** | [#8726](https://github.com/zeroclaw-labs/zeroclaw/pull/8726) | TUI 环境中环境变量泄露风险 | PR 待合并 |
| **⏳ 待合入** | [#8741](https://github.com/zeroclaw-labs/zeroclaw/pull/8741) | 浏览器截图路径越权写入 | PR 待合并 |
| **⏳ 待合入** | [#8725](https://github.com/zeroclaw-labs/zeroclaw/pull/8725) | Webhook 未配置 Secret 时直接启动监听器 | PR 待合并 |
| **⏳ 待合入** | [#8690](https://github.com/zeroclaw-labs/zeroclaw/pull/8690) | `/model --agent` 越权修改全局 Agent 模型 | PR 待合并 |

---

## 6. 功能请求与路线图信号

### 🧭 确定路线图方向
| Feature/ROADMAP | 状态 | 信号解读 |
|---|---|---|
| **轻量化核心（RFC #6165）** | 已接受，进行中 | 确立未来架构方向：长尾集成外迁至 Skills/MCP/Plugin |
| **SOP 控制平面 5/5 (Tracker #8288)** | 实施中 | SOP 正在从简单工作流升格为一等公民特性，拥有 Daemon 控制面和图形编辑器 |
| **Schema V4 破坏性清理 (#8310)** | 开放 | 项目决心清理废弃配置，减轻历史负担，属于重大重构信号 |
| **WASM 插件生命周期钩子 (RFC #7822)** | 已接受 | 打开沙盒插件生态的基础设施即将落地 |
| **OpenAI Chat Completions 适配器 (RFC #8603)** | 审查中 | 明确走向通用 API 网关，降低第三方客户端接入门槛 |

### 🌟 社区强需求
- **Bocha AI 网页搜索提供商** ([#8737](https://github.com/zeroclaw-labs/zeroclaw/pull/8737)) — 专为大陆用户设计，解决 DuckDuckGo/Brave 被墙的问题，体现本地化运营策略。
- **Cron 任务暴露 `uses_memory` 参数** ([#8676](https://github.com/zeroclaw-labs/zeroclaw/pull/8676)) — 让定时 Agent 任务拥有“记忆”能力，完善自动化场景闭环。
- **SOP 多阶段路由 (**when** 假值流转)** ([#8719](https://github.com/zeroclaw-labs/zeroclaw/issues/8719)) — 用户强烈要求 SOP 的 `when` 条件为假时不应结束，而应进入下一个步骤，以实现循环+收尾的工作流模式。

---

## 7. 用户反馈摘要

从今日 Issues 与 PR 评论中提炼的真实用户声音：

| 痛点/需求 | 用户场景 | 关联链接 |
|---|---|---|
| **语音转录开箱即坏** | “新装系统，按文档初始化配置，`local_whisper` 功能是坏的，看日志才发现是 config 模板有错。” | [#8718](https://github.com/zeroclaw-labs/zeroclaw/issues/8718) |
| **浏览器工具导致 Agent 死锁** | “跑在后台服务器上没有显示器，`browser_open` 直接卡死不返回。” | [#8560](https://github.com/zeroclaw-labs/zeroclaw/issues/8560) |
| **无法在 Android Termux 上运行** | “安卓手机上想跑个 Agent 实例，但编译和预编译二进制都不兼容 aarch64。” | [#7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911) |
| **Bedrock 模型被缓存功能阻塞** | “我想用 Nova 2 Lite 但 cachePoint 功能报错，而且没法在配置里关掉。” | [#8720](https://github.com/zeroclaw-labs/zeroclaw/issues/8720) |
| **高熵检测器误杀日志** | “安全检测把我的日志文件名 `report_20260705` 给 `[REDACTED_HIGH_ENTROPY_TOKEN]` 了。” | [#8722](https://github.com/zeroclaw-labs/zeroclaw/issues/8722) |
| **SOP 非预期终止** | “工作流中一个循环步骤结束后，`when` 条件为假时 SOP 直接退出，没法接一个总结步骤，很崩溃。” | [#8719](https://github.com/zeroclaw-labs/zeroclaw/issues/8719) |
| **迫切需求：OpenAI 适配层** | “我们用 Open WebUI 管理聊天前端，希望能直接连 ZeroClaw 的 Agent。” | [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) |
| **大陆地区搜索受限** | “DuckDuckGo 和 Brave 在大陆用不了，等了很久终于来了搜狗的平替 Bocha AI。” | [#8737](https://github.com/zeroclaw-labs/zeroclaw/pull/8737) |

---

## 8. 待处理积压

### 🚨 全项目最高优先级：PR 审查与合并积压
当前共有 **43 条** 活跃 PR 等待合并。大量修复关键 Bug（鉴权、安全、运行时崩溃）的 PR 和引入重大特性的 PR 被长时间搁置。**强烈建议核心维护者团队尽快组织 PR 审查会议或设立“合并日”，疏通这一瓶颈。**

### 📌 长期滞留工单
- **[Feature] 清理无用分支** ([#6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715)) — 自 **5月16日** 起提交，建议清理仓库中 200+ 已合并但未删除的无用分支。目前状态为 `blocked`，长期无人推进。
- **[Support] Android Termux 安装支持** ([#7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911)) — 自 **6月18日** 起开放，等待用户反馈 `needs-author-action`。若该场景有明确产品定位，建议维护者主动介入协助复现。
- **[RFC] 轻量化内核边界** ([#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)) — 自 **4月27日** 提出，虽已接受为 `status:in-progress`，但至今仍无对应的实施 PR 或 roadmap 时间表，存在烂尾风险。
- **[Tracker] v0.8.3 发布支持** ([#8073](https://github.com/zeroclaw-labs/zeroclaw/issues/8073)) — 作为版本发布追踪器，它的搁置直接决定了 0.8.3 版本无法发版，风险等级评定为 `risk:high`。

---

**总结：** ZeroClaw 项目当前处于“高产但低效消化”的状态。社区贡献极其活跃，但审查与合并流程严重落后于产出速度。三个 P1 级稳定性 Bug 悬而未决，多个安全修复 PR 排队等待合入。如果不尽快解决 PR 积压问题，该项目的高活跃度可能因贡献者疲劳而迅速转向。核心维护团队需要立即介入，打破这一瓶颈。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-07-06

**数据来源：** GitHub (github.com/sipeed/picoclaw) 过去 24 小时活动快照

---

## 1. 今日速览

项目今日活跃度中等，核心亮点在于社区反馈的联动闭环。过去 24 小时内，共有 **2 个 Issue** 更新（1 个高优特性持续讨论，1 个 Bug 因超时关闭）和 **5 个 PR** 更新（1 个合并，4 个待审）。最值得关注的是，一个长期困扰社区的“失忆”Bug（#3150）虽已关闭，但根因已被明确定位，直接催生的修复 PR（#3226）已经提交，体现了社区驱动的快速诊断能力。与此同时，加密核心替换和 DeltaChat 重构等长期议题也在稳步推进。

**活跃度评估：** 📊 社区参与稳定，重度设计讨论（加密库替换）与紧急 Bug 修复并行，项目健康度良好。

---

## 2. 版本发布

今日无新版本发布。但根据开放 PR 的破坏性变更程度（如 #3222 移除密码配置），预计下一个版本将包含显著的 Breaking Changes。

---

## 3. 项目进展
 
- **修复已合并：** [#3189 - fix(line)](https://github.com/sipeed/picoclaw/pull/3189)，对 LINE 通道的错误处理进行了微小的防御性修复（显式忽略 Close 错误）。
- **关键 Bug 修复已就绪：** [#3226 - fix(tools)](https://github.com/sipeed/picoclaw/pull/3226) 直接瞄准了用户痛点最大的“失忆”问题。修复了 `write_file` 工具的覆盖提示逻辑，避免了其“诱导”AI Agent 覆盖自身记忆文件 `MEMORY.md`。这是对 AI 核心体验（记忆持久化）的关键守护。
- **核心模块重构：** [#3222 - refactor(deltachat)](https://github.com/sipeed/picoclaw/pull/3222) 对 DeltaChat 集成进行了全面清理（精简 320 行），移除了遗留功能、硬编码的中继列表副本以及不安全的密码式邮箱配置。这标志着 DeltaChat 作为去中心化通信模块正趋于成熟。
- **基础设施清理：** [#3191](https://github.com/sipeed/picoclaw/pull/3191) 清理了 `.gitignore` 重复项；[#3192](https://github.com/sipeed/picoclaw/pull/3192) 将 GoReleaser 的 Docker 基础镜像升级到 Alpine 3.23，保持了构建环境的一致性。

**总结：** 项目今日向前迈进主要体现在 **“收敛技术债务”（-320LOC重构、依赖升级）**与 **“修复核心生命力”（记忆工具修复）** 两个方面。

---

## 4. 社区热点

- **最沸沸扬扬的联动事件：Bug #3150 ⇄ Fix #3226**
  Issue [#3150（自修复失忆）](https://github.com/sipeed/picoclaw/issues/3150) 虽因标记为 `stale` 而自动关闭，但其根因的发现路径本身成为了社区热点。用户描述的“AI 变白痴”现象本质上是 `write_file` 工具的响应文本 `file: … already exists. Set overwrite=true` 直接“教导” Agent 进行破坏性覆盖。这个分析在 PR **#3226** 的描述中被清晰揭露，引发了社区对 **“如何设计安全工具以避免诱导模型犯错”** 的广泛讨论。

- **高优特性持续发酵：Issue #3088**
  [#3088（使用 Vodozemac 替代 libolm）](https://github.com/sipeed/picoclaw/issues/3088) 依然保持着较高的热度（6 条评论，2 个 👍）。社区成员反复强调在 AI 助手日益个人化的今天，抛弃未维护的 `libolm`、拥抱可审计的矩阵官方加密库是保障用户隐私的根基。

---

## 5. Bug 与稳定性

| 严重程度 | 问题描述 | 状态 | 修复 PR |
| :--- | :--- | :--- | :--- |
| **🔴 P0 (严重)** | **Agent 长期记忆丢失（“失忆”）** <br>根因：`write_file` 的覆盖提示误导模型。 | 原 Issue #3150 因超时关闭；<br>根因已在 #3226 中被完全理解并修复。 | [#3226 待审核](https://github.com/sipeed/picoclaw/pull/3226) |
| **🟢 P3 (低)** | LINE 通道 `resp.Body.Close()` 错误未处理。 | 已合并 | [#3189 已合并](https://github.com/sipeed/picoclaw/pull/3189) |

**特别提示：** P0 级的“失忆”Bug 是目前限制用户体验的首要瓶颈。尽管 Issue 已关，但核心维护者应优先 Review **#3226**，避免因工具设计缺陷导致的“AI 体验降级”进一步扩散。

---

## 6. 功能请求与路线图信号

- **强烈信号1：核心安全库革命（#3088）**
  将 `vodozemac` 作为编译时可选依赖以完全替代 `libolm`。这不仅是依赖升级，更是架构级别的安全基座更换。鉴于 `libolm` 已被官方宣布弃用，此特性极有可能会成为 **v0.3.0** 或下一个次要版本的核心亮点。

- **强烈信号2：去中心化网络成为一等公民（#3222）**
  DeltaChat 模块的深度重构（移除密码安全漏洞、引用官方中继列表）表明项目在战略上正在向“无需中心化 API Key 也能正常工作”的方向演进。这符合个人 AI 助手的自主权诉求。

- **弱信号：Agent 工具设计哲学反思（#3226）**
  该 PR 暗示了未来的思路转向：不应让通用文件工具（`write_file`）直接操作核心认知文件（`MEMORY.md`）。社区可能会呼吁推出专门的 `memory` 工具或禁止直接覆盖记忆文件，以彻底杜绝误操作。

---

## 7. 用户反馈摘要

从 #3150 的评论与 #3226 的修复逻辑中，我们可以提炼出用户的真实痛点：

- **痛点1：“我的 AI 是个健忘症患者”**：用户期望 AI 能记住长期对话背景，但当前的工具机制（诱导覆盖）让这种期待化为泡影。用户体验从“智能助手”降级为“每次都要重新介绍的陌生人”。
- **痛点2：“工具在帮倒忙”**：用户敏锐地指出，问题不在于 Agent 的能力，而在于框架提供给 Agent 的工具存在设计缺陷。“`Set overwrite=true to replace it`” 这段文本不应被呈现给 Agent，因为它直接提供了一种错误的解决方案。
- **诉求**：用户希望框架能够智能识别**“更新/追加”**与**“覆盖/重置”** 的语义差异，并在 Agent 做出危险动作时进行强有力的阻拦，而非提供操作指导。

---

## 8. 待处理积压

| 条目 | 类型 | 开放时长 | 影响 | 建议 |
| :--- | :--- | :--- | :--- | :--- |
| **#3088** | 🚀 功能 | 27 天 | 阻塞加密安全路线的推进 | 虽然是高优，但仅停留在设计讨论。建议维护者指派责任人，或发起一次设计决策 (RFC) 投票。 |
| **#3191 / #3192** | 🧹 杂务 | 9 天 | 基础设施清理 | 风险极低的纯清理 PR，建议尽快合并，以减少 CI/配置的冲突可能。 |
| **#3222** | 🔧 重构 | 3 天 | 影响 DeltaChat 集成用户 | 代码删除量大（-320 LOC），涉及 JSON-RPC 秘密管理重构，需要核心成员深度 Code Review，以防破坏现有用户使用。 |
| **#3226** | 🐛 修复 | 1 天 | 直接影响所有用户的核心体验 | **紧急。** 这是解决 P0 级“失忆”Bug 的唯一方案。必须给予最高 Review 优先级并尽快合入，避免 Issue #3150 的负面体验继续影响新用户。 |

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 QwenPaw 项目 2026-07-06 日动态日报。

---

### 📊 QwenPaw 项目动态日报 | 2026-07-06

> 数据周期：过去 24 小时 | 数据驱动 · 专业解读

---

#### 1. 今日速览

过去 24 小时内，QwenPaw 项目活跃度极高，社区围绕 v1.1.12.post2 版本进行了深度使用与压力测试。尽管昨日无 **新版本发布** 或 **PR 合并**，但提交了 12 个新 Issue 和 5 个新 PR。其中，多项高等级 Bug 被精准定位并已附带修复 PR（如 #5786、#5783），表明了维护团队对社区反馈的快速响应。此外，2 位首次贡献者提交了代码修复，项目开发者生态呈现出健康的成长态势。

---

#### 2. 版本发布

（无）

---

#### 3. 项目进展

尽管昨日暂无 PR 被合并至主分支，但项目在开发管道（Development Pipeline）上取得了实质性推进，大量高质量的修复与功能代码处于“待合入”状态：

- **🧠 内存系统架构演进**：`@jinliyl` 提交了 PR [#5777](https://github.com/agentscope-ai/QwenPaw/pull/5777) ，引入**基于会话的自动记忆轮次状态管理**，对 Agent 的长程记忆能力进行了关键性重构。该功能正等待架构级 Code Review。
- **🐛 关键 Bug 修复集**：`@yutai78786` 提交了 PR [#5786](https://github.com/agentscope-ai/QwenPaw/pull/5786)，一次性修复了三个 Bug（包含 #5709、#5773），其中对 **跨 Provider 模型压缩阈值显示错误** 的修复直击多配置用户的痛点。
- **⏰ 调度系统时区修复**：`@wananing` 提交了 PR [#5783](https://github.com/agentscope-ai/QwenPaw/pull/5783)，修复了 Cron 任务 API 返回时间硬编码为 UTC 的严重设计缺陷（关联 Issue #5779）。
- **👋 新贡献者注入**：`@Osamaali313` 提交了其首个 PR（[#5791](https://github.com/agentscope-ai/QwenPaw/pull/5791)/[#5792](https://github.com/agentscope-ai/QwenPaw/pull/5792)），修复了数字格式化边界问题和工具消息清洗逻辑。

---

#### 4. 社区热点

昨日社区讨论呈现出“高期待”与“高要求”并行的态势：

- **V2.0 的全民期待**：Issue [#5770](https://github.com/agentscope-ai/QwenPaw/issues/5770) 虽由 Bot 用户发起，但“希望V2.0的正式版推出之后，能够惊艳所有人”的呼声得到了社区共鸣，是项目健康度和用户信心的积极信号。
- **深度诊断与快速修复**：Issue [#5784](https://github.com/agentscope-ai/QwenPaw/issues/5784) 的作者通过阅读源码树精准定位了压缩阈值显示错误的根因，并在数小时内收到了对应的修复 PR（#5786）。这种高质量“漏洞挖掘→代码修复”的协作模式已成为该社区的标志性特征。
- **飞书渠道稳定性焦虑**：Issue [#5757](https://github.com/agentscope-ai/QwenPaw/issues/5757) （飞书消息首次回复后挂起）持续获得关注。用户反映无论是 Docker 自部署还是官方云平台均存在此问题，凸显了核心 IM 集成稳定性的紧迫性。

---

#### 5. Bug 与稳定性

昨日 Bug 报告密集，按严重等级排列如下：

| 严重程度 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| 🔴 崩溃级 | [#5789](https://github.com/agentscope-ai/QwenPaw/issues/5789) | 上下文压缩时模型输出超出 JSON Schema 约束导致 `validate()` 崩溃 | 无修复 PR |
| 🔴 阻断级 | [#5757](https://github.com/agentscope-ai/QwenPaw/issues/5757) | 飞书渠道首次回复后无响应，阻断核心通信流程 | 无修复 PR |
| 🟡 功能受阻 | [#5784](https://github.com/agentscope-ai/QwenPaw/issues/5784) | 同名模型跨 Provider 时，前端压缩阈值显示错误 | **关联 PR #5786** |
| 🟡 功能受阻 | [#5779](https://github.com/agentscope-ai/QwenPaw/issues/5779) | Cron API 返回的 `last_run_at` 硬编码为 UTC 而非用户时区 | **关联 PR #5783** |
| 🟡 功能受阻 | [#5782](https://github.com/agentscope-ai/QwenPaw/issues/5782) | Google Gemini Embedding 通过 OpenAI SDK 调用时 `index=None` 导致向量搜索静默回退 | 无修复 PR |
| 🟡 功能受阻 | [#5781](https://github.com/agentscope-ai/QwenPaw/issues/5781) | 离线 Code 模式因缺少在线资源无法预览文件 | 无修复 PR |
| 🟡 功能受阻 | [#5788](https://github.com/agentscope-ai/QwenPaw/issues/5788) | 技能列表滚动加载失效，仅限于 20 个元素 | 无修复 PR |
| 🟢 体验级 | [#5787](https://github.com/agentscope-ai/QwenPaw/issues/5787) | 移动端 WebUI 所有页面底部内容被截断 | 无修复 PR |
| 🟢 体验级 | [#5790](https://github.com/agentscope-ai/QwenPaw/issues/5790) | Agent 响应完成后加载动画未消失 | 无修复 PR |

---

#### 6. 功能请求与路线图信号

- **👥 团队级多用户管理（#5780）**：这是昨日最具战略意义的 Feature Request。用户明确指出当前“单 Bot 账号”模式无法满足团队协作需求，缺乏用户策略和访问控制。这强烈指向了项目从“个人助手”向“企业平台”演进的关键路线图缺口，预计将是中长期的开发重点。
- **💻 Coding 模式增强（#5785）**：用户要求在 Coding 模式下能够选择隐藏文件（以 `.` 开头的文件）。这是一个精准的开发者体验改进点，实现成本低，受益面明确。
- **🧠 自动记忆管理（PR #5777）**：昨日提交的新 PR 标志着项目正在主动重构 Agent 的长期记忆机制，这是提升 Agent 自主性和复杂任务处理能力的必经之路。

---

#### 7. 用户反馈摘要

- **核心痛点**：
    - **集成稳定性**：飞书渠道的通信卡死（#5757）在不同环境均可复现，是当前最影响重度用户信赖感的痛点。
    - **配置兼容性**：多 Provider 场景（#5784）和 Google Gemini 适配（#5782）的 Bug 暴露了版本迭代中对复杂拓扑配置的测试覆盖存在短板。
    - **离线可用性**：Code 模式离线不可用（#5781）限制了特定场景（如内网开发）的使用。
- **使用场景**：
    - 团队通过企业 IM 进行协同是明显的增长用例（#5757, #5780）。
    - 开发者用户是高频 Bug 提交和功能建议的主力（#5784, #5785）。
- **社区情绪**：整体积极且专业。用户愿意通过阅读源码来报告 Bug（#5784），新贡献者主动提交修复（#5791, #5792），且对 V2.0 抱有高期待（#5770）。

---

#### 8. 待处理积压

针对维护团队的提醒与关注点：

- **[🔴事故] 用户流失风险：** `#5757`（飞书中断）和 `#5789`（压缩崩溃）是当前影响最严重的 Issue，持续无官方回应或修复方案，可能导致核心用户流失。
- **[🟡首次贡献者关怀]：** 新手贡献者 `@Osamaali313` 提交的 PR `#5791` 和 `#5792` 正在等待 Review。轮替审阅和第一时间反馈是留住新参与者的重要环节。
- **[🟡架构级功能积压]：** `#5777`（自动记忆管理）作为大型功能 PR，建议维护团队尽快安排架构审核，避免因审批周期过长导致后续出现大规模代码冲突。
- **[🟡长期 Bug]：** `#5757` 于 2026-07-03 创建，至今已有 3 天，无任何官方标签或指派，建议纳入 Hotfix 观察清单。

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是为您生成的 hermes-agent 项目每日动态日报。

---

### hermes-agent 项目动态日报（2026-07-06）

---

#### 1. 今日速览
过去 24 小时，Hermes Agent 项目保持 **极高** 的社区活跃度。共处理 326 条 Issue 更新（其中 228 条新开/活跃）及 500 条 PR 更新（138 个已合并/关闭）。核心开发者（@teknium1）主导了多项高难度修复，特别是在 **MCP 弹性**与 **DeepSeek 崩溃** 问题上取得了关键进展。社区层面，关于 **Dashboard 主题可读性** 与 **自定义 Agent 编排** 的讨论热度最高。项目整体展现出从核心架构推进转向 **生态打磨与稳定性优先** 的态势，健康度优秀。

---

#### 2. 版本发布
无。项目近期处于高频率小迭代周期，社区 PR 正快速汇入主干。

---

#### 3. 项目进展
过去 24 小时内共合并/关闭 138 个 PR，主要进展如下：

- **核心稳定性攻坚**
  - **P1 Bug 修复**：彻底解决了 **DeepSeek v4** 在长时间工具调用后触发 HTTP 400 的错误（[#56980](https://github.com/NousResearch/hermes-agent/issues/56980)），这是今日最重要的稳定性修复。
  - **MCP 框架重连弹性升级**：@teknium1 提交了针对 MCP 的重大修复（[#59222](https://github.com/NousResearch/hermes-agent/pull/59222)），引入了重连预算重置、沉降服务器自检及恢复注册机制，杜绝了 MCP 服务器“永久性假死”问题。

- **多智能体与委派**
  - 强化了 `delegate_task` 功能，多项请求关闭：允许传递 Provider/Model 参数（[#5012](https://github.com/NousResearch/hermes-agent/issues/5012)）及标准化子运行时元组（[#25386](https://github.com/NousResearch/hermes-agent/pull/25386)），多模型编排功能日趋成熟。

- **平台与网关增强**
  - **Telegram**：恢复了被破坏的工具进度分组显示（[#59223](https://github.com/NousResearch/hermes-agent/pull/59223)）。
  - **Cron**：修复了定时任务投递路由，确保 `deliver=all` 等指令正确到达主频道（[#59212](https://github.com/NousResearch/hermes-agent/pull/59212)）。

- **安全与开发者体验**
  - **安全审查**：完成了 Webhook 消息体大小限制的全面扫描，覆盖 SMS、Feishu、WhatsApp 等平台（[#59215](https://github.com/NousResearch/hermes-agent/pull/59215)）。
  - **CLI 修复**：改进了 `/resume` 命令以显示所有来源（CLI/TUI/WebUI）的会话（[#59225](https://github.com/NousResearch/hermes-agent/pull/59225)），修复了 Termux 上的 venv 恢复路径（[#59216](https://github.com/NousResearch/hermes-agent/pull/59216)）。

---

#### 4. 社区热点
- **🔥 界面主题引发大讨论**（[#18080](https://github.com/NousResearch/hermes-agent/issues/18080)）：获得 **46 个 👍** 和 **27 条评论**。用户直言当前主题字体和配色极不标准，严重影响 Dashboard 可读性，这是社区情感共鸣最强的话题。
- **🔥 自定义 Agent 编排需求强烈**（[#9459](https://github.com/NousResearch/hermes-agent/issues/9459)）：用户希望借鉴 `oh-my-opencode-slim`，通过配置文件定义智能体角色，以便搭建高度定制化的专家团队。该议题获 **18 个 👍**。
- **🔥 桌面端工作区选择**（[#40297](https://github.com/NousResearch/hermes-agent/issues/40297)）：长期桌面用户希望在会话中动态切换工作目录，而非仅在启动时绑定，体现了对现代 IDE 级体验的期待，获 **10 个 👍**。

---

#### 5. Bug 与稳定性
| 严重程度 | 议题 | 状态 | 简述 |
| :--- | :--- | :--- | :--- |
| **P1 严重** | [#56980](https://github.com/NousResearch/hermes-agent/issues/56980) | **已关闭** | **DeepSeek v4 长会话 Tool Call 崩溃**。累计 30+ 轮消息后触发 HTTP 400，已于今日修复。 |
| **P2 高** | [#55658](https://github.com/NousResearch/hermes-agent/issues/55658) | 开放 | **更新后无法启动**。需社区协助复现，影响面较广。 |
| **P2 高** | [#18304](https://github.com/NousResearch/hermes-agent/issues/18304) | 开放 | **成本监控全局失效**。所有 Provider 的 token 及费用统计始终为 0，严重影响生产环境计费追踪。 |
| **P2 高** | [#44666](https://github.com/NousResearch/hermes-agent/issues/44666) | 开放 | **配置静默错误**。`api_key_env` 配置项被代码忽略，自定义 Provider 认证形同虚设。 |
| **P2 高** | [#58646](https://github.com/NousResearch/hermes-agent/issues/58646) | 开放 | **QQ 机器人适配器启动崩溃**。网关传递的 `is_reconnect` 参数不被支持，导致 TypeError。 |
| **P2 高** | [#43963](https://github.com/NousResearch/hermes-agent/issues/43963) | 开放 | **路径扩展异常未捕获**。`~user` 路径展开抛出 `RuntimeError`，导致 Agent 单轮任务直接崩溃。 |
| **P2 高** | [#58437](https://github.com/NousResearch/hermes-agent/issues/58437) | 开放 | **MoA 静默模式崩溃**。聚合器丢弃 `tool_calls` 导致 `empty_response_exhausted`。 |
| **P2 高** | [#48056](https://github.com/NousResearch/hermes-agent/issues/48056) | 开放 | **Telegram DM 话题定时投递异常**。Cron 任务无法保持在指定话题内。 |

---

#### 6. 功能请求与路线图信号
- **🚀 明确的路线图：模型路由一体化**
  过去 24 小时，关于动态/手动模型切换的多个核心 Issue 被关闭（[#16525](https://github.com/NousResearch/hermes-agent/issues/16525), [#5012](https://github.com/NousResearch/hermes-agent/issues/5012) 等）。暴露 `model_switch` 为 Agent 工具、`delegate_task` 携带模型参数等功能已处于合并尾声。这意味着 **根据任务复杂度自动路由模型** 的能力即将随下一版本作为核心功能落地。

- **🧠 记忆子系统架构重构信号**
  - **#47349**（[Configurable Memory Backends](https://github.com/NousResearch/hermes-agent/issues/47349)）与 **#42864**（[第三方 scope-recall 存储提供者](https://github.com/NousResearch/hermes-agent/issues/42864)）暗示官方正在对当前硬编码的 `MEMORY.md` / `USER.md` 机制进行重大升级，将引入可配置的记忆后端。

- **🔒 企业级安全与治理**
  - **#51221**（[User-Configurable Runtime Approval](https://github.com/NousResearch/hermes-agent/issues/51221)）虽已关闭，但讨论表明社区对企业级的安全审批工作流（如对文件写操作进行二次确认）的呼声日益增长，很可能是下一阶段企业版功能的前置信号。

---

#### 7. 用户反馈摘要
- **主要痛点**：
  - “当前仪表盘主题的**字体和颜色选择非常不标准**，尤其是**细体衬线字体加上极低的对比度**，让 Dashboard 几乎无法阅读。”（#18080）
  - “每次上下文压缩都会产生 `My Chat #2`, `My Chat #3`... **侧边栏变得极其混乱**。”（#38763）
  - “成本统计彻底失灵了，我们无法追踪不同模型的花费。”（#18304）
- **期望**：
  - “希望 `delegate_task` 能像 oh-my-opencode-slim 那样支持从配置文件读取**智能体角色**，这样我就可以构建不同的专家团队。”（#9459）
  - “需要一个**更强大的内存系统**，我不想用 `memory.md`，我想用专用的第三方服务存储和检索记忆。”（#47349）

---

#### 8. 待处理积压
- **⚠️ #18304 - 成本监控为 0**（P2, 已活跃超一月）：核心计费功能完全失效，严重阻碍项目在生产环境的采用，亟需团队审查。
- **⚠️ #18080 - 主题可读性**（P3, 27 条评论, 46 👍）：虽然优先级标注为 P3，但其社区热度已远超阈值，维护者应重新评估其优先级并给予官方回应。
- **⚠️ #38763 - 上下文压缩产生孤儿会话**（P2）：直接影响 WebUI 和桌面的核心用户体验，侧边栏无限膨胀的问题建议纳入 UI 重构路线图。
- **⚠️ #6653 - openai-codex 跨 Profile 重认证循环**（P2, 复杂 Bug）：多实例管理员模式下的老大难问题，涉及认证边界处理，影响专业用户工作流。

</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*