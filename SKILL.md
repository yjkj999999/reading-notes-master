---
name: reading-notes-master
description: |
  一图解千言的出版级可视化读书笔记生成器（Chart-First 图表驱动 v2.4）。
  基于 31 份精选读书笔记语料（约 2,600 页）双透镜研究：排版美学（design_metrics）+
  视觉密度（visual_metrics：逐页图像/矢量/字符实测），融合 awesome-design-md 出版级令牌 v2。
  6 大叙事原型、9 大页面模块、20 组主题色映射、10+6 类图表组件、12 类文字→图表自动映射；
  v2.1 新增情绪营销方法论库（五点情绪开关 × 五色情绪光谱 × 实证案例库）；
  v2.2 新增咨询级页面工艺库（四弧线叙事/标题纪律/页面角色/五区骨架+收束唯一/
  关系→图型选型+数据契约/反模式红线/瀑布对账/图示语义/模块填充 P-D-F-X-V/
  容量硬网格/验收四门禁+12 问，见 references/consulting-craft.md）；
  v2.3 新增图形资产管线——原样复刻 × 从文字生成全栈工具链
  （位图→矢量描摹 vtracer/potrace、Real-ESRGAN 4× 超分、mermaid/markmap 图表即代码、
  clip 文本→SVG、cognigraph MCP 集成，4 个开箱即用包装脚本，见 references/graphics-toolchain.md）；
  v2.4 新增设计智能前置层（Step 0）——全量收录四大设计技能：
  ui-ux-pro-max 检索引擎（67 风格/161 配色/57 字体搭配/13 技术栈规范 + design-system 生成器，
  纯标准库本地 BM25，英文关键词检索）+ ui-ux-pro-max-cn 中文本土化规则
  （中文字体栈/色彩文化/微信小程序规范/Element Plus·Ant Design 等国内栈/五大行业规则）+
  awesome-design-md 54 个真实品牌 DESIGN.md 全量规范（Vercel/Stripe/Linear/Notion/Claude…）+
  awesome-design 20+ 设计技能选型导航；定调从"查内置映射表"升级为"先检索设计智能库再决策"，
  详见 references/design-intelligence/INDEX.md。
  输入一本书的要点/金句/结构，输出图表主导、少文字、出版级排版的读书笔记（HTML/PDF/PPTX/长图）。
  触发词：读书笔记、生成笔记、可视化读书笔记、一图解千言、图表化笔记、读书分享、
  书摘卡片、reading notes、读书笔记PPT、读书报告、精华笔记、营销笔记、情绪开关、
  咨询级笔记、论证型笔记、图形复刻、复刻图表、位图转矢量、图片超分、
  流程图导出、思维导图导出、图表工具链、设计系统、品牌风格、做得像某品牌、
  中文产品设计、UI规范检索、设计风格推荐。
metadata:
  author: wdj
  version: 2.4.0
  license: MIT-0
---

# 一图解千言 · 出版级读书笔记生成器（reading-notes-master v2.3.1）

将任何一本书的精华内容，转化为**图表主导、少文字、一图解千言**的出版级读书笔记。
双透镜实证：排版美学来自 31 份样本的程序化实测（字体/字号/色板/结构）；
**视觉语法**来自 30 份语料逐页扫描（图像/矢量对象 + 字符密度 → `notes_study/visual_metrics.json`）：
冠军语料图表主导页占比 73%–98%、每页字符中位数 106–204c、反面教材文字墙 1,025c/页。
**核心原则：先图后文。每一页先选器型，再填文字；选不出器型的内容不配单独立页。**

## 快速开始

0. **设计智能前置**（v2.4 新增，Step 0）：判语言受众 → 跑 `design-intelligence/ui-ux-pro-max/scripts/search.py`
   英文关键词检索 → 指定品牌则读对应 DESIGN.md → 产出《设计决策单》（风格/主色/字体/禁项）。
   完整流程与降级路径见 `references/design-intelligence/INDEX.md`。
1. **收集原料**：书名、作者及履历、2–3 个核心问题、章节结构、每章要点与金句、推荐背书（可选）。
2. **选原型**：查 `references/content-framework.md` §3（六大叙事原型决策树）。
3. **图表化转译**（v2 核心步）：逐条扫每章要点，按 `references/visual-grammar.md` §2 映射表
   把文字转成器型清单（见"时间"画轴线、见"编号"拆卡片、见"数字"放大数、见"框架"连节点…）。
