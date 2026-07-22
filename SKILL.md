---
name: landfall
description: >-
  Create a bold, visually striking landing page — unconventional layouts, GSAP scroll animations,
  SVG elements, clip-path dividers, real depth and layering. Use this skill whenever the user wants
  a landing page, homepage, product page, marketing page, campaign page, event page, or any
  single-page site that needs to impress. Trigger on: 帮我做一个落地页, 做个首页, 产品展示页, 活动页,
  营销页, 官网首页, landing page, product page, promo page, make me a homepage, build a product
  showcase, create a campaign page. Workflow: asks one question about the product, then opens a live
  browser preview of 57 city-inspired visual styles to click-select, lets the user pick
  typography/nav/color tone/hero variant/features variant/page sections interactively, then outputs
  a complete multi-file site (index.html + style.css + main.js + SVG sprite) with real product copy.
---

# Landing Page Builder

## Philosophy

This skill produces landing pages that are **visually audacious** — not the typical nested-container, card-grid, predictable web template. Every output should feel like a deliberate design artifact:

- **布局大胆** — Clip-path dividers instead of horizontal lines. Type bleeding off-screen. Elements breaking out of their grid. Full-viewport headlines.
- **SVG 作为设计核心** — Not decorative sprinkles. SVG paths animate on scroll, icons have personality, background textures from `<feTurbulence>` noise.
- **层次感与深度** — GSAP ScrollTrigger creates genuine spatial depth: sections that overlap and cover the previous one, sticky panels pinned while content slides over them, parallax on separate z-layers.
- **背景质感** — Every section has texture. Never a flat solid background.
- **导航惊喜** — The nav is never a standard horizontal bar.

---

## Bundled Assets (USE THESE — do not reinvent)

This skill comes with pre-built assets. Read and use them directly:

| File | What's in it | When to use |
|------|-------------|-------------|
| `assets/style-preview-template.html` | 57-city style preview cards | Step 2: `sed` fill `__PRODUCT_NAME__` + `__PRODUCT_HEADLINE__`, save as `style-preview.html`, open |
| `assets/options-preview-template.html` | Interactive demos: nav styles, color variants, transition styles, hero/features/testimonials variants | Step 3: `sed` fill city color tokens + product name, save as `options-preview.html`, open |
| `assets/textures.css` | 6 CSS texture classes (`.texture-kyoto`, `.texture-paris`, `.texture-tokyo`, etc.) | Copy the matching class into `style.css` |
| `assets/gsap-snippets.js` | 9 GSAP animation + utility functions (blur entrance, line reveal, parallax, sticky steps, blast menu, magnetic pill, hero demo stepper, animated count, dark mode toggle) | Copy the relevant functions into `main.js` |
| `assets/clip-paths.css` | 8 clip-path divider classes (`.clip-diagonal-br`, `.clip-parallelogram`, `.clip-arc-bottom`, etc.) | Use at least 2 in `style.css` for section dividers |
| `assets/sections/hero-variants.html` | 7 Hero section templates (全屏铺张/分屏张力/极简下降/产品演示/文字爆炸/杂志撕裂/弹出卡片) | Step 4: pick the variant matching the user's typography preference, copy and adapt |
| `assets/sections/features-variants.html` | 6 Features section templates (大数字/交替展示/时间线/本托格子/水平滚动/问答展开) | Step 4: pick based on content type (stats → big number, how-it-works → timeline) |
| `assets/sections/testimonial-variants.html` | 6 Testimonials templates (紧凑卡片/单列引用/马赛克拼贴/滚动横条/对话气泡/头像墙) | Step 4: pick based on testimonial volume and visual style preference |
| `assets/sections/conversion-variants.html` | Pricing table, FAQ, brand wall, power CTA | Step 4: copy relevant section, all use CSS custom properties |
| `assets/sections/footer-variants.html` | 3 Footer templates (极简单行/多列链接/杂志编辑) | Step 4: pick based on page complexity and brand tone |
| `assets/sections/page-variants.html` | 3 Sub-page templates (关于我们/联系方式/博客列表) | Step 4: when user requests multi-page site |
| `assets/sections/form-variants.html` | 3 Form section templates (邮件订阅/等待列表/内嵌联系表单) | Step 4: when page needs a form section |
| `assets/sections/extra-variants.html` | 6 Extra section templates (团队/数据统计/Logo滚动/作品集/技术集成/时间线) | Step 4: pick based on product type and content needs |
| `references/product-demo-hero.md` | Product demo hero principles + scene design guide | Read when user wants to show product workflow in hero (see Step 3/4) |

