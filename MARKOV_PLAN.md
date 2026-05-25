# Markov Chains - Bilingual LaTeX Project

## Status: v2.0 (2026-05-25) - Major Expansion & Pedagogical Rewrite

Bilingual Vietnamese-English rewrite of core Markov chain theory for PhD study at University of Debrecen.

**Output:** `main.pdf` (~90-100 pages target, compiled with XeLaTeX)

**v2.0 Changes:**
- Expanded from ~54 pages to ~90-100 pages
- Pedagogical rewrite: storytelling, analogies, real-world examples BEFORE formulas
- Ch 9: Major expansion (+14-18 pages) — absorption probabilities, mean absorption times, M/M/1 queue
- Ch 4: Added intuitive openers, random walk proof, Ehrenfest N=4, rate of convergence
- Ch 7: Added detailed balance condition, convergence rate theorem
- Ch 6: Added Polya's theorem, better analogies, more exercises
- Ch 5: Added full Gambler's Ruin solution (algebraic)
- Appendix: Added generating functions, Markov/Chebyshev inequalities, joint distributions

---

## Primary Source

| Field | Detail |
|-------|--------|
| **Book** | *Notes on Markov Chains* |
| **Author** | Nicolas Privault |
| **Institution** | Nanyang Technological University (MAS328) |
| **Year** | 2011 |
| **PDF** | `Nicolas Privault-Notes on Markov chains_2011.pdf` |
| **Total pages** | 285 |
| **Chapters covered** | Ch 1 (appendix), Ch 4-7, Ch 9 |

---

## Complementary & Reference Books

### Discrete-Time Markov Chains (Ch 4-7)
| Book | Author(s) | Notes |
|------|-----------|-------|
| *Introduction to Probability Models* (12th ed.) | Sheldon M. Ross | Ch 4: excellent examples, queueing applications |
| *Probability and Random Processes* (4th ed.) | Grimmett & Stirzaker | Ch 6: rigorous treatment with good exercises |
| *Introduction to Stochastic Processes* (2nd ed.) | Gregory F. Lawler | Concise, PhD-level, discrete chains focus |
| *Markov Chains* (Cambridge) | J.R. Norris | The standard graduate reference; complete proofs |
| *Finite Markov Chains and Algorithmic Applications* | Olle Haggstrom | Short, algorithmic perspective, mixing times |

### Continuous-Time Markov Chains (Ch 9)
| Book | Author(s) | Notes |
|------|-----------|-------|
| *Markov Chains* | J.R. Norris | Ch 2-3: continuous-time, birth-death, generators |
| *Stochastic Processes* (2nd ed.) | Sheldon M. Ross | Ch 5-6: Poisson process, continuous-time chains |
| *An Introduction to Stochastic Modeling* (4th ed.) | Pinsky & Karlin | Ch 4-5: birth-death, queueing, good for applications |
| *Continuous-Time Markov Chains and Applications* | Yin & Zhu | Advanced; regime-switching, two-time-scale models |

### Probability Background (Appendix)
| Book | Author(s) | Notes |
|------|-----------|-------|
| *A First Course in Probability* (10th ed.) | Sheldon M. Ross | Undergraduate review; conditional expectation |
| *Probability and Measure* (3rd ed.) | Patrick Billingsley | Rigorous measure-theoretic foundation |
| *Understanding Markov Chains: Examples and Applications* | Nicolas Privault | Companion to our primary source; more examples |

### Simulation & Applied Markov Chains
| Book | Author(s) | Notes |
|------|-----------|-------|
| *Simulation Modeling and Analysis* (6th ed.) | Averill M. Law | Available locally; simulation of stochastic systems |
| *Monte Carlo Statistical Methods* (2nd ed.) | Robert & Casella | MCMC, Metropolis-Hastings, Gibbs sampling |
| *Markov Chain Monte Carlo in Practice* | Gilks, Richardson & Spiegelhalter | Applied MCMC with real examples |

---

## Project Structure

```
markov_chains_bilingual/
  main.tex                      # Master file, preamble, XeLaTeX Vietnamese support
  main.pdf                      # Compiled output
  MARKOV_PLAN.md                # This file
  README.md                     # GitHub README
  chapters/
    ch4_discrete.tex            # Ch 1: Chuoi Markov thoi gian roi rac
    ch5_first_step.tex          # Ch 2: Phan tich buoc dau tien
    ch6_classification.tex      # Ch 3: Phan loai trang thai
    ch7_limiting.tex            # Ch 4: Phan phoi gioi han va dung
    ch9_continuous.tex          # Ch 5: Chuoi Markov thoi gian lien tuc
    appendix_prob.tex           # App A: Nen tang xac suat
```

---

## Chapter Map (Source -> Bilingual)

