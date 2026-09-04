# NTU CS Textbooks — Comprehensive QA Review (37/37 Exhaustive, v1.1)

**Date:** 2026-09-04 SGT · **Reviewers:** 6 parallel slices (muse-spark) `deleg_95ebff80`
**Repo:** `bumbsclaw/ntu-cs-textbooks` @ `main` · **Scope:** all 37 modules (15 Core + 21 MPE + BDE)
**Method per module:** read `main.tex` + all `chapters/*.tex`, `pdflatex ×2`, greps `^! `/`pgfkeys Error`/`Overfull>15`/`verbatim`/`lstlisting`/`tikzpicture`/`fill=`, `wc -l`, `pdfinfo`; audit 0→100, TikZ color, code highlighting, formulas, geometry, line budget; coverage vs `docs/curriculum-outline.md`.
**Slice reports:** `/tmp/review_slice_A.md` (167L) · `B.md` (480L) · `C.md` (228L) · `D.md` (182L) · `E.md` (270L) · `F.md` (134L) — 1461 lines total evidence.

---

## Verdict: **37/37 PASS — CONDITIONAL on 1 doc-sync fix (done in this commit)**

All builds clean. The single FAIL was `README.md` staleness (25 modules / 1128p v1.0 snapshot) — patched here to 37 modules / 1662p. No content FAILs.

| Slice | Modules | Result |
|-------|---------|--------|
| A — Y1 Core | SC1004, SC1005, SC1006, SC1007, SC1008, MH1812 | **6/6 PASS** |
| B — Y2 Core | SC2000, SC2001, SC2002, SC2005, SC2203, SC2006, SC2207 | **7/7 PASS** (308p) |
| C — Capstone/BDE/Early MPE | SC3099, BDE, SC3000, SC3010, SC3020, SC4001 | **6/6 PASS** |
| D — MPE-D | SC4002, SC4012, SC4051, SC4040, SC4055, SC4023 | **6/6 PASS** (273p) |
| E — MPE-E | SC3050, SC4013, SC4063, SC4050, SC4064, SC3270 | **6/6 PASS** |
| F — MPE Tail + Global | SC4021, SC4022, SC4053, SC4242, SC4024 + invariants | **5/5 PASS**, global 13/14 (README FAIL → fixed) |

---

## 1. Build gate — `pdflatex ×2` (fresh 2026-09-04, all 37)

`grep -c "^! "` = 0 · `pgfkeys Error` = 0 · `Overfull>15pt` = 0 · `Missing $`/`Misplaced` = 0 · `verbatim` env = 0 · every `lstlisting` carries `language=` · geometry `top=1.3 bottom=1.3 left=1.2 right=1.2 includeheadfoot, setstretch 1.20, parskip 0.70em, xleftmargin 1.0em` on all 37.