**The quality guarantee of this skill comes from using these assets.** They encode specific design decisions that make outputs distinct. Don't describe what to do — copy the code and adapt it.

---

## The Workflow

### Step 1: Understand the Product

Use `AskUserQuestion` to ask:

> "告诉我你的落地页是关于什么的——产品/服务名称，以及一句话介绍。"

Wait for the answer before proceeding.

**Detect the conversation language:** If the user wrote their answer in English, set `LANG_VALUE=en` for all subsequent preview commands. If in Chinese, use `LANG_VALUE=zh`. This determines the UI language of the preview pages.

**Check if the user needs sub-pages:** After getting the product info, ask:

> "除了主页之外，是否还需要其他页面？可以选择：关于我们 / 联系方式 / 博客列表，或者只需要一个单页落地页就够了。"

Record the user's choice. If they want sub-pages, note which ones (about / contact / blog). This will be used in Step 4 to generate additional HTML files.

### Step 2: Generate the Style Preview

Fill in the two placeholders and open the result — do NOT read the template file into context:
- `PRODUCT_NAME` → the product name from Step 1
- `PRODUCT_HEADLINE` → a short punchy phrase (3–5 words) that captures the product's essence

```bash
_SKILL_DIR=$(ls -d ~/.agents/skills/landfall 2>/dev/null || ls -d ~/.claude/skills/landfall 2>/dev/null)
PYTHON=$(command -v python3 2>/dev/null || command -v python 2>/dev/null || echo "")
if [ -n "$PYTHON" ]; then
  # Python available (macOS / Linux / WSL / Windows with Python)
  # LANG_VALUE detected in Step 1 (zh or en)
  "$PYTHON" "$_SKILL_DIR/assets/scripts/run_preview.py" \
    --template "$_SKILL_DIR/assets/style-preview-template.html" \
    --output   ./style-preview.html \
    --port     17433 \
    --timeout  300 \
    "LANG=$LANG_VALUE" \
    "PRODUCT_NAME=ACTUAL_PRODUCT_NAME" \
    "PRODUCT_HEADLINE=ACTUAL_HEADLINE" \
    "RECEIVER_PORT=17433"
else
  # No Python — substitute via sed and open as a local file.
  # The submit button falls back to clipboard copy automatically.
  sed "s/__PRODUCT_NAME__/ACTUAL_PRODUCT_NAME/g; s/__PRODUCT_HEADLINE__/ACTUAL_HEADLINE/g" \
    "$_SKILL_DIR/assets/style-preview-template.html" > ./style-preview.html
  open ./style-preview.html 2>/dev/null || xdg-open ./style-preview.html 2>/dev/null \
    || echo "Open in browser: $(pwd)/style-preview.html"
  echo "Python not found — no live bridge. The submit button will copy the city name to clipboard. Paste it here."
fi
```

Replace `ACTUAL_PRODUCT_NAME` and `ACTUAL_HEADLINE` with the real values from Step 1 in the script arguments.

> **Windows PowerShell (no WSL/Git Bash):** Run `run_preview.ps1` directly — it has the same interface. See `assets/scripts/run_preview.ps1` for usage.

