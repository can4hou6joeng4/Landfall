<div align="center">

# 🏝️ Landfall

**描述你的产品，选择一座城市的美学，生成一个惊艳的落地页。**

[![GitHub release](https://img.shields.io/github/v/release/can4hou6joeng4/Landfall)](https://github.com/can4hou6joeng4/Landfall/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/can4hou6joeng4/Landfall?style=social)](https://github.com/can4hou6joeng4/Landfall)

[🌐 在线演示](https://can4hou6joeng4.github.io/Landfall/) · [📋 更新日志](CHANGELOG.md) · [🤝 贡献指南](CONTRIBUTING.md) · [🇬🇧 English](README.md) · [🇯🇵 日本語](README.ja.md)

</div>

---

一个 [Claude Code](https://claude.ai/claude-code) 技能。告诉它你的产品是什么，选一座城市的设计风格，就能得到一个带 GSAP 动画、clip-path 分隔线、SVG 纹理和真实层次感的完整落地页。

> 不是千篇一律的卡片网格模板，每一个输出都是设计作品。

## 💡 为什么选择 Landfall？

大多数落地页生成器只是换了配色的 Bootstrap 模板。Landfall 的思路不同——**57 种城市风格，每一种都是完整的设计系统**：独立的字体、色板、纹理、动效曲线和图标美学。京都和拉各斯完全不同，拉各斯和棕榈泉也截然不同。

## ⚡ 快速开始

```bash
npx skills add can4hou6joeng4/Landfall -a claude-code -g -y
```

然后对 Claude 说：

```
帮我做一个落地页
```

技能会引导你选择城市风格、布局选项，然后生成完整站点：

```
你的产品/
├── index.html        # 导航、Hero、板块、页脚
├── style.css         # 设计 token、纹理、clip-path
├── main.js           # GSAP ScrollTrigger 动画
└── assets/icons.svg  # 匹配城市美学的 SVG 精灵图
```

## ✨ 核心特性

🎨 **设计系统**

- 57 种城市美学——每座城市拥有独特的字体、配色、纹理和动效
- 3 种色调——城市原色 / 暗黑奢华 / 明亮现代
- 🌓 暗色模式切换，localStorage 持久化

🧩 **页面板块**

- 7 种 Hero · 6 种功能 · 6 种评价 · 4 种导航
- 3 种页脚 · 3 种表单 · 6 种扩展板块（团队、统计、画廊、时间线...）
- 4 种板块过渡风格——几何锐利 / 有机柔和 / 渐变融合 / 极简线条

🔄 **工作流**

- 🖥️ 浏览器端交互式城市选择器——没有命令行菜单
- 📄 多页面支持——关于、联系、博客子页面
- 🚀 一键部署到 Netlify、Vercel 或 GitHub Pages
- 💻 跨平台——Python 3.6+ / macOS / Windows PowerShell

## 🛠️ 工作流程

1. **描述** — 产品名称 + 一句话介绍
2. **选择** — 在浏览器中浏览 57 张城市风格卡片
3. **定制** — Hero、导航、色调、过渡效果
4. **生成** — 完整站点文件写入项目目录
5. **预览** — 自动在浏览器中打开
6. **部署** — 可选一键发布

## 🗣️ 触发词

```
帮我做一个落地页 · 做个首页 · 产品展示页 · 活动页 · 营销页 · 官网首页
landing page · product page · promo page · make me a homepage
```

## 📂 项目结构

<details>
<summary><kbd>展开文件树</kbd></summary>

```
SKILL.md                            # 技能定义文件
assets/
├── style-preview-template.html     # 57 城市风格交互式选择器
├── options-preview-template.html   # 布局/导航/色调选择器
├── clip-paths.css                  # 板块分隔线库
├── gsap-snippets.js                # GSAP 动画模式
├── textures.css                    # 纯 CSS 背景纹理
├── sections/                       # 预构建板块模板
│   ├── hero-variants.html          # 7 种 Hero 样式 (A–G)
│   ├── features-variants.html      # 6 种功能布局 (A–F)
│   ├── testimonial-variants.html   # 6 种评价样式 (A–F)
│   ├── footer-variants.html        # 3 种页脚样式
│   ├── form-variants.html          # 3 种表单板块
│   ├── extra-variants.html         # 6 种扩展板块
│   ├── page-variants.html          # 多页面模板
│   └── conversion-variants.html    # 定价、FAQ、CTA
└── scripts/
    ├── run_preview.py              # 跨平台预览启动器
    ├── run_preview.ps1             # Windows PowerShell 启动器
    ├── get_city_tokens.py          # 城市色彩 token 提取器
    └── extract_variant.py          # 板块变体提取器
references/
├── city-styles.md                  # 57 城市设计参数
├── nav-catalog.md                  # 4 种导航实现
├── imagery-derivation.md           # 非城市描述 → token 映射
└── product-demo-hero.md            # 产品演示 Hero 指南
evals/
└── evals.json                      # 评估测试用例
```

</details>

## 🎯 设计哲学

1. 🚫 **禁止纯白背景** — 暖中性色、冷灰调或深暗色
2. 🔤 **至少两种字体** — 展示用标题字体 + 干净的无衬线正文
3. 🖼️ **SVG 作为设计核心** — 不是装饰点缀
4. 🎞️ **GSAP 空间深度** — 视差层、粘性面板、交错揭示
5. 📐 **禁止克隆网格** — 每个板块都有视觉层级

## 📄 许可证

[MIT](LICENSE)