4. **取色排页**：《设计决策单》优先，其次查 `references/design-system.md` §3.2 改模板 `:root` 三变量换肤；
   按九大模块序列复制模板 section，内容页按 **图解页:hero图文页 ≈ 6:4** 配比铺器型，每 2–3 页切 `.alt`。
5. **导出**：按 `templates/output-pipelines.md` 出 PDF/PPTX/长图。

## 工作流（六步法 v2.4：设计智能前置→选型→定调→转译→排页→导出）

### Step 0 设计智能前置（v2.4 新增）——先检索，后决策

**任何笔记动笔前必跑**，把"凭内置映射表猜风格"升级为"证据驱动定调"：

1. **判语言/受众**：书籍内容或目标读者为中文 → 先读 `references/design-intelligence/ui-ux-pro-max-cn/SKILL.md`
   （中文字体栈/色彩文化/微信小程序规范/国内技术栈/五大行业规则/中文交付清单）。
2. **跑引擎检索**（英文关键词；中文需求先译再检，如"教育平台首页"→ `education platform landing page`）：
   ```bash
   python3 references/design-intelligence/ui-ux-pro-max/scripts/search.py "<english query>" --domain style
   # 定调三件套：--domain style（风格）/ color（配色）/ typography（字体）
   # 按需追加：--domain landing|product|chart|ux；--stack html-tailwind|nextjs|react|vue…
   # 一键聚合：--design-system -p "项目名"（五域汇总推荐；勿加 --persist，那会往 cwd 写文件）
   ```
3. **品牌风格**：用户指定品牌（"做得像 Vercel/Notion"）→ 读 `references/design-intelligence/awesome-design-md/references/<brand>.md`，
   取令牌并入模板 `:root`；未指定 → 按该技能"项目类型→推荐品牌"表主动推荐 3–5 个让用户选。
4. **产出《设计决策单》**并带入后续步骤：风格方向 / 主色与辅色（hex）/ 字体搭配 / 器型偏好 / 禁项
   （品牌 Do's&Don'ts + 中文场景禁忌，如电商忌大面积暗色、金融忌红色表亏损）。
5. **超出覆盖**：需求在四层能力之外 → 查 `references/design-intelligence/awesome-design/SKILL.md`
   决策表，向用户推荐外部技能（只推荐，不擅自安装）。

> 引擎不可用（无 python3/脚本报错）→ 降级读 `design-intelligence/ui-ux-pro-max/data/{styles,colors,typography}.csv`；
> 再不济退回内置映射表，不阻塞交付。中文场景永远可读 cn 规则（纯 Markdown 无执行依赖）。

### Step 1 选型
- 数据/年表多 → **D 数据复盘型**；名家背书强 → **E 背书营销型**；步骤工具清晰 → **B 工具方法型**；
- 章节多需自测 → **C 结构化文档型**；故事案例为主 → **A 叙事演绎型**；条目可分组 → **F 主题分组型**。

### Step 2 定调
- **《设计决策单》（Step 0 产出）优先于内置映射表**：两者冲突时以检索结果为准，并在交付说明中注明依据。
- 未跑 Step 0 时主题色查映射表（投资红 `#C20001` / 金融史青绿 `#208A88` / 战略蓝 `#537CC3` / 科技暗色 / 治愈薄荷绿 / 心理暖土系…）。
- **营销/情绪类内容**（出现痛点/痒点/爽点/燃点/爆点、情绪开关、三感三力等信号）→ 直接取
  `references/emotion-marketing.md` §1 五色情绪光谱（酒红/暖橙/金/猩红/电紫 + 暖纸 + 深紫墨），
  案例与四法矩阵同文件 §2–§4。
- 字体四字重 ≤700；字号阶梯（16:9）：封面 64–120 / 篇章 42–56 / 页标 34–40 / 正文 20–24 / 注释 14–18。
- v2 质感：负字距渐进、展示行高 1.08–1.15、耳语边框 + 三级柔影 + 圆角 8/12/16。详见 `references/design-tokens.md`。

