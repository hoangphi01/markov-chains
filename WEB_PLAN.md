# WEB_PLAN.md - LaTeX to Web Conversion Strategy

## Architecture

Jekyll-based framework with data-driven navigation. Add a chapter by creating one file + one YAML entry.

## Layout: 3-Column Grid

```
+------------------+------------------------+------------------+
|  LEFT (220px)    |  CENTER (flex)         |  RIGHT (240px)   |
|  Table of        |  Main content          |  Sidebar:        |
|  Contents        |  (chapter text,        |  - Key symbols   |
|  (auto from      |   formulas, examples)  |  - Quick refs    |
|   chapters.yml)  |                        |  - Vietnamese-   |
|                  |                        |    English terms |
+------------------+------------------------+------------------+
```

On mobile (<900px): single column, TOC collapses to top, sidebar moves below content.

## File Structure

```
docs/
  _config.yml                     # Jekyll config
  _data/
    chapters.yml                  # Single source of truth for chapter order, titles, URLs
  _layouts/
    default.html                  # Base: <head>, MathJax, CSS (framework + book)
    chapter.html                  # 3-column: nav + content + sidebar (auto prev/next)
  _includes/
    mathjax.html                  # MathJax v3 config + custom macros (\PP, \E, etc.)
    nav.html                      # Data-driven chapter list (from chapters.yml)
    components/
      box-start.html              # Box open (params: type, title)
      box-end.html                # Box close
      example-start.html          # Example open (params: title)
      example-end.html            # Example close
      exercise-start.html         # Exercise open (params: title)
      exercise-end.html           # Exercise close
    sidebars/
      default.html                # Fallback sidebar (key symbols)
      ch1.html - ch5.html         # Per-chapter sidebar content
      appendix.html               # Appendix sidebar
  _chapter_template.html          # Copy this to create new chapters
  Gemfile                         # Ruby dependencies (jekyll ~> 4.3)
  .gitignore                      # Exclude _site/, .jekyll-cache/
  css/
    framework.css                 # Reusable grid, box structure, nav, responsive (any book)
    book.css                      # Literata font, sepia palette, box colors (this book)
  js/nav.js                       # TOC active state tracking, smooth scroll
  index.html                      # Landing page (standalone, no layout)
  ch1.html - ch5.html             # Chapter pages (Jekyll front matter + layout)
  appendix.html                   # Appendix page (Jekyll front matter + layout)
```

### CSS Architecture

**`framework.css`** - reusable for any book:
- 3-column grid layout (`.page-wrapper`, `.toc`, `.content`, `.sidebar`)
- Box structure with CSS custom properties (`--box-header`, `--box-bg`, `--box-border`)
- Global `--box-radius: 20px` in `:root` — controls border-radius for ALL boxes
- Typography, tables, navigation, responsive breakpoints

**`book.css`** - specific to this Markov Chains book:
- Literata font, sepia color palette
- Box type colors via CSS custom properties:
  - `.box.definition` — green (`#2e7d32`)
  - `.box.theorem` — red (`#b71c1c`)
  - `.box.formula` — gold (`#c49000`)
  - `.box.summary` — blue (`#1565c0`)
- Example/exercise styling, proof blocks

### IMPORTANT: Use .html, NOT .md

Chapter files **must** be `.html`, not `.md`. Reason:
- `.md` files go through Markdown processing, which **corrupts** raw HTML tags and MathJax
- `.html` files with front matter get the same Jekyll layout/include benefits but **skip** Markdown conversion

## .tex -> HTML Mapping

### Environments — Use Component Includes

| LaTeX Environment | Jekyll Include | Params |
|---|---|---|
| `\section{}` | `<h2 id="...">Title <small>(English)</small></h2>` | — |
| `\subsection{}` | `<h3 id="...">Title <small>(English)</small></h3>` | — |
| `\begin{dinhnghia}[Title]` | `{% include components/box-start.html type="definition" title='Title' %}` | type, title |
| `\begin{dinhly}[Title]` | `{% include components/box-start.html type="theorem" title='Title' %}` | type, title |
| `\begin{congthuc}` | `{% include components/box-start.html type="formula" %}` | type |
| `\begin{tomtat}` | `{% include components/box-start.html type="summary" title='Title' %}` | type, title |
| `\end{dinhnghia/dinhly/...}` | `{% include components/box-end.html %}` | — |
| `\begin{example}[Title]` | `{% include components/example-start.html title='Title' %}` | title |
| `\end{example}` | `{% include components/example-end.html %}` | — |
| `\begin{exercise}[Title]` | `{% include components/exercise-start.html title='Title' %}` | title |
| `\end{exercise}` | `{% include components/exercise-end.html %}` | — |
| `\begin{proof}` | `<div class="proof">` (auto prefix "Chứng minh." + QED) | — |
| `\begin{itemize}` | `<ul>` | — |
| `\begin{enumerate}` | `<ol>` | — |
| `\begin{align*}` | `\begin{align*}` in MathJax (keep as-is) | — |
| `\begin{bmatrix}` | `\begin{bmatrix}` in MathJax (keep as-is) | — |
| `\begin{tabular}` | `<table>` | — |

### Inline Commands

