# CLAUDE.md - AI Assistant Context

## Project Overview

Bilingual Vietnamese-English Markov Chains study notes for PhD research at University of Debrecen.
Based on *Notes on Markov Chains* by Nicolas Privault (NTU, 2011).

Two output workflows:
1. **PDF** (primary): LaTeX source -> XeLaTeX -> `main.pdf` (~77 pages, 6 chapters)
2. **Web** (secondary): LaTeX source -> static HTML lessons in `docs/`

## File Structure

```
markov_chains_bilingual/
  main.tex                    # Master LaTeX file (XeLaTeX, Vietnamese via polyglossia)
  main.pdf                    # Compiled output
  chapters/
    ch0_intro.tex             # Ch 0: Introduction - Stochastic Processes & Random Walks
    ch4_discrete.tex          # Ch 1: Discrete-Time Markov Chains
    ch5_first_step.tex        # Ch 2: First Step Analysis
    ch6_classification.tex    # Ch 3: Classification of States
    ch7_limiting.tex          # Ch 4: Limiting and Stationary Distributions
    ch9_continuous.tex        # Ch 5: Continuous-Time Markov Chains
    appendix_prob.tex         # Appendix A: Probability Background
  docs/                        # Jekyll web book (3-column layout, MathJax)
    _data/chapters.yml        # Single source of truth for chapter order/titles/URLs
    _layouts/default.html     # Base layout (loads framework.css + book.css + MathJax)
    _layouts/chapter.html     # 3-column layout with auto prev/next from data
    _includes/
      nav.html                # Data-driven chapter navigation
      mathjax.html            # MathJax v3 config
      components/             # 6 reusable includes (box, example, exercise start/end)
      sidebars/               # Per-chapter sidebar content
    css/framework.css         # Reusable grid, box structure, nav (any book)
    css/book.css              # Literata font, sepia palette, box colors (this book)
    js/nav.js                 # TOC active state tracking
    index.html                # Landing page (standalone)
    intro.html, ch1-ch5.html, appendix.html  # Chapter pages (layout + slug + sections)
  MARKOV_PLAN.md              # Project plan with progress tracker
  WEB_PLAN.md                 # Web conversion strategy
  README.md                   # GitHub README
```

## Key Conventions

- **Commit prefixes**: `feat:`, `fix:`, `docs:`, `style:`, `refactor:`
- **No co-author lines** in commits
- Vietnamese is the primary language; English terms appear in `\en{}` (italic) and `\term{}` (bold)
- Custom tcolorbox environments: `tomtat` (blue), `dinhnghia` (green), `dinhly` (red), `congthuc` (yellow)
- Math macros: `\PP`, `\E`, `\N`, `\Z`, `\R`, `\ind`

## LaTeX Compilation

```bash
cd markov_chains_bilingual/
xelatex main.tex && xelatex main.tex  # 2 passes for TOC
```

## Web Details

- Jekyll framework with data-driven navigation (`_data/chapters.yml`)
- MathJax v3 for LaTeX math rendering
- 3-column layout: left TOC | center content | right sidebar
- CSS split: `framework.css` (reusable) + `book.css` (this book's theme)
- Global `--box-radius: 20px` CSS variable for all boxes
- 6 component includes: box-start/end, example-start/end, exercise-start/end
- Add new chapter: 1 YAML entry + 1 HTML file (nav/prev/next auto-update)
- GitHub Pages compatible
- See WEB_PLAN.md for .tex -> HTML mapping and component usage

## Chapter Mapping (Source -> Our Numbering)

| Our Ch | Source Ch | Topic |
|--------|----------|-------|
| 0 | Intro + Ch 3 | Introduction: Stochastic Processes & Random Walks |
| 1 | Ch 4 | Discrete-Time Markov Chains |
| 2 | Ch 5 | First Step Analysis |
| 3 | Ch 6 | Classification of States |
| 4 | Ch 7 | Limiting and Stationary Distributions |
| 5 | Ch 9 | Continuous-Time Markov Chains |
| A | Ch 1 | Probability Background |
