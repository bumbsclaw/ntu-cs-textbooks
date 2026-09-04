# NTU BSc Computer Science — Complete Textbook Series (0→100)

> **37 textbooks · 1662 pages · 135 AU verified · 0→100 ground-up · color TikZ + highlighted code · small-screen optimized · exhaustive MPE catalogue**
>
> **Repo:** `bumbsclaw/ntu-cs-textbooks` — all PDF LaTeX, `pdflatex×2` verified 0 ! 0 >15.
> Tags: `v1.0` (25/25, 1128p) · `v1.1-exhaustive` (37/37, 1662p). Comprehensive QA: `REVIEW-COMPREHENSIVE.md` (37/37 PASS 2026-09-04).

## 135 AU Structure (verified 17+16+47+35+20=135)
- **Programme Core 47 AU (15 courses):** SC1004, SC1005, MH1812, SC1006, SC1007, SC1008, SC2000, SC2002, SC2001, SC2005, SC2203, SC2006, SC2008, SC2207, SC3099 — all 15 DONE ✓
- **College Core 16 AU:** SC1003, HW0288, SC3920 — covered in BDE & College/Core Guide
- **MPE 35 AU (9 courses, ≥4 SC4xxx) + exhaustive catalogue (21 MPEs):** SC3000, SC3010, SC3020, SC3050, SC3270, SC4001, SC4002, SC4012, SC4013, SC4021, SC4022, SC4023, SC4024, SC4040, SC4050, SC4051, SC4053, SC4055, SC4063, SC4064, SC4242 — all 21 DONE ✓ (covers every public SC3xxx/SC4xxx in `docs/curriculum-outline.md` §4)
- **BDE 20 AU + University Core 17 AU:** BDE Guide (32p) covers categories, double-count rules, sample plans

## Module Index (pages, lines, verification)
| Code | Title | AU | Pages | Lines | TikZ | QA |
|------|-------|----|-------|-------|------|----|
| SC1004 | Linear Algebra for Computing | 4 | 43 | 1637 | 23 | PASS |
| SC1005 | Digital Logic | 3 | 37 | 1619 | 48 | PASS |
| SC1006 | Computer Organisation & Architecture | 3 | 71 | 1893 | 43 | PASS |
| SC1007 | Data Structures & Algorithms | 3 | 37 | 1650 | 24 | PASS |
| SC1008 | C/C++ Programming | 3 | 43 | 1704 | 24 | PASS |
| MH1812 | Discrete Mathematics | 3 | 45 | 2078 | 24 | PASS |
| SC2000 | Probability & Statistics | 3 | 40 | 1673 | 20 | PASS |
| SC2001 | Algorithm Design & Analysis | 3 | 53 | 2070 | 44 | PASS v3 |
| SC2002 | Object-Oriented Design & Programming | 3 | 44 | 1654 | 28 | PASS |
| SC2005 | Operating Systems | 3 | 36 | 1629 | 24 | PASS |
| SC2006 | Software Engineering | 3 | 48 | 1616 | 26 | PASS |
| SC2203 | Automata, Computability & Complexity | 3 | 42 | 1620 | 25 | PASS |
| SC2008 | Computer Network | 3 | 50 | 1665 | 26 | PASS |
| SC2207 | Introduction to Databases | 3 | 45 | 1641 | 24 | PASS |
| SC3099 | Capstone Project | 4 | 46 | 1710 | 24 | PASS |
| SC3000 | Artificial Intelligence | 3 | 46 | 1762 | 20 | PASS |
| SC3010 | Computer Security | 3 | 51 | 1673 | 24 | PASS |
| SC3020 | Data Analytics & Mining | 3 | 48 | 1746 | 23 | PASS |
| SC3050 | Advanced Computer Architecture | 3 | 51 | 1647 | 24 | PASS |
| SC3270 | Reasoning About Programs | 3 | 44 | 1607 | 24 | PASS |
| SC4001 | Neural Networks & Deep Learning | 3 | 46 | 1621 | 22 | PASS |
| SC4002 | Natural Language Processing | 3 | 47 | 1964 | 24 | PASS |
| SC4012 | Software Security | 3 | 46 | 1649 | 26 | PASS |
| SC4013 | Application Security | 3 | 49 | 1624 | 24 | PASS |
| SC4021 | Information Retrieval | 3 | 45 | 1668 | 24 | PASS |
| SC4022 | Network Science | 3 | 42 | 1688 | 24 | PASS |
| SC4023 | AI for Software Engineering | 3 | 49 | 1623 | 20 | PASS |
| SC4024 | Data Visualisation | 3 | 41 | 1737 | 23 | PASS |
| SC4040 | Advanced Topics in Algorithms | 3 | 45 | 1725 | 25 | PASS |
| SC4050 | Parallel Computing | 3 | 42 | 1631 | 28 | PASS |
| SC4051 | Distributed Systems | 3 | 45 | 1707 | 25 | PASS |
| SC4053 | Blockchain Technology | 3 | 41 | 1636 | 24 | PASS |
| SC4055 | Introduction to Quantum Computing | 3 | 42 | 1633 | 26 | PASS |
| SC4063 | Network Security | 3 | 45 | 1707 | 25 | PASS |
| SC4064 | GPU Programming | 3 | 45 | 1632 | 24 | PASS |
| SC4242 | Compiler Techniques | 3 | 40 | 1677 | 25 | PASS |
| BDE | BDE & College/University Core Guide | 20 | 32 | 1063 | 14 | PASS |

**Total: 37 modules · 1662 pages · ~25M PDFs · all 0 ! 0 Overfull>15 0 pgfkeys**

## Build Invariants (all PASS)
- **0→100:** From zero (no bachelor's assumed), intuition → picture → formal, ground-up
- **Color TikZ where useful:** fills blue!15, green!20, orange!15, violet!10, yellow!12, legends
- **Code:** `lstlisting[language=Python/C/Java/SQL]` with colors, never `verbatim` for code
- **Small-screen:** geometry 1.3/1.2cm, `setstretch 1.20`, `parskip 0.70em`, TikZ scales 0.70-0.82
- **QA:** `pdflatex×2` → grep `!`, `pgfkeys`, `Overfull>15pt`, `hyperref Warning` — all 0

## Quick Start
```bash
git clone https://github.com/bumbsclaw/ntu-cs-textbooks
cd ntu-cs-textbooks
# Each module:
cd modules/SC2001 && pdflatex -interaction=nonstopmode main.tex && pdflatex -interaction=nonstopmode main.tex
# Or batch:
for m in modules/*/; do (cd "$m" && pdflatex -interaction=nonstopmode main.tex && pdflatex -interaction=nonstopmode main.tex); done
```

## Curriculum Sources
- CCDS official: ntu.edu.sg/computing, AY2024-25 study plan PDF, curriculum 135 AU table
- NTUMods 17 modules, Reddit r/NTU, HWZ — private drives excluded per policy
- Full outline: `docs/curriculum-outline.md` + adversarial review `docs/curriculum-outline-review.md`

## Resume Protocol
- `progress.md` is the only resume truth — first PENDING row is next. Branch `main`, remote `origin` bumbsclaw/ntu-cs-textbooks. PDFs tracked via `git add -f`.
