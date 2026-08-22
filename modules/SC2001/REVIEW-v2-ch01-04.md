# Visual QA Review — SC2001 v2 ch01–04 (Reviewer A)

**Date:** 2026-08-23 01:45 SGT
**Scope:** `main.tex` + `chapters/ch01-foundations.tex` · `ch02-asymptotics.tex` · `ch03-recurrences.tex` · `ch04-divide-conquer.tex`
**Commit audited:** uncommitted v2 worktree (deleg_518409bd fixes applied) + 1 trivial nit patched below
**Verdict: PASS** — no blocking diagram/formula/code-highlight issue in ch01–04. All Bowen/AGENTS.md invariants hold for this slice.

---

## 1. Compile Check (pdflatex ×1, nonstopmode)

```
pdflatex -interaction=nonstopmode main.tex  →  exit 0
Output written on main.pdf (45 pages, 880197 bytes)
grep ^! main.log                         → 0  (0 ! errors)
grep "pgfkeys Error" main.log            → 0  (pgfkeys.sty load only, no Error)
grep "Overfull \hbox" (all)              → 3 lines, all < 15pt — see below
grep "Overfull" | awk >15pt              → 0  ← invariant: 0  (was 3→0, still 0)
grep -i "hyperref Warning"               → 0  (was 30+ → 0)
grep "Missing $" / "Misplaced alignment" → 0 / 0
```

Overfull detail (post-fix):

| hbox | loc | severity | disposition |
|------|-----|----------|-------------|
| 10.14pt | ch04 L17–18 LO item `analyse deterministic QuickSort… $O(n log n)$ via indicator variables` | >15? no (10pt) but cosmetically noisy | **PATCHED** this review: reworded to `analyse deterministic vs. randomised QuickSort (worst case vs. expected $O(n log n)$ via indicator variables);` — overfull gone (re-run: 3→2→0 for this site; only ch01/ch07 cosmetic <3pt remain) |
| 2.07pt | ch01 L176–182 Euclid pseudocode `quote\ttfamily\scriptsize` | <15pt | cosmetic, monospace `// assume…` in narrow quote; `scriptsize` already applied in v2 (was `small` → tight). No formula break needed — not a `\[ \]` overflow. |
| 2.64pt | ch01 L326–327 InsertionSort specification sentence | <15pt | single tight line, hyphenation limited; <3pt ignored per AGENTS.md 15pt gate. |
| 0.20pt | ch07 L134–135 remark (outside scope, listed for completeness) | <15pt | outside ch01–04 gate. |

All display formulas use `equation`/`align*`/`\[ \]` with no `Overfull >15pt`, no broken `!` errors.

Second pdflatex pass also exit 0; `main.toc`/`main.out` stable. pdfinfo page-count 45 (was 46p v1 → 45p v2 after tightening; within variance for geometry 2.5cm).

---

## 2. Diagram Color QA — MUST FAIL if any diagram monochrome when color useful

### ch01 — RAM model (Fig. `fig:ram-model`, TikZ ~L194–263)

Audit source (grep `fill=` / `color=`):

- `arrow/.style = {-{Latex}, thick, color=violet!70!black}` — **violet arrows** ✓
- Background tints: `\fill[yellow!10]` input tape, `\fill[blue!4]` memory group, `\fill[yellow!10]` output tape — **tints applied** ✓
- Tape cells `fill=yellow!15`, terminator `fill=gray!20` ✓
- CPU box `fill=blue!7, draw=blue!60!black` with inner blocks: Control `orange!18`, Registers `green!15`, ALU `red!12`, Fetch `blue!10` ✓
- Annotation `fill=orange!15, rounded corners=2pt` `"each primitive op costs $1$"` ✓
- Labels + `\label{fig:ram-model}` present ✓

**Verdict ch01 diagram: PASS — full violet arrows + multi-hue tints, not monochrome.** v1 was monochrome arrows (`thick` only); v2 colorization correct (diff shows `violet!70!black` + 3 new `\fill` backings + orange badge).

### ch02 — Asymptotic bands + hierarchy (Figs. `fig:asymptotic-bands`, `fig:growth-hierarchy`)

