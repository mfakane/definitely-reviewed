# definitely-reviewed

A responsive scholarly CSS theme that gives Markdown-derived documents the typesetting and visual appearance of academic papers and technical reports.

[日本語](./README.ja.md) | **English**

**Markdown in. Academia out.**

Brings the scholarly aesthetic to your documents while keeping content in standard, semantic HTML. It has zero dependencies on JavaScript or specific Markdown processors—simply include `definitely-reviewed.css` and add the designated classes.

> The visual appearance of rigor should not be confused with methodological rigor.

## Features

- **Scholarly Typography**
  - Combines serif body text, sans-serif metadata, and monospace code.
  - Supports a paper-like header comprising title, authors, affiliations, metadata, and abstract.
- **Responsive Multi-column Layout**
  - Displays content in two columns on wide viewports while maintaining a comfortable reading measure (line length).
  - Automatically collapses to a single column when container width becomes constrained.
  - Uses CSS Container Queries and Multi-column Layout rather than rigid, fixed breakpoints.
- **Markdown Friendly**
  - Seamlessly handles standard HTML elements: headings, paragraphs, lists, links, code blocks, blockquotes, tables, images, and more.
  - Even if the stylesheet is removed, content and document structure remain clean semantic HTML.
- **Rich Support for Figures, Code, and Equations**
  - Dedicated styling for `figure`, `figcaption`, code listings, tables, and equations.
  - Use `dr-wide` for wide figures or code listings spanning across columns.
  - Supports output from tools like KaTeX, MathJax, Mermaid, and SVG without being tied to any specific renderer or library.
- **Dual Support for Web and Print**
  - Provides a default Web theme with `prefers-color-scheme: dark` support.
  - Switch to a monochrome print-like theme using `data-dr-theme="paper"`.
  - Automatically optimizes margins, A4 sizing, columns, links, and toolbars when printing.
- **Optional Playfulness**
  - Add administrative stamps like `Accepted` or `Preprint` using `dr-stamp` or `data-stamp`.
  - Purely opt-in cosmetic decorations that do not alter the semantic meaning or content of the document.

## Use Cases

- Technical reports, design docs, and research notes generated from Markdown
- Scholarly / paper-like pages on personal websites or documentation portals
- Long-form technical documentation featuring equations, code snippets, and diagrams
- Documents that require both comfortable in-browser reading and high-quality PDF/print output
- When you want the visual gravitas of an academic paper without dealing with heavy typesetting systems (like LaTeX) or convoluted templates

While usable for short, single-column blog posts, this theme shines most with substantial documents containing section headings, figures, and tables.

## Installation

This theme is provided in several ways:

