# OpenClaw 生态日报 2026-07-20

> Issues: 365 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-19 22:41 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)
- [AstrBot](https://github.com/AstrBotDevs/AstrBot)

---

## OpenClaw 项目深度报告

好的，这是根据您提供的 OpenClaw 项目数据生成的 2026-07-20 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-07-20

## 1. 今日速览

项目在 `v2026.7.2-beta.3` 发布后进入超高活跃期。过去 24 小时内，Issue 更新量达 **365 条**（新开/活跃 237，关闭 128），PR 更新量高达 **500 条**（合并/关闭 160，待合并 340），展现了顶级的迭代节奏。尽管 Beta 阶段存在一些严重的回归问题，但核心维护者（@steipete, @giodl73-repo）响应迅速，在 Agent 核心修复、跨平台兼容性以及大规模后台架构（如新 “Claw” 管理体系与本地化框架）上推进显著。项目生态热度极高，社区对安全性与企业级可用性的诉求日趋强烈。

## 2. 版本发布

- **版本**: `v2026.7.2-beta.3`
- **核心看点**:
  - **远程编码会话**: 支持在云端 Workers 上运行 Control UI 会话，将计算资源与本地环境解耦，并能在终端中直接恢复 OpenCode 和 Pi 会话。
  - **原生自动化与节点**: 扩充了底层自动化能力。*(注：原 Release 数据截断，具体节点类型未完全展示)*
- **迁移建议**: Beta 阶段升级较快，建议在生产测试环境充分验证后再覆盖生产节点。

## 3. 项目进展

过去 24 小时内，共 **160 个 PR 被合并/关闭**，大量核心问题得到解决：

- **Agent 核心稳定性** (@steipete): 
  - 修复了新建命名工作区被错误标记为“已孵化”导致首次交互异常的 `hatch` 状态问题 ([#111553](https://github.com/openclaw/openclaw/pull/111553))。
  - 修复了多工作区新人引导推荐状态全局共享的冲突问题 ([#111560](https://github.com/openclaw/openclaw/pull/111560))。
  - 修复了 `doctor` 命令在自定义状态目录下无法可靠修复活动配置文件的问题 ([#111555](https://github.com/openclaw/openclaw/pull/111555))。
- **Telegram 通道健壮性** (@MongLong0214): 修复了 Telegram DM 频道处理程序阻塞后永久“死亡”的问题，引入了监督式网关重启机制 ([#107547](https://github.com/openclaw/openclaw/pull/107547))。
- **UI 与测试基建** (@steipete): 
  - 修复了多用户网关下聊天发送者身份显示 UUID 而非用户名的缺陷 ([#111537](https://github.com/openclaw/openclaw/pull/111537))。
  - 修复了 Control UI 测试套件中跨文件 Mock 泄漏导致的随机失败 ([#111554](https://github.com/openclaw/openclaw/pull/111554))。
  - 修复了跨测试文件的插件运行时状态泄漏 ([#111556](https://github.com/openclaw/openclaw/pull/111556))。
- **大规模架构推进**: 
  - “**Claw**” 代理管理标准系列 PR（如 #101755, #101328 等）与**本地化框架 5 层基础 PR**（#111541~#111545）正在整编并推进审核，标志着项目正迈向声明式管理与全栈国际化。

## 4. 社区热点

- 🌟 **[#75] Linux/Windows 桌面 App 需求**
  评论 114 条，获赞 80。虽然创建已逾半年，但仍是社区最强烈的呼声。社区对跨平台原生体验的渴求超过预期。
  [查看详情](https://github.com/openclaw/openclaw/issues/75)

- 🌟 **[#109867] Beta.2 迁移脚本阻塞 Gateway 启动 P0**
  获赞 7 个。该 Bug 直接导致用户升级后无法启动，虽已被 Beta.3 紧急修复，但暴露了数据库迁移在 Beta 流程中的测试盲区。
  [查看详情](https://github.com/openclaw/openclaw/issues/109867)

- 🌟 **[#79077] Telegram Guest Bot 与 Bot-to-Bot 支持**
  获赞 8 个。社区对 Telegram 2026.5.7 发布的新 Bot 特性非常兴奋，渴望 OpenClaw 快速跟进，体现了用户对前沿即时通讯集成的期望。
  [查看详情](https://github.com/openclaw/openclaw/issues/79077)

- 🌟 **[#44431] 浏览器工具现场测试报告**
  用户 @ibadukefan 基于对 9 个邮件服务商的自动化测试，提交了涵盖缺乏 CSS 选择器等 7 条深度改进建议。这种高质量的反馈是项目打磨核心体验的宝贵财富。
  [查看详情](https://github.com/openclaw/openclaw/issues/44431)

## 5. Bug 与稳定性

**P0 (阻塞性)**
- **[#109867](https://github.com/openclaw/openclaw/issues/109867)**: Beta.2 数据库迁移在添加列前创建索引，导致 Gateway 启动崩溃。**状态: 已在 Beta.3 中修复，但需观察是否完全恢复。**

**P1 (严重回归/数据潜在丢失)**
- **[#109490](https://github.com/openclaw/openclaw/issues/109490)**: Codex 服务端 `releaseTurnAfterTerminalDynamicTool` 机制导致在发送进度消息后交互中断，后续 Agent 工作不执行。
- **[#111519](https://github.com/openclaw/openclaw/issues/111519)**: `2026.7.2-beta.3` 中 Telegram DM 回复无法正确绑定回原始消息。*(新发回归)*
- **[#85246](https://github.com/openclaw/openclaw/issues/85246)**: 在 npm 全局安装+launchd 管理场景下，UI 更新按钮导致 Gateway 死锁。
- **[#108075](https://github.com/openclaw/openclaw/issues/108075)**, **[@108238](https://github.com/openclaw/openclaw/issues/108238)**: (已关闭) 2026.7.1 的 Provider Schema 拒绝和 Context 用量误报问题。

**P2 (影响功能体验)**
- **[#93139](https://github.com/openclaw/openclaw/issues/93139)**: `write` 工具和 Heredocs 将字符串中的 `\n` 解析为字面量而非换行符。
- **[#110065](https://github.com/openclaw/openclaw/issues/110065)**: 运行时读取 `compaction.enabled` 字段，但配置 Schema 拒绝该字段，导致用户配置无效。
- **[#103198](https://github.com/openclaw/openclaw/issues/103198)**: WebChat 发送图片附件时，路径映射出错，Agent 工具接收到的是 `image_0` 而非真实文件路径。

## 6. 功能请求与路线图信号

**安全成为企业级绝对主线**
- **[#7707](https://github.com/openclaw/openclaw/issues/7707)**: **内存信任标签**。防止 Agent 被不可信源（网页、邮件）隐藏的指令攻击。
- **[#10659](https://github.com/openclaw/openclaw/issues/10659)**: **蒙版密钥**。Agent 可使用 API 密钥但不可读取明文，防止提示词注入导致凭据泄露。
- **[#13583](https://github.com/openclaw/openclaw/issues/13583)**: **强制执行钩子**。在金融、安全等场景机械性地确保 Agent 在回复前调用特定工具。
- **趋势分析**: 这三者非单纯的“增强”，而是为将 Agent 部署到关键业务进场的必需品。`@steipete` 在近期的 Dashboard 与 Custodian 更新中也大量涉及权限边界，暗示下一版本的安全模块将迎来大改。

**编排与自动化**
- **[#110950](https://github.com/openclaw/openclaw/issues/110950)**: “万物皆为 Cron” 提案。意图统一心跳、监视器和调度任务，是 OpenClaw 迈向操作系统级 Agent 管理的有力信号。
- **[#9912](https://github.com/openclaw/openclaw/issues/9912)**: 限制 Agent 迭代轮次 (`maxTurns/maxToolCalls`)。这反映了高级用户在使用不同模型（如 KIMI K2）时对 Agent 失控的担忧。

**平台扩展**
- **[#75](https://github.com/openclaw/openclaw/issues/75)**: Linux/Windows App（长期搁置，急需产品决策）。
- **[#78963](https://github.com/openclaw/openclaw/issues/78963)**: WhatsApp 仅监听/仅 Hooks 模式。

## 7. 用户反馈摘要

- **满意点**: 
  - 项目迭代速度令多数用户满意（“没想到一天能关 160 个 PR”的节奏）。
  - 对远程编码和 Telegram 功能的及时更新给予了正面评价。
- **痛点**:
  - **“升级如开盲盒”**: 用户抱怨几乎每次 Beta 升级都伴随回归（#108075, #108238, #111519），且插件版本漂移（#83337）缺乏有效的兼容性警告，导致升级后通道静默失效。
  - **配置复杂性增加**: Schema 与运行时行为不一致（#110065）、不友好的错误提示（#9409）、以及浏览器工具缺乏 CSS 选择器（#44431），让用户觉得微调 Agent 行为门槛较高。
  - **对“自主权”的博弈**: 用户既想要 Agent 的聪明能干，又在努力为其套上“缰绳”。调用限制（#9912）、拒绝列表（#6615）、子 Agent 广播控制（#8299）等请求，反映了从“能用”到“用好”阶段的典型阵痛。

## 8. 待处理积压

**长期未结大热/重要 Issue**
- **[:#75 Linux/Windows App](https://github.com/openclaw/openclaw/issues/75)**: 已创建 7 个月，P2，仍卡在 `needs-product-decision`。鉴于其 80 个赞和 114 条评论的社区热度，建议维护者尽快给出时间表或阶段性回应。
- **[#10659 Masked Secrets](https://github.com/openclaw/openclaw/issues/10659)**: P1 需求，依然卡在产品决策，与 P1 标签矛盾。
- **[#99910 Memory Dreaming 导致事件循环阻塞~10mins](https://github.com/openclaw/openclaw/issues/99910)**: 2026-07-04 创建的 P1 Bug。该问题会导致 Gateway 无响应、通道掉线，甚至可能丢失短时记忆持久化机会，但目前仍无明确 Fix PR，是稳定性的一个重大隐患。

**需维护者重点审核的重磅 PR (审核压力预警)**
- **Claw 系列 PR** (`@giodl73-repo`):
  - 包括 #101755, #101328, #101973, #102982, #102406, #102383 等 10 余个 PR。
  - 影响范围: Agent 生命周期、MCP 所有权、Cron 管理、分组更新。
  - 当前状态: 多为 `status: 📣 needs proof` | Size: XL。这套声明式 Agent 管理体系体量极大，将对核心 Team 的 Code Review 带宽构成严峻考验。
- **本地化 5 层基础 PR** (`@giodl73-repo`): #111541~#111545。同样为 Size: XL，面临堆叠式审核挑战。

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析（2026-07-20）

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于**高速迭代与结构性分化并存**的阶段。头部项目日 PR 吞吐量可达数百，但合并率普遍偏低（8%–25%），维护带宽成为共同瓶颈。社区诉求从“能用”快速转向“可信、可管、可运维”：安全治理（权限门控、密钥保护）、记忆一致性、跨平台体验与插件化架构成为多项目共振的技术主线。与此同时，用户对迭代速度的高期待与回归问题频发之间的矛盾加剧，“升级即风险”的反馈在多项目中出现，提示生态需在速度与质量之间建立更平衡的社区治理机制。

## 2. 各项目活跃度对比

| 项目 | 今日 Issue 更新（新开+活跃 / 关闭） | 今日 PR 更新（待合并 / 合并关闭） | 版本发布 | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 365（237 / 128） | 500（340 / 160） | v2026.7.2-beta.3 | 中高 – 迭代极快但回归多发，核心维护响应及时 |
| **Zeroclaw** | ~100 条（Issue+PR 合计） | 4 合并/关闭（合并率 8%） | 无 | 中低 – 社区沸腾但审查瓶颈显著，S0 安全漏洞未修复 |
| **PicoClaw** | 3（2 / 1） | 3（3 / 0） | 无 | 低 – 活跃度低，关键启动 Bug (#3265) 无修复关联 |
| **QwenPaw** | 11（10 / 1） | 6（6 / 0） | 无 | 中 – 性能与安全 PR 质量高但合并率为零，维护积压 |
| **hermes-agent** | ~500（未明确关闭数） | ~500（61 合并/关闭） | 无 | 中高 – 海量社区贡献，P0 并发修复落地，但积压严重 |
| **AstrBot** | 6（3 / 3） | 6（5 / 1） | 无 | 高 – 平衡的修复与开发节奏，社区生态健康 |

*注：Zeroclaw、hermes-agent 因日均更新量极高，精确细分数未完全披露，表中采用日报给出的总量。*

## 3. OpenClaw 在生态中的定位

- **核心参照地位**：OpenClaw 是唯一维持日更新 500+ PR 且合并率达 32%（160/500）的项目，体现了最活跃的维护者投入和社区信任度。其 Release 节奏（Beta 阶段仍高频发版）与架构前瞻性（“Claw”声明式管理、5 层本地化框架）为同类项目树立了参照坐标。
- **技术路线差异**：强调 **远程编码解耦**（云端 Worker 运行 Control UI）和 **企业级安全原语**（内存信任标签、蒙版密钥、执行钩子），目标是将 Agent 从对话工具升级为可信基础设施。相比之下，hermes-agent 更关注本地模型与高级定制，Zeroclaw 聚焦插件化与隐私优先，OpenClaw 的路线更为系统化。
- **社区规模**：以绝对活跃度计，OpenClaw 与 hermes-agent 构成第一梯队。但 OpenClaw 的 Issue 关闭率（35%）和 PR 合并率均高于 hermes-agent，治理效率领先。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目（典型诉求） | 趋势解读 |
|---|---|---|
| **Agent 安全与权限治理** | OpenClaw（内存信任标签、掩码密钥、强制钩子）、Zeroclaw（#7947 S0 管道绕过漏洞、KeySource 抽象）、QwenPaw（CIDR 白名单、沙箱回退可配置）、hermes-agent（PreToolUse Hook、响应头 RPM 限流） | 安全已从“增强”演变为“必选”，项目纷纷将策略注入与运行时门控作为基础设施。 |
| **记忆/上下文一致性与持久化** | OpenClaw（Memory Dreaming 阻塞）、Zeroclaw（#8891 持久化记忆、#9048 分离会话历史与长期记忆）、hermes-agent（#27013 上下文完全丢失、#509 认知记忆系统）、AstrBot（#9240 主动消息上下文缺失） | 记忆混乱是破坏信任的核心痛点，结构化记忆（多轮边界、角色分离、持久化）成为下一阶段竞争焦点。 |
| **跨平台桌面与客户端体验** | OpenClaw（#75 Linux/Windows App 诉求 80 赞）、PicoClaw（#3265 配置阻塞崩溃）、QwenPaw（#6252 Linux 缩放快捷键失灵）、hermes-agent（#63078 空白会话、#67600 侧栏消失） | 桌面端稳定性与原生体验仍远未成熟，是获取非技术用户的关键瓶颈。 |
| **插件化 / 可扩展架构** | Zeroclaw（WASM 插件化 PR #8863/#8855）、OpenClaw（Claw 代理管理标准）、AstrBot（插件市场与审核 #7060）、PicoClaw（社区贡献 PR 功能明确） | 从单体走向生态已成共识，但运行时隔离（WASM）和治理规则（审核/版本兼容）尚未出现主导方案。 |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 关键技术架构特点 |
|---|---|---|---|
| **OpenClaw** | 全能型 Agent 操作系统：远程编码、自动化、声明式管理、企业安全 | 企业级用户、高级开发者、运维团队 | 模块化单体 + 声明式 Claw 管理 + 独立本地化层 |
| **Zeroclaw** | 隐私优先、多频道（TG/Discord/SMTP）集成、轻量可嵌入 | 隐私敏感用户、频道重度集成者 | 微内核 + WASM 插件隔离 + 成本追踪 |
| **PicoClaw** | 极简、嵌入式、边缘部署 | 资源受限 / 嵌入式场景 | 轻量化 Gateway，对第三方供应商依赖低 |
| **QwenPaw** | 与 AgentScope 生态深度耦合、沙箱安全、性能优化 | 学术/研究人员、AI 应用开发者 | 沙箱隔离 + MCP 驱动 + 可配置回退策略 |
| **hermes-agent** | 本地模型（MoE）深度优化、高级用户定制、网关并发 | 本地 LLM 爱好者、技术极客 | 高并发网关 + KV Cache 压缩 + 配置自然语义扩展 |
| **AstrBot** | 即时通讯机器人、插件市场、多平台（QQ/Web/钉钉） | 社区运营、Bot 开发者 | 消息中间件 + 插件系统 + WebUI 管理 |

## 6. 社区热度与成熟度分级

- **第一梯队（极高活跃、快速迭代）**  
  **OpenClaw**、**hermes-agent**：日更新 300–500 条，PR/Issue 数量远超其他项目，核心功能周级迭代。但 OpenClaw 结构更清晰（架构 PR 与 Bug 修复分流明显），hermes-agent 则呈现社区诉求爆炸但维护者响应相对滞后的态势。

- **第二梯队（活跃但瓶颈显著）**  
  **Zeroclaw**、**QwenPaw**：社区贡献意愿强（Zeroclaw 日更 100 条，QwenPaw 连续高质量 PR），但合并率极低（8%、0%），严重依赖少数核心维护者，治理流程亟待优化。Zeroclaw 处于架构重构期（ADR 批量提交），QwenPaw 则面临性能与安全的双线推进压力。

- **第三梯队（稳定低活跃、质量巩固阶段）**  
  **AstrBot**、**PicoClaw**：社区体量较小，但 AstrBot 保持健康的新陈代 rate（Issue 关闭率 50%，有小幅但稳定的合并），适合对稳定性要求高的用户。PicoClaw 活跃度最低且关键 Bug 悬停，处于早期培育阶段。

## 7. 值得关注的趋势信号与开发者启示

1. **“安全是准入证，而非加分项”**：OpenClaw 的钩子机制、Zeroclaw 的管道漏洞、hermes-agent 的 PreToolUse Hook 共同表明，Agent 工具执行的强制策略正在成为标配。开发者选型时应评估项目对权限模型（RBAC/ABAC）和密钥管理的原生支持程度。
2. **记忆基础设施决定体验上限**：从 hermes-agent 的“完全失去项目上下文”到 Zeroclaw 的重构记忆子系统，社区正在从“对话历史”走向“结构化认知记忆”。若项目缺乏记忆边界管理或持久化方案，长期复杂任务几乎不可用。
3. **插件化架构仍缺统一标准**：WASM（Zeroclaw）、声明式 Claw（OpenClaw）、Python 插件（AstrBot）三种路线并存，未见融合趋势。开发者需根据自身技术栈与隔离要求谨慎选择，并关注未来生态兼容性风险。
4. **社区治理瓶颈正在抑制创新**：多个项目合并率不足 10%，大量高质量 PR 等待数周甚至数月。这警示后来者：在选型时不仅看功能，更要评估维护团队的响应效率和贡献者文档（CONTRIBUTING.md、RFC 流程）的健全程度。
5. **边缘/离线场景仍为短板**：PicoClaw 启动崩溃、QwenPaw 离线无法预览文件、hermes-agent 本地 MoE 性能衰退——说明主流项目对纯离线环境的投入仍不足。若目标部署在安全隔离或低带宽环境，需额外验证基础链路的健壮性。

---

*本报告基于 2026-07-20 各项目 GitHub 社区公开动态生成，数据来源及详细分析见附带的项目日报。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，这是您要求的 Zeroclaw 项目 2026-07-20 动态日报。

---

### Zeroclaw 项目动态日报 (2026-07-20)

---

#### 1. 今日速览

过去24小时内，Zeroclaw 项目展现出**极高的社区活跃度**，Issue 与 PR 更新总量达到 100 条，项目几乎处于“沸腾”状态。然而，**仅 4 个 PR 被合并/关闭（合并率 8%），形成了明显的审查瓶颈**，大量工作处于待审查/待响应状态。项目当前没有发布新版本，开发火力集中在**核心内存子系统重构**、**WASM 插件化架构**以及**安全加固**三大领域。尽管架构讨论热火朝天，但在解决高优先级 Bug（如 S0 安全漏洞 #7947 和 S1 频道阻塞 #8505）上仍需投入硬资源。整体健康度呈现**高投入、高阻塞**的拉锯态势。

---

#### 2. 版本发布

（本轮无新版本发布）

---

#### 3. 项目进展

尽管 PR 合并放缓，但在功能落地和架构固化方面仍有实质推进：

*   **频道功能落实**：`#2079` (恢复 GitHub 原生频道) 和 `#6378` (Discord 频道白名单) 被关闭，标志着频道配置粒度得到增强。`#5573` (SMTP 邮件频道) 和 `#7248` (持久化缓存 Token 成本记录) 的关闭为自动化工作流和财务追踪带来了直接利好。
*   **文档架构体系建立**：贡献者 `@Audacity88` 集中提交了 5 个以上的 ADR 架构记录 PR（`#9163` [内存边界], `#9167` [多智能体边界], `#9168` [实时配置], `#9132` [后台任务], `#9170` [Agent 生命周期]）。这是一个明确的信号，表明项目在高速迭代后开始系统性地进行**架构定稿与知识沉淀**。
*   **CI 增强 (进行中)**：`#9166` 引入了差异感知的 Semgrep 扫描，旨在解决 CI 中大量误报基线噪音，这对提升代码审查质量具有重要意义。

---

#### 4. 社区热点

本日讨论最激烈的议题反映了社区对项目发展的核心诉求：

*   **治理与发展流程优化 (`#6808` - 14 条评论)**：关于“工作看板、面板自动化与标签清理”的 RFC 是今日的最热议题。社区成员普遍认为当前的标签系统难以追踪，提议通过机器人自动化来减少维护者的手动操作负担。这直接反映了项目**当前协作流程正在承受高压**，社区自发的寻求系统化解决方案。
    *   **链接**：[#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)
*   **核心记忆体架构重构 (`#8891` - 7 条评论, `#9048` - 6 条评论)**：追踪器 `#8891` (持久化内存上线) 和 RFC `#9048` (分离会话历史与长期记忆) 构成了最大的讨论集群。用户对现有“记忆混淆”的感受强烈，推动这一非功能性重构成为当前阶段的技术“主战场”。
    *   **链接**：[#8891](https://github.com/zeroclaw-labs/zeroclaw/issues/8891) , [#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)
*   **密钥管理安全化 (`#9127` - 7 条评论)**：关于抽象 `KeySource` trait 的 RFC 获得了深度讨论。这表明随着项目进入企业级试用阶段，用户对**密钥的安全注入与分类管理**提出了更高要求。
    *   **链接**：[#9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127)

---

#### 5. Bug 与稳定性

报告期内，Bug 修复工作亮点不多，但严重问题的存在感很强：

*   **S0 - 安全风险**: `#7947` (execute_pipeline 绕过工具权限门控)。这是一个典型的“混淆代理”漏洞，管道执行无视代理级别工具策略，可导致未授权操作。**目前暂无修复 PR 关联，是项目最大的技术债务之一。**
    *   **链接**：[#7947](https://github.com/zeroclaw-labs/zeroclaw/issues/7947)
*   **S1 - 工作流阻断**:
    *   `#8505` ([Bug]: Telegram 频道无法配置)。用户反馈“`channels doctor` 显示未配置，机器人不回复”，这是一个直接影响用户接入率的严重问题。
    *   `#8559` ([Bug]: 退出网页聊天窗口导致 Agent 停止工作)。用户反馈“在工作时被中断”，这严重削弱了 Agent 作为后台助手的实用性。
    *   **链接**：[#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505) , [#8559](https://github.com/zeroclaw-labs/zeroclaw/issues/8559)
*   **S2/S3 - 次要问题**:
    *   `#7808` (CLI 密钥粘贴无反馈) 和 `#9117` (Windows 下 ZeroCode 无法启动) 虽然严重度较低，但直接影响了开发者/Windows 用户的首次体验。
*   **Fix PRs 在途**:
    *   `#9105` 试图修复 Lucid 内存后端在 ARM 架构下的冷启动超时问题。
    *   `#9181` 修复 Nextcloud Talk 频道的签名认证方式。
    *   `#9007` 修复运行时历史记录按轮次裁剪而非字符裁剪，以防结构化数据损坏。

---

#### 6. 功能请求与路线图信号

*   **确定性纳入（已有对应开发中 PR）**:
    *   **频道流式化**：Telegram 多消息模式 (`#8445` -> `#8561`) 和 DingTalk 流式消息 (`#8228`) 正在推进，距离最终合并仅差代码审查。
    *   **运行时插件化**：社区与维护者共同推进的 `#8850` (RFC) 已产出实际的 WIT 接口与实现 PR (`#8863`, `#8855`)。这表明 Zeroclaw 正在从紧耦合的二进制向**动态可扩展的 Plugin 生态演进**，是 0.9 版本的核心战略。
*   **高社区呼声，或纳入后续版本**:
    *   **实时语音频道**：`#7943` 的设计获得了不少关注，定位为“仅文本传输协议”的语音接口，避免了复杂音频处理。
    *   **动态模型切换**：无论是 llama.cpp 模型路由器 (`#7539`) 还是通用多模型切换 (`#8600`)，都反映了用户在使用本地/多种模型时的痛点。
    *   **隐私优先搜索**：`#5316` (SearXNG 支持) 建议增加隐私友好的搜索引擎，收到 5 条评论，代表了特定用户群体的强烈需求。

---

#### 7. 用户反馈摘要

*   **核心痛点**：
    *   **“配置即崩溃”**：Telegram 频道无法配置 (`#8505`) 是最大的用户情绪燃点。
    *   **“窗口一关，活就白干”**：Web 界面退出导致后台任务终止 (`#8559`)，这是设计哲学与用户预期（Agent 应持续运行）之间的冲突。
    *   **“Windows 支持形同虚设”**：`#9117` 暴露了 Windows 平台缺乏开箱即用的体验。
    *   **“安全信任感缺失”**：`#7947` 的安全漏洞直接让用户对 Agent 的工具控制能力产生担忧。
*   **积极反馈与场景**：
    *   用户 `@MaoJianwei` 对于 SMTP 邮件频道的实现表示满意 (`#5573` now CLOSED)，印证了“定时任务”+“邮件报告”是一个切实的高频场景。
    *   `@Audacity88` 被多次提及负责文档和 RFC 编写，社区对于这种主动的架构治理行为给予了很高的认可度。
    *   用户对 OpenTelemetry (`#6641`) 等可观测性特性的推进表现出高度兴趣，这标志着社区从“能用就行”向“可运维”转变。

---

#### 8. 待处理积压

以下条目长期未取得关键进展，或处于“等待作者响应”的阻塞状态，需引起维护团队注意：

*   **插件化路线图被“卡喉咙”**：`#8863` (WASM WebSocket 支持) 和 `#8855` (频道镜像插件) 这两个 XL 级别的 PR 已标记 `needs-author-action` 超过 10 天。作为 0.9 版本的核心基石，如果长期失联，整个基于 WASM 的插件生态将无法推进。
*   **重构分支面临漂移风险**：`#9013` (配置重构) 和 `#9007` (运行时历史裁剪修复) 同样是 `needs-author-action`。随着每日 50 个 PR 涌入，这些大改的分支若再不推进，将面临严重的合并冲突。
*   **长期悬而未决的社区需求**：
    *   **SearXNG 搜索支持 (`#5316`)**：从 4 月提出至今，代码层面无实质性进展。
    *   **Slack 线程深度集成 (`#6055`)**：用户期望 bot 能主动获取上下文，而非仅基于 Mention 回复。
*   **维护者行动建议**：
    1.  **投入紧急资源**处理 `#7947` (S0) 和 `#8505` (S1)。
    2.  **复核 `needs-author-action`** 标记下的核心 PR，主动联系作者 `@JordanTheJet` 等人，为 0.9 版本扫清障碍。
    3.  考虑对小体量的修复/文档 PR（如 `#9181`, `#9175`）开启“快速车道”，以提升吞吐率，改善目前合并率过低的局面。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 PicoClaw（github.com/sipeed/picoclaw）GitHub 数据生成的 2026-07-20 项目动态日报。

---

## PicoClaw 项目动态日报 | 2026-07-20

### 1. 今日速览

过去 24 小时，PicoClaw 保持着社区驱动的稳定反馈节奏。共有 3 个 Issue 产生更新（含 1 个已关闭），3 个 Pull Request 处于活跃状态，项目未发布新版本。**当日活跃度评估为中等。** 值得关注的是，社区报告了一例导致 Gateway 完全无法启动的严重崩溃（#3265），同时也贡献了一例针对 Antigravity 认证令牌刷新的修复方案（#3267）。整体来看，社区反馈质量和深度较高，但 Issue 与 PR 的积压时间在拉长，维护者响应速度是当前项目健康度的主要关注点。

### 2. 版本发布
无新版本发布。

### 3. 项目进展

今日 **没有 PR 被合并或关闭**，因此暂无新的代码变更落地至主分支。目前有 3 个关键 PR 正在推进中，一旦合并将显著改善项目的稳定性和可观测性：
- **#3267 (新提交):** 修复 Antigravity 令牌刷新时的权限范围错误。
- **#3251:** 捕获 Anthropic 供应商的 Prompt 缓存 Token 计费指标，增强成本监控。
- **#3202:** 修复路由 ID 标准化函数中下划线处理不当的边界问题。

### 4. 社区热点

- **#3252 [`splitKnownProviderModel` 逻辑缺陷](https://github.com/sipeed/picoclaw/issues/3252) (8天未关闭)**
  这是目前最活跃的技术讨论点。用户发现当模型 ID 包含已知供应商别名时，`factory.go` 中的字符串切割逻辑会错误剥离供应商前缀。该讨论触及了核心路由配置的可靠性，虽然维持了 1 条评论，但其逻辑复杂性吸引着深度用户持续关注。

- **#3265 [Gateway 启动崩溃](https://github.com/sipeed/picoclaw/issues/3265) (新提交)**
  尽管评论数为 0，但该 Issue 迅速成为社区焦点。它描述了一个极其严重的用户体验问题——即使不配置 Deltachat 模块，Gateway 也无法启动。这种阻塞性 Bug 通常会引发极高的用户讨论意愿。

### 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 修复状态 |
|---|---|---|---|
| **严重 (Critical)** | [#3265](https://github.com/sipeed/picoclaw/issues/3265) | Gateway 启动失败，报错 `channel deltachat has unknown type deltachat`，即使 `config.json` 中未配置该模块 | ❌ 未关联 PR，待排查 |
| **高 (High)** | [#3252](https://github.com/sipeed/picoclaw/issues/3252) | `splitKnownProviderModel` 在特定模型命名下会错误剥离供应商前缀，导致模型识别异常 | ❌ 未关联 PR，社区讨论中 |
| **中 (Medium)** | [#3266](https://github.com/sipeed/picoclaw/issues/3266) (已关闭) | 微信渠道在非视觉模型下收到图片时，处理顺序错误，导致用户在图片保存前看到模型报错 | ✅ 已关闭 |
| **附带修复** | [#3267 (PR)](https://github.com/sipeed/picoclaw/pull/3267) | Antigravity 主认证成功但令牌刷新失败，错误原因为传递了错误的认证范围 Scope | 🛠️ 已提交 PR 待 Review |

### 6. 功能请求与路线图信号

- **Anthropic Prompt 缓存计费 (PR #3251):** 社区主动为 Anthropic 供应商提供缓存 Token 计数功能。这表明高级用户正在对 AI 调用成本进行精细化运营，**该功能极有可能被纳入下个版本**。
- **路由 ID 边界鲁棒性 (PR #3202):** 对 `NormalizeAgentID` 等函数的修复，显示出用户对 Agent/Account 命名规则的灵活性与一致性有较高要求，暗示着项目正被应用于更复杂的命名场景。
- **多供应商认证可靠性 (PR #3267 & Issue #3265):** 本周 Bug 集中在 Antigravity 和 Deltachat 等非主流供应商上。社区测试面正在扩大，**非核心供应商/渠道的集成稳定性**是当前路线图中必须解决的短板。

### 7. 用户反馈摘要

- **强烈挫败感 (配置阻塞):** “按照文档配置了 config.json，没有配置任何 Deltachat 相关的内容，但 Gateway 因为 Deltachat 的问题无法启动。” —— 反馈来自 #3265，体现了配置解析逻辑不健壮对入门用户的打击。
- **合理但尖锐的批评 (流程缺陷):** “微信渠道在非视觉模型下，先直接调用模型报错，再把图片保存下来。用户会看见一个报错信息，体验很差。” —— 来自 #3266，用户指出了事件处理管线的顺序问题。
- **企业级运维需求 (成本可见性):** “无法查看 Prompt Cache 是否生效，就没办法估算实际调用成本。” —— 来自 #3251 的 PR 描述，反映了 B 端或高频用户对成本透明度的刚需。
- **社区正向贡献 (快速修复):** 贡献者 @sarff 在提交 Issue 的同时直接给出了修复代码（#3267），体现了 PicoClaw 社区的技术深度与互助文化。

### 8. 待处理积压

以下 Issue 及 PR 已悬而未决超过一周，可能影响社区信心，建议维护者尽快响应：

- **PR [#3202](https://github.com/sipeed/picoclaw/pull/3202) (积压 19 天)** - 修复路由 ID 标准化。作者 @Osamaali313 等待 Review 中。
- **PR [#3251](https://github.com/sipeed/picoclaw/pull/3251) (积压 8 天)** - Anthropic 缓存指标捕获。功能价值清晰，建议尽快合并或给出修改意见。
- **Issue [#3252](https://github.com/sipeed/picoclaw/issues/3252) (积压 8 天)** - Provider 前缀剥离 Bug。属于核心解析逻辑错误，直接影响模型选择功能，建议下周内给出初步指导。

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>

好的，各位维护者与社区成员，以下是基于 QwenPaw (github.com/agentscope-ai/qwenpaw) 在 2026年7月20日的 GitHub 活动数据生成的动态日报。

---

## **QwenPaw 项目动态日报 | 2026-07-20**

### 1. 今日速览

今日项目活跃度中等偏高。过去24小时内，社区提交了 **11 个 Issue** 和 **6 个 Pull Request**，显示出用户积极尝试和使用新功能的热情。然而，**PR 合并率为 0%**（6个待合并），**Issue 关闭率仅为 9%**（1/11），表明维护团队在代码审核和问题响应方面面临一定压力，项目整体推进速度暂未跟上社区贡献的步伐。值得关注的是，性能优化（如MCP驱动并行化）和安全增强（如CIDR支持）是今日社区贡献的两大热点。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日无任何 PR 被合并或关闭，项目主干代码未见实质性推进。

尽管如此，有 **6 个高质量的 PR** 正等待审核，一旦合并，将显著提升项目的可维护性和安全性：
-   **安全增强**: `#6259` [PR](https://github.com/agentscope-ai/QwenPaw/pull/6259) 为免认证白名单添加了 CIDR 支持，方便运维人员管理内部网络。
-   **功能扩展**: `#6262` [PR](https://github.com/agentscope-ai/QwenPaw/pull/6262) 增加了“一键复制Agent配置”功能，提升用户体验。
-   **核心Bug修复**: `#6247` [PR](https://github.com/agentscope-ai/QwenPaw/pull/6247) 修复了因文件名过长导致的历史记录搜索崩溃问题（`OSError: [Errno 36]`）。
-   **治理改进**: `#6256` [PR](https://github.com/agentscope-ai/QwenPaw/pull/6256) 让沙箱不可用时的回退行为变得可配置，增强了对安全策略的控制。
-   **CLI 增强**: `#6251` [PR](https://github.com/agentscope-ai/QwenPaw/pull/6251) 为 CLI 添加了脚本友好型的环境变量读取功能。
-   **UI/UX 重构**: `#6195` [PR](https://github.com/agentscope-ai/QwenPaw/pull/6195) 将聊天控制台的Token使用信息重构为会话级别指示器，减少界面噪音。

### 4. 社区热点

今日最活跃的议题主要集中在 **性能优化** 和 **用户界面体验** 上。

-   **🔥 性能优化呼声最高**: `#6193` [MCP drivers start sequentially instead of in parallel](https://github.com/agentscope-ai/QwenPaw/issues/6193)
    -   **动态**: 该Issue虽已存在几天，但今日仍获4条评论，讨论热烈。
    -   **诉求**: 用户 `@zsrmoyanzsr` 指出 MCP 驱动串行初始化导致启动缓慢（8个客户端需~40秒），并通过技术分析指出问题所在。社区对此高度共鸣，期望能并行初始化以提升8倍速度。这是对项目核心性能的明确改进需求。

-   **🤔 用户界面体验分歧**: `#6240` [末尾出现注释显示](https://github.com/agentscope-ai/QwenPaw/issues/6240)
    -   **动态**: 该 Bug 已于今日被关闭，但获得3条评论。
    -   **诉求**: 用户报告在对话末尾看到不应出现的原始标记（如 `<!-- ⟦ NEXT_RID 改为 1003...`），这暴露了前端渲染或后端数据处理的问题，影响了用户体验。即使已关闭，其背后反映的“信息泄露”和前端鲁棒性问题值得关注。

### 5. Bug 与稳定性

今日报告了多个 Bug，严重程度不一，但大多数已有对应的修复 PR，情况乐观。

-   **严重**
    -   **`#6246` [`_saved_tool_refs` crashes `recall_history` with OSError: [Errno 36] File name too long](https://github.com/agentscope-ai/QwenPaw/issues/6246)**: 核心功能崩溃。在搜索历史记录时，因处理特定内容（如git diff）导致文件名过长而崩溃。**状态：已有修复 PR `#6247`，亟待合并。**

-   **中等**
    -   **`#6255` [chat error 聊天报错](https://github.com/agentscope-ai/QwenPaw/issues/6255)**: 用户聊天过程中出现 `openai.BadRequestError: Error code: 400`，与参数错误有关，可能影响所有使用OpenAI模型的用户。
    -   **`#6258` [openai 模型最大输出token不生效](https://github.com/agentscope-ai/QwenPaw/issues/6258)**: 配置的最大输出Token设置无效，可能导致API调用成本超支或输出被截断。
    -   **`#6257` [Multiple tool calls produce identical thinking output](https://github.com/agentscope-ai/QwenPaw/issues/6257)**: 单次多工具调用时，思考过程重复，影响用户体验和分析能力。
    -   **`#6261` [离线环境使用code模式，无法预览文件内容](https://github.com/agentscope-ai/QwenPaw/issues/6261)**: 核心功能在离线环境下降级，限制了特定用户场景（如安全环境）的使用。
    -   **`#6252` [Desktop (Tauri) mode — Zoom shortcuts not working on Linux](https://github.com/agentscope-ai/QwenPaw/issues/6252)**: 桌面端跨平台适配问题，影响Linux用户的可访问性。

### 6. 功能请求与路线图信号

社区正在积极贡献新功能，今日提交的多个Feature Request和PR为项目未来的发展方向提供了明确信号。

-   **高可能性纳入下一版本**
    -   **安全策略细化**: PR `#6259` (CIDR支持) 和 `#6256` (沙箱回退配置) 直指企业级部署的安全和运维需求，代码质量高，预计会很快被合并。
    -   **可复用工作流编排**: Issue `#6163` [Feature: Reusable Workflow Orchestration with Audit Trail](https://github.com/agentscope-ai/QwenPaw/issues/6163) 提出了一个具有审计追踪的可复用工作流概念，这标志着社区对 QwenPaw 从“聊天工具”向“自动化平台”演进的期待。
    -   **个性化Agent记忆**: Issue `#6263` [Feature: Support per-agent auto-memory profiles](https://github.com/agentscope-ai/QwenPaw/issues/6263) 反映了用户希望根据Agent角色定制其记忆格式（如陪伴型用日记，技术型用主题），这是对现有记忆系统的深度优化需求。

-   **UI/UX 体验升级信号**
    -   **结果展示优化**: Issue `#6260` [Feature: 在结果呈现上需要提升](https://github.com/agentscope-ai/QwenPaw/issues/6260) 非常直接地反映了用户对于思考过程过多、结果被淹没的不满。建议折叠思考过程，直接展示最终结果。这与 PR `#6195` 意图减少界面噪音的方向一致，社区对此的呼声很高。

### 7. 用户反馈摘要

-   **性能痛点**: 用户 `@zsrmoyanzsr` 对MCP驱动串行启动导致的 ~40秒启动时间表示不满，并主动提供了性能对比数据和问题定位，体现了核心用户的深度参与和技术期待。
-   **体验痛点**: 多个用户（`@azear`， `@MCQSJ`）对UI/UX提出了批评，特别是希望隐藏冗长的中间过程，直接呈现最终交付结果，并修复界面显示原始标记的错误。这表明当前版本在信息架构和用户体验细节上仍有提升空间。
-   **环境限制**: 来自离线环境用户（`@H-TWINKLE`）的反馈表明，对在线资源的依赖仍然是项目在特定高安全场景下推广的主要障碍。

### 8. 待处理积压

今日暂无长期未响应的重要议题，但以下 **高质量待合并 PR** 值得维护团队优先关注，它们均契合社区的核心需求，且已停留一段时间：

1.  **`#6195` [Refactor the ring from the end of each chat to the chat console](https://github.com/agentscope-ai/QwenPaw/pull/6195)**: 由 `@yuanxs21` 于 2026-07-16 提交，等待人工审核。该 PR 旨在重构UI，减少信息噪声，解决多个用户的痛点。
2.  **`#6256` & `#6259`**: 分别由首次贡献者 `@JOJOCrazy123` 和 `@dztyykxx` 提交，对于鼓励外部贡献至关重要，应尽快给予反馈。

</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是为您生成的 hermes-agent 项目 2026-07-20 动态日报。

---

### hermes-agent 项目动态日报 (2026-07-20)

---

#### 1. 今日速览

过去 24 小时，Hermes Agent 项目迎来了海量更新（共 500 条 Issue 与 500 个 PR），社区活跃度极高，但新开/待合并项远超已关闭项，凸显出巨大的维护积压压力。核心工作聚焦于修复最棘手的**会话状态（Session State）并发损坏**问题。尽管今日无正式版本发布，但 61 个 PR 被成功合入或关闭，项目正经历一个高强度的“还债”与优化迭代周期。

---

#### 2. 版本发布

今日无新版本发布。

---

#### 3. 项目进展

过去 24 小时共有 61 个 PR 被合并/关闭，产出效率较高。核心进展包括：

- **关键稳定性修复**：
    - **P0 级 Bug 关闭**：[#64934](https://github.com/NousResearch/hermes-agent/issues/64934) (网关会话并发楔入) 已关闭。该修复解决了网关层因时序问题导致两轮对话在同一个会话上并发运行，从而引发数据损坏和永久楔入的根本性问题，是本轮稳定性提升的最大亮点。
    - **上下文污染修复**：[#14471](https://github.com/NousResearch/hermes-agent/issues/14471) (Agent 注入无关文件) 已关闭。解决了 Agent 在工具路径中发现并使用无关的 `AGENTS.md`/`CLAUDE.md` 文件的问题，净化了 Prompt 组装链路。
- **功能推进**：
    - **配置弹性增强**：[#67696](https://github.com/NousResearch/hermes-agent/pull/67696) 使 `agent.max_turns` 配置项支持 `none` / `unlimited` 等自然语义，优化了配置体验。
    - **看板系统增强**：[#53956](https://github.com/NousResearch/hermes-agent/pull/53956) 为 `hermes kanban dispatch` 命令增加了 `--task` 标记，支持绕过并发限制进行精确任务分发。
    - **运维能力提升**：[#67149](https://github.com/NousResearch/hermes-agent/pull/67149) 一次性引入了多个健康检查与诊断工具（如 `repo_health`, `config_validator` 等），有助于提升线上运维效率。
- **测试与跨平台兼容**：
    - 由 `hermes-orca-bridge` 机器人发起的多个 PR（[#67708](https://github.com/NousResearch/hermes-agent/pull/67708), [#67710](https://github.com/NousResearch/hermes-agent/pull/67710), [#67700](https://github.com/NousResearch/hermes-agent/pull/67700), [#67703](https://github.com/NousResearch/hermes-agent/pull/67703)）正在修复 macOS 平台的多项测试，CI 覆盖正全面铺开。

---

#### 4. 社区热点

- **`#4505`: Ollama 原生 API 优化 (13 条评论)**
    用户 @declan2010 深度对比了 Ollama 原生 `/api/chat` 与 OpenAI 兼容端点的差异，引发了社区对**本地模型流式传输性能**的深度技术探讨。这反映出核心用户群体技术素养极高，对底层优化有极致的追求。
    [链接](https://github.com/NousResearch/hermes-agent/issues/4505)

- **`#509`: 认知记忆系统 (4 👍)**
    该功能请求尽管创建于 3 月初，但今日仍保持高热度。社区对 Agent 的 **“智慧记忆”**（如矛盾检测、置信度感知检索）的呼声持续高涨，这是从“对话机器人”迈向“个人知识助理”的核心诉求。
    [链接](https://github.com/NousResearch/hermes-agent/issues/509)

- **`#67012`: Keepalive 修改导致流式传输断裂 (6 条评论)**
    近期 commit (`8324dd19c`) 引入的 `keepalive_expiry=20s` 修改，被用户 @evandroid 发现会直接破坏 OpenRouter 等基于 Cloudflare 的代理服务的流式传输。这类近期引入的回归问题往往是社区反馈最激烈的地方。
    [链接](https://github.com/NousResearch/hermes-agent/issues/67012)

---

#### 5. Bug 与稳定性 (按严重程度排列)

| 严重程度 | Issue | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **P0 (严重)** | [#4319](https://github.com/NousResearch/hermes-agent/issues/4319) | KV Cache 压缩导致系统 Prompt 重建，本地 MoE 模型性能严重衰退 | 开放 **无 Fix PR** |
| **P1 (高)** | [#30387](https://github.com/NousResearch/hermes-agent/issues/30387) | `hermes -z` 正常响应后退出码 134，破坏 Shell 脚本调用 | 开放 **无 Fix PR** |
| **P1 (高)** | [#27013](https://github.com/NousResearch/hermes-agent/issues/27013) | 会话重启后 Agent 完全丢失项目上下文，产生幻觉 | 开放 **无 Fix PR** |
| **P2 (中)** | [#63078](https://github.com/NousResearch/hermes-agent/issues/63078) | 桌面端首条消息创建空白会话，完全无响应 | 开放 **无 Fix PR** |
| **P2 (中)** | [#59386](https://github.com/NousResearch/hermes-agent/issues/59386) | `delegate_task` 在严格 OpenAI 兼容后端返回不可恢复的 400 错误 | 开放 **无 Fix PR** |
| **P2 (中)** | [#67012](https://github.com/NousResearch/hermes-agent/issues/67012) | `keepalive_expiry=20s` 导致 Cloudflare/OpenRouter 流式传输中断 | 开放 **无 Fix PR** |
| **P2 (中)** | [#62726](https://github.com/NousResearch/hermes-agent/issues/62726) | Dashboard 跨标签页会话窃取（Session Bleed）及 `/new` 操作挂起 | 开放 **无 Fix PR** |
| **P2 (中)** | [#67277](https://github.com/NousResearch/hermes-agent/issues/67277) | Webhook 复用功能加载了默认配置文件而非指定配置文件的技能 | 开放 **无 Fix PR** |
| **P2 (中)** | [#67600](https://github.com/NousResearch/hermes-agent/issues/67600) | **新 Bug**：桌面端 Default 配置文件侧边栏会话列表完全清空 | 开放 **无 Fix PR** |
| **P2 (中)** | [#67368](https://github.com/NousResearch/hermes-agent/issues/67368) | 桌面端 PROJECTS 标签页在渲染后瞬间消失，仅剩 SESSIONS 标签 | 开放 **无 Fix PR** |

---

#### 6. 功能请求与路线图信号

- **即将进入开发通道的信号**：
    - **Agent 行为强制约束**：[#40662](https://github.com/NousResearch/hermes-agent/issues/40662) (PreToolUse Hook) 和 [#25061](https://github.com/NousResearch/hermes-agent/issues/25061) (记忆健康检查 Hook) 均收到强烈诉求。用户希望绕过 LLM 的“近因偏差”，在工具调用前强制执行系统规则。这两个请求均处于 `needs-decision` 状态，若落地将是 Agent 可控性的巨大飞跃。
    - **主动性能防御**：[#7489](https://github.com/NousResearch/hermes-agent/issues/7489) (基于响应头做 RPM 限流) 获得 5 个 👍。社区希望利用 API 返回的头信息主动规避 429 限流，而非被动进行昂贵的重试循环。

- **长期路线图信号**：
    - **知识库深度融合**：[#2736](https://github.com/NousResearch/hermes-agent/issues/2736) (Obsidian Vault 集成) 和 [#509](https://github.com/NousResearch/hermes-agent/issues/509) (认知记忆) 代表了将 Hermes 打造为“个人知识库大脑”的长期愿景。
    - **零摩擦生态导入**：[#524](https://github.com/NousResearch/hermes-agent/issues/524) (Agent 迁移系统) 旨在从 Claude Code、Cursor 等竞品自动导入配置，是降低新用户门槛的战略级功能，目前仍处于立项阶段。

---

#### 7. 用户反馈摘要

- **【最严重痛点】记忆与上下文丢失**：用户 @HECer 在 [#27013](https://github.com/NousResearch/hermes-agent/issues/27013) 中描述了令人沮丧的场景：Telegram 会话因超时重启后，Agent 不仅忘记了项目内容，甚至“以为自己是一个完全不同的项目”。这被社区认为是当前最破坏使用体验的缺陷。
- **【桌面端信任危机】**：用户 @mysoul12138 和 @zakhounet 分别报告了桌面端“空白会话”（[#63078](https://github.com/NousResearch/hermes-agent/issues/63078)）和“侧边栏消失”（[#67600](https://github.com/NousResearch/hermes-agent/issues/67600)）的严重问题。作为主要交互入口，桌面端的稳定性令部分用户感到失望。
- **【近期回退引发不满】**：用户 @evandroid 和 @iversoner 分别遭遇了因`keepalive`修改导致的流式传输断裂（[#67012](https://github.com/NousResearch/hermes-agent/issues/67012)）和因`schema`问题导致的不可恢复 400 错误（[#59386](https://github.com/NousResearch/hermes-agent/issues/59386)）。这表明近期提交在边缘场景中引入了显著的回退。
- **【高价值深度反馈】**：用户 @declan2010（[#4505](https://github.com/NousResearch/hermes-agent/issues/4505)）、@teknium1（[#509](https://github.com/NousResearch/hermes-agent/issues/509), [#624](https://github.com/NousResearch/hermes-agent/issues/624)）等人持续贡献了详尽的《对比分析报告》和严谨的功能设计文档，社区的技术底蕴深厚。

---

#### 8. 待处理积压

- **P0 级 Bug 悬而未决**：[#4319](https://github.com/NousResearch/hermes-agent/issues/4319) (KV Cache 压缩性能倒退) 已开放超过 3 个半月，对使用 Mixtral、Qwen3.5 等 MoE 模型的重度本地用户影响巨大，但目前仍无官方回复或解决时间表。
- **决策层积压严重**：统计中大量 Issue/PR 处于 `needs-decision` 状态（如 [#3523](https://github.com/NousResearch/hermes-agent/issues/3523), [#40662](https://github.com/NousResearch/hermes-agent/issues/40662), [#67277](https://github.com/NousResearch/hermes-agent/issues/67277), [#27013](https://github.com/NousResearch/hermes-agent/issues/27013) 等）。核心团队在技术选型和功能验收上存在明显瓶颈，建议引入 RFC 定期复盘机制或明确决策优先级。
- **社区明星功能停滞**：[#509](https://github.com/NousResearch/hermes-agent/issues/509) (认知记忆操作) 和 [#524](https://github.com/NousResearch/hermes-agent/issues/524) (Agent 迁移系统) 自 3 月初提出以来备受关注，但至今未进入开发里程碑。若能在 `ROADMAP.md` 中披露预估时间线或阶段性结论，将有助于稳定社区预期并吸引更多贡献者。

</details>

<details>
<summary><strong>AstrBot</strong> — <a href="https://github.com/AstrBotDevs/AstrBot">AstrBotDevs/AstrBot</a></summary>

# AstrBot 项目动态日报 (2026-07-20)

## 📅 数据周期
2026-07-19 00:00 – 2026-07-19 24:00 (UTC+8)

---

## 1. 今日速览

过去 24 小时，AstrBot 保持了较高的维护活跃度：**6 个 Issues** 获得更新（新开/活跃 3 个、关闭 3 个），**6 个 Pull Requests** 有变动（待合并 5 个、合并/关闭 1 个）。无新版本发布。  
亮点包括：社区反馈已久的 **WebChat 文件被强制重命名 UUID 的 Bug** 已通过 PR #8486 修复并合入；新的 **钉钉流式 AI 卡片** 和 **多 API Key 模型分发优化** 等特性正在开发中。总体看，项目在 Bug 修复与功能演进间取得平衡，生态维护健康。

---

## 2. 版本发布

无新版本发布。  

---

## 3. 项目进展

过去 24 小时合并/关闭的重要 PR 与 Issues：

### 合并的 Pull Request
- **#8486** — `fix: webchat file attachment renamed with UUID instead of original name`  
  @march-7th-mini  
  WebChat 中通过 `send_message_to_user` 等主动消息发送文件时，文件名会被强制替换为 UUID 格式，与 QQ 等平台行为不一致。该 PR 替换为保留原始文件名并加入去重计数器，彻底解决此问题。（关联 Issue #8470）  
  https://github.com/AstrBotDevs/AstrBot/pull/8486

### 关闭的 Issues
- **#8395** — 插件发布申请：图片反风控插件（astrbot_plugin_image_anti_rc） — 已关闭。  
  https://github.com/AstrBotDevs/AstrBot/issues/8395  
- **#9240** — 功能请求：插件主动消息保存到对话历史 / WebUI 记录 — 已关闭。  
  https://github.com/AstrBotDevs/AstrBot/issues/9240  
- **#8470** — Bug：WebChat 文件被重命名为 UUID — 已关闭（因 #8486 修复）。  
  https://github.com/AstrBotDevs/AstrBot/issues/8470  

这些合入与关闭表明项目在持续解决社区报告的问题，并逐步完善插件生态与平台体验。

---

## 4. 社区热点

### 最活跃的 Issue：**#7060** — 插件「图片精准撤回助手」审核讨论  
（评论数 21，2026-03-28 开启，最后更新 2026-07-19）  
该插件旨在指定用户发送图片时自动检测并撤回（仅限 QQ aiohttp/OneBot V11 平台），适用于群秩序管理。大量评论显示社区对插件审核流程、功能边界和安全性表现浓厚兴趣，同时也反映出插件市场准入机制已成为热门话题。  
https://github.com/AstrBotDevs/AstrBot/issues/7060

### 紧随其后的需求讨论：**#9240** — 插件主动消息保存到对话历史  
（评论 3，已关闭）  
开发者 @fqf060420 提出其邮件推送插件的主动消息无法在 WebUI 和 LLM 上下文中可见，影响使用。该需求引起共鸣，反映了用户对消息完整性和 LLM 上下文感知能力的强烈期待。虽然 Issue 已关闭，但背后的本质诉求仍值得关注。  
https://github.com/AstrBotDevs/AstrBot/issues/9240

---

## 5. Bug 与稳定性

| Bug 编号 | 严重程度 | 描述 | 状态 |
|----------|----------|------|------|
| #8470 | 中 | WebChat 发送文件时文件名被强制改为 UUID（已修复） | 已关闭 / 已合并（#8486） |
| #9176（via #9324） | 中 | 引用过期或不可用的图片占位符导致 agent 请求中止（`No valid file or URL provided`） | PR #9324 待合并 |
| #9232（PR） | 低 | 入站内容安全检查未检测引用消息中的违规文本，存在安全缺口 | PR #9232 待合并 |

- **#8470** 是今日唯一直接报告的 Bug Issue，修复已合入。  
- **#9324** 和 **#9232** 均为当日提交的修复性 PR，旨在增强稳定性与安全，待合并。

整体来看，项目对 Bug 响应及时，修复均已到位或进入 PR 阶段。

---

## 6. 功能请求与路线图信号

### 新提出的功能请求
- **#9282** — WebDAV 自动备份（定时备份配置与数据，提升数据安全性）  
  https://github.com/AstrBotDevs/AstrBot/issues/9282  
- **#9323** — 插件配置保存时添加进度指示通知（防止部分插件导致 WebUI 卡顿）  
  https://github.com/AstrBotDevs/AstrBot/issues/9323  
- **#9240**（已关闭） — 插件主动消息保存到对话历史（需求仍然存在，方向明确）

### 开发中的特性（已有开放 PR 且未关闭）
- **#8890** — 钉钉平台流式 AI 卡片回复（迁移自外部插件，提升钉钉体验）  
  https://github.com/AstrBotDevs/AstrBot/pull/8890  
- **#8360** — 修复插件 README 本地相对路径资源在 WebUI 无法加载的问题（改善插件文档展示）  
  https://github.com/AstrBotDevs/AstrBot/pull/8360  
- **#9325** — 优化 OpenAI 兼容提供商的多 API Key 模型发现：防止不同 Key 暴露不同模型集时导致仪表盘隐藏某些模型  
  https://github.com/AstrBotDevs/AstrBot/pull/9325  

从这些请求与 PR 中可以清楚看到，社区关注点正向 **数据备份、UI 反馈优化、多平台扩展（钉钉）、插件市场体验** 转移，项目维护者若将之纳入规划，将进一步提升用户黏性。

---

## 7. 用户反馈摘要

基于各 Issue/PR 的摘要与评论，提炼出以下核心用户声音：

- **WebChat 文件命名不一致**（#8470 / #8486）  
  “通过 WebChat 发送文件被重命名为 UUID，而在 QQ 平台正常。” — @march-7th-mini  
  用户不仅反馈问题，还定位到两处代码并提交修复 PR，体现了高质量的社区贡献。

- **主动消息缺失在对话历史**（#9240）  
  “邮件推送插件的摘要无法在 WebUI 显示，LLM 也无法感知，用户后续询问时没有上下文。” — @fqf060420  
  直接曝光了 LLM 上下文不完整和 WebUI 不透明的痛点，用户诉求明确：提供 API 将主动消息写回对话。

- **数据备份需求**（#9282）  
  “希望加个定时自动备份，最好支持 WebDAV。” — @Komorebiehco  
  表达了对数据安全和灾难恢复的朴素关切。

- **UI 交互卡顿**（#9323）  
  “部分插件可能因自身原因导致保存配置时 WebUI 卡顿，希望加点进度指示通知。” — @jin6yang  
  注重用户体验细节，对前端反馈有合理期望。

- **插件审核交流活跃**（#7060）  
  21 条评论围绕一个撤回图片插件，用户讨论焦点包括权限安全、功能合规和跨平台支持，侧面说明社区对插件质量审查的投入度较高。

---

## 8. 待处理积压

以下项目开放时间较长，且对用户体验或生态建设影响较大，建议维护者优先关注：

| 编号 | 类型 | 描述 | 开放时长 | 影响 |
|------|------|------|----------|------|
| #7060 | Issue (插件发布) | 图片精准撤回助手审核，评论 21 条，长期未关闭或合并 | 约 4 个月 | 插件市场准入流程需明确 |
| #8890 | PR | 钉钉流式 AI 卡片（L 级改动），#5785 关联，搁置 >1 个月 | 约 1 个月 | 影响钉钉用户流式体验 |
| #8360 | PR | 修复插件 README 本地相对路径图片无法加载，L 级改动 | 约 2 个月 | 影响插件文档展示完整性 |
| #9232 | PR | 内容安全增加引用文本检查，S 级改动 | 约 1 周 | 安全增强，可尽快推进合并 |
| #9282 | Issue | WebDAV 自动备份功能请求 | < 1 周 | 若接纳可尽早标注计划或收集方案 |

及时响应这些积压项，将有助于维持社区贡献热情，减少长尾问题对项目口碑的影响。

---

*报告基于 GitHub 公开数据生成，参考仓库：https://github.com/AstrBotDevs/AstrBot*

</details>

---
*本日报由 [Big Model Radar](https://github.com/huajiao1998/big_model_radar) 自动生成。*