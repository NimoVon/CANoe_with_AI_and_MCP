# DESIGN.md · 深色科技风（Vector 同款）

## 1. 画布与全局母版
- 画布：1280×720（16:9）。
- 安全区 padding：上下 20px、左右 64px。
- 默认三区：
  - A 标题块：0–120px，主标题 34px bold，左侧 8px 强调色竖条。
  - B 内容区：120–660px。
  - C 页脚条：660–720px，左"Vector CANoe AI · 研讨会分享"，右页码 `NN / 23`（14px 灰字）。
- 封面 / 章节扉页 / 结束页可用自定义版式（省略 C 区或弱化）。

## 2. 颜色系统（≤ 核心色 + 中性）
| 角色 | hex | 用途 |
| --- | --- | --- |
| 背景 bg | `#0B1220` | 页面底色、大色块 |
| 面板 surface | `#16203A` | 卡片/容器背景 |
| 主色 primary | `#38BDF8` | 标题竖条、强调线、链接、图标 |
| 强调 accent | `#F97316` | 焦点数字、标签、CTA |
| 品牌红 red | `#EF4444` | Vector 品牌点缀、关键警示 |
| 文本 text | `#E5EDF7` | 正文 |
| 次要 muted | `#94A3B8` | 副标、注释、页脚 |
- 色彩面积：背景/大色块主色 ≤60%；面板辅色 ≤30%；强调色 ≤10%（Hero 页可到 15–20%）。
- 中性（文本/边框）占剩余。
- 渐变：`linear-gradient(135deg,#0B1220 0%,#16203A 100%)` 用于封面/章节/结束背景；卡片头部可用 `linear-gradient(135deg,#38BDF8,#0EA5E9)`。
- 半透明：`rgba(56,189,248,0.08)` 面板叠层；背景图叠 `rgba(11,18,32,0.55)` 蒙版保证白字可读。

## 3. 字体系统
- 字体家族（≤2）：中文/正文 `"PingFang SC","Microsoft YaHei","Source Han Sans SC",sans-serif`；拉丁/数字 `"Inter","Helvetica Neue",Arial,sans-serif`。统一用一套 stack 即可。
- 字号阶梯：封面主标 64–72；章节大字 60–80；巨型锚点数字 72–110；页面主标 34；卡片小标题 24；正文 20–22；注释/页脚 14。
- 标题 bold，正文 regular，行高 1.5–1.6。锚点数字必须 bold 且与正文明显不同字号。

## 4. 信息密度
- 内容页留白 ≤35%，卡片填充率 ≥85%（高≥380px 卡片正文≥100字）。
- 每页 ≥1 视觉锚点（≥44px 元素 或 ≥40% 面积图）。
- 封面/章节/结束页允许更大留白，但围绕核心元素。

## 5. 配图系统
- 全部为**材料图**（用户提供的 13 张 Vector 官方截图），已复制到 `assets/` 并英文命名，已逐张核对内容/比例/清晰度。
- L1 主视觉：arch_inside_canoue / knowledge_server / ai_package / deliver_glance / getting_started / ai_analysis / agentic_config / orchestrator / roadmap_overview，占单栏 55% 或上区 55%。
- L2 支撑图：knowledge_engineers / harness_llm / ai_roadmap_detail / ai_roadmap_curve，段落旁或右/下区。
- 正文页不用全屏背景图（大图以独立组件占 55% 栏宽出现，四周可见默认深色底）。
- 不改写原图文字；需要精确文字时以干净底图 + Slide 文本叠加。

## 6. 页面映射表（契约）
| # | 文件 | 类型 | 角色 | 版式 | L1 | 字数 | 留白% | 色彩分配 | 关键约束 |
| :- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 01 | 01_cover | cover | hero | 全屏视觉+骑线文字 | — | 40 | 38% | bg60%+primary20%+accent20% | 巨型标题 |
| 02 | 02_catalog | catalog | supporting | 左标题+右内容 | — | 160 | 28% | bg40%+surface30% | 五项每项≥30字 |
| 03 | 03_section1 | section | transition | 巨型数字+章节名 | — | 30 | 45% | bg70%+primary20% | 极简大字 |
| 04 | 04_vision | content | hero | 巨型数字+洞察 | — | 160 | 30% | bg50%+accent20% | ≥48px 数字 |
| 05 | 05_challenges | content | supporting | 左标题+右内容 | — | 320 | 22% | bg40%+surface25% | 禁卡片横排 |
| 06 | 06_section2 | section | transition | 巨型数字+章节名 | — | 30 | 45% | bg70%+primary20% | 极简大字 |
| 07 | 07_mcp | content | supporting | 左标题+右内容 | — | 260 | 24% | bg45%+surface25% | 禁卡片横排 |
| 08 | 08_architecture | content | supporting | 左文字+右大图 | arch_inside_canoue | 240 | 26% | bg45%+surface20% | 图占右55% |
| 09 | 09_usemodes | content | supporting | 非对称双栏 | harness_llm(L2) | 240 | 24% | bg45%+surface20% | 60:40 |
| 10 | 10_section3 | section | transition | 巨型数字+章节名 | — | 30 | 45% | bg70%+primary20% | 极简大字 |
| 11 | 11_knowledge | content | hero | 左大图+右文字 | knowledge_server | 220 | 28% | bg45%+surface20% | 图占左55% |
| 12 | 12_aipackage | content | supporting | 上大图+下卡片 | ai_package | 220 | 26% | bg45%+surface20% | 图占上55% |
| 13 | 13_deliver | content | hero | 左大图+右文字 | deliver_glance | 200 | 28% | bg45%+surface20% | 图占左55% |
| 14 | 14_section4 | section | transition | 巨型数字+章节名 | — | 30 | 45% | bg70%+primary20% | 极简大字 |
| 15 | 15_gettingstarted | content | supporting | 左大图+右文字 | getting_started | 220 | 26% | bg45%+surface20% | 图占左55% |
| 16 | 16_analysis | content | supporting | 左文字+右大图 | ai_analysis | 220 | 26% | bg45%+surface20% | 图占右55% |
| 17 | 17_agenticconfig | content | supporting | 左大图+右文字 | agentic_config | 220 | 26% | bg45%+surface20% | 图占左55% |
| 18 | 18_orchestrator | content | hero | 上大图+下卡片 | orchestrator | 200 | 28% | bg45%+surface20% | 图占上55% |
| 19 | 19_section5 | section | transition | 巨型数字+章节名 | — | 30 | 45% | bg70%+primary20% | 极简大字 |
| 20 | 20_roadmap | content | hero | 左大图+右内容 | roadmap_overview | 220 | 26% | bg45%+surface20% | 图占左55% |
| 21 | 21_qa | content | supporting | 左标题+右内容 | — | 360 | 20% | bg40%+surface25% | 禁卡片横排 |
| 22 | 22_glossary | content | supporting | 左标题+右内容 | — | 300 | 20% | bg40%+surface25% | 表格化 |
| 23 | 23_ending | ending | hero | 全屏视觉+骑线文字 | — | 50 | 40% | bg60%+accent20% | 收束金句 |
