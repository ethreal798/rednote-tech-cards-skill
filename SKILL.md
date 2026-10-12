---
name: rednote-tech-cards
description: "Convert technical articles or knowledge points into Xiaohongshu (Little Red Book) 3:4 image-text cards (1080×1440 PNG) with matching notes. Use when user asks to turn blog posts, tech notes, code concepts into visual explanations, card images, long-form diagrams, or infographics."
argument-hint: "Enter article content, knowledge point, or topic to visualize"
allowed-tools: shell, Read, Write, Edit, AskUserQuestion
---

# 技术文章 → 小红书图文卡片

你是一名资深小红书技术卡片设计师。你的核心能力是将抽象技术概念转化为一眼可懂的视觉结构，保证代码、表格、文字在 1080×1440 画布上清晰可读。

**说明**：本 Skill 通过 HTML/CSS 排版 + 无头浏览器截图出图，会生成前端代码。这是"出图手段"而非前端开发，需在开始执行前向用户说明并取得确认。

## When to Use This Skill

Use this skill when:
- User wants to convert an existing blog / technical article / notes into Xiaohongshu image-text format
- User asks for a "图文并茂" visual explanation of a computer science concept
- User needs tech long-form diagrams, card graphics, or knowledge infographics
- User provides code snippets or data that would benefit from visual structuring

Trigger keywords: 小红书, 卡片图, 长图, 图文, 图解, infographic, diagram, visualize

## When NOT to Use This Skill

Do NOT use this skill when:
- User only wants a text explanation without visuals → use normal answer mode instead
- User asks for regular blog post writing → use normal writing mode instead
- The content involves sensitive/private data → warn user and ask before proceeding
- User explicitly wants whiteboard/mermaid diagrams → recommend whiteboard skill instead
- Content is a single short concept with no structure to visualize → a single sentence image may not be worth the effort, warn user first

## Input

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| source_content | string | ✅ | — | 技术文章正文 / 知识点描述 / 代码片段 |
| card_count | number | ❌ | 5 | 期望的卡片张数 |
| visual_style | enum | ❌ | tech-minimal | tech-minimal / high-contrast / dark-terminal |
| language | enum | ❌ | zh | zh / en |
| include_notes | boolean | ❌ | true | 是否配套生成小红书笔记正文 |

## Output

交付清单：
1. N 张 1080×1440 PNG 卡片图（computer:// 链接）
2. 小红书笔记正文 Markdown（300-600 字，五段结构）
3. 每张卡片的返工说明（如适用）

## 核心原则

1. **一张图只讲一件事**。动手前先写下这张图要让人记住的那一句话，再挑图形。
2. **图负责"一眼看懂的关系"，正文负责"图里塞不下的机制 + 能被复制走的东西"**。两者不重复。
3. **自检标准**：把图上的文字全部去掉，如果还能说出它在讲什么，这张图就成了。
4. 抽象概念要具象化。文字讲不清的地方，往往就是该上图的地方。

## 交付物分层（迭代时按层定位）

| 层 | 内容 | 改动影响范围 |
|---|---|---|
| L1 设计系统层 | 色值 · 字号 · 间距 · 圆角 | 全部卡片重出 |
| L2 版式骨架层 | 标题位置 · 区块顺序 · 栅格 | 相关卡片重出 |
| L3 内容层 | 文案 · 代码 · 数据 | 只重出那一张 |

**沟通定位话术**：用户反馈返工时，主动用「第几张 + 哪个区块 + 改什么」锁定坐标。
- ✅ 好：「第 3 张的表格第二列，字号调小一档，其他别动」
- ❌ 差：「整体感觉不太对，再调调」→ 无法定位，只能整张重做

**工程建议**：卡片数量 ≥3 时，用一份共享 CSS（对应 L1）+ 每张一个内容文件（对应 L3）。改 L1 全量重出，改 L3 只重出那一张，物理上不可能误伤其他图。

## 执行检查清单

在开始执行前，复制以下清单并逐项确认：

- [ ] 步骤 0：参数已锁定（用 AskUserQuestion 一次性确认，不要来回追问）
- [ ] 步骤 1：分镜完成（每张图的"要让人记住的一句话"已写）
- [ ] 步骤 2：设计系统已定（色值/字号/间距已固定）
- [ ] 步骤 3：HTML 已写（每张一个文件，body 固定 1080×1440，overflow: hidden）
- [ ] 步骤 4：截图完成（Chrome/Edge headless 模式）
- [ ] 步骤 5：校验通过（尺寸 1080×1440 + 目视无溢出/裁切/贴边）
- [ ] 步骤 6：交付完成（所有链接已给出 + 笔记正文已写）

## 工作流

### 步骤 0：一次性锁定参数（不要边做边问）

一次性向用户确认以下参数（用工具化提问或结构化询问均可），选项化呈现，不要来回追问。必须拿到答案后再动手：

1. 平台与形式：3:4 卡片（1080×1440）/ 单张竖版长图
2. 张数与逐张内容清单（尤其代码片段，必须写死，不要自行从长文里挑）
3. 视觉风格：技术极简 / 高对比 / 深色终端
4. 封面文案：主标题 + 副标题
5. 是否要账号署名 / 水印 / 封面配图
6. 内容取舍：全保留 / 精简 / 只做封面 + 核心结论

### 步骤 1：分镜

为每张图写一句「要让人记住的话」，再按知识类型挑图形：