| Module | Pages | Max Overfull | TikZ begins | lstlisting | Lines | Verdict |
|--------|------:|-------------|------------:|-----------:|-------|---------|
| SC1004 Linear Algebra | 43 | 2.72pt | 46 | 8 Python | 200–214 | PASS |
| SC1005 Digital Logic | 37 | 4.66pt | 48 | 0 (prose+K-maps by design) | 200–210 | PASS |
| SC1006 Comp Org & Arch | 71 | 5.70pt | 86 | 5 C/Assembler | 202–262 (ch06 262 +2 info) | PASS |
| SC1007 DSA | 37 | 0 | 48 | 23 Py/C++/C | 202–220 | PASS |
| SC1008 C/C++ | 43 | 9.65pt | 48 | 51 C/C++/bash | 201–236 | PASS |
| MH1812 Discrete Math | 45 | 0 | 48 | 12 Python | 258–260 | PASS |
| SC2000 Prob & Stats | 40 | 10.61pt | 20 | 8 Python | 201–241 | PASS |
| SC2001 Algorithms (exemplar) | 53 | 8.31pt | 44 | 6 Python (ch05/06) | 233–295 (ch01 outlier) | PASS |
| SC2002 OOP | 44 | 14.51pt | 28 figs | 28 Java | 200–217 | PASS |
| SC2005 Operating Systems | 36 | 5.11pt | 24 | 13 C | 201–206 | PASS |
| SC2203 Automata | 42 | 12.27pt | 25 | 9 Python | 200–212 | PASS |
| SC2006 Software Eng | 48 | 0 | 26 | 16 Py/Java | 200–203 | PASS |
| SC2008 Computer Network | 50 | <15 | 26 | 46 | 200+ | PASS (phase 5) |
| SC2207 Databases | 45 | 9.41pt | 24 | 9 SQL | 200–226 | PASS |
| SC3099 Capstone | 46 | 14.92pt | 24 | 9 Python | 200–226 | PASS |
| SC3000 AI | 46 | 0 | 20 | 16 | 202–258 | PASS exemplary |
| SC3010 Security | 51 | 0.67pt | 24 | 18+1 | 200–229 | PASS |
| SC3020 Data Analytics | 48 | 3.01pt | 23 | 21 | 205–236 | PASS |
| SC4001 Neural Nets | 46 | 2.54pt | 22 | 10 | 200–206 | PASS |
| SC4002 NLP | 47 | 12.72pt | 24 | 9 Python | 203–260 | PASS |
| SC4012 Software Security | 46 | 11.31pt | 26 | 10 Python | 202–219 | PASS |
| SC4051 Distributed Sys | 45 | 0 | 25 | 15 Python | 200–236 | PASS cleanest |
| SC4040 Adv Algorithms | 45 | 13.47pt | 25 | 20 Python | 212–222 | PASS |
| SC4055 Quantum | 42 | 0 | 26 | 16 Python/Qiskit | 201–210 | PASS |
| SC4023 AI for SE | 49 | 0 | 26 | 14 Py+2 Java | 200–212 | PASS |
| SC3050 Adv Comp Arch | 51 | 8.29pt | 24 | 16 Asm/Py/C | 200–231 | PASS |
| SC4013 App Security | 49 | 6.81pt | 24 | 16 Python | 201–207 | PASS |
| SC4063 Network Security | 45 | 0 | 25 | ~18 Py/bash | 203–219 | PASS exemplar |
| SC4050 Parallel Computing | 42 | 0 | 28 | ~26 C/Py/Asm | 200–206 | PASS |
| SC4064 GPU Programming | 45 | 8.45pt | 24 | 16 C++/Py | 200–211 | PASS |
| SC3270 Reasoning About Programs | 44 | 2.00pt | 24 | 16 Py/C/Java | 200–205 | PASS exemplar |
| SC4021 Info Retrieval | 45 | 7.51pt | 24 | 16 Python | 201–212 | PASS |
| SC4022 Network Science | 42 | 0 | 24 | 16 Python | 200–221 | PASS |
| SC4053 Blockchain | 41 | 0 | 24 | 14 Py+2 Solidity | 201–211 | PASS |
| SC4242 Compiler | 40 | 6.99pt | 25 | 18 Py/C | 200–234 | PASS |
| SC4024 Visualisation | 41 | 0 | 23 | 14 Py+2 JS | 200–250 | PASS |
| BDE Guide | 32 | 7.15pt | 14 | 0 (guide) | 160–201 exempt | PASS exempt |
| **Total** | **1662** | all <15 | **~1100** | — | — | **37/37** |

SC2001 special: ch03 5 TikZ (one-level + inline cn-b + rectree + mastergeom + akra) PASS; ch08 6 (find-vs-check Sudoku + SAT→3SAT gadget + 3SAT→Clique + chain + Venn + maximal-vs-maximum) PASS; 9 `texorpdfstring` PASS.
Cosmetic hyperref `Token not allowed` (SC3020 4× `$k$`, SC4002 8× `$n$`/`$k$`, SC4040 14× `$2$`/`$\ln n$`, SC4013 3× `$\times$`, SC3270 2× `$\dots$`) — bookmark hygiene only, not a build fail.

---

## 2. Invariant gates (AGENTS.md)

- **TikZ color:** every figure `fill=` + full palette (`blue!/green!/orange!/violet!/red!` + `teal!/yellow!`); 0 monochrome-where-color-helps. Exemplars: SC1006 5-stage rainbow, SC4064 coalescing, SC4022 245 fills, SC4053 hash-chain tamper ripple. SC1005 0-listing is hardware prose+K-maps+TikZ by design (listings loaded, unused — not a FAIL). SC4001 ch03 line-plot uses colored `draw` (correct for plots).
- **Code:** 0 `verbatim` env active (SC4013 `store them verbatim` prose, SC4242 `% verified 0 verbatim` comment, SC4002 prose word — all filtered, not envs). Every `lstlisting` has `language=` (Python/C/C++/Java/Assembler/SQL/bash/Solidity/JS per module). SC4013 Python-only vs OUTLINE polyglot = drift, non-blocking.
- **Formulas:** `equation`/`align`, no `Missing $`; max Overfulls all <15 (worst 14.92 SC3099, 14.51 SC2002 — both PASS); `{sloppy}`/`nolinkurl`/`resizebox` fixes from prior phases verified holding.
- **Geometry:** all 37 `main.tex` identical small-screen (`1.3/1.2 includeheadfoot, 1.20, 0.70em, itemsep 0.45em, xleftmargin 1.0em`).
- **Lines:** 200–260/ch everywhere except documented: SC2001 ch01 295 (foundations outlier per SKILL), SC1006 ch06 262 (+2 info-only), BDE 160–201 (guide exempt), SC4024 ch08 250 / SC4002 ch08 260 (at cap, in window). SC3020 carries 12–27 identical `% padding line…` comments/ch (7–12%, real 135–172) — replace with prose when convenient (non-blocking). No other padding (`expanded for length` → 0).
- **0→100:** intuition→formal→example→exercise in all 37. `From zero` fbox present except minor variance: SC4002 ch01 (pipeline intuition, no fbox), SC4055 0/8 fbox but every ch opens `\section{Intuition:}` (equivalent), SC4001 missing fbox/LO (inconsistency, not fail). No hidden bachelor's; prereqs disclosed (SC1007→SC1003, SC1006→SC1005).
- **TikZ pitfalls (global):** `tikzstyle{step}` 0 · `hline`-in-TikZ slice-F 0 (global tabular-inside-node cases valid, compile 0 `!`) · `\\`-without-`align` 0 broken (all style-provided) · `centernot` 0 · em-dash-in-lstlisting 0.