Tell the user: "我在浏览器里打开了57种城市风格的预览卡片，每个都是真实渲染效果。向下滚动可以看到全部——从京都到拉各斯到棕榈泉，再到伊斯坦布尔、迈阿密、成都、哥本哈根、维也纳、开普敦、波哥大、阿姆斯特丹、贝鲁特、波特兰，以及上海、北京、重庆、西安、杭州、深圳夜、敦煌、苏州、拉萨、罗马、布拉格、墨尔本、雅典、卡萨布兰卡、釜山、巴厘岛、多伦多、特拉维夫、华沙、孟买夜，还有新加入的大阪、清迈、米兰、台北、新奥尔良、苏黎世、温哥华。选好之后直接点卡片发送给我；如果本地桥接没有连上，也可以复制城市名告诉我。如果57个城市都不对，直接用自己的语言描述给我也行。"

### Step 3: Open the Interactive Options Preview

The user has chosen their city. Now open the visual options preview so they can *feel* the layout and nav choices instead of reading descriptions.

> **If the user clicked "让 AI 来选" (city = `__AI_CHOOSE__`):** Skip the preview entirely. Instead, look back at the conversation to understand the product's audience, industry, and tone. Then pick the single most fitting city from `references/city-styles.md` and briefly explain why (2–3 sentences). Confirm with the user: "我为你选了 [城市]——[理由]. 继续吗？" Then proceed to Step 3 with that city.

**3a — Get city color tokens (script, not file read)**

Run `get_city_tokens.py` to extract just the 5 color values — do NOT read `city-styles.md` into context:

```bash
_SKILL_DIR=$(ls -d ~/.agents/skills/landfall 2>/dev/null || ls -d ~/.claude/skills/landfall 2>/dev/null)
PYTHON=$(command -v python3 2>/dev/null || command -v python 2>/dev/null || echo "")
# Outputs CITY_BG=, CITY_SURFACE=, CITY_INK=, CITY_MUTED=, CITY_ACCENT=
eval $("$PYTHON" "$_SKILL_DIR/assets/scripts/get_city_tokens.py" "ACTUAL_CITY_NAME")
```

Replace `ACTUAL_CITY_NAME` with the city name the user chose (Chinese or English). The script handles both. If the city isn't found, it exits 1 — in that case fall back to reading the `### Colors` section of `references/city-styles.md` manually.

**3b — Generate and open options-preview.html**

Use the `$CITY_*` variables from 3a. Do NOT read the template file into context:

```bash
if [ -n "$PYTHON" ]; then
  # LANG_VALUE detected in Step 1 (zh or en)
  "$PYTHON" "$_SKILL_DIR/assets/scripts/run_preview.py" \
    --template "$_SKILL_DIR/assets/options-preview-template.html" \
    --output   ./options-preview.html \
    --port     17432 \
    --timeout  300 \
    "LANG=$LANG_VALUE" \
    "PRODUCT_NAME=ACTUAL_PRODUCT_NAME" \
    "PRODUCT_HEADLINE=ACTUAL_HEADLINE" \
    "CITY_NAME=ACTUAL_CITY_NAME" \
    "CITY_BG=$CITY_BG" \
    "CITY_SURFACE=$CITY_SURFACE" \
    "CITY_INK=$CITY_INK" \
    "CITY_MUTED=$CITY_MUTED" \
    "CITY_ACCENT=$CITY_ACCENT" \
    "CITY_DARK_BG=#0e0c09" \
    "CITY_DARK_SURFACE=#1e1b16" \
    "CITY_DARK_INK=#f2ede4" \
    "CITY_DARK_ACCENT=$CITY_ACCENT" \
    "CITY_BRIGHT_BG=#fdf9f2" \
    "CITY_BRIGHT_SURFACE=#fffdf8" \
    "CITY_BRIGHT_INK=#1a1510" \
    "CITY_BRIGHT_ACCENT=$CITY_ACCENT" \
    "RECEIVER_PORT=17432"
else
  sed \
    -e "s/__PRODUCT_NAME__/ACTUAL_PRODUCT_NAME/g" \
    -e "s/__PRODUCT_HEADLINE__/ACTUAL_HEADLINE/g" \
    -e "s/__CITY_NAME__/ACTUAL_CITY_NAME/g" \
    -e "s/__CITY_BG__/$CITY_BG/g" \
    -e "s/__CITY_SURFACE__/$CITY_SURFACE/g" \
    -e "s/__CITY_INK__/$CITY_INK/g" \
    -e "s/__CITY_MUTED__/$CITY_MUTED/g" \
    -e "s/__CITY_ACCENT__/$CITY_ACCENT/g" \
    -e "s/__CITY_DARK_BG__/#0e0c09/g" \
    -e "s/__CITY_DARK_SURFACE__/#1e1b16/g" \
    -e "s/__CITY_DARK_INK__/#f2ede4/g" \
    -e "s/__CITY_DARK_ACCENT__/$CITY_ACCENT/g" \
    -e "s/__CITY_BRIGHT_BG__/#fdf9f2/g" \
    -e "s/__CITY_BRIGHT_SURFACE__/#fffdf8/g" \
    -e "s/__CITY_BRIGHT_INK__/#1a1510/g" \
    -e "s/__CITY_BRIGHT_ACCENT__/$CITY_ACCENT/g" \
    "$_SKILL_DIR/assets/options-preview-template.html" > ./options-preview.html
  open ./options-preview.html 2>/dev/null || xdg-open ./options-preview.html 2>/dev/null \
    || echo "Open in browser: $(pwd)/options-preview.html"
  echo "Python not found — no live bridge. Use the copy button in the preview and paste the result here."
fi
```