| Bilingual Ch | Source Ch | Vietnamese Title | English Title | Est. Pages |
|-------------|-----------|-----------------|---------------|-------|
| 1 | Ch 4 (pp 63-77) | Chuoi Markov thoi gian roi rac | Discrete-Time Markov Chains | 10-12 |
| 2 | Ch 5 (pp 79-97) | Phan tich buoc dau tien | First Step Analysis | 16-18 |
| 3 | Ch 6 (pp 99-109) | Phan loai trang thai | Classification of States | 10-12 |
| 4 | Ch 7 (pp 111-121) | Phan phoi gioi han va dung | Limiting and Stationary Distributions | 14-16 |
| 5 | Ch 9 (pp 141-183) | Chuoi Markov thoi gian lien tuc | Continuous-Time Markov Chains | 22-26 |
| A | Ch 1 (pp 9-33) | Nen tang xac suat | Probability Background | 8-10 |

---

## Key Topics Covered

### Discrete-Time (Ch 1-4)
- Markov property, transition matrices, Chapman-Kolmogorov
- Two-state chain: diagonalization, P^n, limiting distribution, convergence rate
- First step analysis: hitting probabilities, mean hitting/absorption times
- **Gambler's Ruin: full algebraic solution** (NEW in v2.0)
- First return times, number of returns, geometric distribution of visits
- Communicating classes, irreducibility, recurrence vs transience
- **Polya's recurrence theorem** (NEW in v2.0)
- Positive/null recurrence, periodicity, ergodicity
- Limiting distributions, stationary distributions (pi = piP)
- **Detailed balance condition, reversibility** (NEW in v2.0)
- **Convergence rate: spectral gap, |lambda_2|^n** (NEW in v2.0)
- Convergence theorem: irreducible + aperiodic + positive recurrent

### Continuous-Time (Ch 5)
- Poisson process: independent/stationary increments, intensity lambda
- Birth and death processes: birth/death rates, exponential sojourn times
- Continuous-time Markov property, transition semigroup P(t)
- Infinitesimal generator Q, Kolmogorov forward/backward equations
- Matrix exponential P(t) = e^{tQ}
- Two-state continuous chain: explicit solution, comparison with discrete
- Stationary distribution: piQ = 0 (vs piP = pi in discrete)
- **M/M/1 queue example** (NEW in v2.0)
- Embedded chain: discretization of continuous process, 5-state example
- **Absorption probabilities: explicit formula with rho^i** (NEW in v2.0)
- **Mean absorption times: sojourn time analysis** (NEW in v2.0)
- **Relation between continuous and embedded stationary distributions** (NEW in v2.0)

### Probability Background (Appendix A)
- Probability spaces, sigma-algebras, conditional probability
- Random variables, distributions (Bernoulli, Binomial, Poisson, Exponential, Gaussian)
- Key property: min of independent exponentials, competing exponentials
- Expectation, variance, conditional expectation, tower property
- **Probability generating functions** (NEW in v2.0)
- **Markov and Chebyshev inequalities** (NEW in v2.0)
- **Joint distributions and conditional density** (NEW in v2.0)

---

## Pedagogical Approach (v2.0)

Each section follows this structure:
1. **Story/real-world analogy** — 2-3 sentences to build intuition
2. **Key idea** — in `tomtat` box, plain Vietnamese
3. **Formal definition** — in `dinhnghia` box
4. **Formulas** — in `congthuc` box
5. **Worked example** — step by step
6. **Summary** — what to remember

Storytelling patterns used:
- **Markov property** → Con kiến trên bàn cờ (ant on chessboard)
- **Transition matrix** → Bản đồ xác suất (probability map between cities)
- **Recurrent vs Transient** → Quán café quen vs quán ghé qua
- **Stationary distribution** → Dân số ổn định (stable population after migration)
- **Poisson process** → Xe buýt đến trạm (bus arrivals at stop)
- **Generator matrix Q** → "Tốc độ" thay vì "xác suất"
- **Birth-death process** → Số khách trong quán café

---

## Bilingual Format Conventions

- **Vietnamese** primary text with full diacritics
- **English** terms in `\en{}` (italic) and `\term{}` (bold Vietnamese)
- Custom tcolorbox environments:
  - `tomtat` (blue): summary boxes
  - `dinhnghia` (green): definitions
  - `dinhly` (red): theorems
  - `congthuc` (yellow): key formulas
- Standard theorem environments: `theorem`, `proposition`, `corollary`, `definition`, `example`, `exercise`
- Math commands: `\PP`, `\E`, `\N`, `\Z`, `\R`, `\ind`

---

## Compilation

Requires XeLaTeX (for Vietnamese Unicode support).

```bash
cd markov_chains_bilingual/
xelatex main.tex && xelatex main.tex  # 2 passes for TOC/cross-refs
```

Or upload to [Overleaf](https://www.overleaf.com) and set compiler to XeLaTeX.