| LaTeX Command | HTML |
|---|---|
| `$...$` | `\(...\)` (MathJax inline) |
| `\[...\]` | `\[...\]` (MathJax display) |
| `\term{X}` | `<strong>X</strong>` |
| `\en{X}` | `<em>(X)</em>` |
| `\textbf{X}` | `<strong>X</strong>` |
| `\textit{X}` | `<em>X</em>` |
| `\emph{X}` | `<em>X</em>` |
| `\label{...}` | `id="..."` on parent element |
| `\ref{...}` | `<a href="#...">` |
| `\eqref{...}` | `\eqref{...}` (MathJax handles) |
| `\PP` | `\PP` (MathJax macro) |
| `\E` | `\E` (MathJax macro) |
| `\N`, `\Z`, `\R` | Keep as-is (MathJax macros) |
| `\ind` | `\ind` (MathJax macro) |

### MathJax Configuration

MathJax v3 with custom macros (defined in `_includes/mathjax.html`):

```html
<script>
MathJax = {
  tex: {
    macros: {
      PP: "\\mathbb{P}",
      E: "\\mathbb{E}",
      N: "\\mathbb{N}",
      Z: "\\mathbb{Z}",
      R: "\\mathbb{R}",
      ind: "\\mathbf{1}"
    },
    tags: 'ams'
  }
};
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>
```

## Adding a New Chapter (2 steps + optional sidebar)

### Step 1: Add entry to `_data/chapters.yml`

```yaml
- slug: ch6
  url: /ch6.html
  nav_title: "Ch 6: Tiêu đề ngắn"
  heading: "Chương 6: Tiêu đề đầy đủ"
  heading_en: "English Title"
```

Navigation and prev/next links update **automatically** from data order.

### Step 2: Create chapter file

```bash
cp docs/_chapter_template.html docs/ch6.html
```

Edit front matter:

```yaml
---
layout: chapter
slug: ch6
sections:
  - id: section-1
    title: "1. Tên mục"
  - id: bai-tap
    title: "Bài tập"
---
```

Write content using component includes (see `_chapter_template.html` for full examples):

```html
{% include components/box-start.html type="definition" title='Định nghĩa (Tên -- <em>English</em>)' %}
<p>Nội dung...</p>
{% include components/box-end.html %}

{% include components/example-start.html title='Ví dụ: Tên' %}
<p>Nội dung...</p>
{% include components/example-end.html %}
```

### Step 3 (optional): Create sidebar

Create `_includes/sidebars/ch6.html` and add a case in `_layouts/chapter.html`:

```liquid
{% when 'ch6' %}{% include sidebars/ch6.html %}
```

### That's it!

No need to edit `nav.html`, `index.html`, or any other chapter's front matter.

## Right Sidebar Content (per chapter)

| Chapter | Sidebar Content |
|---|---|
| All | Key symbols: \(\PP\), \(\E\), \(\pi\), \(\lambda\), \(\mu\) |
| Ch 1 | P_{i,j} notation, row-sum=1, eigenvalues, \(\lambda_2 = 1-a-b\) |
| Ch 2 | FSA formula template, boundary conditions table, (I-Q)^{-1} |
| Ch 3 | Recurrent vs Transient comparison table, period definition |
| Ch 4 | \(\pi = \pi P\), convergence conditions checklist, detailed balance |
| Ch 5 | Q vs P comparison table, Exp distribution properties, \(\pi Q = 0\) |
| Appendix | Distribution table (name, PMF/PDF, E, Var) |

## .tex to HTML Conversion Workflow

When converting a new `.tex` chapter to HTML:

1. Read the `.tex` file and identify all sections, environments, examples, exercises
2. Add entry to `_data/chapters.yml`
3. Create `.html` file with front matter (`layout: chapter`, `slug`, `sections`)
4. Convert LaTeX environments to Jekyll includes:
   - `\begin{dinhnghia}` → `{% include components/box-start.html type="definition" title='...' %}`
   - `\begin{dinhly}` → `{% include components/box-start.html type="theorem" title='...' %}`
   - `\begin{congthuc}` → `{% include components/box-start.html type="formula" %}`
   - `\begin{tomtat}` → `{% include components/box-start.html type="summary" title='...' %}`
   - Close all with `{% include components/box-end.html %}`
   - `\begin{example}` → `{% include components/example-start.html title='...' %}`
   - `\begin{exercise}` → `{% include components/exercise-start.html title='...' %}`
5. Keep all LaTeX math as-is (MathJax renders it). Keep `\PP`, `\E`, etc. as macros.
6. Replace `\term{X}` with `<strong>X</strong>`, `\en{X}` with `<em>(X)</em>`
7. Convert `$...$` to `\(...\)` for inline math
8. Convert `\begin{itemize}` to `<ul>`, `\begin{enumerate}` to `<ol>`
9. Convert `\begin{tabular}` to HTML `<table>`
10. Keep `\begin{align*}`, `\begin{equation}`, `\begin{bmatrix}` as-is for MathJax
11. Create sidebar `_includes/sidebars/chN.html` and add case in layout

## Local Development

```bash
cd docs/
gem install bundler
bundle install
bundle exec jekyll serve    # http://localhost:4000
```

## GitHub Pages Deployment

Automatic via GitHub Actions (`.github/workflows/pages.yml`).
Push to `main` branch -- Jekyll builds and deploys automatically.
