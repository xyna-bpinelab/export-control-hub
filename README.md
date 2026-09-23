# 安全保障貿易管理ナビ

経済産業省の安全保障貿易管理（外為法・政省令・通達）を、**図解・表・カード中心**で整理した実務・学習向けサイトです。長文を読まずに要点をつかめるよう、Mermaid のフローチャート、比較タブ、強調ボックスで構成しています。

**公開サイト：** https://xyna-bpinelab.github.io/export-control-hub/

> 本サイトは学習・整理用の非公式資料です。規制対象・しきい値・国グループは政省令改正で頻繁に変わります。実際の判断は、必ず経済産業省「安全保障貿易管理」ページの最新の法令・通達・Q&A で確認してください。

## 内容

| # | カテゴリ | 主な内容 |
|---|---|---|
| 01 | 全体像 | 案件発生〜記録保存のフロー、法体系、国グループ、用語集 |
| 02 | リスト規制 | 1〜15項（3の2項を含む）の対象としきい値の例 |
| 03 | キャッチオール規制 | 用途要件・需要者要件・インフォーム要件、16項(1)特定品目、外国ユーザーリスト、おそれの強い貨物例、明らかガイドライン |
| 04 | 役務取引 | 技術提供、みなし輸出、特定類型 |
| 05 | 特例・例外 | 少額・無償・携帯品・公知技術 等 |
| 06 | 許可申請 | 個別許可と包括許可 |
| 07 | 社内体制 | 輸出者等遵守基準、CP、記録保存 |
| 08 | 違反事例 | 罰則・行政制裁・過去の事例 |
| 09 | 関連法令 | 法令・通達の一覧と公式リンク |

コンテンツは `content/ja/docs/` 配下にあります。

## ローカルで動かす

### 必要なもの

| ツール | バージョン | 用途 |
|---|---|---|
| [Hugo](https://gohugo.io/) **extended** | 0.110〜0.145（CI は 0.123.7） | サイト生成 |
| [Go](https://go.dev/) | 1.22 以上 | Hugo Modules（Docsy）の取得 |
| [Node.js](https://nodejs.org/) | 20 以上 | 本番ビルドの PostCSS |

> テーマの [Docsy](https://www.docsy.dev/) は v0.11.0 を使っています。v0.12 以降は Hugo 0.146 以上が必要です。Hugo を上げる場合は Docsy もあわせて更新してください。

### 手順

```bash
npm install            # PostCSS（autoprefixer）をインストール
hugo server            # http://localhost:1313/ でプレビュー（Docsy などの Hugo Modules は go.mod の版で自動取得）
npm run build          # 本番ビルド（public/ に出力）
```

> **注意：** 引数なしの `hugo mod get` は Docsy を最新版に上げてしまい、Hugo 0.123 では動かなくなります。Docsy の版を変える場合は `hugo mod get github.com/google/docsy@v0.11.0` のように版を指定してください。

## 公開（GitHub Pages）

`main` ブランチに push すると、GitHub Actions（`.github/workflows/pages.yml`）がサイトをビルドして GitHub Pages に公開します。Actions タブから手動で実行することもできます。

## 書き方のルール

### 強調ボックス（callout）

```markdown
{{% callout type="warning" title="任意のタイトル" %}}
本文（Markdown 可）
{{% /callout %}}
```

| type | 用途 | 既定のタイトル |
|---|---|---|
| `info` | 要点 | ポイント |
| `note` | 補足 | 補足 |
| `tip` | 実務のコツ | 実務のコツ |
| `warning` | 注意点 | 申請時の注意 |
| `danger` | 違反リスク | 違反リスク |
| `case` | 失敗事例 | 失敗事例 |
| `exception` | 法律上の例外 | 法律上の例外 |

### 図・タブ

- 図は ` ```mermaid ` のコードブロックで書きます。判断の分岐は `X("❓ …")` の角丸ノードにし、`classDef q` で黄色にしています（既存ページを参照）。
- 比較はタブ（`{{< tabpane text=true >}}` と `{{% tab header="…" %}}`）で並べます。

### 注意

- Hugo 0.123 の Markdown は、`**…）**は` のように**全角の括弧・句読点で終わる太字の直後に文字が続く**と太字になりません。その場合は `<strong>…</strong>` を使います。
- 数値・品目・条文番号は、出典（経済産業省の法令・通達・Q&A、e-Gov）で確認したものだけを書きます。

## 構成

```text
content/ja/            # コンテンツ（トップページと docs/ 配下）
layouts/shortcodes/    # callout ショートコード
layouts/_default/      # Docsy の baseof.html の上書き（scripts のキャッシュ回避）
assets/scss/           # 配色・表・図のスタイル
hugo.toml              # サイト設定（Mermaid の設定を含む）
.github/workflows/     # GitHub Pages への自動公開
```