### Step 3 图表化转译（Chart-First 核心）
- 对每章要点逐条跑 `visual-grammar.md` §2 映射表，产出**全书器型清单**（页号→器型→素材），
  动笔写 HTML 前完成；器型优先级按实测信号强度：时间线/阶段带 ≫ 编号卡 ≫ 大数字/公式卡 ≈ 框架图
  ≫ 流程链 ≫ 图标网格 ≈ 双栏对比 ≫ 漏斗 ≈ 环形 ≫ 金字塔 ≫ 象限。
- 铁律：数字必须可视化（大数字卡/图表标注）；同一章器型不相邻重复；全书 ≥6 种器型、每章 ≥2 种。
- 选不出器型的内容（纯故事/情绪）→ hero 整页图 + ≤80 字 + 图注药丸，或降级并入相邻页。
- **论证型内容页**（商业书/方法论书/数据复盘类，出现"因为/导致/证明/取决于"等论证信号）→
  升级到 `references/consulting-craft.md` 工艺：标题改判断句（§2）、按叙事弧线排页（§1）、
  图型过数据契约（§5）、机制图带证据状态（§8）。
- **图表类型交叉验证**（v2.4）：器型清单中的"数据关系"类（趋势/对比/占比/分布/漏斗），
  可用 `design-intelligence/ui-ux-pro-max/scripts/search.py "<data relationship>" --domain chart`
  校验图表选型与配色/可访问性建议，与 `chart-catalog.md` 冲突时取更具体的可访问性指引。
- **中文场景加固**（v2.4）：受众为中文读者时，器型与措辞过 `design-intelligence/ui-ux-pro-max-cn/SKILL.md`
  行业规则（如教育类忌花哨动画、金融类数字用等宽字体），落地到组件文案与图表标注。

### Step 4 排页与预算裁剪
- 页面序列：`封面 → 书档速览 stat卡 → 作者 → [背书] → [为什么读] → 目录 → (篇章 → 内容页×n)×PART → 金句×2–3 → 思维导图 → 封底`。
- 文字预算硬上限：图解页 ≤120 字、卡片页 ≤150 字，单页 >300 字=文字墙违规必须返工；
  超页时先砍文字页、不砍器型页。
- 器型实现查 `references/chart-catalog.md`（10 类组件 HTML/SVG）；每页 ≥1 个视觉锚点，0 锚点页禁发。
- **品牌风格对齐**（v2.4）：若 Step 0 选了品牌 DESIGN.md，其 Do's&Don'ts 与组件规范视为硬约束
  （如 Vercel 黑白精准、Stripe 紫渐变+轻字重），与本文件其他规则冲突时品牌规范优先。
- **中文交付清单**（v2.4，中文受众必过）：中文字体栈 fallback 完整 / 中文行高 ≥1.6 /
  按钮与 CTA 为中文 / 数字字体与中文协调 / 375–1440px 覆盖主流中文设备 / 中文屏幕阅读器兼容。
- **论证页按咨询级五区骨架排布**（`consulting-craft.md` §4）：结论型标题→主展品→支持证据+限定→
  含义或行动→来源；每页恰 1 个收束、标题全页最大字级；同排模块填充率差 ≤15pp（§9）；
  16:9 容量先算后填（§10），超容量砍内容不缩字号。

### Step 5 导出交付
- `templates/reading-notes-template.html` 为骨架（12 类页面示例与 SVG 组件）。
- 导出命令与命名规范见 `templates/output-pipelines.md`。

## 风格定制（v2 出版级令牌）

模板 `:root` 分两层，换肤只动第一层：主题层 `--c-primary / --c-primary-soft / --c-accent`
（**先查《设计决策单》，再查映射表**）；质感层（勿动）暖墨/耳语边框/三级柔影/圆角阶梯/暖纸 `#F7F5F2`/衬线。
内容页每 2–3 页加一次 `.alt`；金句页自动衬线 500。护栏详见 `references/design-tokens.md`。
v2.4 起主题层令牌可来自三处：Step 0 检索结果 > 品牌 DESIGN.md > 内置映射表。

## 图形资产管线（v2.3 新增）——任何图型/图片/图表，复刻或生成双通道

笔记所需图形资产，两条路径全覆盖（工具版本/安装/踩坑详见 `references/graphics-toolchain.md`）：

- **路径 A · 原样复刻**（复刻既有 PDF/PPTX 笔记的图形）：
  PyMuPDF 分层提取 → sn-image-base VLM 看图 → `scripts/superres.sh` 4× 超分（Real-ESRGAN）→
  `scripts/bitmap2vector.sh` 位图→矢量描摹（vtracer 彩色 / potrace 黑白）→ 组件重画。
  位图照片先超分再描摹，质量翻倍。
