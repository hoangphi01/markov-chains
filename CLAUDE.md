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
    ch4_discrete.tex          # Ch 1: Discrete-Time Markov Chains
    ch5_first_step.tex        # Ch 2: First Step Analysis
    ch6_classification.tex    # Ch 3: Classification of States
    ch7_limiting.tex          # Ch 4: Limiting and Stationary Distributions
    ch9_continuous.tex        # Ch 5: Continuous-Time Markov Chains
    appendix_prob.tex         # Appendix A: Probability Background
  docs/                        # Static HTML lessons (3-column layout, MathJax)
    index.html                # Landing page
    ch1.html - ch5.html       # Chapter pages
    appendix.html             # Appendix page
    css/style.css             # Minimal grid layout
    js/nav.js                 # TOC active state tracking
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

- Pure static HTML/CSS/JS, no frameworks, no build step
- MathJax v3 for LaTeX math rendering
- 3-column layout: left TOC | center content | right sidebar (key symbols, quick refs)
- GitHub Pages compatible (no server-side code)
- See WEB_PLAN.md for .tex -> HTML mapping

## Chapter Mapping (Source -> Our Numbering)

| Our Ch | Source Ch | Topic |
|--------|----------|-------|
| 1 | Ch 4 | Discrete-Time Markov Chains |
| 2 | Ch 5 | First Step Analysis |
| 3 | Ch 6 | Classification of States |
| 4 | Ch 7 | Limiting and Stationary Distributions |
| 5 | Ch 9 | Continuous-Time Markov Chains |
| A | Ch 1 | Probability Background |
