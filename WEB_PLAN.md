# WEB_PLAN.md - LaTeX to Web Conversion Strategy

## Architecture

**Current (6 chapters):** Standalone HTML files -- work directly in browser or GitHub Pages.
**Scaling (10+ chapters):** Jekyll layouts + includes -- shared nav, sidebars, MathJax config.

Both modes coexist. Current HTML files work standalone. New chapters can use Jekyll front matter + layouts.

## Layout: 3-Column Grid

```
+------------------+------------------------+------------------+
|  LEFT (200px)    |  CENTER (flex)         |  RIGHT (200px)   |
|  Table of        |  Main content          |  Sidebar:        |
|  Contents        |  (chapter text,        |  - Key symbols   |
|  - Ch 1          |   formulas, examples)  |  - Quick refs    |
|  - Ch 2          |                        |  - Vietnamese-   |
|  - ...           |                        |    English terms |
|  - Appendix      |                        |                  |
+------------------+------------------------+------------------+
```

On mobile (<768px): single column, TOC collapses to top nav, right sidebar moves below content.

## File Structure

```
docs/
  index.html          # Landing page with chapter list and overview
  ch1.html            # Discrete-Time Markov Chains (from ch4_discrete.tex)
  ch2.html            # First Step Analysis (from ch5_first_step.tex)
  ch3.html            # Classification of States (from ch6_classification.tex)
  ch4.html            # Limiting and Stationary Distributions (from ch7_limiting.tex)
  ch5.html            # Continuous-Time Markov Chains (from ch9_continuous.tex)
  appendix.html       # Probability Background (from appendix_prob.tex)
  css/style.css       # Grid layout, typography, box styles
  js/nav.js           # TOC active state, smooth scroll
```

## .tex -> HTML Mapping

### Environments

| LaTeX Environment | HTML Element | CSS Class | Border Color |
|---|---|---|---|
| `\section{}` | `<h2>` | -- | -- |
| `\subsection{}` | `<h3>` | -- | -- |
| `\begin{dinhnghia}[...]` | `<div class="box definition">` | `.definition` | green |
| `\begin{dinhly}[...]` | `<div class="box theorem">` | `.theorem` | red |
| `\begin{congthuc}` | `<div class="box formula">` | `.formula` | gold |
| `\begin{tomtat}` | `<div class="box summary">` | `.summary` | blue |
| `\begin{example}[...]` | `<div class="example">` | `.example` | -- |
| `\begin{exercise}[...]` | `<div class="exercise">` | `.exercise` | -- |
| `\begin{itemize}` | `<ul>` | -- | -- |
| `\begin{enumerate}` | `<ol>` | -- | -- |
| `\begin{align*}` | `\begin{align*}` in MathJax | -- | -- |
| `\begin{bmatrix}` | `\begin{bmatrix}` in MathJax | -- | -- |
| `\begin{proof}` | `<div class="proof">` | `.proof` | -- |
| `\begin{tabular}` | `<table>` | -- | -- |

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
| `\PP` | `\mathbb{P}` |
| `\E` | `\mathbb{E}` |
| `\N`, `\Z`, `\R` | `\mathbb{N}`, `\mathbb{Z}`, `\mathbb{R}` |
| `\ind` | `\mathbf{1}` |

### MathJax Configuration

MathJax v3 with custom macros to match LaTeX preamble:

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

## Conversion Notes per Chapter

### ch1.html (from ch4_discrete.tex)
- 5 sections + exercises
- Key formulas: P^n, Chapman-Kolmogorov, two-state P^n formula
- Multiple matrix examples (render as MathJax bmatrix)
- Ehrenfest chain example with N=4 matrix

### ch2.html (from ch5_first_step.tex)
- Hitting probabilities, mean hitting times, first return times
- Block matrix form (Q, R, I)
- Gambler's Ruin with full algebraic solution
- Fish maze example

### ch3.html (from ch6_classification.tex)
- Communicating classes, irreducibility
- Recurrent vs transient (with comparison table)
- Polya's theorem
- Periodicity, ergodic definition

### ch4.html (from ch7_limiting.tex)
- Limiting and stationary distributions
- Detailed balance condition
- Convergence theorem (main result)
- Rate of convergence, spectral gap
- Summary table of methods

### ch5.html (from ch9_continuous.tex)
- Poisson process, birth-death processes
- Generator matrix Q, Kolmogorov equations
- Two-state continuous chain (explicit P(t))
- M/M/1 queue, embedded chain
- Absorption probabilities and mean absorption times

### appendix.html (from appendix_prob.tex)
- Probability spaces, conditional probability
- Discrete and continuous distributions (tables)
- Exponential distribution properties (key for Ch 5)
- Generating functions, inequalities

---

## Jekyll Structure

All chapters use Jekyll front matter + shared layouts. No boilerplate duplication.