The dark variant (`__CITY_DARK_*`) is always the luxury/night treatment — near-black bg, warm light text, same accent. The bright variant is always the fresh/modern treatment — near-white bg, dark text, same accent. The city's identity comes from the base colors and accent, not from the dark/bright shell.

> **Windows PowerShell (no WSL/Git Bash):** Run `run_preview.ps1` directly. See `assets/scripts/run_preview.ps1` for usage.

When the script exits, it prints the result JSON to stdout. If it times out, ask the user to type their choice manually before proceeding.

Tell the user: "在浏览器里打开了一个互动选择页——有排版、导航的实际演示效果，还有三种色调的对比，以及板块间过渡风格的可视化预览。可以点击全屏菜单看它怎么爆开，把光标移近底部胶囊感受磁性效果。全部选好之后，点底部的「告诉 Agent →」按钮，我会自动收到结果并继续生成；如果本地桥接没有连上，再把复制结果贴给我就可以。"

**If the user chose a non-city description** (scene, era, material, emotion): read `references/imagery-derivation.md` to derive the design token system first, use those derived colors as the `CITY_*` arg values above, then proceed normally.

If the script prints JSON, parse it directly and continue to Step 4 with `city`, `layout`, `nav`, `tone`, `transitions`, `hero`, `features`, and `sections`. If it times out, ask the user to paste their choices manually before proceeding.

**Additional choices not in the preview JSON** — these are determined by the agent based on Step 1 and the product context:
- `footer`: Pick A (minimal), B (multi-column), or C (editorial) from `footer-variants.html` based on page complexity
- `form`: Pick NEWSLETTER, WAITLIST, or CONTACT_INLINE from `form-variants.html` if the user's sections include a form need, or skip if not
- `pages`: List of sub-pages from Step 1 (e.g. `["about", "contact"]`), or empty if single-page

### Step 4: Generate the Landing Page

Output into `{product-name}-landing/`:

```
{product-name}-landing/
├── index.html
├── style.css
├── main.js
├── about.html          ← optional sub-pages
├── contact.html        ← optional sub-pages
├── blog.html           ← optional sub-pages
└── assets/
    └── icons.svg
```

**Multi-page support:** If the user requests sub-pages (about, contact, blog), generate them as separate HTML files in the same directory. Each sub-page:
- Shares the same `style.css`, `main.js`, and `assets/icons.svg` as `index.html`
- Uses the same nav (with links updated to point to sibling pages) and footer
- Content comes from `assets/sections/page-variants.html` (variants: `ABOUT`, `CONTACT`, `BLOG`)
- Has its own `<title>` and `<meta>` tags following the SEO baseline (Design Law 11)

Extract sub-page content in the Bash Assembly step:
```bash
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/page-variants.html" ABOUT >> "$_OUT/_pages.html"
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/page-variants.html" CONTACT >> "$_OUT/_pages.html"
```