- CDN: [jsDelivr](https://www.jsdelivr.com/package/npm/definitely-reviewed)
- npm: [npm](https://www.npmjs.com/package/definitely-reviewed)
- Git: [GitHub](https://github.com/mfakane/definitely-reviewed)

### Method A. Use CDN

Load the CSS via a public URL from [jsDelivr](https://www.jsdelivr.com/package/npm/definitely-reviewed).

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/definitely-reviewed@1.0.0/definitely-reviewed.css">
```

### Method B. Install via npm

Install the package with the following command:

```bash
npm install definitely-reviewed
```

Any other package manager that supports npm packages (e.g. yarn, pnpm, deno) can be used.

### Method C. Clone from GitHub

Clone the repository from GitHub and include the CSS from the root directory.

```bash
git clone https://github.com/mfakane/definitely-reviewed.git
```

## Getting Started

### 1. Include the CSS

Copy `definitely-reviewed.css` into your project or load it via a public URL.

```html
<link rel="stylesheet" href="./definitely-reviewed.css">
```

No external fonts or JavaScript are required. If the fonts specified in the CSS are unavailable on the user's system, it gracefully falls back to system fonts.

### 2. Basic HTML Structure

Apply `dr-page` to the page body, `dr-shell` to the outer wrapper, and `dr-paper` to the document container. Wrap the header and body content in `dr-header` and `dr-body`, respectively.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Technical Report</title>
  <link rel="stylesheet" href="./definitely-reviewed.css">
</head>
<body class="dr-page">
  <main class="dr-shell">
    <article class="dr-paper">
      <header class="dr-header">
        <p class="dr-kicker">Technical Report</p>
        <h1 class="dr-title">Document Title</h1>
        <p class="dr-authors">Author Name</p>
        <p class="dr-affiliation">Affiliation</p>
        <p class="dr-meta">September 2026 · Version 1.0</p>
        <div class="dr-abstract">
          Place your abstract or executive summary here.
        </div>
      </header>

      <div class="dr-body">
        <h2>1. Introduction</h2>
        <p>Main content goes here.</p>

        <h2>2. Implementation</h2>
        <p>Headings, lists, code, and tables can be written as standard HTML.</p>
      </div>
    </article>
  </main>
</body>
</html>
```

`dr-kicker`, `dr-authors`, `dr-affiliation`, `dr-meta`, and `dr-abstract` are optional helper classes for the header. Use only the elements you need.

## Theme Switching

### Web Theme (Default)

When `data-dr-theme` is omitted, the standard screen-reading theme is used. It features a bright palette by default and automatically switches to dark mode if selected by the OS.

```html
<html lang="en">
```

### Paper Theme

To achieve an appearance closer to physical print or monochrome paper, add `data-dr-theme="paper"` to the `html` element or the document wrapper.

```html
<html lang="en" data-dr-theme="paper">
```

In Paper theme, backgrounds, text, and accent colors switch to high-contrast monochrome, while drop shadows and rounded corners are disabled.

## Useful Elements and Classes

### Figures, Code Listings, and Captions

```html
<figure class="dr-figure">
  <img src="figure.svg" alt="System architecture diagram">
  <figcaption class="dr-caption">Figure 1. System architecture</figcaption>
</figure>

<figure class="dr-listing">
  <pre><code>const answer = 42;</code></pre>
  <figcaption class="dr-caption">Listing 1. Sample code</figcaption>
</figure>
```

### Spanning Across Columns (Full-Width Elements)

To display large figures, code listings, or tables across the entire width spanning both columns, add the `dr-wide` class.

```html
<figure class="dr-figure dr-wide">
  <img src="wide-figure.svg" alt="Full-width diagram">
  <figcaption class="dr-caption">Figure 2. Full-width diagram spanning columns</figcaption>
</figure>
```

When a heading (`h2`, `h3`, `h4`) is immediately followed by a `dr-wide` element, the heading also automatically spans across columns, preventing it from being awkwardly stranded at the bottom of the preceding column. On narrow screens, the layout automatically reverts to a single column, naturally disabling multi-column spanning.

### Mathematical Equations

Rendering math equations is not the responsibility of the CSS theme itself. However, wrapping equations generated by KaTeX or MathJax in `dr-equation` enables horizontal scrolling on overflow and prevents awkward page or column fragmentation.

```html
<div class="dr-equation">
  <!-- KaTeX / MathJax rendered equation -->
  E = mc<sup>2</sup>
</div>
```

### Notes and References

```html
<div class="dr-note">
  Important supplementary information goes here.
</div>

<ol class="dr-references">
  <li>Reference entry title.</li>
  <li>Another reference.</li>
</ol>
```

### Stamps

Stamps are decorative elements rather than semantic status indicators.

```html
<span class="dr-stamp" data-kind="accepted">Accepted</span>
<span class="dr-stamp" data-kind="preprint">Preprint</span>
```

Supported `data-kind` values are `confidential`, `accepted`, `preprint`, and `rejected`. To display a watermark stamp across the entire paper, specify `data-stamp` on `dr-paper`:

```html
<article class="dr-paper" data-stamp="Definitely Reviewed">
  ...
</article>
```

## Customization

Colors, padding, fonts, and column widths can be customized by overriding the CSS custom properties defined in `:root`.

```css
:root {
  --dr-accent: #245b73;
  --dr-font-serif: "Noto Serif JP", serif;
  --dr-column-width: 30rem;
  --dr-paper-max: 76rem;
}
```

Key variables include:

| Variable | Description |
| --- | --- |
| `--dr-paper` / `--dr-page` | Background colors for the paper surface and outer page |
| `--dr-ink` / `--dr-muted` | Foreground text colors for primary body and secondary/muted text |
| `--dr-accent` | Accent color for links, notes, blockquotes, etc. |
| `--dr-paper-max` | Maximum width of the document |
| `--dr-column-width` | Ideal / target width for a single column |
| `--dr-column-gap` | Gap between columns |
| `--dr-pad-inline` / `--dr-pad-block` | Document inner padding (horizontal and vertical) |
| `--dr-font-serif` / `--dr-font-sans` / `--dr-font-mono` | Font families for body text, UI elements, and code |

The theme utilizes modern CSS features such as `color-mix()`, Container Queries, and Multi-column Layout. Please check browser compatibility for your target environment.

## Demo

The included [`index.html`](./index.html) is an interactive demonstration containing sample papers in both English and Japanese. Use the toolbar at the top of the page to switch between languages and toggle between the Web and Paper themes.

To preview locally, start any static file server from the repository root and open `index.html`. No server-side runtime or build step is required.

## Repository Structure

- [`definitely-reviewed.css`](./definitely-reviewed.css): The core CSS theme stylesheet
- [`index.html`](./index.html): Interactive demo and test page

Demo-specific classes (`dr-demo-*`) and language-switching attribute selectors in `index.html` are not required for general use. When integrating into your own project, simply adopt the components you need.

## License

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/)
