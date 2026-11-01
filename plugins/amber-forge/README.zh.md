# Amber Forge 琥珀圣炉

DeepSeek Harness 的琥珀色 CRT 复古界面皮肤 —— 社区插件。

English: [README.md](README.md)

## 传承

琥珀圣炉以《战锤 40,000》中的**机械神教**（Adeptus Mechanicus，火星的机械教团）为题材渊源。皮肤借用的是这一文化语汇，而非任何游戏素材：以琥珀 CRT 模拟机魂终端，以齿轮与骷髅构成的圣徽替代产品默认品牌标记，把新会话口号改写为机械神教偈语。

本皮肤为非官方同人作品：与 Games Workshop 无隶属关系，亦未获其授权或背书。

## 功能

以下皆为客户端呈现层；host 半区不含任何逻辑——仅声明 `name` / `inject` 与一个空的 `apply()`，一切行为都在客户端半区。

### 主题令牌

覆写 **14 枚主题令牌**（`theme.overrideTokens`）：基础/图层/浮层底色、两级边框、品牌主色、主与次标签色、错误/成功/警告三态色、侧栏填充色，以及输入光标所用的 business 状态色。

### 深层调色板覆写

把 **23 枚深层静态调色板**（`--dsw-static-blue-*` 12 枚、`--dsw-static-deepseek-*` 11 枚）由官方蓝改为琥珀色，使产品中依调色板取色的界面一同转琥珀。

### 排版

以 `body, body *:not(.katex)` 将全站字体统一为单一等宽字族（`Consolas, ui-monospace, 'Cascadia Mono', 'JetBrains Mono', 'IBM Plex Mono', 'SF Mono', monospace`）。

刻意排除 KaTeX 数学排版子树：KaTeX 自带的 `KaTeX_*` 字族声明不带 `!important`，若无条件强制会破坏公式字形。

### CRT 磷光效果

以固定定位伪元素叠加扫描线与屏幕曲率暗角；全站文字琥珀辉光、琥珀选区、琥珀滚动条（轨道/滑块/悬停三态）。

### 品牌圣徽

注册 `sidebar.brand.mark` 与 `conversation.hero.brand.mark`，以内嵌 SVG 圣徽（齿轮骷髅，474x474，100 条路径 + 琥珀圆底）替代默认标记；圆外四角透明。新会话页按槽位尺寸双倍绘制，标题区改为居中纵列，并熄灭产品自带的游鱼动效。

### 新会话口号

将新会话页标题（`hero.headline`）改为「铸造圣火永不熄灭」。替字按结构定位元素（`[class*="headline"] > [class*="titleGroup"]`）并直改文本节点，配 `MutationObserver` 以在重渲染与语言包切换后自动重替；同元素的 CSS 规则作为兜底。

### 对话模式选择器

把模式座席的长度上限由 240px 提至 264px、下拉条目由 280px 提至 308px（各 +10%），使较长的模式名在省略号截断前尽量完整显示。

## 截图

![新会话圣徽与口号](assets/screenshot-emblem.png)
![对话模式选择器长度](assets/screenshot-selector.png)

## 安装

```sh
dsh plugin add https://github.com/HCGuo2000/hcguo-public/tree/main/plugins/amber-forge
```

`package.json` 已声明 `dsh.bundle.patch`，可经常规 bundle 路径安装；其 `platform: web` 的客户端半区由 `exports["./client"]` 提供，皮肤本体即由此载入。

## 兼容

- 已在 DSH `0.1.7-rc.1` 上实测。
- 官方 `@deepseek-ai/*` 一律以 **peerDependencies** 声明（绝不进 dependencies），并带显式预发布分支，以便预发布版 harness 正常解析。

## 说明

皮肤以子串方式锚定产品生成的类名（该类名哈希随构建变化），并在可能波及旁支组件处用 `:has()` 收窄；若产品改版更名，对应规则会静默失效而非破坏页面，皮肤其余部分不受影响。

## 许可

MIT
