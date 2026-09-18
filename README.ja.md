<div align="center">

# 🏝️ Landfall

**製品アイデアを入力するだけで、57の都市デザインシステムから美しいランディングページを生成。**

[![GitHub release](https://img.shields.io/github/v/release/can4hou6joeng4/Landfall)](https://github.com/can4hou6joeng4/Landfall/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/can4hou6joeng4/Landfall?style=social)](https://github.com/can4hou6joeng4/Landfall)

[🌐 デモ](https://can4hou6joeng4.github.io/Landfall/) · [📋 変更履歴](CHANGELOG.md) · [🤝 コントリビュート](CONTRIBUTING.md) · [🇬🇧 English](README.md) · [🇨🇳 中文](README.zh-CN.md)

</div>

---

[Claude Code](https://claude.ai/claude-code) のスキル。製品を説明し、都市の美学を選ぶだけで、GSAPアニメーション、clip-pathディバイダー、SVGテクスチャ、本物の奥行きを持つ本番環境対応サイトが完成します。

> ありきたりなカードグリッドテンプレートではありません。すべての出力がデザイン作品です。

## 💡 なぜ Landfall？

多くのジェネレーターは色を変えただけの同じBootstrapレイアウトを提供します。Landfallのアプローチは根本的に異なります。**57の都市スタイルはそれぞれ完全なデザインシステム**：独自のフォント、カラーパレット、テクスチャ、モーションカーブ、アイコン美学を持っています。京都はラゴスとまったく違い、ラゴスはパームスプリングスとまったく違います。

## ⚡ クイックスタート

```bash
npx skills add can4hou6joeng4/Landfall -a claude-code -g -y
```

Claudeに話しかけてください：

```
ランディングページを作って
```

スキルが都市スタイルの選択、レイアウトオプションを案内し、完全なサイトを生成します：

```
your-product/
├── index.html        # ナビ、ヒーロー、セクション、フッター
├── style.css         # デザイントークン、テクスチャ、clip-path
├── main.js           # GSAP ScrollTrigger アニメーション
└── assets/icons.svg  # 都市美学に合わせたSVGスプライト
```

## ✨ 特徴

🎨 **デザインシステム**

- 57の都市美学 — 都市ごとに独自のフォント、配色、テクスチャ、モーション
- 3つのカラートーン — オリジナル / ダークラグジュアリー / ブライトモダン
- 🌓 ダークモード切替（localStorageで永続化）

🧩 **ページセクション**

- 7種ヒーロー · 6種フィーチャー · 6種テスティモニアル · 4種ナビ
- 3種フッター · 3種フォーム · 6種拡張セクション（チーム、統計、ギャラリー、タイムライン...）
- 4種セクションディバイダー — ジオメトリック / オーガニック / ブレンド / ミニマル

🔄 **ワークフロー**

- 🖥️ ブラウザベースのインタラクティブ都市ピッカー — CLIメニュー不要
- 📄 マルチページ対応 — About、Contact、Blogサブページ
- 🚀 ワンクリックデプロイ — Netlify、Vercel、GitHub Pages
- 💻 クロスプラットフォーム — Python 3.6+ / macOS / Windows PowerShell

## 🛠️ 使い方

1. **説明** — 製品名 + 一行の紹介
2. **選択** — ブラウザで57枚の都市スタイルカードを閲覧
3. **カスタマイズ** — ヒーロー、ナビ、カラートーン、トランジション
4. **生成** — プロジェクトに完全なサイトファイルを書き出し
5. **プレビュー** — ブラウザで自動的に開く
6. **デプロイ** — ワンクリックで公開（任意）

## 🗣️ トリガーフレーズ

```
ランディングページを作って · ホームページを作って · 製品ページ · プロモページ
帮我做一个落地页 · landing page · product page · make me a homepage
```

## 📂 プロジェクト構成

<details>
<summary><kbd>ファイルツリーを展開</kbd></summary>

```
SKILL.md                            # スキル定義
assets/
├── style-preview-template.html     # 57都市インタラクティブピッカー
├── options-preview-template.html   # レイアウト/ナビ/カラー選択
├── clip-paths.css                  # セクションディバイダーライブラリ
├── gsap-snippets.js                # GSAPアニメーションパターン
├── textures.css                    # CSSのみの背景テクスチャ
├── sections/                       # プリビルトセクションテンプレート
│   ├── hero-variants.html          # 7種ヒーロースタイル (A–G)
│   ├── features-variants.html      # 6種フィーチャーレイアウト (A–F)
│   ├── testimonial-variants.html   # 6種テスティモニアルスタイル (A–F)
│   ├── footer-variants.html        # 3種フッタースタイル
│   ├── form-variants.html          # 3種フォームセクション
│   ├── extra-variants.html         # 6種拡張セクション
│   ├── page-variants.html          # マルチページテンプレート
│   └── conversion-variants.html    # 料金、FAQ、CTA
└── scripts/
    ├── run_preview.py              # クロスプラットフォームプレビューランチャー
    ├── run_preview.ps1             # Windows PowerShellランチャー
    ├── get_city_tokens.py          # 都市カラートークン抽出
    └── extract_variant.py          # セクションバリアント抽出
references/
├── city-styles.md                  # 57都市デザインパラメータ
├── nav-catalog.md                  # 4種ナビ実装
├── imagery-derivation.md           # 非都市記述 → トークンマッピング
└── product-demo-hero.md            # 製品デモヒーローガイド
evals/
└── evals.json                      # 評価テストケース
```

</details>

## 🎯 デザイン哲学

1. 🚫 **`#ffffff`の背景禁止** — ウォームニュートラル、クールティント、ディープダーク
2. 🔤 **最低2つの書体** — ディスプレイ見出し + クリーンなサンセリフ本文
3. 🖼️ **SVGがデザインの核心** — 装飾的な飾りではない
4. 🎞️ **GSAPの奥行き** — パララックスレイヤー、スティッキーパネル、スタッガードリビール
5. 📐 **クローングリッド禁止** — すべてのセクションに視覚的階層を

## 📄 ライセンス

[MIT](LICENSE)
