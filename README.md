# Markov Chains - Bilingual Vietnamese-English Notes

Comprehensive bilingual (Vietnamese-English) lecture notes on Markov Chain theory, written in LaTeX with a pedagogical storytelling approach.

## Overview

These notes cover discrete-time and continuous-time Markov chains at the graduate level, based primarily on Nicolas Privault's *Notes on Markov Chains* (NTU, 2011). The text is written in Vietnamese with English terminology throughout, making it suitable for Vietnamese-speaking students studying probability theory in English-language programs.

**Target audience:** PhD/Master students in Mathematics, Statistics, or related fields.

## Read Online

Browse the lessons at: **https://hoangphi01.github.io/markov-chains/**

Static HTML pages with MathJax rendering -- no installation needed.

## Features

- Bilingual format: Vietnamese explanations with English technical terms
- Pedagogical approach: real-world analogies and stories before formal definitions
- Color-coded theorem boxes (definitions, theorems, formulas, summaries)
- Extensive worked examples with full computation steps
- Exercises at the end of each chapter
- Web version with 3-column layout (TOC, content, quick reference sidebar)

## Contents

| Chapter | Topic | Pages |
|---------|-------|-------|
| 1 | Discrete-Time Markov Chains | ~12 |
| 2 | First Step Analysis | ~18 |
| 3 | Classification of States | ~12 |
| 4 | Limiting and Stationary Distributions | ~16 |
| 5 | Continuous-Time Markov Chains | ~26 |
| A | Probability Background (Appendix) | ~10 |

**Key topics:** Markov property, transition matrices, Chapman-Kolmogorov equation, gambler's ruin, hitting probabilities, recurrence/transience, Polya's theorem, ergodicity, stationary distributions, detailed balance, convergence rates, Poisson processes, birth-death processes, infinitesimal generators, absorption probabilities, M/M/1 queues.

## Compilation

Requires **XeLaTeX** (for Vietnamese Unicode support via `fontspec` + `polyglossia`).

```bash
cd markov_chains_bilingual/
xelatex main.tex && xelatex main.tex
```

Or upload to [Overleaf](https://www.overleaf.com) and set compiler to XeLaTeX.

### Dependencies

- `fontspec`, `polyglossia` (Vietnamese language support)
- `amsmath`, `amssymb`, `amsthm`, `mathtools`
- `tcolorbox` with `theorems`, `breakable`, `skins` libraries
- `enumitem`, `hyperref`, `bookmark`, `xcolor`

## Project Structure

```
markov_chains_bilingual/
├── main.tex                    # Master LaTeX document
├── main.pdf                    # Compiled PDF (~77 pages)
├── chapters/                   # LaTeX source chapters
│   ├── ch4_discrete.tex
│   ├── ch5_first_step.tex
│   ├── ch6_classification.tex
│   ├── ch7_limiting.tex
│   ├── ch9_continuous.tex
│   └── appendix_prob.tex
├── docs/                       # Web lessons (GitHub Pages)
│   ├── index.html              # Landing page
│   ├── ch1.html - ch5.html     # Chapter pages
│   ├── appendix.html           # Probability background
│   ├── css/style.css           # 3-column layout
│   ├── js/nav.js               # TOC navigation
│   ├── _layouts/               # Jekyll layouts (for scaling)
│   ├── _includes/              # Shared components (nav, sidebars)
│   └── _chapter_template.html  # Template for new chapters
├── CLAUDE.md                   # AI assistant context
├── MARKOV_PLAN.md              # Project plan & references
├── WEB_PLAN.md                 # Web conversion strategy
└── README.md                   # This file
```

## References

**Primary source:**
- Privault, N. (2011). *Notes on Markov Chains*. MAS328, Nanyang Technological University.

**Complementary references:**
- Norris, J.R. (1997). *Markov Chains*. Cambridge University Press.
- Ross, S.M. (2019). *Introduction to Probability Models* (12th ed.). Academic Press.
- Grimmett, G. & Stirzaker, D. (2020). *Probability and Random Processes* (4th ed.). Oxford.

## License

These notes are for educational purposes. The mathematical content is based on standard textbook material. Please cite the original sources if using in academic work.

## Author

Compiled for PhD research at University of Debrecen (Debreceni Egyetem), Hungary.
