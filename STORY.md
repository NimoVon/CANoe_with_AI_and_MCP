# STORY.md · Vector CANoe AI 研讨会分享

## ① 用户意图对齐

- **目标受众**：团队内部技术分享 + 个人记录存档（工程师同事、自己复盘）。
- **核心目标**：让听众快速理解 Vector 把 AI 引入 CANoe 的整体方案（MCP + Knowledge Server + AI Package + 4 代理 + 路线图），并能复述关键结论与版本边界。
- **PPT 长度**：约 21–23 页（Hero 占比约 25%）。
- **视觉调性**：深色科技、克制专业、信息密度中高、与 Vector 官方深色幻灯片视觉统一。
- **内容边界**：
  - 必讲：背景愿景、五大挑战、MCP、架构、两种使用方式、Knowledge Server、AI Package、4 代理、演示要点、路线图、精选问答、术语表。
  - 不讲：逐行演讲逐字稿、与主题无关的闲谈。
  - 禁碰：编造官方译名/版本号；把 CANoe 当"独木舟"等错译。

## ② 页面布局骨架

章节数：**5 章**，对应 5 个 `type: section` 扉页，编号 01–05 连续，与目录逐字一致。

| 目录章节 | section 扉页 | 页码区间 |
| --- | --- | --- |
| 01 背景与愿景 | 03_section1 | 3 |
| 02 解决方案 · MCP 与架构 | 06_section2 | 6 |
| 03 核心组件 | 10_section3 | 10 |
| 04 实战演示 | 14_section4 | 14 |
| 05 路线图与问答 | 19_section5 | 19 |

- **Hero 页**：封面(1)、愿景巨型数字(4)、结束页(23)。占比约 3/23 ≈ 13%——偏低，追加章节扉页作为 transition 视觉节奏页，整体 Hero/transition 视觉重量页约 8 页（含 5 章节扉页+封面+结束+愿景+路线图冲击），满足 20–30% 区间。
- **rhythm**：封面 peak → 目录 valley → 章节 transition → 内容 valley/peak 交替；连续 ≥3 valley 用 transition 打断（章节扉页承担）。
- **非对称版式预算**：全篇 ≥40% 用非对称（左大图+右文字 / 左标题+右内容 / 上大图+下卡片 / 巨型数字）。仅封面、目录、章节扉页、对比页允许对称/特殊版式。

## ③ 页面大纲（23 页）

| # | 文件 | 类型 | 角色 | rhythm | 版式 | 主视觉 | 关键约束 |
| :- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 01 | 01_cover | cover | hero | peak | 全屏视觉+骑线文字 | 深色渐变+网格，Vector 红/青强调 | 巨型标题，禁装饰小图 |
| 02 | 02_catalog | catalog | supporting | valley | 左标题+右内容 | 五章列表 | 每项≥30字 |
| 03 | 03_section1 | section | transition | transition | 巨型数字+章节名 | 大号 01 | 极简大字 |
| 04 | 04_vision | content | hero | peak | 巨型数字+洞察 | 40 年 / 公式 | ≥48px 锚点数字 |
| 05 | 05_challenges | content | supporting | valley | 左标题+右内容 | 5 挑战列表 | 禁等宽卡片横排 |
| 06 | 06_section2 | section | transition | transition | 巨型数字+章节名 | 大号 02 | 极简大字 |
| 07 | 07_mcp | content | supporting | valley | 左标题+右内容 | MCP 概念 | 禁卡片横排 |
| 08 | 08_architecture | content | supporting | valley | 左文字+右大图 | arch_inside_canoue | 图占右 55% |
| 09 | 09_usemodes | content | supporting | valley | 非对称双栏 | harness_llm(L2) | 60:40 对比 |
| 10 | 10_section3 | section | transition | transition | 巨型数字+章节名 | 大号 03 | 极简大字 |
| 11 | 11_knowledge | content | hero | peak | 左大图+右文字 | knowledge_server | 图占左 55% |
| 12 | 12_aipackage | content | supporting | valley | 上大图+下卡片 | ai_package | 图占上 55% |
| 13 | 13_deliver | content | hero | peak | 左大图+右文字 | deliver_glance | 图占左 55% |
| 14 | 14_section4 | section | transition | transition | 巨型数字+章节名 | 大号 04 | 极简大字 |
| 15 | 15_gettingstarted | content | supporting | valley | 左大图+右文字 | getting_started | 图占左 55% |
| 16 | 16_analysis | content | supporting | valley | 左文字+右大图 | ai_analysis | 图占右 55% |
| 17 | 17_agenticconfig | content | supporting | valley | 左大图+右文字 | agentic_config | 图占左 55% |
| 18 | 18_orchestrator | content | hero | peak | 上大图+下卡片 | orchestrator | 图占上 55% |
| 19 | 19_section5 | section | transition | transition | 巨型数字+章节名 | 大号 05 | 极简大字 |
| 20 | 20_roadmap | content | hero | peak | 左大图+右内容 | roadmap_overview + ai_roadmap_detail(L2) | 图占左 55% |
| 21 | 21_qa | content | supporting | valley | 左标题+右内容 | 6 条精选问答 | 禁等宽卡片 |
| 22 | 22_glossary | content | supporting | valley | 左标题+右内容 | 术语表 | 表格化 |
| 23 | 23_ending | ending | hero | peak | 全屏视觉+骑线文字 | 收束金句 | 禁装饰小图 |

> 说明：原转录中挑战编号从"一/二"跳到"五"，第 3、4 项缺失，第 5 页按内容补全归类并标注；第 21 页 Q6（token/次数）原稿未作答，标注"未作答"。
