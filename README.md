# Markov Chains - Bilingual Vietnamese-English Notes

Comprehensive bilingual (Vietnamese-English) lecture notes on Markov Chain theory, written in LaTeX with a pedagogical storytelling approach.

## Overview

These notes cover discrete-time and continuous-time Markov chains at the graduate level, based primarily on Nicolas Privault's *Notes on Markov Chains* (NTU, 2011). The text is written in Vietnamese with English terminology throughout, making it suitable for Vietnamese-speaking students studying probability theory in English-language programs.

**Target audience:** PhD/Master students in Mathematics, Statistics, or related fields.

## Features

- Bilingual format: Vietnamese explanations with English technical terms
- Pedagogical approach: real-world analogies and stories before formal definitions
- Color-coded theorem boxes (definitions, theorems, formulas, summaries)
- Extensive worked examples with full computation steps
- Exercises at the end of each chapter

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
├── main.tex                    # Master document
├── main.pdf                    # Compiled output
├── MARKOV_PLAN.md              # Detailed project plan & references
├── README.md                   # This file
└── chapters/
    ├── ch4_discrete.tex        # Discrete-time Markov chains
    ├── ch5_first_step.tex      # First step analysis
    ├── ch6_classification.tex  # Classification of states
    ├── ch7_limiting.tex        # Limiting & stationary distributions
    ├── ch9_continuous.tex      # Continuous-time Markov chains
    └── appendix_prob.tex       # Probability background
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
