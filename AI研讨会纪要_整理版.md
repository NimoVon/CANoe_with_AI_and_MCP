# Vector CANoe AI 网络研讨会纪要（整理版）

> **会议官方标题**：Masterclass AI - Accelerate Your Workflows in CANoe with AI & MCP (October 13)
>
> 说明：本纪要基于两份原始转录稿合并整理——`AI研讨会记录.md`（含结构化聊天问答，缺路线图）与 `AI研讨会.md`（含路线图与口头答疑片段，缺结构化问答）。两份开头均约 188 行的内容重复副本，已去重。原稿机器翻译错译较多（如把汽车软件 **CANoe** 误译为"独木舟/皮划艇"、把 **Vector** 误译为"维克托/维特拉"、把 **LLM** 误译为"法学硕士"、把 **token** 误译为"手续费"、把 **MCP** 误译为"航海控制面板"等），本版已统一修正。专名首次出现时标注英文。

---

## 一、会议基本信息

| 项目 | 内容 |
| --- | --- |
| 主题 | Vector 将 AI 能力引入 CANoe：AI Package、MCP（模型上下文协议）与 Vector Knowledge Server |
| 主办方 | Vector Informatik（汽车工业软件公司） |
| 主讲人 | Daniela（产品概览与架构讲解）；Tobias（演示环节主讲，用户确认其为主持人之一；原转录个别处写作 "Camilla"，疑为同一人/转录误差） |
| 主持人 | Thomas Balster（负责发布活动链接与开场引导） |
| 答疑人 | David Kruse（签名 DK，在聊天区回答提问，共回复 26 次）；部分问题由其他参与者（如 Joakim Robakowski）补充回答 |
| 时间线索 | 聊天记录时段为下午 **15:07–16:08**（共 95 条消息；具体日期原稿未注明） |
| 相关活动 | Next Horizons（Vector 跨行业活动，11 月举办），报名链接：https://www.nexthorizons.com |

---

## 二、核心内容

### 1. Vector 的定位与愿景

- Vector 在汽车相关领域深耕近 40 年。
- 核心公式：**领域专长（Domain expertise）＋ 你的数据（your data）＋ 你已信任的 Vector 工具 ＝ 融入工作流的 AI**，目标是"把复杂变为进展（turning complexity into progress）"。
- 未来展望：以"霹雳游侠（Knight Rider）"应用为例，演示一个**端到端的 AI 工作流**——
  - 从需求文件出发，自动生成单元测试与虚拟 ECU（vECU）的配置代码；
  - 执行小规模（smoke）测试；
  - 分析并高亮测试报告；
  - 通过 SDX 部署功能，应用在"beacon drive"上运行。
  - 该流程跨越多个工具、贯穿整个 Vector 工具链，意味着工作方式的实质改变。
- 工作模式：把任务交给**编排器（orchestrator，即主代理）**，由它决定每次调用哪个**专用代理（specialized agent）**，并管理代理之间的交接；另有可选的**观察者（observer）**通过 Web 仪表板监控整个流程。**人在回路（human in the loop）**在其中起关键作用。
- 该工作流已在研发中，并非纯概念；想看实际效果可参加 11 月的 Next Horizons 活动。

### 2. 当前工程团队面临的挑战

> 注：原演讲中挑战编号从"一""二"直接跳到"五"，中间第三、第四项在转录中缺失或合并，本版据内容补全归类并标注缺口。

- **挑战一：重复性手工工作**。调试时常陷入循环——查测试报告、翻 trace（通信记录）、处理报文阻塞、全部重跑，周而复始；测试用例编写、REST 总线仿真、配置也都是手工点击完成。
- **挑战二：依赖大量专业知识**。要懂领域总线系统与协议，还要会写代码、做配置，门槛高。
- **挑战三/四（转录缺失）**：从上下文推断应包含两点——① 找到正确文档本身耗时费力；② 把你的配置/数据库等上下文喂给 AI 直接处理，或因 token 成本高而非常昂贵（原文在此处提到 token costs）。
- **挑战五：答案缺乏依据（ungrounded）**。通用大语言模型（LLM）给不出针对汽车领域、更别说针对你当前工程的具体答案。