Read `_pages.html` alongside other staging files, then write each sub-page as a complete HTML document wrapping the nav + page content + footer.

#### 4a — Bash Assembly (do this first, before writing any file)

**The goal is to avoid outputting bundled asset code as model tokens.** Instead, use Bash to copy and pipe the ready-made assets into the output files. Only product-specific content (copy, tokens, overrides) is written by the model.

**Step 1 — Set up directories**

```bash
_SKILL_DIR=$(ls -d ~/.agents/skills/landfall 2>/dev/null || ls -d ~/.claude/skills/landfall 2>/dev/null)
_OUT="./{product-name}-landing"
mkdir -p "$_OUT/assets"
```

**Step 2 — Assemble section variants into a staging file**

Plan which variants to use (see table below), then pipe each into a staging file:

```bash
# Replace B / C / B / PRICING with the user's actual choices
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/hero-variants.html" B > "$_OUT/_sections.html"
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/features-variants.html" C >> "$_OUT/_sections.html"
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/testimonial-variants.html" B >> "$_OUT/_sections.html"
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/conversion-variants.html" PRICING >> "$_OUT/_sections.html"
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/conversion-variants.html" CTA >> "$_OUT/_sections.html"
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/footer-variants.html" B >> "$_OUT/_sections.html"
# If user needs a form section, add it:
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/form-variants.html" NEWSLETTER >> "$_OUT/_sections.html"
# If user requested sub-pages, extract them:
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/page-variants.html" ABOUT >> "$_OUT/_pages.html"
python3 "$_SKILL_DIR/assets/scripts/extract_variant.py" \
  "$_SKILL_DIR/assets/sections/page-variants.html" CONTACT >> "$_OUT/_pages.html"
```

For testimonials use: `A`, `B`, `C`, `D`, `E`, `F`
For conversion sections use: `PRICING`, `COMPARE_PRICING`, `BRAND_WALL`, `CTA`, `FAQ_A`, `FAQ_B`
For footer use: `A` (minimal), `B` (multi-column), `C` (editorial)
For forms use: `NEWSLETTER`, `WAITLIST`, `CONTACT_INLINE`
For sub-pages use: `ABOUT`, `CONTACT`, `BLOG`

**Step 3 — Copy bundled CSS utilities into style.css base**

```bash
# Texture: use --texture flag (never read full city-styles.md)
python3 "$_SKILL_DIR/assets/scripts/get_city_tokens.py" "CITY_NAME" --texture > "$_OUT/_texture.css"
# Clip-paths: copy all classes, model picks which to apply via class names
cat "$_SKILL_DIR/assets/clip-paths.css" >> "$_OUT/_texture.css"
```

**Step 4 — Copy GSAP snippets into main.js base**

```bash
cat "$_SKILL_DIR/assets/gsap-snippets.js" > "$_OUT/_gsap-base.js"
```

Now read the staging files (`_sections.html`, `_texture.css`, `_gsap-base.js`, and `_pages.html` if sub-pages were requested) to understand what's available, then write the final output files.

#### 4b — Section Variant Reference

Common page sequences:
- SaaS tool: Hero D → Features C → Features A → Testimonials A → Pricing → FAQ A → Newsletter → CTA → Footer B
- Agency portfolio: Hero A → Features B → Testimonials C → Contact Inline → CTA → Footer C
- Developer tool: Hero B → Features C → Features A → Testimonials A → Pricing → FAQ B → Newsletter → CTA → Footer B
- Luxury product: Hero C → Features B → Testimonials B → CTA → Footer C
- B2C app: Hero E → Features E → Testimonials F → Waitlist → CTA → Footer A
- Startup pre-launch: Hero G → Features D → Waitlist → FAQ A → Footer A

