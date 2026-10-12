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