### 3. 解决方案：MCP（模型上下文协议，Model Context Protocol）

- MCP 是 AI 与应用程序之间的**开放标准接口**，最初由 Anthropic 开发，现为厂商中立的开放标准，在行业内广泛使用。
- Vector 正将 MCP 及 MCP 服务器引入越来越多 Vector 工具，并不断用新 MCP 工具扩展能力。
- 对 **CANoe**（Vector 的汽车工业软件）而言，AI 现在能触及两样东西：
  1. **Vector Knowledge Server（Vector 知识服务器）**——解决"答案无依据"问题，AI 在缺知识时即时获取针对性知识，减少幻觉、提升答案质量；
  2. **CANoe 本体（通过内置 MCP 服务器）**——解决"缺少工具访问"问题，AI 可从中检索数据、控制 CANoe 等。
- 此外，**CANoe AI Package** 提供代理（agents）与技能（skills），让 AI 能承接真实任务（如写 CAPL 代码、分析 trace 数据），直至完整的"代理式工作流（agentic workflow）"。

### 4. CANoe AI 架构：Vector 提供 vs 用户自带

- **红色部分（Vector 提供，共三项）**：CANoe AI Package、Vector Knowledge Server、以及 CANoe 本体（内置 MCP 服务器与 AI 助手）。
- **蓝色部分（用户侧）**：工程师（提出目标/任务，写成提示词 prompt）、**AI 运行时/框架（harness，承载 LLM）**、以及你自己的上下文（项目数据、规范、需求、数据库）。
- **关键原则——自带模型（Bring Your Own Model, BYOM）**：Vector **不提供 LLM 本身**，用户需自带 LLM 端点（endpoint），通过已有订阅（如 GitHub Copilot、Claude）或在 VS Code、命令行工具（如 Claude Code）甚至自训模型中使用；IT 部门通常是获取端点的渠道。

### 5. 两种使用方式

- **方式一：IDE 内的聊天客户端**（如已购 GitHub Copilot / Claude 许可）。最适合开发者、高级用户、写代码/跑多步工作流/做 CI/CD 的人；LLM 端点经订阅提供，在 IDE 内配置。
- **方式二：CANoe 内置 AI 助手**。聊天窗口直接嵌在 CANoe 中，推荐给不熟悉或不便使用 VS Code 的人、主要工作在 CANoe 上的人，以及 AI 新手。
- 补充（聊天区 Joakim Robakowski）：**CANoe AI Assistant 只是一个可选的聊天界面**，若你已在使用 VS Code + Claude Code 或 GitHub Copilot，则不需要 CANoe AI Assistant。

### 6. Vector Knowledge Server（知识服务器）

- 通用 LLM 并非汽车/CANoe 专家；当 LLM 不确定或需要特定知识时，可通过 MCP 调用知识服务器，从而获得更准确、更高质量、更少幻觉的答案——答案基于 Vector 的知识而非臆测。
- **模型本身不变**：无需训练或微调，知识服务仅在你提问/提交任务时检索相关文档并注入上下文；**不会使用你的数据训练模型**。
- 使用需以 **Vector ID 认证**登录。除 LLM 自动调用外，用户也可直接经 MCP 查询 CANoe 相关问题。
- 四步示例（"如何在 Trace 窗口设置过滤器？"）：
  1. 用户提问（Ask） → 2. 检索（Retrieve） → 3. 依据文档作答（Ground） → 4. 输出答案（Answer）。
- 价值：更快得到答案（免手动翻文档）、更少幻觉、单一可信来源（single source of truth）。
- 数据来源与部署（聊天区补充）：知识服务器主要由 **CANoe 帮助与知识库**填充，**每次发布至少更新一次**；**目前无法部署在客户自有基础设施上，由 Vector 托管**。

### 7. CANoe AI Package（AI 软件包）