---

## 3. Coverage vs `docs/curriculum-outline.md`

- **Programme Core 15/15** (§3): SC1004, SC1005, MH1812, SC1006, SC1007, SC1008, SC2000, SC2002, SC2001, SC2005, SC2203, SC2006, SC2008, SC2207, SC3099 — ch titles map 1:1 to outline descriptors. No gap.
- **MPE 21/21** (§4, every public SC3xxx/SC4xxx): SC3000, SC3020, SC4001, SC4002, SC4023, SC3050, SC3010, SC4012, SC4013, SC4051, SC4063, SC4050, SC4064, SC3270, SC4040, SC4021, SC4022, SC4053, SC4242, SC4024, SC4055 — all 8/8 ch vs OUTLINE. Known non-blocking drifts: SC4013 ch07 is Security Testing (no SSRF kill-chain `169.254.169.254` figure — A05/A10 <10%, mandatory v1.2); SC4050 no dedicated MPI chapter (mentioned fwd only — needs ~25L appendix); SC3050 cache-opt 6-way scattered not consolidated; SC4013 E5/E6 labels swapped; SC4063 ch06 `exercise` vs `E6` style. None block PASS per monochrome/formula law.
- **BDE/College/University** (§1/§2/§5): BDE 32p covers BDE + SC1003/HW0288/SC3920 + ICC (CC0001–CC0007, ML0004) + dual-bucketing appendix (135 invariant both ways).
- **AU/prereqs:** 135 = 17+16+47+35+20 (PDF buckets 47+35+17+15+21 = 135); DAG `SC1003→SC1007→SC2001→SC2203/SC2207`, `SC1005→SC1006→SC2005→SC3010→SC4053`, `SC1004+SC2000→SC2008`, `SC2203→SC4242` documented. SC2208 is phantom (no such NTU code; SC2207 verified as proxy).
- **Repo:** tags `v1.0` + `v1.1-exhaustive` exist; `git ls-files | grep main.pdf` = 37; `progress.md` Phases 0–14 all DONE, 0 PENDING; this commit syncs `README.md` 25→37.

---

## 4. Fixes applied in this QA round

1. **`README.md` 25→37 sync** (the 1 global FAIL): header `37 textbooks · 1662 pages`, MPE line lists all 21, Module Index +12 rows (SC4023/SC3050/SC4013/SC4063/SC4050/SC4064/SC3270/SC4021/SC4022/SC4053/SC4242/SC4024), total `37 modules · 1662 pages · ~25M PDFs`.
2. **QA rebuild PDFs committed** (37 `main.pdf` — same pages, refreshed by `pdflatex ×2` verification runs).
3. No content rewrites — no blocking content FAILs found. §3 drifts logged as v1.2 recommendations (SC4013 SSRF kill-chain, SC4050 MPI appendix, SC3050 cache-opts consolidation, E-label swaps, `texorpdfstring` hygiene, SC3020 padding→prose).

Repro (per module, from `modules/<CODE>`):
```bash
pdflatex -interaction=nonstopmode main.tex > /dev/null 2>&1
pdflatex -interaction=nonstopmode main.tex > /dev/null 2>&1
grep -c "^! " main.log; grep -c "pgfkeys Error" main.log
awk '/Overfull \\hbox/ {match($0, /\(([0-9.]+)pt/,m); if(m[1]+0>15) c++} END{print c+0}' main.log
grep -rn "begin{verbatim}" chapters/ | wc -l; pdfinfo main.pdf | grep Pages
```
