# [プロジェクト名]

> このファイルは各プロジェクトの `CLAUDE.md` として使用するテンプレートです。
> `[...]` の部分をプロジェクトに合わせて書き換えてください。

---

## プロジェクト概要

**目的**: [このプロジェクトが解決する課題・提供する価値]
**対象ユーザー**: [利用者]
**制作物タイプ**: [Webアプリ / ダッシュボード / プレゼン / レポート]

---

## デザインルール

このプロジェクトは **instyle.group デザインシステム** に完全準拠する。
詳細仕様: [`design.md`](./design.md) を参照。

### 必須ルール（常に守ること）

**カラー**
- CSS変数 `--color-*` を使用する（ハードコードしない）
- アクセントカラーは `--color-accent`（ラベル・タグ背景）または `--color-accent-dark`（サイドバー・強調パネル背景）
- 同画面で3色以上のアクセントを使わない

**タイポグラフィ**
- フォント: `Lato`（英数字）+ `Noto Sans JP`（日本語）
- タイプスケールは **モジュラースケール Major Third 1.25 / base 14px**（Liquid 版は 1.333 で別物）：Display 43 / H1 34 / H2 27 / H3 22 / H4 18 / Body 14 / Small 11 / Caption 9 px
- 最小フォントサイズ: `0.6875rem (11px)` ／ Caption (9px) はチャート目盛り専用
- 見出しは最大3階層（H2 → H3 → Body）
- **明朝体（`--font-serif: 'Shippori Mincho'`）は既定では使わない**。ユーザーから「明朝で」「serif で」「エディトリアルっぽく」と明示指示があった時のみ使用。eyebrow / 見出し / ステップ番号などには tracked sans（`font-size: 0.625rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.12em;`）を使う

**ハイライト色 `--color-highlight: #E2DD2A`**
- **本文中で立たせたい語句のポイントマーキング専用**（蛍光ペン風）
- 実装: `mark, .mark { background: linear-gradient(180deg, transparent 60%, var(--color-highlight) 60%); padding: 0 2px; }`
- 1 ページに 2〜3 箇所まで
- CTA / アイコン背景 / 見出し全体 / サイドバー / ヘッダー帯など面要素には**使わない**

**角丸（クロソイド式 / Squircle・必須）**
- 全要素の角丸は **連続曲率（superellipse）** を使う。円弧角丸は使わない
- `corner-shape: superellipse(2.5)` を `--corner-shape` トークンとして定義し、`*` セレクタで全要素にデフォルト適用
- radius スケール: `--r-sm: 8px` / `--r: 12px` / `--r-lg: 20px` / `--r-xl: 28px` / `--r-pill: 999px`
- ピル形状（999px）は corner-shape の効果が出ない（stadium 形）のでそのまま
- 未対応ブラウザは通常 `border-radius` にフォールバック（視覚劣化のみ・追加対応不要）

**スペーシング**
- 8pxグリッドを基準にする（4, 8, 12, 16, 24, 32, 48, 64, 96px）
- 余白は大きめに取る

**コントラスト原則（最重要）**
- 要素の区切りはボーダーラインでなく背景色の差で表現する
- 背景レベル: `--color-bg`(白) → `--color-surface` → `--color-surface-2` → `--color-surface-3` → `--color-text`(最暗)
- `border: 1px solid` は構造的区切りに使わない

**カード**
```css
background: var(--color-surface);  /* 白背景からの差で浮き上がる */
border-radius: 8px;
padding: 24px;
/* border なし・box-shadow なし */
```

**ボタン（Primary）**
```css
background: var(--color-text);     /* #35362D — 最大コントラスト */
color: var(--color-text-inverse);
border: none;
border-radius: 6px;
padding: 10px 20px;
font-size: 0.875rem;
```

**ボタン（Secondary）**
```css
background: var(--color-surface);  /* ページ背景(白)から浮かせる */
color: var(--color-text);
border: none;
border-radius: 6px;
padding: 10px 20px;
```

**インプット**
```css
background: var(--color-surface);  /* フィールドをsurfaceで示す */
border: none;
border-radius: 6px;
padding: 10px 14px;
```

**アニメーション**
- Duration: `150ms`（ホバー等）/ `250ms`（展開・遷移）
- Easing: `cubic-bezier(0.4, 0, 0.2, 1)`

---

## 技術スタック

- **フレームワーク**: [React / Next.js / Vanilla HTML+CSS]
- **スタイリング**: [Tailwind CSS / CSS Variables / CSS Modules]
- **チャートライブラリ**: [Recharts / Chart.js / D3]
- **アイコン**: lucide-react

---

## ファイル構成

```
./
├── CLAUDE.md          ← このファイル
├── design.md          ← デザイン詳細仕様
├── index.html         ← エントリーポイント（またはそれに相当するもの）
└── src/
    ├── styles/
    │   └── tokens.css ← CSS変数
    └── components/
```

---

## CSS変数（tokens.css に定義 / または HTML head に直接記述）

```css
:root {
  --color-bg:          #FFFFFF;
  --color-surface:     #F3F1EE;
  --color-surface-2:   #E6E2D7;
  --color-surface-3:   #E1DCD0;
  --color-border:      #C4C1B0;
  --color-border-dark: #82837A;
  --color-text:         #35362D;
  --color-text-muted:   #82837A;
  --color-text-light:   #C4C1B0;
  --color-text-inverse: #F3F1EE;   /* #35362D / #82837A 背景上はこちら */
  --color-accent:       #C4C1B0;
  --color-accent-light: #82837A;
  --color-accent-dark:  #E6E2D7;
  --color-success:     #16A34A;
  --color-warning:     #D97706;
  --color-error:       #C6292C;
  --color-info:        #2563EB;
  --color-highlight:   #E2DD2A;   /* マーカー・強調背景・小面積アクセント */

  /* Radius scale（クロソイド前提でやや大きめ） */
  --r-sm:   8px;
  --r:      12px;
  --r-lg:   20px;
  --r-xl:   28px;
  --r-pill: 999px;

  /* クロソイド式角丸（CSS Borders Level 4） */
  --corner-shape:      superellipse(2.5);
  --corner-shape-soft: superellipse(2);
  --corner-shape-hard: superellipse(3.5);

  --font-sans: 'Lato', 'Noto Sans JP', sans-serif;
  --transition-fast:   150ms cubic-bezier(0.4, 0, 0.2, 1);
  --transition-normal: 250ms cubic-bezier(0.4, 0, 0.2, 1);
}

/* 全要素にデフォルト適用 */
* { corner-shape: var(--corner-shape); }
```

---

## Google Fonts 読み込み（HTML head）

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Lato:wght@100;300;400;700&family=Noto+Sans+JP:wght@400;500;700&family=Shippori+Mincho:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

---

## 制作上の注意点

- [プロジェクト固有の注意点があればここに追記]
- データはモックで構わないが、実際の業務に近い現実的な数値・ラベルを使う
- 日本語と英語が混在する場合、フォントの混在に注意（`font-family` の順序を守る）

---

*テンプレートバージョン: 1.0 | instyle.group Creative Team*