- 包含三部分：**代理（agents）**、**技能（skills）**、预配置的 **MCP 服务器**。
  - 代理：为特定任务预定义的专职角色，如编码代理（写/解释/优化代码，并通过 MCP 用 CANoe 编译核验）。
  - 技能：代理可复用的领域专长，约 20 个，跨代理共享（如"如何用 C#/Python 写 CAPL 代码"）。
  - 两个预配置 MCP 服务器：Vector Knowledge Server ＋ CANoe MCP 服务器（覆盖其余 CANoe 功能）。
- 以插件形式提供，易于安装；含 README 逐步指引。
- 兼容 **CANoe 20 Service Pack 2（CANoe 20 SP2）**；可从 Vector 官网下载（聊天区也会发链接）。
- 文档位于 CANoe 帮助中：Software Interfaces → AI Features → MCP，含说明、教程与入门指南。

### 8. 交付内容总结

- Vector 侧提供：CANoe 内置 AI 助手，以及**已部署的 4 个代理**——
  1. **Discovery 代理**：将 AI 能力（代理/技能/MCP 工具）与你 CANoe 配置中的元素匹配，并建议可运行的工作流；
  2. **Configuration 代理**：读取并可修改你的配置；
  3. **Coding 代理**：面向 CAPL 与 Python；
  4. **Analysis 代理**：帮你分析数据。
- 四个代理共享一套技能；另提供大量 MCP 工具。
- 第三支柱——**一切皆代码（Everything as Code）**：可用 YAML 描述测试单元与测试树；全部以 Vector Knowledge Server 为根基。
- 用户侧可扩展：自带 LLM 端点（强制）、可选自带代理/技能/MCP 工具，以及自己的项目上下文。Discovery 代理也会把你的自定义能力纳入建议。代理与技能均为**人类可读**，可按需修改。

### 9. 演示环节（Tobias 主讲）

1. **安装 AI Package**：需 CANoe 20 SP2；从 Vector 官网下载；官网提供 Copilot、Claude Code、CANoe 内置聊天界面及其他 harness 的安装指南与完整文档。
2. **CANoe 内置聊天客户端配置**：顶部工具栏"AI Assistant"→ 设置 → 配置 LLM（命名、选供应商如 OpenAI/Anthropic/Google、填 API Key 与端点 URL、选模型版本）→ 选代理文件（markdown）→ 开关技能 → 配置 MCP 服务器（填入文档中的 URL，如 Vector Knowledge Server）→ 连接即就绪。
3. **VS Code（Copilot）配置**：打开 Copilot 聊天 → 设置 → 插件 → 从本地路径安装 "Canoe Copilot" 插件（含所有代理、技能与预配置 MCP 服务器）→ 选代理即可开始。
4. **工作流一 · 分析工作流**：用 Protocol Monitor（协议监控器）分析日志文件与通信，代理自动读日志、定位错误与时间戳、生成概览与建议，并可创建过滤器聚焦出错服务，大幅加快问题定位。
5. **知识服务器查询示例**：直接问"Trace 窗口文档"，代理检索 Vector 文档并给出摘要＋原文链接，点击直达帮助页。
6. **工作流二 · 扩展现有配置**：在一个含 CAN 与 LIN 网络的配置中，仅用自然语言要求"在 CAN 与 LIN 间实现网关节点"，代理即向配置添加网关节点、生成（空）CAPL 脚本；再要求其实现网关行为，代理补全代码；最后让其运行测量并聚焦网关流量，验证代码确实生效。
7. **工作流三 · 编排器驱动的代理式工作流**：以"车窗升降（window lift）ECU"为例，用 **编排器（orchestrator）** 统筹 **编码代理 / 测试运行代理 / 测试报告代理**，读取测试规范（vTEST Studio 生成）后自动实现测试用例、运行测试、产出报告。采用子代理的好处是各自上下文干净、专注度高；编排器仅看各代理结果，可据结果动态决定下一步、迭代编码或测试，而非固定顺序的流水线。

### 10. 产品路线图（Roadmap，Daniela 收尾演讲）

