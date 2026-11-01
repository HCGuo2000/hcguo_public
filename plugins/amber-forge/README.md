# Amber Forge

An amber CRT-style UI skin for DeepSeek Harness — community plugin.

## Theme

Amber Forge takes its register from the **Adeptus Mechanicus** of Warhammer 40,000 — the machine cult of Mars. The skin borrows that vocabulary, not any game asset: an amber CRT palette for a cogitator terminal, a gear-and-skull emblem in place of the product's brand mark, and a new-session slogan written as a machine-cult verse.

This is an unofficial, fan-made skin: not affiliated with, endorsed by, or sponsored by Games Workshop.

## What it does

Everything below is client-side presentation. The host half carries no logic of its own: it declares `name` / `inject` and an empty `apply()`, and all behaviour lives in the client half.

### Theme tokens

Overrides **14 theme tokens** (`theme.overrideTokens`): base/layer/overlay backgrounds, two border levels, brand primary, primary and secondary label colours, error/success/warning state colours, the sidebar fill, and the business state colour that the composer caret uses.

### Deep palette overrides

Re-points **23 static palette entries** (`--dsw-static-blue-*` x 12, `--dsw-static-deepseek-*` x 11) from the shipped blues to ambers, so the brand-coloured surfaces in the product turn amber too.

### Typography

Forces one monospace stack (`Consolas, ui-monospace, 'Cascadia Mono', 'JetBrains Mono', 'IBM Plex Mono', 'SF Mono', monospace`) across the whole UI with `body, body *:not(.katex)`.

KaTeX's math subtree is excluded on purpose: KaTeX declares its own `KaTeX_*` families without `!important`, so an unconditional `!important` font rule would break formula rendering.

### CRT effects

Scanlines and a screen-curvature vignette as fixed pseudo-elements, an amber text glow on `body`, amber text selection, and amber scrollbars (track, thumb, hover).

### Brand mark

Registers `sidebar.brand.mark` and `conversation.hero.brand.mark` with an inlined SVG emblem (gear-and-skull, 474x474, 100 paths plus an amber disc). The corners outside the disc are transparent. In the hero area the emblem is drawn at double the slot size, the stage is re-laid-out as a centred column, and the product's own fish animation is switched off.

### New-session slogan

Replaces the hero headline text (`hero.headline`) with `铸造圣火永不熄灭`. The replacement finds the element by structure (`[class*="headline"] > [class*="titleGroup"]`) and rewrites its text node, with a `MutationObserver` so it survives re-renders and locale switches; a CSS rule on the same element is the fallback.

### Agent-preset selector

Raises the preset seat's max width from 240px to 264px and its dropdown item max width from 280px to 308px — a 10% increase each — so longer preset names fit before the label is ellipsised.

## Screenshots

![New-session emblem and slogan](assets/screenshot-emblem.png)
![Agent-preset selector widths](assets/screenshot-selector.png)

## Install

```sh
dsh plugin add https://github.com/HCGuo2000/hcguo-public/tree/main/plugins/amber-forge
```

`package.json` declares `dsh.bundle.patch`, so the plugin is installable through the normal bundle path. On `platform: web` its client half is served from `exports["./client"]`, which is what loads the actual skin.

## Compatibility

- Tested on DSH `0.1.7-rc.1`.
- `@deepseek-ai/*` packages are declared as **peerDependencies**, never dependencies, with explicit prerelease branches so prerelease harness builds resolve.

## Scope

The skin targets the product's generated class names by substring (`[class*="_seat"]`, `[class*="headline"]`, ...) because those hashes change per build; selectors are narrowed with `:has()` where a broader match could touch unrelated components. If a future product release renames a structure, the matching rule simply stops applying instead of breaking the page — the rest of the skin stays.

## License

MIT