```
docs/
  _config.yml                 # Jekyll config
  _layouts/
    default.html              # Base: <head>, MathJax, <body>
    chapter.html              # 3-column: nav + content + sidebar
  _includes/
    mathjax.html              # MathJax v3 config + custom macros (\PP, \E, etc.)
    nav.html                  # Shared chapter list (edit once, updates all pages)
    sidebars/
      default.html            # Fallback sidebar (key symbols)
      ch1.html - ch5.html     # Per-chapter sidebar content
      appendix.html           # Appendix sidebar
  _chapter_template.html      # Copy this to create new chapters
  Gemfile                     # Ruby dependencies (jekyll ~> 4.3)
  .gitignore                  # Exclude _site/, .jekyll-cache/
  css/style.css               # Shared styles (3-column grid, boxes, typography)
  js/nav.js                   # TOC active state tracking, smooth scroll
  index.html                  # Landing page (standalone, no layout)
  ch1.html - ch5.html         # Chapter pages (Jekyll front matter + layout)
  appendix.html               # Appendix page (Jekyll front matter + layout)
```

### IMPORTANT: Use .html, NOT .md

Chapter files **must** be `.html`, not `.md`. Reason:
- `.md` files go through Markdown processing, which **corrupts** raw HTML tags and MathJax
- `.html` files with front matter get the same Jekyll layout/include benefits but **skip** Markdown conversion
- The content is already HTML -- no Markdown conversion needed

### How a Chapter File Looks

```html
---
layout: chapter
title: "Ch N: Vietnamese Title"
chapter_num: N
heading: "Chuong N: Vietnamese Title"
heading_en: "English Title"
prev_url: /chN-1.html
prev_title: "Chuong N-1"
next_url: /chN+1.html
next_title: "Chuong N+1"
sections:
  - id: section-id
    title: "Section Title"
---

<!-- Only content here -- no <html>, <head>, <nav>, <sidebar>, <script> -->

<h2 id="section-id">Section Title</h2>
<p>Content with math: \(\PP(X = k)\)</p>

<div class="box definition">
  <p class="box-title">Dinh nghia</p>
  <p>Definition text...</p>
</div>
```

The layout (`_layouts/chapter.html`) automatically adds:
- `<head>` with MathJax config and CSS
- Left nav with chapter list + section list (from front matter)
- Right sidebar (from `_includes/sidebars/chN.html`)
- Prev/next chapter navigation
- `nav.js` script

### Adding a New Chapter (Step by Step)

**Step 1:** Copy the template
```bash
cp docs/_chapter_template.html docs/ch6.html
```

**Step 2:** Fill in front matter
```yaml
---
layout: chapter
title: "Ch 6: Vietnamese Title"
chapter_num: 6
heading: "Chuong 6: Vietnamese Title"
heading_en: "English Title"
prev_url: /ch5.html
prev_title: "Chuong 5"
next_url: /ch7.html
next_title: "Chuong 7"
sections:
  - id: section-1-id
    title: "1. Section Title"
  - id: exercises
    title: "Bai tap"
---
```

**Step 3:** Write content using these CSS classes

| Class | Use for | Border |
|-------|---------|--------|
| `<div class="box definition">` | Dinh nghia | Green |
| `<div class="box theorem">` | Dinh ly, Menh de, He qua | Red |
| `<div class="box formula">` | Cong thuc quan trong | Gold |
| `<div class="box summary">` | Tom tat | Blue |
| `<div class="example">` | Vi du | Gray border |
| `<div class="exercise">` | Bai tap | Purple left border |
| `<div class="proof">` | Chung minh (auto prefix + QED) | None |

Each box should have: `<p class="box-title">Title</p>` as the first child.

Math: `\(...\)` for inline, `\[...\]` for display. MathJax macros available: `\PP`, `\E`, `\N`, `\Z`, `\R`, `\ind`.

**Step 4:** Create sidebar include
```bash
# Create docs/_includes/sidebars/ch6.html with key formulas and references
```

**Step 5:** Register the new chapter in 3 places

1. **`_includes/nav.html`** -- add a new `<li>` entry:
```html
<li><a href="{{ '/ch6.html' | relative_url }}" {% if page.chapter_num == 6 %}class="current"{% endif %}>Ch 6: Short Name</a></li>
```

2. **`_layouts/chapter.html`** -- add a case for the sidebar:
```liquid
{% when 6 %}{% include sidebars/ch6.html %}
```

3. **`index.html`** -- add a chapter card in the grid.

**Step 6:** Update prev/next links
- Update the **previous chapter's** `next_url` and `next_title` in its front matter.

### Local Development

```bash
cd docs/
gem install bundler
bundle install
bundle exec jekyll serve    # http://localhost:4000
```

### GitHub Pages Deployment

Automatic via GitHub Actions (`.github/workflows/pages.yml`).
Push to `main` branch -- Jekyll builds and deploys automatically.

### .tex to HTML Conversion Workflow

When converting a new `.tex` chapter to HTML:

1. Read the `.tex` file and identify all sections, environments, examples, exercises
2. Create the `.html` file with front matter
3. Convert environments using the mapping table (see top of this document)
4. Keep all LaTeX math as-is (MathJax renders it)
5. Replace `\term{X}` with `<strong>X</strong>`, `\en{X}` with `<em>(X)</em>`
6. Convert `$...$` to `\(...\)` for inline math
7. Convert `\begin{itemize}` to `<ul>`, `\begin{enumerate}` to `<ol>`
8. Convert `\begin{tabular}` to HTML `<table>`
9. Keep `\begin{align*}`, `\begin{equation}`, `\begin{bmatrix}` as-is for MathJax
