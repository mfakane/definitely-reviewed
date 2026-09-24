# definitely-reviewed

Markdown から生成した文書に、論文や技術報告書のような組版を適用するレスポンシブ CSS テーマです。

**日本語** | [English](./README.md)

**Markdown in. Academia out.**

学術文書の佇まいを取り入れつつ、本文の構造はセマンティックな HTML のまま保ちます。JavaScript や特定の Markdown 処理系に依存せず、`definitely-reviewed.css` を読み込んで所定のクラスを指定するだけで利用できます。

> 見た目の「査読済み感」と、実際の査読・研究上の厳密さは別物です。

## 特徴

- **学術文書らしいタイポグラフィ**
  - セリフ体を基本とした本文、サンセリフ体のメタ情報、等幅体のコードを組み合わせます。
  - タイトル、著者、所属、メタ情報、要旨を含む論文風のヘッダーを構成できます。
- **レスポンシブな 2 段組**
  - 広い画面では読みやすい本文幅を保ちながら 2 段組で表示します。
  - コンテナ幅が狭くなると自動的に 1 段組へ切り替わります。
  - 固定のブレークポイントではなく、CSS の Container Queries と Multi-column Layout を利用しています。
- **Markdown フレンドリー**
  - 見出し、段落、リスト、リンク、コード、引用、表、画像など、一般的な HTML 要素をそのまま扱えます。
  - スタイルシートを外しても、情報構造と本文は通常の HTML として保持されます。
- **図表・コード・数式に対応**
  - `figure`、`figcaption`、コードブロック、表、数式用の領域を用意しています。
  - 段組みを横断する図やコードには `dr-wide` を指定できます。
  - KaTeX、MathJax、Mermaid、SVG などの出力を、特定のライブラリに依存せず利用できます。
- **Web と印刷の両対応**
  - `prefers-color-scheme: dark` に対応した Web テーマを提供します。
  - `data-dr-theme="paper"` で白黒の紙面風テーマに切り替えられます。
  - 印刷時は余白、A4 サイズ、段組み、リンク、ツールバーを用紙向けに最適化します。
- **任意の遊び心**
  - `dr-stamp` や `data-stamp` を使って、`Accepted` や `Preprint` などのスタンプを表示できます。
  - 文書の内容や意味に影響を与えない、完全にオプトインの装飾です。

## 想定する用途

- Markdown から生成する技術報告書、設計書、研究ノート
- 個人サイトやドキュメントサイトの論文風ページ
- 数式、コード、図表を含む長文の技術文書
- ブラウザでの閲覧と PDF や紙への印刷を両立したい文書
- 「論文らしい外観」は欲しいが、大がかりな組版システムや複雑なテンプレートは導入したくない場合

ブログ記事のような短い 1 カラムのコンテンツにも利用できますが、見出しや図表を含むまとまった文書で特に効果を発揮します。

## インストール

本テーマは以下の複数の手段で提供されています。