> 本节省自 `AI研讨会.md`（`AI研讨会记录.md` 未含此节）。时间表述为相对节点，具体发布月份以官方为准。

- **已发布（CANoe 20 SP2）**：
  - CANoe MCP 服务器（Desktop 桌面版），配套大量 MCP 工具；
  - 内置聊天客户端（AI Assistant）；
  - Vector Knowledge Server（知识服务器）；
  - CANoe AI Package（代理 agents + 技能 skills）。
  - 已演示的用例：测试用例的设计/管理、测试执行与报告、VCDL 支持；诊断案例（设置部分 IP trace 过滤器）、CANoe 配置的读取与修改。
- **2026 年底前规划**：
  - 将 MCP 支持扩展到 **CANoe Server 版（无界面/测试台用）**、**CANalyzer**、以及**测量与标定版（CANoe .MAT）**；
  - **vTEST Studio** 计划推出自有 MCP 服务器（聊天区补充：**将于 11 月随 CANoe 21 发布**）；
  - 扩展 MCP 工具覆盖 **trace 与分析、数据库访问、面板（panels）**；
  - 新增代理与技能，支撑围绕上述主题的代理式工作流。
- **2027 年及以后**：持续扩展 MCP 能力、代理、技能与知识服务器；构建覆盖**应用与通信的仿真、分析、测试**的工作流。
- **更宏观的 Vector AI 路线图**："我们已进入新阶段——MCP 正进入越来越多 Vector 工具，并启用了首批代理式工作流。"2027 年在代理式工作流基础上持续扩展 AI 能力、自动化更多流程；更远未来将扩展到更大规模、更复杂的**端到端代理式工作流**（即开场展示的"霹雳游侠"式场景），目标是帮助工程师更高效、更快推进开发周期。

---

## 三、问答环节（Q&A，整理自聊天区）

> 主持人 Thomas Balster 于 15:13 提示："如有关于演讲主题的问题，请在此聊天窗口提出，Tobias 和 David 期待为您解答。"聊天区共 95 条消息、**跨度 15:07–16:08**，David Kruse 回复 26 次。以下按时间顺序整理，**未作答项已标注**；标记 **【你】** 者为本次研讨会中你本人提出的提问。

**Q1 — 授权/费用（Vaibhav Bait，15:15）**
MCP 功能需要单独购买，还是随 CANoe 工具及授权一起提供？
**A（David Kruse，15:17）**：随 **CANoe 20 SP2** 一同提供，使用普通授权即可，**无需单独购买** MCP 功能（自 CANoe 20 SP2 起可用）。

**Q2 — 支持的版本（Venkata Sai Teja Nallapati，15:15；Ashwin Malpe，15:15 同类问）**
该能力从哪个 CANoe 版本开始？CANoe MCP 支持哪些版本？
**A（David Kruse，15:17）**：**CANoe 20 SP2**。（注：Ashwin 的同主题提问未另作答，答案同上。）

**Q3 — 旧版本兼容性（Cristina Croitoru，15:18）**
能否用于旧版本，例如 CANoe 17？
**A（David Kruse，15:20）**：**旧版 CANoe 不提供 MCP 接口**，因此不支持。

**Q4 — 数据处理与隐私（Roman Psenica，15:17）**
数据如何处理？是本地存储，还是发送到本环境之外的服务器？
**A（David Kruse，15:19）**：你的 **AI 运行时（harness）** 会把数据发往其所用的 **AI 模型**处处理（例如 Anthropic 或 OpenAI）。

**Q5 — 改写/优化既有 CAPL 脚本（Venkata Sai Teja Nallapati，15:18）**
能否用 CANoe AI 修改或改进现有 CAPL 脚本，以消除偶发/不稳定测试？
**A（David Kruse，15:20）**：**可以，这是 AI 功能的典型用例**。得益于 CANoe AI Package 中发布的"如何写 CAPL 代码"技能，AI 很擅长编写 CAPL 代码。