- **路径 B · 从文字生成**：
  流程/时序/甘特 → `scripts/mermaid-export.sh`（mmdc 三格式，已绕开 -w/-H 与 Chromium 下载坑）；
  全书结构一图流 → markmap（md→交互 HTML）；坐标轴级精确图表 → `scripts/clip-chart.sh`（.clp 文本→SVG）；
  MCP 宿主可直连 cognigraph-mcp-server（4 工具，配置见 graphics-toolchain.md §5）。

**对接工作流**：Step 3 器型清单中"流程/关系"类优先 B4 出 SVG 内嵌；Step 4 需要位图素材先 A6 超分；
Step 5 导出前统一 16:9 校验。中国市场约定：涨红跌绿、货币 ¥。

## 质量核对清单（Chart-First 出版级标准）

- [ ] **图表主导页（一个器型占版面 ≥60%）占内容页 ≥60%**（对齐冠军语料下沿 73%×0.8）
- [ ] **每页 ≤150 字正文**（图解页 ≤120）；全文搜索无 >300 字的单页文字墙
- [ ] **数字 100% 可视化**：无数字埋在段落中；关键数字用 stat 大数字卡/图表标注
- [ ] 器型多样性：全书 ≥6 种、每章 ≥2 种、同款器型不相邻重复
- [ ] 每页 ≥1 视觉锚点；≤3 族色彩；金句带引号引用原书并标章节
- [ ] 封面含书名大字+作者+笔记署名+定位语；书档速览页存在（stat 卡）
- [ ] 字号阶梯、负字距渐进、无 #000 纯文本、无 800/900 字重、阴影全出自三级柔影栈
- [ ] 暖纸 `.alt` 每 2–3 内容页一换；页眉页脚齐全；数据图表标出处；金融涨红跌绿
- [ ] **论证页通过咨询级工艺**（v2.2）：标题是判断句且为全页最大字级、每页恰 1 收束、
      图型过数据契约、无反模式红线（伪 3D/双轴伪相关/半径气泡/只报均值/截轴不声明）、来源齐全
- [ ] **设计智能层通过**（v2.4）：Step 0 已跑且《设计决策单》存在；主题色/字体可溯源到检索结果或品牌规范；
      品牌页遵守其 Do's&Don'ts；中文受众通过中文交付清单（字体栈/行高≥1.6/中文 CTA/375–1440px）
- [ ] 思维导图收尾 + 封底 Thank You；HTML 逐页无溢出无滚动条

## 参考文件索引

