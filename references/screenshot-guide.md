# 无头浏览器截图指南

将 HTML 卡片文件渲染为 1080×1440 PNG 图片。

## 前置条件

Windows 系统 + Chrome 或 Edge 浏览器 + PowerShell。

## 步骤 1：探测浏览器路径

```powershell
$paths = @(
  "C:\Program Files\Google\Chrome\Application\chrome.exe",
  "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe",
  "C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe",
  "C:\Program Files\Microsoft\Edge\Application\msedge.exe"
)
$chrome = $paths | Where-Object { Test-Path $_ } | Select-Object -First 1

if (-not $chrome) {
  Write-Error "Chrome/Edge not found. Please install one of them first."
  exit 1
}
Write-Output "Using: $chrome"
```

## 步骤 2：单张截图

```powershell
$htmlPath = "<你的 HTML 文件完整路径>"
$pngPath  = "<输出 PNG 完整路径>"
$url = "file:///" + ($htmlPath -replace '\\','/')

& $chrome --headless=new --disable-gpu --hide-scrollbars --no-first-run `
  --force-device-scale-factor=1 --virtual-time-budget=3000 `
  --window-size=1080,1440 --screenshot="$pngPath" "$url" 2>$null
```

## 步骤 3：批量截图（多张卡片时）

```powershell
$htmlDir = "<HTML 卡片目录>"
$outDir  = "<PNG 输出目录>"

Get-ChildItem "$htmlDir\*.html" | ForEach-Object {
  $name = $_.BaseName
  $url = "file:///" + ($_.FullName -replace '\\','/')
  $png = Join-Path $outDir "$name.png"
  & $chrome --headless=new --disable-gpu --hide-scrollbars --no-first-run `
    --force-device-scale-factor=1 --virtual-time-budget=3000 `
    --window-size=1080,1440 --screenshot="$png" "$url" 2>$null
  Write-Output "Screenshot saved: $png"
}
```

## 关键参数说明

| 参数 | 值 | 作用 |
|------|----|------|
| `--headless=new` | new | 使用新版 headless 模式，渲染更完整 |
| `--force-device-scale-factor=1` | 1 | **关键**：DPI 缩放设为 1，保证输出就是精确的 1080×1440 |
| `--virtual-time-budget` | 3000 | 等待 3 秒让字体和 CSS 动画完成渲染 |
| `--window-size` | 1080,1440 | 浏览器窗口尺寸，与卡片尺寸一致 |
| `--hide-scrollbars` | — | 隐藏滚动条，不出现在截图里 |
| `--no-first-run` | — | 跳过首次启动向导 |

## 校验截图尺寸

```powershell
Add-Type -AssemblyName System.Drawing
$img = [System.Drawing.Image]::FromFile($pngPath)
Write-Output "Size: $($img.Width)x$($img.Height)"
$img.Dispose()
```

预期输出：`Size: 1080x1440`。如果不是，检查 `--force-device-scale-factor` 是否生效。