**Q6 — 调用次数与 token（Venkata Sai Teja Nallapati，15:22，未作答）**
是否不依赖 token？能否不限次数使用，直到测试得到预期结果？
（注：原转录中 David 未对此条回复，可能受时段限制；可理解为调用次数取决于你所带 LLM 端点的额度与策略。）

**Q7 — 向知识服务器添加自定义信息（Schäfer，15:19）**
能否向知识服务器添加自定义信息（如自定义 DLL 或自有项目最佳实践），例如在对应文件夹创建 markdown？
**A（David Kruse，15:28）**：思路是——Vector 提供"AI 如何使用 CANoe"的知识与上下文，你提供关于自身流程与工具的额外上下文。**推荐做法是你自行开发并注册到 AI 运行时（harness）的技能（Skills）**，这样独立于 Vector 知识服务器（该服务器本身不支持添加自定义信息）。

**Q8 —【你】公司数据安全（15:26）**
用在线大语言模型做编码任务时，如何保障公司数据安全？
**A（David Kruse，15:31）**：这需要**由你自己、并经由你与 AI 供应商的合同**来决定；Vector 只提供与 CANoe 及 CANoe 相关文件交互的 AI 工具。**由你决定允许 AI 读取哪些文件、选择哪家 AI 供应商**。

**Q9 — 客户数据/IP 保护、知识服务器来源与自托管（Siddharth Amondikar，15:29）**
客户特定数据与 IP 经 MCP 送入 CANoe 时如何保障？Vector Knowledge Server 由哪些数据来源填充、多久更新一次？能否部署在我们自己的服务器上？
**A（David Kruse，15:34）**：
1. 需由你自己确保所用 AI 代理有权查看你的 CANoe 项目文件——**CANoe MCP Server 只提供查看/编辑 CANoe 配置的工具，数据不在 Vector 服务器上处理**；
2. 知识服务器主要由 **CANoe 帮助与知识库**填充，**每次发布至少更新一次**；
3. **目前无法在客户自有基础设施上部署知识服务器，由 Vector 托管**。

**Q10 — ALM 集成（Polarion）（Loic，15:28）**
能否接入 Polarion 这类 ALM，获取需求、测试用例与缺陷？
**A（David Kruse，15:29）**：**可以**。目标是 AI 代理能访问你所需的全部工具与上下文；AI 会协同使用**多个 MCP 服务器**完成跨工具的复杂用例，例如把需求关联到 CANoe 测试用例。

**Q11 —【你】AI 生成的 .can 文件识别（15:44）**
AI 代理生成的 `.can` 文件如何让 CANoe 正确识别？此前不用 CANoe AI Package 生成测试代码时，CANoe 无法识别生成的文件；已发布的技能支持这一功能吗？
**A（David Kruse，15:46）**：写仿真时，**CANoe MCP Server** 提供在仿真节点添加 `.can` 文件的功能；若是测试文件，可通过 **`.vtestunit.yaml`** 配置文件添加；AI 还能通过 MCP Server **编译 `.can` 文件，获得直接反馈并自行修正**引入的错误。

**Q12 —【你】DeepSeek 连接问题（15:51）**
CANoe 20 似乎对 DeepSeek 支持不佳，填入 DeepSeek API key 后连接失败，是 demo 版限制还是 DeepSeek 近期更新所致？
**A（David Kruse，15:52）**：**已知问题**，将在 **CANoe 21** 中修复，也可能通过补丁修复。

**Q13 —【你】多供应商 API 配额（15:59，未作答）**
若在 CANoe 中配置 GPT API、在 AI 代理中配置 Claude API，会有什么影响？主要消耗哪个的用量配额？
（原转录未见回复。）

**Q14 — 从需求自动生成 CAPL 测试脚本（Sandeep，15:52）**
能否从需求自动生成 CAPL 测试脚本？
**A（David Kruse，15:53）**：**可以，这正是目标用例**；将在 Next Horizons 的大型演示中展示——AI 仅基于需求即可实现并测试一个完整功能。