- CDN: [jsDelivr](https://www.jsdelivr.com/package/npm/definitely-reviewed)
- npm: [npm](https://www.npmjs.com/package/definitely-reviewed)
- Git: [GitHub](https://github.com/mfakane/definitely-reviewed)

### Method A. CDN を利用する

[jsDelivr](https://www.jsdelivr.com/package/npm/definitely-reviewed) の public URL を使用して CSS を読み込みます。

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/definitely-reviewed@1.0.0/definitely-reviewed.css">
```

### Method B. npm からインストールする

以下のコマンドでパッケージをインストールします。

```bash
npm install definitely-reviewed
```

npm パッケージをサポートするその他のパッケージマネージャ (e.g. yarn, pnpm, deno) も利用できます。

### Method C. GitHub から clone する

GitHub からリポジトリを clone して、ルートに存在する CSS を取り込みます。

```bash
git clone https://github.com/mfakane/definitely-reviewed.git
```

## 導入

### 1. CSS を読み込む

`definitely-reviewed.css` をプロジェクトに配置するか、公開 URL から読み込みます。

```html
<link rel="stylesheet" href="./definitely-reviewed.css">
```

外部フォントや JavaScript は必須ではありません。CSS で指定されているフォントが利用できない場合は、OS の代替フォントにフォールバックします。

### 2. 基本の HTML 構造を用意する

ページ全体に `dr-page`、外側のラッパーに `dr-shell`、文書本体に `dr-paper` を指定します。ヘッダーと本文は、それぞれ `dr-header` と `dr-body` で囲みます。

```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>技術報告書</title>
  <link rel="stylesheet" href="./definitely-reviewed.css">
</head>
<body class="dr-page">
  <main class="dr-shell">
    <article class="dr-paper">
      <header class="dr-header">
        <p class="dr-kicker">Technical Report</p>
        <h1 class="dr-title">文書のタイトル</h1>
        <p class="dr-authors">著者名</p>
        <p class="dr-affiliation">所属</p>
        <p class="dr-meta">2026 年 9 月 · Version 1.0</p>
        <div class="dr-abstract">
          文書の要旨をここに記載します。
        </div>
      </header>

      <div class="dr-body">
        <h2>1. はじめに</h2>
        <p>本文をここに記載します。</p>

        <h2>2. 実装</h2>
        <p>見出し、リスト、コード、表などを通常の HTML として記述できます。</p>
      </div>
    </article>
  </main>
</body>
</html>
```

`dr-kicker`、`dr-authors`、`dr-affiliation`、`dr-meta`、`dr-abstract` はヘッダー用の補助クラスです。必要な要素のみを適宜利用してください。

## テーマの切り替え

### Web テーマ（標準）

`data-dr-theme` を指定しない場合は、画面閲覧向けの標準テーマが適用されます。明るい配色を基本とし、OS がダークモードに設定されている場合は自動的にダークテーマへ切り替わります。

```html
<html lang="ja">
```

### Paper テーマ

紙面や白黒印刷に近い外観にしたい場合は、`html` または文書を囲む要素に `data-dr-theme="paper"` を指定します。

```html
<html lang="ja" data-dr-theme="paper">
```

Paper テーマでは、背景・文字・アクセントカラーをモノトーン基調にし、影や角丸を無効化します。

## 便利な要素とクラス

### 図、コード、キャプション

```html
<figure class="dr-figure">
  <img src="figure.svg" alt="システム構成図">
  <figcaption class="dr-caption">図 1. システム構成</figcaption>
</figure>

<figure class="dr-listing">
  <pre><code>const answer = 42;</code></pre>
  <figcaption class="dr-caption">Listing 1. サンプルコード</figcaption>
</figure>
```

### 段組みを横断する要素（全幅表示）

本文中の大きな図、コード、表などを段組みをまたいで全幅表示するには、`dr-wide` を追加します。

```html
<figure class="dr-figure dr-wide">
  <img src="wide-figure.svg" alt="本文幅いっぱいの図">
  <figcaption class="dr-caption">図 2. 段組みを横断する図</figcaption>
</figure>
```

直前の見出し（`h2`、`h3`、`h4`）に `dr-wide` 要素が続く場合、その見出しも同様に全幅へ広がり、見出しだけが前の段に取り残されるのを防ぎます。狭い画面では自動的に 1 段組へ切り替わるため、`dr-wide` の横断表示は自動で解除されます。

### 数式

数式の描画機能自体は本テーマに含まれませんが、KaTeX や MathJax などで生成した数式を `dr-equation` で囲むことで、横スクロールの適用や段組み内での意図しない改段・分割を防止できます。

```html
<div class="dr-equation">
  <!-- KaTeX / MathJax などの描画結果 -->
  E = mc<sup>2</sup>
</div>
```

### 注記と参考文献

```html
<div class="dr-note">
  重要な補足情報をここに記載します。
</div>

<ol class="dr-references">
  <li>参考文献のタイトル。</li>
  <li>別の参考文献。</li>
</ol>
```

### スタンプ

スタンプは状態管理用ではなく、装飾用のオプションです。

```html
<span class="dr-stamp" data-kind="accepted">Accepted</span>
<span class="dr-stamp" data-kind="preprint">Preprint</span>
```

利用できる `data-kind` は `confidential`、`accepted`、`preprint`、`rejected` です。文書全体にスタンプを表示する場合は、`dr-paper` に `data-stamp` を指定します。

```html
<article class="dr-paper" data-stamp="Definitely Reviewed">
  ...
</article>
```

## カスタマイズ

配色、余白、フォント、段組み幅などは、`:root` で定義された CSS カスタムプロパティを上書きして変更できます。

```css
:root {
  --dr-accent: #245b73;
  --dr-font-serif: "Noto Serif JP", serif;
  --dr-column-width: 30rem;
  --dr-paper-max: 76rem;
}
```

主な変数は次のとおりです。

| 変数 | 役割 |
| --- | --- |
| `--dr-paper` / `--dr-page` | 文書面とページ背景の色 |
| `--dr-ink` / `--dr-muted` | 本文色と補助情報の色 |
| `--dr-accent` | リンク、注記、引用などのアクセント色 |
| `--dr-paper-max` | 文書の最大幅 |
| `--dr-column-width` | 1 段あたりの推奨幅 |
| `--dr-column-gap` | 段の間隔 |
| `--dr-pad-inline` / `--dr-pad-block` | 文書内側の余白 |
| `--dr-font-serif` / `--dr-font-sans` / `--dr-font-mono` | 本文、UI、コードのフォント |

`color-mix()`、Container Queries、Multi-column Layout などの比較的新しい CSS 機能を使用しています。対象ブラウザでのサポート状況を確認したうえでご利用ください。

## デモ

リポジトリ内の [`index.html`](./index.html) は、英語と日本語のサンプル文書を収録したデモです。画面上部のツールバーから、表示言語や Web / Paper テーマを切り替えられます。

ローカルで確認する場合は、リポジトリのディレクトリで任意の静的ファイルサーバーを起動し、`index.html` を開いてください。本 CSS テーマの利用にサーバーサイド処理は必要ありません。

## ファイル構成

- [`definitely-reviewed.css`](./definitely-reviewed.css): CSS テーマ本体
- [`index.html`](./index.html): 動作確認用のデモページ

デモ用の `dr-demo-*` クラスや言語切り替え用の属性セレクターは、テーマ本体の利用には必須ではありません。導入時は必要な部分のみを取り入れてご利用ください。

## ライセンス

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/)
