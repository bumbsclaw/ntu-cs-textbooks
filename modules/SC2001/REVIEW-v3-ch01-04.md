# SC2001 v3 ch01–04 Visual + Ground-Up Re-QA — Second Eyes (Reviewer B)

**Date:** 2026-08-23 SGT · **Scope:** `main.tex` + `chapters/ch01-foundations.tex` · `ch02-asymptotics.tex` · `ch03-recurrences.tex` · `ch04-divide-conquer.tex`
**Base:** `00bd4d5` (+ dirty v3 worktree, 9 files changed, 2121L incl. main) · **Method:** fresh visual + ground-up read + `pdflatex×2 -interaction=nonstopmode` + `grep ^! / pgfkeys / Overfull / Missing` + TikZ color grep
**Verdict: PASS** — no blocking monochrome / >15pt overflow / zero-prior gap remains in ch01–04 for second-eyes re-QA. One >15pt overflow patched below; isolated ch01–04 now 0 overfull.

---

## 1. Compile Gate (`pdflatex×2`)

| Run | Exit | `^!` | `pgfkeys Error` | `Missing $` | Overfull total / >15pt | PDF |
|-----|------|------|-----------------|-------------|------------------------|-----|
| isolated ch01–04 (main14b.tex) P2 | 0 | 0 | 0 | 0 | **0 / 0** | 689K, 24p |
| full book (main.tex) P2 | 0 | 0 | 0 | 0 | 4 / **0 in ch01–04** | 982K, 53p (small-screen geometry: top/bottom 1.3cm, left/right 1.2cm, setstretch 1.20) |

Before fix, isolated ch01–04 had 1 × 27.84pt at `ch01 L185–223` (RAM paragraph); full had 6 including that. After trivial nits, isolated 1→0. Remaining 4 full-book overfulls are **outside scope** (ch05–08: `ch06 L72–73 1.50pt`, `ch06 L227–232 8.32pt`, `ch07 L95–105 36.63pt*`, `ch08 L11–12 1.69pt`; *file-line greps show these resolve to `ch06`, `ch07`, `ch08` — no line maps to ch01–04 source).
`*` 36.63pt is `ch07 L95–105` inside `fig:heap` caption area — large but outside this gate; noted for ch05–08 owner, not a ch01–04 FAIL.

Display formulas: all in `equation` / `align*` / `\[ \]` — no raw `$...$` spanning lines, no `Misplaced alignment`. Grep `verbatim` in ch01–04: 0; `lstlisting` in ch01–04: 0 (pseudocode uses `quote+\ttfamily+\scriptsize` per Ch01 §1.4 convention — not `verbatim`, so AGENTS.md invariant satisfied; `listings` preamble defines keyword/comment/string colors).

---

## 2. Diagram QA — FAIL if monochrome when color useful

**Gate:** every TikZ where color aids pedagogy must have `fill=` / `color=` with palette `blue!x, green!x, orange!x, violet!x, red!x, teal!x, yellow!x` and `caption+\label`.