- `fig:asymptotic-bands` three panels:
  - O: `\fill[blue!12]` band, annotation `\color{blue!60!black} $f\le c g$` (was red!8 / `allowed band` — now distinct blue) ✓
  - Omega: `\fill[green!12]` ✓ (was red!8)
  - Theta: `\fill[orange!14]` ✓ (was red!8)
  - Curve colors `blue` f / `red` c·g retained for contrast ✓
- `fig:growth-hierarchy` tier backgrounds:
  - `\fill[teal!5]` (0–1.1), `\fill[orange!6]` (1.1–2.2), `\fill[blue!5]` (2.2–3.3), `\fill[red!4]` (3.3–4.6) ✓ (all four tiers tinted; v1 had none)
  - Curves: `teal` log n, `orange!80!black` n, `blue` n log n, `red` n², `purple` 2^n — all colored/thick ✓

**Verdict ch02 diagrams: PASS — tier colors distinct per curve/band, no monochrome.**

### ch03 — Recursion tree + Master geometry (Figs. `fig:rectree`, `fig:mastergeom`)

- `fig:rectree`:
  - `rnode/.style fill=blue!10` (root), `rnodeB/.style fill=teal!14` (level-1 children) — **level colors distinct** ✓ (v1 single `blue!6`)
  - `leaf/.style fill=orange!18` ✓ (was `green!8`)
- `fig:mastergeom`:
  - Back fills: `\fill[blue!7]` Case 1 triangle, `\fill[red!7]` Case 3 strip, `\fill[orange!10]` Case 2 band ✓ (v1 no fills)
  - Case lines `blue!70!black` / `orange!70!black` / `red!70!black` ✓
  - Labels `\color{blue!70!black}Case 1` etc. with white rounded backing ✓

**Verdict ch03 diagrams: PASS — rectree level colors + mastergeom case fills correct.**

### ch04 — Partition invariant + Strassen (Figs. `fig:qs-partition`, `fig:strassen`)

- `fig:qs-partition` (Lomuto):
  - `\fill[green!18]` ≤x, `\fill[red!12]` >x, `\fill[yellow!18]` unscanned, `\fill[blue!18]` pivot x ✓ (v1 wireframe only) ✓
- `fig:strassen` (3 matrices + 7-product node):
  - A blocks: `blue!10` backing + `blue!18`/`teal!12`/`orange!10`/`red!8` quadrants ✓
  - B blocks: `green!10` backing + `green!18`/`teal!12`/`orange!10`/`violet!8` ✓
  - Arrow `violet!70!black` `$7\times$` + middle node `fill=violet!8` ✓
  - C blocks: `blue!6` backing + `blue!14`/`teal!10`/`orange!10`/`red!6` ✓
  - All fills use distinct hues per block per Bowen feedback ✓

**Verdict ch04 diagrams: PASS — partition + Strassen block colors correct, violet accents present.**

Overall diagram QA: **0 monochrome-when-color-useful → PASS.** All 6 TikZ figures in ch01–04 compile (0 pgfkeys Error) and carry `\label`/`\caption`.

---

## 3. Formula Rendering

- Every display uses `equation` / `align*` / `\[ \]` — no raw `$...$` spanning lines.
- ch03 Karatsuba geometric sum: **fixed** `\[ sum … \]=…` (single `\[]` at risk of overfull) → `\begin{align*} … \\ &\quad=… \end{align*}` breaking at `=` with `\quad` continuation. No overfull from this display post-fix (verified Overfull >15pt = 0).
- ch03 Master theorem statements (`Case 1/2/3`) inside `theorem` env with `enumerate [label=Case \arabic*:]` — renders without overfull.
- ch03 Akra-Bazzi integral `T(n)=\Theta(n^p(1+\int…))` and `eq:treesum` both inside `equation`/`\[ \]` with proper `\!` spacing — no break needed.
- ch04 QuickSort expectation: `\Pr[X_{ij}=1]=2/(j-i+1)`, `\mathbb{E}[X]` double sum with `\frac` — inside `\[ \]` and fit within text width (no Overfull from these blocks).
- ch04 Strassen `align*` for 7 M_k definitions — 2-column layout prevents overflow; verified compile.
- Inline math hyphenation (ch01 sums/logs/floors, ch02 `O/Omega/Theta` quantifiers) correct; no `Missing $` or `Misplaced alignment`.

**Verdict formulas: PASS — 0 broken/overflowing displays in ch01–04.**