**Q15 — DoIP / CAN 协议测试用例（vivek Yaragatti，16:00）**
能否生成 DoIP 与 CAN 协议的测试用例？
**A（David Kruse，16:01）**：**可以**。若结合 **CANdelaStudio MCP Server（随 Version 25 发布）** 会更强——它让 AI 能访问诊断描述（CANdelaStudio）。

**Q16 — 外部日志分析与外部代理（Mohamed Liwa Troudi，15:30）**
若测试程序与外部工具交互并产生额外日志/数据用于判定 Pass/Fail，AI 代理能否扩展去分析、关联这些产物（而非只看 CANoe 的 BLF/HTML 报告）？能否向 CANoe 添加外部代理？
**A（David Kruse，15:37）**：**可以**。AI 代理可访问的不止 CANoe 工具，也能分析外部数据、结合外部工具与 CANoe 能力；建议**添加描述你的环境与工作流的自定义技能**。

**Q17 — 集成 Copilot / Claude 与 AI Assistant 定位（Grzegorz Pasterny，15:29；Joakim Robakowski，15:37）**
能否把你们的 AI 能力集成到 Copilot 或 Claude？（为何还要在 CANoe 里选 LLM？）
**A（David Kruse，15:35/15:36）**：**Copilot 与 Claude 均支持**，安装包内的 `Readme.html` 含安装指引（下载地址见下方官方链接）。Joakim 补充：**CANoe AI Assistant 只是一个可选的聊天界面**，若你已使用 VS Code + Claude Code 或 GitHub Copilot，则不需要 CANoe AI Assistant。

**Q18 — Copilot 基础版 vs 高级版（Loic，15:32）**
使用 Copilot 基础版与高级版有何限制差异？
**A（David Kruse，15:44）**：（基础版）可用的**模型更弱、用量额度更少**。

**Q19 — 录播与视频（Roman Psenica 15:23；Bacheikh 15:34；praveen 16:04）**
能否提供本次介绍的录播 / 视频？
**A（Thomas Balster；David Kruse 15:43）**：**会**；演讲链接将在数日内通过邮件分享，相关视频可在官网观看（见下方官方链接）。

**Q20 — vTESTstudio 测试用例规范（Andrea Carnelli，16:03）**
vTESTstudio 里的"测试用例规范"是什么？只是从 Polarion 导入的需求列表，还是供代理翻译成 CAPL 函数/测试用例的详细描述？
**A（Joakim Robakowski，16:06）**：在 vTESTstudio（或 YAML 测试单元）中处理的是 **trace items（可追溯项）**，可源自需求或测试规范，分别称为**"需求驱动"或"用例驱动"**工作流。参见官方 Traceability 帮助页。

**Q21 — 硬件兼容性 VN1640（Varsha Verma，16:00；由其他参与者回复）**
CANoe 20 是否兼容 VN1640 硬件？
**A（Tiwari Nikhil，16:04）**：兼容；**所有较新的 NVLM 授权模型均兼容 VN1640**。

**未作答提问汇总**（聊天区未获 Vector 方回复，供后续跟进）：

- CANoe < 20 的向后兼容性（Alain Fernandez，15:59）
- 录制过程中能否做实时分析（Loic，15:59）
- 能否自动生成面板（panels）（Loic，16:00）
- 许可证是否比 CANoe 19 更贵（Loic，16:03）
- AI 功能是否限时免费（Jacob, Nathanael，16:06）
- 聊天区数据是否留在本地/是否经 Vector 云处理（Hariharan，16:05）
- vTestStudio 从哪个版本开始支持 AI（约 15:45）

**聊天区发布的官方链接**（建议收藏）：

| 用途 | 链接 |
| --- | --- |
| CANoe AI 产品页 | https://www.vector.com/canoe-ai |
| AI Package 下载页 | https://www.vector.com/en/product/canoe/canoe-ai-features/canoe-ai-package/ |
| 视频/演示页 | https://www.vector.com/en/product/canoe/canoe-ai-features/ |
| 反馈问卷 | https://www.vector.com/canoe-ai-mcp-feedback |