| Fig | Location | Color evidence | Catch |
|-----|----------|----------------|-------|
| `fig:sets-functions` | ch01 L29–65 | `fill=blue!10` Venn, `fill=orange!18` subset, `fill=green!10`/`violet!10` domain/codomain ellipses, `blue!60!black` injective arrows / `red!70!black` non-injective merge, `fill[green!60!black]`/`red!70!black` quantifier dots | PASS — Venn/arrow placed **before** formal sets (L26 `picture→words→definition`) |
| sums (Gauss/geometric/floor) | ch01 L95–125 | `fill=blue!55`/`orange!65`/`orange!25` dot pairing, `fill=green!18` tree nodes, `fill=blue!60!black` floor dot, `red!70!black` <1 brace | PASS |
| `fig:ram-model` | ch01 L186–222 | `arrow color=violet!70!black`, `\fill[yellow!10]` tapes, `\fill[blue!4]` memory group, tape cells `yellow!15`/`gray!20`, CPU `blue!7+blue!60!black`, Control `orange!18`, Registers `green!15`, ALU `red!12`, Fetch `blue!10`, badge `orange!15` | PASS — patched `resizebox{\linewidth}{!}` (see §5) |
| `array-barrier` (invariant) | ch01 L242–255 | `fill=green!18` sorted / `yellow!18` unsorted / `gray!12` done, barrier `red!70!black` | PASS — `Recipe` remark + this figure **before** formal (LI1–3) L256 |
| `fig:asymptotic-bands` | ch02 L48–99 | `fill=blue!12` O band, `fill=green!12` Omega, `fill=orange!14` Theta, curves `blue`/`red`, `green!60!black`/`red!60!black` so/omega labels, `fill[teal!5/orange!6/blue!5/red!4]` hierarchy tiers (L166–169), curves `teal`/`orange!80!black`/`blue`/`red`/`purple` | PASS — `Picture first.` L46 then figure before `O/Ω/Θ` defs L101 |
| `fig:onelevel` | ch03 L11–37 | `rbox fill=blue!12`, `cbox fill=teal!14`, `fill=orange!14` general root | PASS — one-level expansion **before** general `T(n)=aT(n/b)+f(n)` eq L40 |
| `fig:rectree` / `fig:mastergeom` / cn-b trick | ch03 L92–158 | `rnode blue!10`, `rnodeB teal!14`, `leaf orange!18`; mastergeom `\fill[blue!7/red!7/orange!10]` + lines `blue/orange/red 70!black`; cn-b gap bar `blue!10`/`orange!14` + `teal!70!black` brace | PASS |
| `fig:dc-tree` | ch04 L32–47 | `fill=blue!14` root, `fill=green!14` children, `fill=green!8` grandchildren, badge `orange!12` | PASS — two-level D&C tree before recurrence L48 |
| `fig:qs-partition` | ch04 L82–100 | `\fill[green!18]` ≤x, `red!12` >x, `yellow!18` unscanned, `blue!18` pivot | PASS |
| `fig:qs-indicator` | ch04 L108–132 | `fill[blue!12]` interval Z_ij, `orange!` harmonic triangle (90−12k opacity), badge `orange!18`, `blue!60!black` brace | PASS — indicator picture before double-sum algebra |
| `fig:strip` | ch04 L143–161 | `\fill[gray!6]` strip, `\fill[orange!10]` δ×2δ rect, `gray!60` grid, `blue!60!black` points, diagonal `δ/√2` label | PASS — strip sparsity figure before lemma L163 |
| `fig:strassen` | ch04 L200–236 | A `blue!10/18`, `teal!12`, `orange!10`, `red!8`; B `green!10/18`, `teal!12`, `orange!10`, `violet!8`; arrow `violet!70!black 7×`, mid node `violet!8`, C `blue!6/14` etc. | PASS — block colors + `7×` annotation distinguish quadrants |

Overall: **0 monochrome-when-color-useful → PASS.** All TikZ compile 0 `pgfkeys Error`, carry `\caption` + `\label`.

---

## 3. Formula

- `align*` for Strassen 7 M_k (ch04 L192–197), Karatsuba geometric sum broken at `=` with `\frac` continuation (ch03 L125–126), QuickSort `E[X]=Σ 2/(j-i+1)` inside `\[ \]`.
- Master theorem `c⋆=log_b a` with `Case 1/2/3` inside `theorem` enumerate — no overflow.
- Akra–Bazzi integral `Θ(n^p(1+∫ f(u)/u^{p+1} du))` properly braced.
- No display exceeds \linewidth after ch01–04 isolate; `Overfull \hbox >15pt = 0` authoritative.

---

## 4. 0→100 Ground-Up (assume zero bachelor's — FAIL if gap)