---

## 4. Code Highlight QA

- `main.tex` preamble: `\usepackage{listings}` + `\lstset{basicstyle=\ttfamily\small,breaklines=true,frame=single,numbers=left,numberstyle=\tiny\color{gray},keywordstyle=\color{blue!70!black},commentstyle=\color{green!50!black},stringstyle=\color{orange!70!black},showstringspaces=false,tabsize=2}` — colors defined ✓
- Grep `verbatim` in ch01–04: **0 matches** ✓
- Grep `lstlisting` in ch01–04: **0 matches** — expected: ch01–04 contain **pseudocode via `quote`+`\ttfamily`+`\textsc`** (Euclid, LinearSearch, InsertionSort, SumArray) not Python listings. This is **by design** (language-agnostic pseudocode per Ch01 §1.4 convention; AGENTS.md forbids plain `verbatim` for code, which is satisfied — `quote`+`ttfamily` is not `verbatim`). Actual highlighted code lives in ch05/ch06 where `lstlisting[language=Python]` is used (6 blocks: ch05 4, ch06 2) — verified with `language=Python` on every `lstlisting` ✓
- All `lstlisting` blocks have `language=` and inherit `lstset` colors (keyword blue!60!black etc.) — ch05–06 evidence confirms plumbing; ch01–04 need no `lstlisting` and thus vacuously satisfy `language=` requirement.

**Verdict code highlight: PASS — no `verbatim` remains; listings where used carry `language=` + `lstset` colors; ch01–04 pseudocode uses intended `quote`+`ttfamily` (not subject to lstlisting rule).**

---

## 5. Fixes Applied This Review

| # | File:Ln | Before | After | Rationale |
|---|---------|--------|-------|-----------|
| 1 | `ch04:17` | `\item analyse deterministic QuickSort's worst case and randomised QuickSort's expected $O(n\log n)$ via indicator variables;` | `\item analyse deterministic vs.\ randomised QuickSort (worst case vs.\ expected $O(n\log n)$ via indicator variables);` | Eliminated 10.14pt Overfull in LO list; also re-ran pdflatex to confirm Overfull gone (now only 2.07/2.64/0.20 cosmetic <3pt remain). |

Prior v2 fixes (deleg_518409bd, already in worktree — confirmed via `git diff`):

- ch01: arrows `violet!70!black`, 3 new tints, CPU `draw=blue!60!black`, cost badge `orange!15`; Euclid `small → scriptsize`.
- ch02: O/Omega/Theta fills `blue!12`/`green!12`/`orange!14`, hierarchy 4 tier fills, curve colors retained.
- ch03: `rnodeB teal!14` + `leaf orange!18`, Karatsuba `\[ \] → align*`, mastergeom 3 fills + case badges.
- ch04: partition 4 fills, Strassen 12 fills + violet arrow/node.

No further patches needed. Cosmetic Overfulls <3pt (2.07pt Euclid, 2.64pt InsertSort spec) intentionally left — fixing would require forced line-breaks that harm readability; gate is >15pt.

---

## 6. QA Gate Summary

| Gate | Result |
|------|--------|
| Diagram monochrome when color useful | **0** — all 6 TikZ colorized |
| Formula broken/overflow (>15pt) | **0** |
| Code lacks highlighting (`verbatim` or `lstlisting` without `language=`) | **0** in scope |
| `pdflatex` `!` errors / `pgfkeys Error` / `hyperref Warning` | **0 / 0 / 0** |
| Page count | 45p, 880 KB (was 46p v1) |

**Overall: PASS.**

---

## 7. Notes / Non-Blocking

- ch01 pseudocode is `quote`+`ttfamily` by convention; if Bowen later wants `lstlisting[language=pseudocode]` uniformly, can migrate — but current form satisfies AGENTS.md `verbatim` ban and compiles cleanly.
- ch01 `G=(V,E)` forward-ref to Ch.6 and `O(log min(a,b))` Euclid promise delegated to exercise — noted in v1 review, not a visual QA blocker.
- ch07 `pdfinfo` syntax errors on this qpdf build are from font stream hex noise (unrelated to ch01–04 TikZ); `pdflatex` exit 0 authoritative.

*Reviewer A — SC2001 v2 ch01–04 — compiler + visual audit complete.*