**补充链接（Ziggy，15:19）**：https://vector.zf-world.com/vlm/faq/23/ （相关 FAQ 参考，非提问）

**口头答疑补充（主持人现场口述，整理自 `AI研讨会.md`，原转录对版本名有误差）**：有参与者询问各 CANoe 版本的区别，主持人区分如下——

- **CANoe Desktop 桌面版**：带图形界面（GUI），更适合交互式操作与日常使用；本场演示均基于此版。
- **CANoe Server 版（无界面/headless）**：适合在测试台（test bench）上无人值守地批量跑测试，无需 GUI。
- **CANoe 测量与标定版（CANoe .MAT，原转录误作 "Mattech"）**：面向测量与标定（measurement & calibration）场景。

> 注：原转录把 "Server Edition" 听成 "Survey Edition"、"CANoe" 听成 "kinematic"，上述为据上下文还原的准确含义。

---

## 四、术语表（中英对照，统一译法）

| 英文 / 原文 | 本纪要译法 | 说明 |
| --- | --- | --- |
| CANoe | CANoe（保留） | Vector 公司的**汽车工业软件**，非"独木舟/皮划艇" |
| Vector | Vector（保留） | 德国汽车软件公司，非"维克托/维特拉"，**也非数学词"向量"** |
| MCP | 模型上下文协议（MCP） | Model Context Protocol，开放标准接口，非"航海控制面板" |
| LLM | 大语言模型 | Large Language Model，非"法学硕士" |
| orchestrator | 编排器 / 协调器 | 统筹各专用代理的主代理 |
| agent | 代理 | AI 中的专职角色（区别于"代理商"） |
| harness | AI 运行时 / AI 框架 | 承载并运行 LLM 的环境，非"马具" |
| token | 令牌 / token | LLM 计费与上下文单位，非"手续费" |
| skill | 技能 | 代理可复用的领域专长 |
| CAPL | CAPL（保留） | CANoe 的专用编程语言 |
| ECU | 电子控制单元 | Electronic Control Unit |
| vECU | 虚拟电子控制单元 | virtual ECU |
| SDX | SDX（保留） | Vector 的软件交付/部署相关组件 |
| BYOM | 自带模型 | Bring Your Own Model |
| human in the loop | 人在回路 / 人工介入 | 关键操作需人工审批 |
| agentic workflow | 代理式工作流 | 多代理协作完成任务的流程 |
| RAG | 检索增强生成 | Retrieval Augmented Generation，知识服务器的底层机制 |
| CANdelaStudio | CANdelaStudio（保留） | Vector 诊断描述工具，已发布自有 MCP 服务器 |
| Next Horizons | Next Horizons（保留） | Vector 跨行业活动 |

---

## 五、待确认 / 说明

1. **挑战编号缺口**：原演讲挑战从"一/二"跳到"五"，第三、第四项在转录中缺失或合并，已在第二节据上下文补全归类，建议向主办方核实原始分类。
2. **演讲者姓名**：概览由 Daniela 讲解、演示由 Tobias 主讲；原转录中出现的 "Camilla" 疑为 Tobias 的转录误差或与第三方主持人混淆，已按你提供的"Tobias Osterloh 为主持人之一"校正。
3. **专名保留**：CANoe、Vector、MCP、CAPL、SDX、LLM、Next Horizons 等均为产品或协议专有名词，按行业惯例保留英文，避免歧义。
4. **日期**：官方标题标注为 **(October 13)**；聊天记录时段为下午 **15:07–16:08**（95 条消息）。年份按上下文记为 2026。
5. **未作答提问**：除 Q6（token/调用次数）外，另有 7 条未获回复的提问已汇总于第三节"未作答提问汇总"，建议后续向 Vector 反馈问卷或官方渠道确认。
6. **两份源文件互补**：`AI研讨会记录.md` 含结构化聊天问答但**缺路线图**；`AI研讨会.md` 含路线图与口头答疑片段但**缺结构化问答**。两份开头均约 188 行重复副本。本纪要已合并两者，并去重、修正译法，为目前最完整的整理版本。