| If the user needs... | Use this template | Variant |
|---------------------|-------------------|---------|
| Hero — massive bold statement | 全屏铺张 | A |
| Hero — product visual + headline | 分屏张力 | B |
| Hero — elegant, story-first | 极简下降 | C |
| Hero — product has a workflow to show | 产品演示型 | D (also read `references/product-demo-hero.md`) |
| Hero — typography-led, high-impact | 文字爆炸型 | E |
| Hero — editorial storytelling | 杂志撕裂型 | F |
| Hero — playful product launch | 弹出卡片型 | G |
| Features — data/metrics focus | 大数字 | A |
| Features — product screenshots | 交替展示 | B |
| How it works — step-by-step | 时间线 | C |
| Features — modular story blocks | 本托格子型 | D |
| Features — browseable capability ribbon | 水平滚动卡带型 | E |
| Features — objection handling | 问答展开型 | F |
| Pricing table | 定价表 | PRICING |
| Pricing comparison with toggle | 对比定价表 | COMPARE_PRICING |
| Testimonials — compact grid | 紧凑卡片网格 | A |
| Testimonials — magazine style | 单列引用墙 | B |
| Testimonials — masonry layout | 马赛克拼贴 | C |
| Testimonials — horizontal scroll | 滚动横条 | D |
| Testimonials — conversation bubbles | 对话气泡 | E |
| Testimonials — avatar wall | 视频头像墙 | F |
| Trusted brand logos | 品牌墙 | BRAND_WALL |
| Final CTA | 强力CTA区 | CTA |
| FAQ — editorial layout | 编辑排版型 | FAQ_A |
| FAQ — card grid | 全宽焦点型 | FAQ_B |
| Footer — minimal single row | 极简单行 | A (footer-variants.html) |
| Footer — multi-column links | 多列链接 | B (footer-variants.html) |
| Footer — editorial with watermark | 杂志编辑型 | C (footer-variants.html) |
| Sub-page — About / Brand story | 关于我们 | ABOUT (page-variants.html) |
| Sub-page — Contact with form | 联系方式 | CONTACT (page-variants.html) |
| Sub-page — Blog post listing | 博客列表 | BLOG (page-variants.html) |
| Form — Newsletter subscribe | 邮件订阅 | NEWSLETTER (form-variants.html) |
| Form — Waitlist signup | 等待列表 | WAITLIST (form-variants.html) |
| Form — Inline contact form | 内嵌联系表单 | CONTACT_INLINE (form-variants.html) |
| Team member cards | 团队成员 | TEAM (extra-variants.html) |
| Stats / Numbers showcase | 数据统计 | STATS (extra-variants.html) |
| Logo infinite scroll | 品牌滚动墙 | LOGO_SCROLL (extra-variants.html) |
| Gallery / Portfolio grid | 作品集展示 | GALLERY (extra-variants.html) |
| Integrations / Tech stack | 技术集成 | INTEGRATIONS (extra-variants.html) |
| Timeline / Milestones | 时间线 | TIMELINE (extra-variants.html) |

#### 4c — Write the Output Files