| Check | Spec | Found | Verdict |
|-------|------|-------|---------|
| **From zero box** | Bold box stating no prior needed | ch01 L9 `fbox From zero: we build here, no MH1812/SC1007 needed.` + prerequisites gated on ch01 below | PASS |
| **Venn/arrow** | Picture before formal sets | `fig:sets-functions` L29 before `Discrete Mathematics Refresher` formalism L26–70; dots+ellipses before injective/surjective defs | PASS |
| **Quantifiers picture-first** | Dots before ∀/∃ | `green!60!black` all-green vs one red counterexample L76–83 before Def L84–91, De Morgan `swap + flip` | PASS |
| **Sums intuition-first** | Derivation before list | Gauss pairing L93–103, geometric tree L104–112, harmonic/ log ruler / floor number-line L113–126 — each picture then closed form | PASS |
| **Timed story** | Two-program table before asymptotics | `tab:shape-wins` L29–39 `3n²+5n` vs `100n` table, crossover n₀≈33, shape wins narrative before `Why Asymptotics` formalism | PASS |
| **Bands before O/Ω/Θ** | Picture then quantifiers | L46 `Picture first.` + Fig L48–99 before Def L101–115, `o/ω` dashed narrowing band, quantifier order remark L116 | PASS |
| **One-level tree** | Expansion before general recurrence | `fig:onelevel` L11–37 (MergeSort + general `a children`) before `T(n)=aT(n/b)+f(n)` L40, floors/ceilings boxed L46 | PASS |
| **Bridge tree→substitution** | Tree suggests, substitution proves | ch03 L54 `Bridge—tree suggests, substitution proves.` + `cn-b` trick picture L67–78 absorbing `+1` with gap `b−1≥0` | PASS |
| **Master geometry** | Picture before cases | `fig:mastergeom` walk-through L160 before `thm:master` L162 — shrinking/flat/increasing narrative maps to Case 1/2/3 + gap box n=1024 numeric | PASS |
| **Akra-Bazzi checklist** | Lopsided tree + checklist before integral | `fig:akra` L205–234 — unbalanced depths + violet checklist TikZ before formula L237–244 | PASS |
| **D&C micro-primer** | Indicator/linearity from zero | ch04 L71–75 `Micro-primer: Indicator Variables` — `X=1[E]`, `E[X]=Pr[E]`, 2-coin example before QuickSort `Pr=2/(k+1)` | PASS |
| **Invariant recipe** | Words + barrier before formal LI1–3 | Remark `Recipe—words before formal` L241 + barrier TikZ L242–255 before `Definition Loop invariant` L256 | PASS |
| **Zero-prior gap** | No assumed maturity leak | Ch01 E1.1 warm-up predicate; ch02 Expectation micro-primer L192 + bridge recurrence example L208 already; ch04 prerequisites explicitly `Ch.2 / Ch.1 / Micro-primer §prob-primer` | PASS |

INTUITION-FIRST order holds throughout: figure/table ≥½ page before its theorem/definition in every case above.

---

## 5. Fixes Patched This Review (trivial nits only)

| # | File:Line | Before | After | Rationale |
|---|-----------|--------|-------|-----------|
| 1 | `ch01 L188 / L219` | `\begin{tikzpicture}[` … `\end{tikzpicture}` at natural width 12pt-wide (spans −6.35→5.55) | Wrapped in `\resizebox{\linewidth}{!}{%` … `}%` | Clamped the sole ch01–04 `27.84pt` Overfull (RAM model) to 0; preserves violet arrows + all fills |
| 2 | `ch01 L223` | `\texttt{LOAD,STORE,ADD,…WRITE}` single unbreakable word | `\texttt{LOAD}, \texttt{STORE}, …` comma-separated | Previously caused isolated 27.84pt para overflow (line 185–223); split allows line-break between instructions (recommended by line 72 pattern elsewhere) |

No other patches needed. Cosmetic <15pt overfulls in full build are outside ch01–04 (see §1) and left for their chapter owners.

Prior consolidated fixes verified present: ch04 `fig:dc-tree` + micro-primer, ch05 timeline+exchange+numeric, ch07 queue/heap border+wave-fronts — unchanged in this re-QA.

---

## 6. Verdict Detail

| Gate (AGENTS.md) | ch01–04 result |
|------------------|----------------|
| Diagram monochrome when color useful | **0** |
| Formula broken / `Overfull >15pt` | **0** (isolated 0, full-book in-scope 0) |
| Code lacks highlighting (`verbatim` or `lstlisting` without `language=`) | **0** — `verbatim` 0, `lstlisting` where used have `language=` |
| `pdflatex×2` `!` / `pgfkeys Error` | **0 / 0** (both isolated and full P2) |
| 0→100 zero-prior gap | **0** — From zero box, Venn/arrow, timed story, one-level tree all present and correctly ordered |

**Overall ch01–04: PASS.** Second-eyes re-QA confirms consolidated `deleg_36609dd3` — ready to commit v3 ch01–04 slot; no further visual/ground-up work required for this slice.

*Reviewer B — fresh visual+ground-up re-QA — compiler + picture-first audit complete.*