| 文件 | 内容 | 何时读 |
|---|---|---|
| `references/design-intelligence/INDEX.md` | **v2.4 新增：设计智能层总索引——四层能力架构/Step 0 前置检索流程/命令速查/降级路径/来源许可** | **Step 0 第一站，动笔前必读** |
| `references/design-intelligence/ui-ux-pro-max/` | **v2.4 全量收录：设计智能检索引擎**（SKILL.md 工作流 + scripts/ 4 个纯标准库脚本 + data/ 31 张 CSV：67 风格/161 配色/57 字体/13 技术栈/UX 规范/图表选型/落地页模式 + references/ 上游原文） | Step 0 检索；Step 2 定调；Step 3 图表选型交叉验证 |
| `references/design-intelligence/ui-ux-pro-max-cn/` | **v2.4 全量收录：中文本土化设计规则**（中文字体栈/中国色彩文化/微信小程序规范/国内技术栈/五大中文行业规则/中文交付清单） | 中文受众场景，Step 0/4 必读 |
| `references/design-intelligence/awesome-design-md/` | **v2.4 全量收录：54 个真实品牌 DESIGN.md 完整规范**（references/ 下按品牌名取文件，每份 9 节：主题/色板/字体/组件/布局/阴影/禁忌/响应式/提示词） | 用户指定品牌或需品牌级质感时 |
| `references/design-intelligence/awesome-design/` | **v2.4 全量收录：20+ 设计技能选型导航**（按任务/按框架决策表 + 安全扫描方法） | 需求超出四层覆盖时 |
| `references/visual-grammar.md` | **一图解千言视觉语法：实证基线+三铁律+12 类文字→图表映射+页面配比公式（v2 新增）** | Step 3 转译前必读 |
| `references/emotion-marketing.md` | **v2.1 新增：情绪营销方法论库（五点情绪开关定义/五色情绪光谱/实证案例库/五点四法观察矩阵/新增 6 器型/认知金句库）** | 营销·销售·产品·增长类内容 Step 1 前必读 |
| `references/consulting-craft.md` | **v2.2 新增：咨询级页面工艺库（四弧线叙事+adds/标题纪律+强词清单/页面角色表/五区骨架+密度三档+收束唯一/关系→图型选型+数据契约/反模式 13 红线/瀑布对账 9 条/图示语义五合同/模块填充 P-D-F-X-V/16:9 容量硬网格/验收四门禁+12 问+返工顺序）** | 商业·方法论·数据复盘类论证页 Step 3/4 必读 |
| `references/design-tokens.md` | v2 出版级质感令牌（暖墨/耳语边框/柔影栈/负字距/护栏） | Step 2 定调 |
| `references/design-system.md` | 版式/字体/字号/主题色映射/图像/页面框架件 | Step 2 定调 |
| `references/content-framework.md` | 九大模块/八模块模板/六原型/金句工程 | Step 1、4 |
| `references/chart-catalog.md` | 10 类组件实现+决策树+图文配比 | Step 4 |
| `references/graphics-toolchain.md` | **v2.3 新增：图形资产管线双路径（A 复刻 7 环节/B 生成 9 环节）+ 7 工具注册表（版本/路径/SHA256）+ 安装命令 + cognigraph MCP 配置 + 10 条踩坑库** | 需要位图描摹/超分/图表即代码/MCP 时 |
| `scripts/bitmap2vector.sh` | 位图→SVG 描摹包装器（vtracer 彩色/potrace 黑白） | 路径 A5 |
| `scripts/superres.sh` | Real-ESRGAN 4× 超分包装器（upscayl-bin） | 路径 A6 |
| `scripts/mermaid-export.sh` | mermaid→SVG/PNG/PDF 包装器（mmdc，复用本机 Chrome） | 路径 B4 |
| `scripts/clip-chart.sh` | .clp 文本→SVG 图表包装器（clip 0.8.0） | 路径 B4+ |
| `references/case-patterns.md` | 31 份语料风格档案+复用规则 | 风格参照 |
| `templates/reading-notes-template.html` | 出版级 HTML 骨架 v2.0（12 类页面，质感令牌内置） | Step 4 |
| `templates/output-pipelines.md` | PDF/PPTX/长图导出管线 | Step 5 |

## 错误处理

- **书中信息不足**（无推荐人/无作者履历）：跳过对应模块，页面序列自动收缩，不留占位符。
- **某章找不到任何器型信号**：该章压缩为 1 页金句页或 1 页 hero 叙事，禁止硬造图表。
- **无法确定主题色**：先跑 Step 0 引擎检索；仍无果则四大家族兜底——商务蓝 `#142534` / 方法论红 `#C20001` / 心理暖土 `#A5300F` / 科技暗色 `#05173E`。
- **导出 PDF 分页错位**：确认每 section 固定 720px 高、无内部溢出；检查 `@page` 尺寸。
- **内容超页**：先砍文字页、不砍器型页；一章最多 2 页；总页数向精华版 30–60 页收敛。
- **图表密度不达标**（<60%）：回 Step 3 重跑映射表——绝大多数"只能写文字"的内容其实是
  未识别的编号/时间/对比/数字信号。
- **设计智能引擎不可用**（v2.4）：无 python3 或脚本报错 → 降级读 `design-intelligence/ui-ux-pro-max/data/{styles,colors,typography}.csv`；
  中文场景无条件读 `ui-ux-pro-max-cn/SKILL.md`；均不可用 → 退回内置映射表并在交付说明中注明"未走检索"。
- **引擎中文检索 0 结果**（v2.4，已知限制）：L3 语料为英文——把需求译成英文关键词重试
  （"金融数据看板"→ `fintech data dashboard`），或直接走 L2 中文规则层。
- **品牌 DESIGN.md 与既有令牌冲突**（v2.4）：品牌 Do's&Don'ts 优先，质感层令牌（暖墨/耳语边框/柔影）保持不动，
  只让主题层向品牌色板靠拢；无法调和时在交付说明中注明取舍。