**index.html** — Write with the Write tool. No markdown block, directly to file.
- Document structure: `<html>`, `<head>` (Google Fonts, GSAP CDN, link to style.css + main.js), `<body>`
- Nav HTML matching the selected nav style
- Paste `<style>` blocks and `<section>` HTML from `_sections.html` in page order
- Replace all placeholder copy with real product copy — fit the city aesthetic's tone of voice
- No Lorem Ipsum, no placeholder text
- Break template uniformity: vary visual weight across items within each section. The template shows a repeating pattern — make one item the focal point (accent background, larger card, featured badge, different internal layout) and let others recede. No section should look like a grid of clones.

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
```

**style.css** — Write with the Write tool. Structure:
1. `:root` block — full design token system: colors from `$CITY_*` tokens, chosen fonts, spacing scale, radii. This is the only part the model writes from scratch.
2. `[data-theme="dark"]` block — dark variant tokens using `$CITY_DARK_*` values from Step 3. This enables runtime dark mode toggle.
3. Paste texture + clip-path CSS from `_texture.css`
4. Nav CSS matching the selected nav style (from `references/nav-catalog.md`)
5. Layout and typography overrides — only what differs from section defaults

`clamp()` for ALL headline font sizes:
- Hero 主标题：`clamp(2.8rem, 7vw, 7rem)` — 铺张型也不超过 7rem
- Section 标题：`clamp(2rem, 4vw, 4rem)`
- 大数字/装饰数字：`clamp(4rem, 10vw, 9rem)`
- 副标题/说明文字：`clamp(1rem, 1.4vw, 1.2rem)`

Do NOT add comments to style.css — they consume tokens and add no value to the output file.

**main.js** — Write with the Write tool. Structure:
1. `gsap.registerPlugin(ScrollTrigger)`
2. Paste the relevant functions from `_gsap-base.js` — required minimum:
   - `initHeroEntrance()` — stagger hero elements in
   - `initParallax()` — at least 2 layers at different speeds
   - Section heading reveals on viewport entry
   - `initStickySteps()` OR `initBlastMenu()` OR `initMagneticPill()` — matching nav/layout
3. `initDarkModeToggle(".theme-toggle")` — enable dark/light mode switching
4. Call sequence at bottom; `ScrollTrigger.refresh()` after fonts load

Do NOT add comments to main.js.

**assets/icons.svg** — SVG sprite with `<symbol>` elements. At minimum: logo mark, nav toggle, arrow, checkmark, 2–3 product-relevant feature icons. Icon style must match the city aesthetic's stroke weight and geometry.

After all files are written, delete the staging files:
```bash
rm -f "$_OUT/_sections.html" "$_OUT/_texture.css" "$_OUT/_gsap-base.js" "$_OUT/_pages.html"
```

### Step 5: Preview the Result

After all files are written, open the generated page in the browser so the user sees it immediately:

```bash
open "$_OUT/index.html" 2>/dev/null || xdg-open "$_OUT/index.html" 2>/dev/null || echo "Preview ready: $(cd "$_OUT" && pwd)/index.html"
```

Tell the user: "落地页已生成并在浏览器中打开。如果需要调整任何细节，随时告诉我。"

### Step 6: Deploy (Optional)

After the user confirms the page looks good, ask if they want to deploy it online:

> "需要我帮你把这个站点部署到线上吗？支持 Netlify、Vercel 和 GitHub Pages 三种方式。"

**Option A: Netlify**

```bash
cd "$_OUT"
npx netlify deploy --dir=. --message="Landing page deploy from landfall"
```

This creates a draft deploy with a preview URL. If confirmed:

```bash
npx netlify deploy --dir=. --prod --message="Production deploy from landfall"
```

**Option B: Vercel**

```bash
cd "$_OUT"
npx vercel --yes
```

This deploys a preview. If confirmed:

```bash
npx vercel --prod --yes
```

**Option C: GitHub Pages**

```bash
cd "$_OUT"
git init && git add -A && git commit -m "deploy: landing page"
gh repo create {product-name}-site --public --source=. --push
gh api -X POST repos/{owner}/{product-name}-site/pages -f source='{"branch":"main","path":"/"}'
```

Then the site will be live at `https://{owner}.github.io/{product-name}-site/`.

**Notes:**
- First-time users will be prompted to log in to the chosen platform via browser
- All three platforms deploy static files directly, no build step needed
- If the user doesn't specify a platform, default to Netlify

---

## Design Laws (Never Break These)

