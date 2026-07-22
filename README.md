<div align="center">

# 🏝️ Landfall

**Turn any product idea into a stunning landing page — powered by 57 city-inspired design systems.**

[![CI](https://github.com/can4hou6joeng4/Landfall/actions/workflows/ci.yml/badge.svg)](https://github.com/can4hou6joeng4/Landfall/actions/workflows/ci.yml)
[![GitHub release](https://img.shields.io/github/v/release/can4hou6joeng4/Landfall)](https://github.com/can4hou6joeng4/Landfall/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/can4hou6joeng4/Landfall?style=social)](https://github.com/can4hou6joeng4/Landfall)

[🌐 Live Demo](https://can4hou6joeng4.github.io/Landfall/) · [📋 Changelog](CHANGELOG.md) · [🤝 Contributing](CONTRIBUTING.md) · [🇨🇳 中文](README.zh-CN.md) · [🇯🇵 日本語](README.ja.md)

</div>

---

A [Claude Code](https://claude.ai/claude-code) skill. Describe your product, pick a city aesthetic, get a production-ready site with GSAP animations, clip-path dividers, SVG textures, and real depth.

> Not another card-grid template. Every output is a design artifact.

## 💡 Why Landfall?

Most generators give you the same Bootstrap-like layout with swapped colors. Landfall takes a different approach — **each of the 57 city styles is a complete design system**: unique fonts, palettes, textures, motion curves, and icon aesthetics. Kyoto feels nothing like Lagos, and Lagos feels nothing like Palm Springs.

## ⚡ Quick Start

```bash
npx skills add can4hou6joeng4/Landfall -a claude-code -g -y
```

Then tell Claude:

```
Build me a landing page for my SaaS product
```

The skill walks you through city selection, layout options, and generates a complete site:

```
your-product/
├── index.html        # Nav, hero, sections, footer
├── style.css         # Design tokens, textures, clip-paths
├── main.js           # GSAP ScrollTrigger animations
└── assets/icons.svg  # SVG sprite in the city aesthetic
```

## ✨ Features

🎨 **Design System**

- 57 city aesthetics — unique fonts, colors, textures, and motion per city
- 3 color tones — original city / dark luxe / bright modern
- 🌓 Dark mode toggle with localStorage persistence

🧩 **Page Sections**

- 7 hero · 6 features · 6 testimonials · 4 nav styles
- 3 footer · 3 form · 6 extra sections (team, stats, gallery, timeline...)
- 4 section divider styles — geometric / organic / blend / minimal

🔄 **Workflow**

- 🖥️ Interactive browser-based city picker — no CLI menus
- 📄 Multi-page support — About, Contact, Blog sub-pages
- 🚀 One-click deploy to Netlify, Vercel, or GitHub Pages
- 💻 Cross-platform — Python 3.6+ / macOS / Windows PowerShell

## 🛠️ How It Works

1. **Describe** — product name + one-line pitch
2. **Pick** — browse 57 city style cards in your browser
3. **Choose** — hero, nav, color tone, transitions
4. **Generate** — full site written to your project
5. **Preview** — auto-opens in browser
6. **Deploy** — optional one-click publish

## 🗣️ Trigger Phrases

```
帮我做一个落地页 · 做个首页 · 产品展示页 · 活动页 · 营销页 · 官网首页
landing page · product page · promo page · make me a homepage
```

## 📂 Project Structure

<details>
<summary><kbd>Expand file tree</kbd></summary>

```
SKILL.md                            # Skill definition
assets/
├── style-preview-template.html     # 57-city interactive picker
├── options-preview-template.html   # Layout/nav/color chooser
├── clip-paths.css                  # Section divider library
├── gsap-snippets.js                # GSAP animation patterns
├── textures.css                    # CSS-only background textures
├── sections/                       # Pre-built section templates
│   ├── hero-variants.html          # 7 hero styles (A–G)
│   ├── features-variants.html      # 6 feature layouts (A–F)
│   ├── testimonial-variants.html   # 6 testimonial styles (A–F)
│   ├── footer-variants.html        # 3 footer styles
│   ├── form-variants.html          # 3 form sections
│   ├── extra-variants.html         # 6 extra sections
│   ├── page-variants.html          # Multi-page templates
│   └── conversion-variants.html    # Pricing, FAQ, CTA
└── scripts/
    ├── run_preview.py              # Cross-platform preview launcher
    ├── run_preview.ps1             # Windows PowerShell launcher
    ├── get_city_tokens.py          # City color token extractor
    └── extract_variant.py          # Section variant extractor
references/
├── city-styles.md                  # 57 city design parameters
├── nav-catalog.md                  # 4 nav implementations
├── imagery-derivation.md           # Non-city description → tokens
└── product-demo-hero.md            # Product demo hero guide
evals/
└── evals.json                      # Evaluation test cases
```

</details>

## 🎯 Design Philosophy

1. 🚫 **No `#ffffff` backgrounds** — warm neutrals, cool tints, or deep darks
2. 🔤 **Two typefaces minimum** — display headlines + clean sans body
3. 🖼️ **SVG as design core** — not decorative sprinkles
4. 🎞️ **GSAP depth** — parallax layers, sticky panels, staggered reveals
5. 📐 **No clone grids** — every section has visual hierarchy

## 📄 License

[MIT](LICENSE)
