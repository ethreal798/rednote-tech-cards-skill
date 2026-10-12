# 设计系统 Token

所有卡片共用的颜色、字号、间距、圆角值。先定死再写 HTML。

## 画布规格

```
画布尺寸：1080 × 1440 px（3:4）
内边距：48 px（四周）
可用区域：984 × 1344 px
```

## 字体栈

| 用途 | font-family |
|------|-------------|
| 中文正文/标题 | `"Microsoft YaHei UI", "Microsoft YaHei", "PingFang SC", "Hiragino Sans GB", sans-serif` |
| 代码/等宽 | `"Cascadia Mono", "Consolas", "Menlo", "Courier New", monospace` |

## 语义色表

| Token | 值 | 用途 |
|-------|----|------|
| `--color-bg` | `#1a1a2e` | 深色终端风格背景 |
| `--color-bg-light` | `#fafafa` | 极简风格背景 |
| `--color-text` | `#222222` | 主文本 |
| `--color-text-secondary` | `#666666` | 次要文本/说明 |
| `--color-accent` | `#ff2442` | 小红书品牌红，用于封面、重点 |
| `--color-success` | `#22c55e` | 正确/通过/绿 |
| `--color-error` | `#ef4444` | 错误/禁止/红 |
| `--color-warning` | `#f59e0b` | 警告/黄 |
| `--color-border` | `#e5e7eb` | 边框/分隔线 |

## 字号阶梯

| Token | 值 | 用途 |
|-------|----|------|
| `--font-xxl` | 72px | 封面大标题 |
| `--font-xl` | 56px | 卡片副标题 |
| `--font-lg` | 40px | 卡片区块标题 |
| `--font-md` | 32px | 卡片正文（推荐最小） |
| `--font-sm` | 26px | 次要说明 |
| `--font-xs` | 20px | 小字/脚注 |
| `--font-code` | 24px | 代码块字号（等宽） |

## 间距阶梯

| Token | 值 | 用途 |
|-------|----|------|
| `--space-2` | 8px | 紧凑间距 |
| `--space-3` | 12px | 小标题与正文 |
| `--space-4` | 16px | 段落间距 |
| `--space-6` | 24px | 区块间距 |
| `--space-8` | 32px | 大区块分隔 |
| `--space-12` | 48px | 页面内边距 |

## 圆角阶梯

| Token | 值 | 用途 |
|-------|----|------|
| `--radius-sm` | 8px | 小标签 |
| `--radius-md` | 12px | 卡片内区块 |
| `--radius-lg` | 24px | 大容器 |
| `--radius-full` | 9999px | 圆形标签 |

## 视觉层次 Token（深色风格 v2，提升质感关键）

### 阴影阶梯

| Token | 值 | 用途 |
|-------|----|------|
| `--shadow-sm` | `0 4px 12px rgba(0,0,0,0.25)` | 小浮层 |
| `--shadow-md` | `0 12px 40px rgba(0,0,0,0.35)` | 常规玻璃卡片 |
| `--shadow-lg` | `0 18px 50px rgba(0,0,0,0.45)` | 中心徽章/重点元素 |
| `--glow-accent` | `0 0 14px rgba(255,45,85,0.55)` | 红色强调发光 |

### 渐变背景方案

| Token | 值 | 用途 |
|-------|----|------|
| `--grad-bg` | `linear-gradient(160deg, #0d1330, #1b2a5e 55%, #22316b)` | 深色风格页面背景 |
| `--grad-accent` | `linear-gradient(135deg, #ff2d55, #ff5f8a 55%, #ff8fa8)` | 中心徽章/重点胶囊 |
| `--grad-cyan` | `linear-gradient(135deg, #36d6ff, #1f9dff)` | 蓝色编号/强调块 |
| `--grad-titlebar` | `linear-gradient(180deg, #ff6384, #ff2d55)` | 标题左侧竖条 |

### 玻璃拟态 Token

| Token | 值 | 用途 |
|-------|----|------|
| `--glass-bg` | `rgba(255,255,255,0.05)` | 玻璃卡片底色 |
| `--glass-brd` | `rgba(255,255,255,0.14)` | 玻璃卡片边框 |
| `--glass-red` | `rgba(255,45,85,0.08)` + 红边框 | 重点强调卡片 |
| `--glass-cy` | `rgba(54,214,255,0.08)` + 青边框 | 冷色调卡片 |

### 编号锚点（视觉抓手）

| Token | 值 | 用途 |
|-------|----|------|
| `--num-red` | 红渐变底 + 白字 + 红色发光 | 步骤编号/章节锚点 |
| `--num-cyan` | 青渐变底 + 白字 + 青色发光 | 冷色调编号 |
| `--num-size` | 46×46px，圆角 14px | 标准编号方块 |

### 光斑装饰（背景层次）

```css
/* 背景光斑 + 网格，制造空间纵深感 */
body::before {
  background:
    radial-gradient(520px 380px at 86% 8%, rgba(255,45,85,0.22), transparent 65%),
    radial-gradient(560px 420px at 8% 92%, rgba(54,214,255,0.16), transparent 65%);
}
body::after {
  background-image:
    linear-gradient(rgba(255,255,255,0.035) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.035) 1px, transparent 1px);
  background-size: 44px 44px;
}
```

### 高对比色参考（深色底文字）

| 文字用途 | 值 | 对比度 |
|---------|----|--------|
| 主标题 | `#FFFFFF` | ~12:1 AAA |
| 次要文字 | `rgba(255,255,255,0.82)` | ~8:1 AAA |
| 强调青色 | `#45d8ff` | ~7:1 AAA |
| 底部说明 | `rgba(255,255,255,0.55)` | ~5:1 AA |

## CSS 变量模板

```css
:root {
  /* Canvas */
  --canvas-w: 1080px;
  --canvas-h: 1440px;
  --canvas-padding: 48px;

  /* Colors */
  --color-bg: #fafafa;
  --color-text: #222222;
  --color-text-secondary: #666666;
  --color-accent: #ff2442;
  --color-success: #22c55e;
  --color-error: #ef4444;
  --color-border: #e5e7eb;

  /* Typography */
  --font-xxl: 72px;
  --font-xl: 56px;
  --font-lg: 40px;
  --font-md: 32px;
  --font-sm: 26px;

  /* Spacing */
  --space-2: 8px;
  --space-4: 16px;
  --space-6: 24px;
  --space-8: 32px;
  --space-12: 48px;

  /* Radius */
  --radius-md: 12px;
  --radius-lg: 24px;
}
```