1. **No `#ffffff` backgrounds.** Not on sections, not on cards. Warm neutrals: `#f5ede0`. Cool: `#edf0ee`. Dark: `#08060f`. Cards get a slight tint, never pure white.
2. **No `#6366f1`.** Color comes from the city style palette.
3. **Decide the transition type independently for each section boundary.** Every pair of adjacent sections has its own visual relationship — don't reuse the same clip-path class everywhere. The user chooses a **transition direction** (geometric sharp / organic soft / cover-blend / minimal line / AI auto) in the options preview. Use that direction to constrain which classes you pick: `GEOMETRIC` → diagonals, chamfers, steps; `ORGANIC` → curves, scallops, arcs; `BLEND` → cover overlays and gradient dissolves; `MINIMAL` → hairline rules. If `__AI_CHOOSE__`, scan the selected city's entry in `references/city-styles.md` for divider/transition language first. Then apply per-boundary logic: consider what the two sections are (hero → features, features → pricing, etc.), their relative energy, and the overall page rhythm. Available classes in `assets/clip-paths.css`: diagonal (`clip-diagonal-*`, `clip-parallelogram`), curved (`clip-round-bottom`, `clip-scallop`, `clip-arc-bottom`), gradient dissolve (`section-dissolve`), flat rule (`section-rule`).
4. **No generic icons.** Match the city style's stroke weight and geometry.
5. **Two typefaces minimum.** Display/serif for headlines + clean sans for body. From `references/city-styles.md`. Decorative/script accent fonts (when a city style mentions one) go on watermarks, pull quotes, or ornamental elements — **never on buttons, nav, or body copy**.
6. **Nav must surprise.** Use the chosen nav from `references/nav-catalog.md` with its full surprise element implemented.
7. **Use bundled assets.** The texture, GSAP snippets, and clip-paths must come from the skill's asset files — not reimplemented from scratch.
8. **`.line-wrap` CJK fix.** Whenever the page has Chinese or Japanese text and uses `.line-wrap { overflow: hidden }` for line reveal animations, add `padding-top: 0.15em; margin-top: -0.15em;` to prevent CJK ascenders from being clipped at the top.
9. **No clone grids.** When a section contains multiple repeating items (feature rows, pricing cards, FAQ items, testimonials), they must not all share the same visual treatment. One item should be the focal point — larger, accented, or with a distinct layout — while others form the supporting cast. A section should feel like a poster with visual hierarchy, not a spreadsheet of identical rows. This is the single biggest cause of pages looking "templated" rather than designed.
10. **Responsive by default.** Every page must work on mobile (375px) through desktop (1440px). Rules:
    - Hero text: use `clamp()` for all font sizes, never fixed `px`/`rem` alone
    - Grid layouts: collapse to single column below 768px via `@media (max-width: 768px)`
    - Navigation: pill nav shrinks gap/padding on mobile; side nav hides on mobile with a toggle
    - Touch targets: all buttons and links minimum 44px height
    - No horizontal scroll: test with `overflow-x: hidden` on `body`, but fix the root cause
    - Images/SVGs: use `max-width: 100%` and `aspect-ratio` to prevent layout shift
11. **SEO baseline.** Every generated `index.html` must include:
    - `<title>` with product name and value proposition (under 60 chars)
    - `<meta name="description">` with a compelling summary (under 155 chars)
    - `<meta property="og:title">`, `og:description`, `og:type` (website)
    - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
    - Semantic HTML: one `<h1>`, sequential heading hierarchy (`h1` → `h2` → `h3`), `<nav>`, `<main>`, `<footer>`
    - `lang` attribute on `<html>` matching the page language
12. **Footer required.** Every page must have a `<footer>` with at minimum: brand name, copyright year, and a link back to top or to the product. No page ends abruptly after the last section.
13. **Accessibility baseline.** Every generated page must:
    - Use the `prefersReducedMotion` guard from `gsap-snippets.js` (function 0)
    - Include `<a class="skip-link" href="#main">` for keyboard users
    - Ensure all interactive elements have visible `:focus-visible` styles
    - Use `aria-expanded` on FAQ accordion triggers and nav toggles

---

## Reference Files

- `references/city-styles.md` — Exact design parameters (fonts, colors, textures, motion, icons) for each city aesthetic
- `references/nav-catalog.md` — 4 nav styles with full implementation notes and GSAP code
- `references/imagery-derivation.md` — How to translate any non-city description (scene, era, material, emotion) into a concrete design token system. Read this whenever the user describes something that isn't one of the 57 city cards.
- `references/product-demo-hero.md` — When and how to build a time-driven product workflow demo in the Hero (Variant D). Includes scene design guide, 3-act structure, onEnter() callback patterns, and product-type → scene mapping table. Read this whenever the user wants to show their product's process in the hero.
