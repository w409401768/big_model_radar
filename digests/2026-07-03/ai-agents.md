# OpenClaw 生态日报 2026-07-03

> Issues: 181 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-07-03 08:10 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [QwenPaw](https://github.com/agentscope-ai/qwenpaw)
- [hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，这是根据您提供的 OpenClaw 项目 GitHub 数据生成的 2026-07-03 项目动态日报。

---

## OpenClaw 项目日报 | 2026-07-03

### 1. 今日速览

今日项目活跃度维持极高水平，24 小时内共处理 **681 条更新**（181 条 Issue + 500 条 PR）。但高活跃度背后潜藏着严重的 **稳定性危机**：v2026.6.11 版本引入的多项回归 Bug（重入锁遗漏、工具空输出）导致大量用户升级后遭遇会话中断。与此同时，项目的底层架构正在经历决定性转折，SQLite 全量存储迁移（PR #98236, #99006）已正式形成补丁，虽然远未达到合并标准，但标志着项目正逐步脱离 JSONL 文件存储时代。当前项目处于 **“狂飙突进”与“信任修复”** 并存的博弈期。

- **活跃度评分：** ⭐⭐⭐⭐⭐（极高）
- **健康度预警：** 🚨回归率高企，发布流程 QA 缺失，需警惕用户信任流失。

### 2. 版本发布

- 过去 24 小时内无新版本发布。社区焦点集中在对现有版本 **v2026.6.11** 暴露的严重回归问题的修复与取证上。

### 3. 项目进展

今日项目在修复与基础设施方面均有显著落地动作：

- **架构迁移（重大推进）：** 全面转向 SQLite 存储的巨大 PR (#98236) 虽然标记为“请勿合并”，但它是未来重构的预览版。同时，`refactor(transcripts): add SQLite storage backend` (PR #99006) 作为独立草案首次提交，标志着会话和转录存储的“地基”正式动工。
- **关键修复就绪：**
  - Gateway 锁文件 FD 泄漏修复 (#99291) 审核中，这是缓解长期 Gateway OOM 的关键补丁。
  - Anthropic 模式下“Thinking Block 签名无效”问题修复 (#99383) 进入活跃审查。
  - HTTP 429（服务过载）与速率限制的错误分类修复 (#99433)，避免错误的重试逻辑。
- **渠道兼容性提升：**
  - Matrix 消息字段标准化 (#99057) 解决 CLI 输出空白表格问题。
  - QQ 机器人回复元数据剥离 (#98037) 解决回复带乱码问题。
  - 飞书 Token 失效自动重试 (#97295) 更新，降低消息发送失败率。
- **CLI 优化：** 命令行别名补全功能获得了社区三个不同方向的贡献（PR #99427, #99423, #99431），体现了开发者对原生 CLI 体验的强烈共鸣。

### 4. 社区热点

过去 24 小时社区讨论热度最高的议题集中在 **会话安全与可靠性**：

1.  **#25592 (33 评论，P1, Diamond Lobster):** **工具调用间文本泄露。** 这是呼声最高的议题，大量评论指出智能体在处理逻辑时输出的中间文本（如错误处理、处理确认）被直接路由到 Slack、iMessage 等可见消息通道，造成隐私和 UX 灾难。 [链接](https://github.com/openclaw/openclaw/issues/25592)
2.  **#88312 (19 评论，P1, Platinum Hermit):** **Codex turn-completion 超时回归。** 曾被修复 (#85107) 的 Bug 再次在 2026.5.27 版本复现。用户 @yair 详细定位了回归版本，并质疑现有回归测试覆盖率不足。 [链接](https://github.com/openclaw/openclaw/issues/88312)
3.  **#92201 (18 评论，P1, Diamond Lobster):** **Anthropic 思维链思考签名验证失效。** 用户在嵌入 Agent Runner 中遭遇间歇性签名无效，由于错误信息过于泛化，系统的自动恢复钩子完全无法触发，导致会话必须手动重置。 [链接](https://github.com/openclaw/openclaw/issues/92201)
4.  **#98416 (9 评论，P1, Diamond Lobster):** **v2026.6.11 构建产物问题。** 源码包含重入锁修复 `d2da8c79d9`，但发布的 dist 包中却**缺失**此修复，直接导致 `reply session initialization conflicted`。社区对发布流程的信任被严重动摇。 [链接](https://github.com/openclaw/openclaw/issues/98416)

### 5. Bug 与稳定性

**严重 Bug 地图**（按影响范围排序）：

| 严重度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| 🔥 安全/行为失真 | #99253 | **智能体伪造用户输入并自行回答**，严重幻觉所致。 | 待安全审查 |
| 🔥 P1 回归 (6.11) | #98416 | **构建产物重入锁缺失**，回复会话初始化冲突。 | 待流程修复 |
| 🔥 P1 回归 (6.11) | #98528 | **工具调用首次后返回空输出**，严重影响代理工作流。 | **已关闭** |
| 🔥 P1 回归 (6.11) | #98614 | `sessions_spawn` 缺少 `operator.write` 权限。 | 需维护者审查 |
| 🔥 P1 稳定性 | #99263 | **Node 26 环境下 Gateway 因 FileHandle GC 崩溃**。 | 待复现 |
| 🔥 P1 稳定性 | #98938 | **Matrix 网关内存泄漏** ~4.2MB/min，每日 OOM。 | 待审查 |
| 🟡 P1 核心机制 | #88312 | **Codex 后端 Turn 完成超时**，阻塞 Telegram 等渠道。 | 待产品决策 |
| 🟡 P1 核心机制 | #25592 | **跨工具文本泄露**，核心 UX 与安全问题。 | 待安全审查 |
| ✅ 已有 Fix PR | #99383 | Anthropic Thinking 签名修复。 | 等待审查 |
| ✅ 已有 Fix PR | #99291 | Gateway 锁文件 FD 泄漏，针对 #98958 修复。 | 等待审查 |
| ✅ 已有 Fix PR | #99433 | HTTP 429 错误分类修复。 | 等待审查 |

### 6. 功能请求与路线图信号

- **多智能体协作 RFC (#35203):** 提出了完整的能力画像、共享黑板和 Token 成本治理方案，是目前最有深度的架构增强提议，暗示当前多智能体架构存在信息孤岛问题。 [链接](https://github.com/openclaw/openclaw/issues/35203)
- **Provider 智能降级 (#47910):** 提出按失败原因（认证失败 vs 速率限制 vs 过载）定向降级 Provider，避免浪费算力在坏了的 Provider 上，极具实用价值。 [链接](https://github.com/openclaw/openclaw/issues/47910)
- **用户体验觉醒：** `#75947`（UI 重做）和 `#11623`（macOS 浮动气泡）表明社区已不再满足于纯 CLI 和“AI 生成的配置页面”，开始要求消费级交互体验。
- **路线图明确信号：**
  - **SQLite 化：** `#98236` 和 `#99006` 表明存储层 Jsonl -> SQLite 迁移是坚定不移的路线图。这是为了解决并发读取和状态一致性问题。
  - **边缘推理：** `#99234` (Ollama 自动发现) 开启了节点端本地推理。配合未来可能的下放模型调用，这是一个重大的私有化部署路线信号。

### 7. 用户反馈摘要

- **更新创伤：** “升级到 `v2026.6.11` 后一切正常，但第二天早上一觉醒来，所有会话全部挂了。我什么都没动。”（@AaronFaby, `#98672`）。这反映向后兼容性体验的缺失及发布前回归测试的严重不足。
- **信息黑洞：** “Android 节点显示 `authentication needed`，但我根本不知道是该扫码、等批准还是重新配对。”（@ccaprani, `#98046`）。错误信息对用户排错几乎无帮助。
- **越界恐惧：** “智能体在回复里伪造了我的一条用户消息，然后自己回答了它。你们管这个叫 UI Bug？这是严重的安全底线失守！”（@Kaze310, `#99253`）。社区对 AI 行为边界的敏感度极高。
- **配置地狱：** “配置页面简直是一堆 AI 生成的配置项堆砌，毫无逻辑可用。”（@msbel5, `#75947`）。开发者追求极致的灵活性，但非技术用户正在被抛弃。

### 8. 待处理积压

请维护团队关注以下长期未响应或停滞的重要议题：

1.  **PR #39059 (2026-03-07):** **强化网关安全性与认证存储密封。** 关于网关超时和认证文件明文存储的修复已停在 `waiting on author` 达四个月之久。在 Token 泄露风险持续存在的当下，这一安全补丁应被优先推动。 [链接](https://github.com/openclaw/openclaw/pull/39059)
2.  **#89147 (2026-06-01):** **Long-thinking 间隙导致 Native Hook 中继饥饿。** 影响所有 Codex 代理的深度推理，虽然被标记为 P2，但一旦触发即导致整个会话停滞，PR 状态停滞。 [链接](https://github.com/openclaw/openclaw/issues/89147)
3.  **#47910 (2026-03-16):** **Provider 按故障类别回退。** 此功能可显著降低生产环境成本和延迟，目前停留在 `needs-product-decision`，缺乏明确的产品决策。 [链接](https://github.com/openclaw/openclaw/issues/47910)
4.  **#32530 (2026-03-03):** **外部工作区自动发现。** 作为降低用户入门门槛的核心功能，长期无人认领。 [链接](https://github.com/openclaw/openclaw/issues/32530)

---
**结论：** OpenClaw 正处于巨人肩膀上的踌躇期——社区活力与代码贡献量极大，但回归问题与发布质量正在消耗用户的耐心。SQLite 迁移是解决底层顽疾的正确方向，但维护团队需尽快收紧发布流程、加速关键安全补丁的合并，以重建信任。

---

## 横向生态对比

# AI 智能体与个人助手开源生态横向对比分析报告（2026-07-03）

---

## 1. 生态全景

今日生态呈现 **“头部狂奔、尾部补课、基础层重构”** 的并行态势。以 OpenClaw 为代表的大型框架贡献量惊人（24h 内 681 条更新），但回归问题和发布质量严重透支用户信任；轻量级项目 PicoClaw 通过快速响应的补丁发布和通道稳定性修复，展现出更稳健的迭代节奏。存储层向 SQLite 迁移、多通道自动重连、Agent 协作总线成为多个项目共同押注的基础设施方向，而智能体行为边界（文本泄露、伪造输入）引发的安全争议，则揭示整个生态在“能力过剩、治理滞后”上的集体短板上。

---

## 2. 各项目活跃度对比

| 项目 | Issues (24h) | PRs (24h) | 新版本发布 | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 181 | 500 | 无（v2026.6.11 存在严重回归） | ⚠️ 高度活跃但回归率高，发布流程缺乏QA，信任危机 |
| **PicoClaw** | 1（关键致命Bug） | 31 | v0.3.1（维护补丁） | ✅ 快速响应能力，配置迁移Bug在24h内已有修复PR |
| **Zeroclaw** | 当日数据未提供 | 当日数据未提供 | 未提供 | — 待后续观察 |
| **QwenPaw** | 当日数据未提供 | 当日数据未提供 | 未提供 | — 待后续观察 |
| **hermes-agent** | 当日数据未提供 | 当日数据未提供 | 未提供 | — 待后续观察 |

> 注：Zeroclaw、QwenPaw、hermes-agent 在本次日报中未提供详细动态，下文对比将重点围绕 OpenClaw 和 PicoClaw 展开。

---

## 3. OpenClaw 在生态中的定位

- **优势**：社区规模与贡献量遥遥领先，覆盖 Provider 类型最广（Anthropic、Codex 等），底层架构前瞻性强（SQLite 迁移、多智能体协作 RFC）。是生态中“定义问题”的项目。
- **劣势**：发布质量失控（v2026.6.11 多次回归、构建产物遗漏关键修复）；配置与错误信息对非技术用户极不友好；安全事件（智能体伪造用户输入）暴露出行为约束缺失。
- **与 PicoClaw 对比**：PicoClaw 体量小但迭代更稳健，当天出现的致命配置迁移 Bug 当天即提交修复 PR，而 OpenClaw 类似问题（构建缺失重入锁）缺乏快速响应机制。PicoClaw 侧重嵌入式/边缘设备 (SiPEED)，更注重部署简便性；OpenClaw 则追求企业级能力（多云、多租户、成本治理），代价是复杂度飙升。
- **与 QwenPaw / hermes-agent 对比**：从项目命名推断，QwenPaw 可能紧密绑定通义千问模型生态，hermes-agent 与 NousResearch 的 Hermes 模型深度耦合；OpenClaw 保持 Provider 无关性，更具通用性，但也更难做深度优化。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **通道连接稳定性** | OpenClaw（Matrix, QQ, 飞书 Token）、PicoClaw（WhatsApp WS 重连, Matrix 重试） | 增加自动重连、Backoff 重试、Token 失效自动刷新，降低用户手动干预 |
| **配置/数据迁移** | OpenClaw（JsonL → SQLite, PR #98236/#99006）、PicoClaw（v2→v3 配置迁移失败 Bug [#3206]） | 需要向后兼容、零停机迁移、失败回滚提示清晰 |
| **多智能体协作** | OpenClaw（RFC #35203 能力画像/共享黑板）、PicoClaw（PR #2937 Agent Collaboration Bus） | Agent 间信息孤岛亟待打破，需定义通信协议、成本治理与权限隔离 |
| **Token/成本可观测性** | OpenClaw（路线图 Token 治理）、PicoClaw（已合并 PR #3156 每轮对话 Token 用量追踪） | 用户和开发者需要细粒度成本监控，以优化 Provider 选择和 Prompt 设计 |
| **安全与行为边界** | OpenClaw（#25592 跨工具文本泄露、#99253 AI 伪造用户输入）、PicoClaw（#3161 exec 绕过全局拒绝） | 智能体输出必须严格受控，不应泄露中间数据或冒充用户；权限模式需“默认拒绝” |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | PicoClaw | QwenPaw（推断） | hermes-agent（推断） |
|---|---|---|---|---|
| **功能侧重** | 全功能 Agent 框架，多 Provider 路由、多智能体编排、成本治理 | 轻量个人助手，侧重边缘部署和多通道（Discord, WhatsApp, Matrix） | 与 Qwen 模型深度配合，强调中文场景与 AgentScope 生态 | 围绕 Hermes 模型进行推理优化与工具调用强化 |
| **目标用户** | 高级开发者、企业部署者，愿接受高复杂度换取灵活性 | 个人用户

---

## 同赛道项目详细报告

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>



</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 **PicoClaw 项目日报 (2026-07-03)**。

---

# PicoClaw 项目日报 | 2026年7月3日

## 1. 今日速览

PicoClaw 项目今日呈现**极高活跃度**，尤其在 Pull Request 方面，过去24小时内有31条更新。项目发布了新的补丁版本 v0.3.1，并针对社区反馈的关键 Bug（如配置迁移报错）迅速给出了修复 PR。令人欣喜的是，开发者们同时提交了多项针对 WhatsApp、Matrix 等不同平台通道的稳定性修复（Websocket 重连），以及面向角色权限控制等新功能的 PR，显示出项目在稳定性和功能扩展上的双重推进。尽管 Issue 数量不多，但其中包含一个影响用户正常使用的关键配置问题，目前已得到快速响应。

## 2. 版本发布

### v0.3.1
- **发布日期**: 2026-07-03
- **变更摘要**: 这是一个维护性发布版本，主要合并了多个依赖更新和改进，具体包括：
    - 合并了来自 `PierreLeGuen` 的 NearAI provider 相关 PR。
    - 合并了来自 `chengzhichao-xydt` 的关于 `codex/store lock type assert` 的修复。
    - 合并了其他一些改进和依赖更新。
- **破坏性变更**: 无。
- **迁移注意事项**: 无特殊操作，常规更新即可。

## 3. 项目进展

今日项目在修复 BUG 和提升系统稳定性方面取得了显著进展，多个关键问题通过 PR 得到解决或处于解决流程中：

- **配置迁移灾难修复**: PR [#3218](https://github.com/sipeed/picoclaw/pull/3218) 提交了针对 Issue [#3206](https://github.com/sipeed/picoclaw/issues/3206) 的修复，解决了 v2 到 v3 配置迁移过程中因 `build_info` 字段缺失导致的报错。这是今日最重要的进展之一。
- **通道稳定性提升**:
    - PR [#3220](https://github.com/sipeed/picoclaw/pull/3220) 为 WhatsApp 通道增加了 websocket 重连机制，解决了长期运行后连接静默断开的问题。
    - PR [#3219](https://github.com/sipeed/picoclaw/pull/3219) 为 Matrix 通道增加了带有 backoff 重试的同步循环，增强了网络中断后的自动恢复能力。
- **安全与功能增强**:
    - PR [#3161](https://github.com/sipeed/picoclaw/pull/3161) 已合并（状态为 CLOSED），修复了 `exec` 命令中自定义允许规则会绕过全局拒绝模式的逻辑缺陷。
    - PR [#3160](https://github.com/sipeed/picoclaw/pull/3160) 已合并（状态为 CLOSED），增加了对跨站点 Launcher 设置请求的防护。

## 4. 社区热点

今日社区焦点主要集中在两个方向：**稳定性和新功能**。

- **关键 BUG 修复与讨论**: Issue [#3206](https://github.com/sipeed/picoclaw/issues/3206) (v2→v3 配置迁移失败) 是今日唯一的 Issue，但直接影响用户升级和使用。它迅速得到了维护者响应并创建了对应的修复 PR [#3218](https://github.com/sipeed/picoclaw/pull/3218)，体现了项目对严重 Bug 的快速反应能力。
- **高价值功能 PR**:
    - PR [#3217](https://github.com/sipeed/picoclaw/pull/3217) (feat(discord): add role-based access control) 提出为 Discord 通道添加基于角色的权限控制，虽然评论不多，但该功能对于社区管理场景有较高价值，获得了 7 个单元测试验证。
    - PR [#2937](https://github.com/sipeed/picoclaw/pull/2937) (Feat/agent collaboration) 仍在持续更新中，尽管标记为 stale，但这一“Agent 协作总线”特性代表了项目未来的重要方向，社区期待度较高。

## 5. Bug 与稳定性

以下为今日记录和修复的 Bug，按严重程度排列：

| 严重程度 | Bug 描述 | Issue/PR 链接 | 状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | v2→v3 配置迁移失败，任何命令都无法使用。 | [#3206](https://github.com/sipeed/picoclaw/issues/3206) | **已修复** (PR [#3218](https://github.com/sipeed/picoclaw/pull/3218)) | 阻塞性问题，已被修复 PR 定位。 |
| **高** | WhatsApp 通道 websocket 静默断连，无法自动恢复。 | [#3220](https://github.com/sipeed/picoclaw/pull/3220) | **待合并** | 新增重连机制的修复方案。 |
| **高** | Matrix 同步循环在网络故障或服务器重启后永久退出。 | [#3219](https://github.com/sipeed/picoclaw/pull/3219) | **待合并** | 新增自动重试机制的修复方案。 |
| **中** | `exec` 命令中，自定义允许规则会绕过全局拒绝模式。 | [#3161](https://github.com/sipeed/picoclaw/pull/3161) | **已合并** | 安全隐患，已修复。 |

## 6. 功能请求与路线图信号

从今日 PR 和 Issue 中可以捕捉到未来版本可能的演进方向：

- **Agent 协作的深化**: PR [#2937](https://github.com/sipeed/picoclaw/pull/2937) (Feat/agent collaboration) 尽管 stale，但仍在推进，表明 Agent 间协作是 PicoClaw 明确的长远目标。
- **平台通道能力增强**:
    - **Discord 权限管理**: PR [#3217](https://github.com/sipeed/picoclaw/pull/3217) 提出的基于角色的访问控制，是 Discord 通道走向生产级应用的必备功能。
    - **DeltaChat 网关**: 已合并的 PR [#3063](https://github.com/sipeed/picoclaw/pull/3063) 显示项目正在拥抱更多去中心化通信协议。
- **LLM 用量追踪**: PR [#3156](https://github.com/sipeed/picoclaw/pull/3156) (已合并) 添加了每轮对话的 token 用量追踪功能，为用户提供了成本监控的能力。

## 7. 用户反馈摘要

- **配置迁移是核心痛点**: 用户 `@OhYash` 在 Issue [#3206](https://github.com/sipeed/picoclaw/issues/3206) 中报告了从 v2 升级到 v3 时，配置文件迁移完全失败，导致 `picoclaw status` 等所有命令都无法执行。这是升级场景下的一个严重用户体验问题，也是最急需解决的问题。目前该问题已被开发团队响应并提交修复。

## 8. 待处理积压

以下是一些长期未响应或标记为 `stale`，但可能对项目未来有重要影响的工作项，建议维护团队关注：

- **PR [#2937](https://github.com/sipeed/picoclaw/pull/2937) (Feat/agent collaboration)**: 已创建超过月余且标记为 `stale`。作为项目中长期战略特性，建议维护者评估其优先级并给出明确反馈，或安排专人持续跟进，避免核心功能被搁置。
- **PR [#3165](https://github.com/sipeed/picoclaw/pull/3165) (fix(openai_compat): recover Seed XML tool calls)**: 已标记为 `stale`，可能涉及与特定 LLM API（如字节跳动的豆包）的兼容性问题。考虑到社区的多样性，此类特定平台的兼容性修复虽非核心，但有助于扩展项目用户群，建议定期审视。

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/qwenpaw">agentscope-ai/qwenpaw</a></summary>



</details>

<details>
<summary><strong>hermes-agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/w409401768/big_model_radar) 自动生成。*