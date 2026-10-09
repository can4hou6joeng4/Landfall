# AGENTS.md

Landfall 是一个 Claude Code skill：根据产品描述和 57 种城市风格设计系统生成落地页（GSAP 动画、clip-path 分隔、SVG 纹理）。仓库本身没有构建步骤，核心是 `SKILL.md` 和它引用的资源。

## 目录

- `SKILL.md` — skill 本体：工作流（了解产品 → 风格预览 → 选项预览 → 生成 → 预览 → 部署）与 Design Laws
- `references/` — `city-styles.md`（全部城市风格，每个城市 6 个必需子章节）、导航目录、配图推导、产品演示 hero
- `assets/` — 预览模板 HTML、各区块变体 `sections/*.html`、`textures.css`、`clip-paths.css`、`gsap-snippets.js`
- `assets/scripts/` — `get_city_tokens.py`（查城市 token）、`run_preview.py` / `run_preview.ps1`（一次性本地预览服务）、`extract_variant.py`
- `demo/` — GitHub Pages 演示；`evals/evals.json` — skill 评测用例

## 常用命令

```bash
python3 assets/scripts/get_city_tokens.py "Kyoto"   # 新增或修改城市后验证
python3 assets/scripts/run_preview.py --help         # 本地预览服务参数
```

没有测试套件和 lint；改了 `references/city-styles.md` 或模板就用上面的脚本验证。

## 约定

- 新增城市风格：在 `references/city-styles.md` 写齐 Fonts / Colors / Texture / Layout character / Motion character / Icons 六节，在两个预览模板中加卡片，必要时在 `get_city_tokens.py` 的 `CJK_ALIASES` 加日文名映射。
- `SKILL.md` 的 front matter（name / description）决定 skill 何时被触发，改动要谨慎。
- commit message：`type: 中文描述`；README 有中 / 英 / 日三份，公共内容需同步。

## 不要做

- 不要把模板改回通用卡片网格风格，也不要违反 `SKILL.md` 中的 Design Laws。
- 不要引入构建工具或 npm 依赖；资源保持可直接被 skill 读取的纯文件。