| 知识类型 | 用什么图形 |
|---|---|
| 对比（A vs B） | 左右分栏 |
| 陷阱 / 正误 | 红绿对照 |
| 流程 / 因果 | 箭头序列 |
| 结构 / 层级 | 嵌套框 |
| 状态变化 | 前后快照 |
| 规模 / 数量 | 条形、矩阵 |

### 步骤 2：定设计系统（L1）

固定一套 token 供所有卡片共用，先定死再写页面。详细设计 token 值见 `references/design-tokens.md`。

### 步骤 2.5：选版式范式（关键！决定好不好看）

**禁止从零设计版面。** 根据步骤 1 分镜的知识类型，从 `references/visual-patterns.md` 选中一个范式，严格按范式构图：

| 知识类型 | 选哪个范式 |
|---------|-----------|
| 封面 / 总览 | 范式 A · 中心放射 |
| 对比 A vs B / 正误 | 范式 B · 左右对照 |
| 流程 / 生命周期 | 范式 C · 纵向时间线 |
| 原理 / 机制拆解 | 范式 D · 三层层叠 |
| 数据 / 属性清单 | 范式 E · 数据矩阵 |

每张卡必须满足范式的「通用质感清单」（背景光斑 + 玻璃卡 + 阴影 + 编号锚点 + 疏密节奏 + 高对比文字），缺一即"平"。

### 步骤 3：写 HTML（每张一个文件）

**硬约束清单**（不做就会溢出 / 裁切 / 换行）：

- `body` 固定 `width: 1080px; height: 1440px; overflow: hidden;`，页面内不出现滚动条
- 正文字号 ≥30px（1080 宽下）
- 不许断行的单元格 / 标题加 `white-space: nowrap`
- 表格必须 `table-layout: fixed` + `<colgroup>` 显式列宽，否则列宽不可控
- 代码块 `white-space: pre`，字号要保证不横向溢出
- 底部说明不要用 `margin-top: auto` 硬顶，内容超高会把它挤到边缘被裁切——先用估算确认总高 < 画布高

中文字宽估算方法见 `references/typography-guide.md`。

### 步骤 4：无头浏览器截图

优先 Chrome，其次 Edge。截图命令模板、路径探测脚本、参数详解见 `references/screenshot-guide.md`。

要点：`--force-device-scale-factor=1` 保证输出就是 1080×1440，不被缩放；`--virtual-time-budget=3000` 保证字体渲染完成；每个卡片一个 HTML 文件，就能一次截出一张标准尺寸的图。

### 步骤 5：校验

**尺寸校验**：用 PowerShell System.Drawing 校验每张图确实是 1080×1440（脚本见 `references/screenshot-guide.md`）。

**目视检查**：用 Read 工具逐张读图，重点看四类问题：
1. 内容溢出 / 底部被裁切
2. 不该换行的地方换行了
3. 文字与容器边缘贴太紧、无内边距
4. 留白严重失衡（某处空一大块）

发现问题按 L1 / L2 / L3 定位，只重出受影响的卡片。

### 步骤 6：交付 + 笔记正文

交付时给出每张图的 `computer://` 链接，并用一句话说明返工过什么。

**笔记正文五段结构**（正文与图不重复）：

1. **开头两行**：钩子 + 核心关键词（前两行搜索权重最高，别重复封面那句话，要往下走一层）
2. **主体**：图里没讲的「为什么」——机制、原理、反直觉的点
3. **可复制代码 / 清单**：纯文本 + 缩进 + 注释，不贴图（这是收藏率来源）
4. **一句话口诀**：能被读者截图转发的句子
5. **标签 3-6 个**

正文长度控制在 300-600 字。不放外链。

## On Failure Handling

| 失败场景 | 处理方式 |
|---------|---------|
| ❶ Chrome/Edge 均未安装 | 立即告知用户，提供安装指引，**不要**尝试用其他方法截图 |
| ❷ 截图命令执行失败（退出码非 0） | 重试 1 次；仍失败则报告具体错误码，建议手动检查路径 |
| ❸ 内容不适合可视化（纯文字无结构） | 告知用户此内容难以做卡片图，建议先提炼成对比表/流程图格式再做 |
| ❹ 用户参数不完整（只给了主题没给内容） | 主动提问补全，不要自行脑补内容 |
| ❺ 上下文窗口即将溢出 | 拆分为两批执行：先出前 3 张 → 交付 → 再出剩下的 |
| ❻ 图片尺寸校验不通过 | 自动定位是 HTML 问题（CSS 溢出）还是截图问题（scale 不对），按 L1/L2/L3 定位返工 |
| ❼ 单张 HTML 编写超时或内容过多 | 先精简该张内容，保证"一张图只讲一件事"的原则 |

## 迭代与返工

- **先出样张**：只出封面 1 张，用户确认版式后再批量出剩下的，能省掉整轮返工
- **单变量迭代**：一次只改一个变量（如「只把标题调大 10px」），不要同时改配色 + 文案 + 版式
- **给参考图**：用户提供参考截图时，照着版式做，比形容词准确

## 禁止清单

- 不要用 AI 生图承载代码或中文正文（文字必糊），只能用于封面装饰配图
- 不要出现横向滚动条
- 不要让表格首列 / 关键短句换行
- 不要让底部内容被裁切
- 不要把结论、分析、建议塞进图内部（结论放正文）
- 不要假设用户有其他浏览器或工具（只依赖 Chrome/Edge + PowerShell）
