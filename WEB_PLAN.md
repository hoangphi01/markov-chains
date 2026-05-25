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
web/
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

## Jekyll Structure (for scaling)

```
web/
  _config.yml                 # Jekyll config, collections
  _layouts/
    default.html              # Base: <head>, MathJax, <body>
    chapter.html              # 3-column: nav + content + sidebar
  _includes/
    mathjax.html              # MathJax v3 config + macros
    nav.html                  # Shared chapter list (edit once, updates all pages)
    sidebars/
      default.html            # Fallback sidebar (key symbols)
      ch1.html - ch5.html     # Per-chapter sidebar content
      appendix.html           # Appendix sidebar
  _chapter_template.html      # Copy this to create new chapters
  Gemfile                     # Ruby dependencies
  .gitignore                  # Exclude _site/, .jekyll-cache/
  css/style.css               # Shared styles (same file)
  js/nav.js                   # Shared JS (same file)
  index.html                  # Landing page
  ch1.html - ch5.html         # Chapter pages (standalone or Jekyll)
  appendix.html               # Appendix page
```

### Adding a New Chapter

1. Copy `_chapter_template.html` to `chN.html`
2. Fill in front matter (title, sections, prev/next links)
3. Write content using CSS classes (definition, theorem, formula, etc.)
4. Create `_includes/sidebars/chN.html` for the right sidebar
5. Add entry in `_includes/nav.html`
6. Add case in `_layouts/chapter.html` for sidebar routing

### Local Development

```bash
cd web/
gem install bundler
bundle install
bundle exec jekyll serve    # http://localhost:4000
```

### Migrating Existing Chapters to Jekyll

To convert a standalone `chN.html` to use Jekyll layouts:

1. Add YAML front matter at top of file
2. Remove everything outside `<main class="content">...</main>` (layout handles it)
3. Remove the `<h1>` tag (layout generates it from front matter)
4. Remove `<div class="chapter-nav">` block (layout handles it)

The content between `<main>` tags stays exactly the same.

### GitHub Pages Deployment

Push to GitHub, enable Pages in repo settings. GitHub Pages has built-in Jekyll support -- no CI needed.
