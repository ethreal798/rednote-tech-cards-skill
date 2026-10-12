# rednote-tech-cards

一个将技术文章 / 知识点转化为小红书 3:4 图文卡片的 AI Agent Skill。

通过 HTML/CSS 排版 + 无头浏览器截图，自动生成统一视觉风格的卡片组，并配套小红书笔记正文。

## ✨ 功能特性

- 🎨 **自动分镜**：根据内容类型（对比、流程图、嵌套结构、状态变化...）匹配最优图形
- 🎯 **统一设计系统**：三种视觉风格可选（技术极简 / 高对比 / 深色终端）
- 📐 **精确尺寸输出**：1080×1440 PNG（3:4），保证不溢出、不裁切
- 📝 **配套笔记正文**：自动生成五段结构小红书笔记（钩子→主体→代码→口诀→标签）
- 🧩 **渐进式披露**：SKILL.md 精简核心指令 + references/ 按需加载参考资料

## 📋 依赖

| 依赖 | 说明 |
|------|------|
| Chrome 或 Edge 浏览器 | 用于无头模式截图 |
| PowerShell（Windows） | 执行截图和校验脚本 |
| 支持 SKILL.md 的 AI Agent | Trae / GitHub Copilot / Claude Code 等 |

## 🚀 安装

### Trae

```bash
cp -r rednote-tech-cards/ ~/.trae/skills/
```

### GitHub Copilot

```bash
cp -r rednote-tech-cards/ ~/.copilot/skills/
```

### Claude Code

```bash
cp -r rednote-tech-cards/ ~/.claude/skills/
```

### 跨项目共享

将整个 `rednote-tech-cards/` 目录放到项目仓库的 `.github/skills/` 或 `.agents/skills/` 下，团队成员自动可用。

## 💬 使用

直接在对话中说：

```
帮我把这篇文章做成小红书卡片：[粘贴文章内容]

把 Python 装饰器做成 5 张图文卡

用 rednote-tech-cards 把 HTTP 缓存机制做成高对比风格
```

### 支持的参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| 卡片数量 | 5 | 可指定任意数量 |
| 视觉风格 | tech-minimal | tech-minimal / high-contrast / dark-terminal |
| 语言 | zh | zh / en |
| 配套笔记 | true | 是否生成小红书笔记正文 |

## 📁 目录结构

```
rednote-tech-cards/
├── SKILL.md                         # 核心指令（~120 行）
├── README.md                        # 本文件
├── LICENSE                          # MIT License
└── references/                      # 参考资料（按需加载）
    ├── screenshot-guide.md          # 截图命令模板
    ├── typography-guide.md          # 中文字宽估算
    └── design-tokens.md             # 设计系统色值/字号
```

## 🛠️ 工作流

```
用户提需求 → 参数锁定 → 分镜设计 → 写 HTML → 无头浏览器截图 → 校验 → 交付
    ↓                    ↓          ↓
 步骤 0             步骤 1      步骤 3
 参数锁定          分镜清单    每张一个文件
```

## ⚠️ 已知限制

- 仅支持 Windows + Chrome/Edge 截图（macOS/Linux 需要自行适配）
- AI 生图仅用于封面装饰，**不要**用于承载代码或中文正文（会糊）
- 上下文窗口溢出时需拆分为多批执行

## 🤝 贡献

欢迎 Issue 和 PR！特别是：
- 新增视觉风格模板
- 适配 macOS/Linux 截图环境
- 补充更多分镜类型示例

## 📄 License

MIT
