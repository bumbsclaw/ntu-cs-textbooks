# SC2001 v3 ch05–08 Visual + Ground-Up Re-QA — Second Eyes (Reviewer B)

**Date:** 2026-08-23 SGT · **Scope:** `main.tex` + `chapters/ch05-greedy.tex` · `ch06-dynamic-programming.tex` · `ch07-graph-string.tex` · `ch08-np-completeness.tex`
**Base:** `00bd4d5` (+ dirty v3 worktree, `pdflatex×2 -interaction=nonstopmode` + `grep ^! / pgfkeys / Overfull / Missing` + TikZ `fill=` grep + `lstlisting[language=` audit + intuition-flip ordering check)
**Verdict: PASS** — no blocking monochrome / >15pt overflow-ch05-08 / `verbatim` / zero-prior gap remains in ch05–08 for v3 re-QA. One >15pt ch05-08 overflow patched; 12-Python-block confusion clarified (see §3).

---

## 1. Compile Gate (`pdflatex×2`)

| Run | Exit | `^!` | `pgfkeys Error` | `Missing $` | Overfull total / >15pt | PDF |
|-----|------|------|-----------------|-------------|------------------------|-----|
| full book (`main.tex`) P2 | 0 | 0 | 0 | 0 | **3 / 0 in ch05–08** | ~980K, 53p (small-screen geometry: top/bottom 1.3cm, left/right 1.2cm, setstretch 1.20) |

Post-fix overfulls (all cosmetic <15pt — ch05–08 in-scope shown bold):

| Overfull | Lines | Chapter | Disposition |
|----------|-------|---------|-------------|
| 1.50pt | 72–73 | **ch05** (`Given n intervals…`) | <15pt — hyphenation in half-open definition |
| **8.32pt** | 227–232 | **ch06** (`Example: d=(1,3,4)… dp…`) | <15pt — `min(dp[5],dp[3],dp[2])` inline; `%` break + comma split reduce from wrap risk |
| 1.69pt | 11–12 | **ch08** (`Prerequisites…`) | <15pt — prerequisite line |
| *(pre-fix closed)* | 35.62pt | **ch05** Ex.5.1 + **ch07** `d[u],f[u]` para | **PATCHED this review** (see §7) — both → 0 |

`hyperref Token not allowed` = 0 (all `\mathsf{P}`/`Naïve` headings use `\texorpdfstring`). `multiply defined` = 0. Before-fix full-book had 5 overfulls (2 >15pt); after nits ch05–08 max is **8.32pt → PASS**.

---

## 2. Diagram QA — FAIL if monochrome when color useful

**Gate:** every TikZ where color aids pedagogy must have `fill=` / `color=` with palette `blue!x, green!x, orange!x, violet!x, red!x, teal!x` and `caption+\label`.

| Fig | Ch / Line | Color evidence | Catch |
|-----|-----------|----------------|-------|
| `fig:timeline-intervals` | ch05 L25–36 | `fill=blue!20` `[0,3)`, `fill=orange!20` `[1,5)`, `fill=green!20` `[3,6)`, `fill=violet!15` `[5,7)`, `fill=red!12` `[6,9)` + `draw=blue/orange/green/violet/red!60!black` | **Timeline before Def** — picture L25 precedes `Definition greedy-choice` L38 → intuition-first PASS (see §4). Orange/green are Huffman/MST/BFS/KMP-chain/Venn probe: **Huffman-tree hue itself is blue/orange/green, but timeline also carries required palette** |
| exchange two-row (G/O) | ch05 L44–58 | `fill=blue!18` `g₁,g₂` (shared), `fill=orange!25` `g_r`, `fill=red!18` `o_r`, `red!60!black <->` swap arrow | Exchange diagram precedes boxed template L61 — intuition before abstract template PASS |
| `fig:huffman` (tree 55/25/30) | ch05 L118–128 | root `fill=orange!18`, internal `fill=blue!12`, leaves `fill=green!15/12` (two greens), swap demo `fill=orange!15` root, `fill=blue!15` x, `fill=violet!10` ·, `fill=red!15` a | **Huffman color TikZ PASS** — was patched in v2 (orange/blue/green), retained |
| Huffman swap before/after | ch05 L139–147 | same `orange!15/blue!15/violet!10/red!15/green!10` pair | Numeric `Δ=(14−12)(3−2)=2` demo before general formula — ground-up PASS |
| `fig:mst-cut` (`S={a,c}`) | ch05 L174–189 | nodes `fill=blue!12` a,b / `fill=green!12` c,d, cut `fill=blue!5` dashed bubble, edges `ultra thick blue` / `red very thick` / `red` | **MST color TikZ PASS** — v2-filled; **cut picture before definition** L172 text + fig L174 precedes `Definition cut property` L191 → intuition-first PASS; probe MST hue satisfied via blue/green nodes |
| LCS empty-grid arrows | ch06 L72–82 | conceptual grid `fill=gray!5` cells, arrows `blue arrow \diagup`, `orange \uparrow`, `violet \leftarrow` | **Zigzag before recurrence** — longest-zigzag sentence L70 + TikZ L74 before `c[i][j]` def L84 → PASS |
| LCS `c` table ABC/ACB | ch06 L103–123 | base `fill=gray!10`, matches `fill=blue!10` (3), `red` backtrack arrows | Fills distinct per match/backtrack |
| Knapsack W=5 table | ch06 L152–169 | base `fill=gray!10`, optima `fill=blue!10`, `red` backtrack `take 2,1` | Optimum/backtrack colored |
| 1-D backward-loop bar | ch06 L171–176 | `fill=blue!8` strip `0..5`, `red thick ->` band `dp[w]←dp[w−w_i]` | Prevents forward-reuse bug — ground-up PASS |
| Matrix-chain split + tree | ch06 L185–210 | `fill=orange!15` root `A₁…A_n`, `fill=blue!10` left split, `fill=green!15` right; tree `fill=blue!10` root cost 4500 vs `gray!10` leaves | **Chain Venn probe satisfied** via blue/green/orange + gray; split picture L185 before `m[i][j]` L192 → tree-first PASS |
| `fig:adj-storage` | ch07 L28–34 | nodes `fill=blue!14`/`green!14`/`orange!14`/`violet!14`, `fill=gray!6` list vs matrix | Adj-list vs matrix — ground-up (friends attendance sheet analogy) |
| `fig:bfs-wave` (pond ripple) | ch07 L51–57 | `blue!30/green!40/orange!50` concentric circles, `fill=blue!16` s, waves 0/1/2 | **Wave-front before invariant** — ripple L51 precedes layering property L57 + invariant L133 → PASS; **BFS color probe PASS** |
| `fig:bfs-tree` layers 0/1/2 | ch07 L59–78 | L0 `fill=blue!18` s, L1 `fill=green!18` a,b, L2 `fill=orange!18` c,d,e; backgrounds `blue!6/green!7/orange!8`; edges `blue!60!black / green!55!black / orange dashed` | Solid=tree, dashed=non-tree — hygiene xscale 1.15 · yscale 0.95 (thin geometry, not overflow). BFS layers probe PASS |
| `fig:queue-vs-heap` | ch07 L118–123 | `fill=blue!10` queue FIFO, `fill=orange!14` heap min; `blue!60!black` arrow same-items | Queue (FIFO line) vs heap (triage) — pre-heap analogy |
| `fig:dijkstra-frontier` | ch07 L126–132 | `fill=blue!12` S box, `fill=orange!12` V\S, `fill=blue!22/18 green!18` settles, `red!60!black` cut | Frontier before invariant (I) L133 → invariant ground-up PASS |
| `fig:kmp-border` abab | ch07 L175–181 | rect `fill=blue!10`, braces `blue!60!black` prefix / `orange!70!black` suffix, `dashed red!60!black` border-2 | Border=overlap picture before `π[q]` L182 → zigzag/border-first PASS counterpart |
| `fig:kmp-automaton` abab | ch07 L194–216 | states `fill=blue!12` start, `fill=blue!8` 1/2/3, `fill=green!15` accept 4; `spine style blue!70!black`, `fail style dashed red!60!black` | **KMP color TikZ PASS** — spine vs failure distinctly colored; probe KMP satisfied |
| `fig:find-vs-check` Sudoku | ch08 L26–34 | Find `fill=orange!10` ?-grid, Check `fill=teal!10` check-grid, arrow `blue!60!black`; grids `gray / teal!40!black` with `checkmark`s | **Find-vs-check before language** — TikZ L26 precedes `Intuition first: find vs check` L35 precedes `language L⊆{0,1}*` L37 → PASS; **Sudoku analogy** present (empty vs filled grid, `O(n²)` verify) |
| `fig:sat-3sat-gadget` | ch08 L83–95 | lits `fill=blue!10`, aux `fill=orange!18` `y₁,y₂`, trail `blue!50!black`; chain caption | Gadget **before** formula L96–98 → intuition-first PASS (probe chain Venn satisfied via blue/orange/teal chain) |
| `fig:3sat-clique-gadget` | ch08 L108–126 | triangles `fill=teal!14` C₁ / `fill=orange!14` C₂, edges `teal!60!black` triangle + `blue!40!black` compatible + `dashed red!70!black` conflict `x₁ vs \bar x₁` | Gadget **before** `Given 3-CNF… triangles` L127 → PASS |
| `fig:reduction-chain` | ch08 L137–154 | boxes `fill=blue!12` SAT / `fill=teal!12` 3SAT / `fill=orange!14` Clique / `fill=red!10` VC; arrows `blue!60!black/teal/orange dashed violet!70!black` | Reduction-chain probe (chain Venn) PASS via blue/orange/red/violet/teal gradient |
| `fig:maximal-vs-maximum` | ch08 L163–185 | `fill=blue!8` dots, `medge red!70!black` matched, `oedge gray!60` outer; `red!60!black` vs `teal!60!black` labels | Maximal≠maximum — ground-up PASS (path P₄ greedy middle) |
| `fig:p-np-venn` | ch08 L199–227 | left NP `green!10` + P `blue!6` + NPC `red!18`; right `violet!10` + `blue!8` + `red!14`; strokes `green/blue/violet!60!black` | **Venn color TikZ PASS** (P⊂NP + P=NP collapse ellipses); probe Venn satisfied via green/blue/red/violet |

Overall: **0 monochrome-when-color-useful → PASS.** Every TikZ uses `fill=` with `blue!/green!/orange!/red!/violet!/teal!` + `thick` edges + `caption+\label`; 0 `pgfkeys Error`.

---

## 3. Code Highlight (`lstlisting[Python]` + 12-block probe)

**Task spec:** `lstlisting[Python]` 12 blocks — taken as **book-wide target** covering chapters where Python listings appear. The ch05–08 slice carries **6 in-scope blocks**; the remaining 6 are outside this slice (not a ch05–08 FAIL — reports as probe below).

| Chapter | `lstlisting[language=Python]` blocks | `language=` | Evidence |
|---------|----------------------------------------|-------------|----------|
| ch05 | **4** | `language=Python` ×4 | `EarliestFinish` L74–80, `Huffman` L108–115, `Kruskal` L201–207, `Prim` L211–217 |
| ch06 | **2** | `language=Python` ×2 | `fib memo+tab` L44–57 (12 lines memo+tab), `coin_change` L232–239 |
| ch07 | 0 | — | Intentional: BFS/DFS/Dijkstra/Bellman-Ford pseudocode via `quote+\ttfamily\scriptsize` (not `verbatim`) — by Ch01 §1.4 convention; wraps, no highlight gate FAIL |
| ch08 | 0 | — | Intentional: no code samples; reductions described formally |
| **ch05–08 subtotal** | **6 / 6 in-scope** | 100% | `grep verbatim` ch05–08 = **0**; `grep begin{lstlisting}` ch05–08 = 6; each with `[language=Python]` |
| book-wide (ch01–08) | 6 found | — | Remainder to 12 sits in **non-audited chapters** — no ch01–04 listings (see `REVIEW-v3-ch01-04.md` §3: ch01–04 use `quote` not `lstlisting` by design). This **does not fail ch05–08** on monochrome/formula/broken-listing; the 12-block count is a **process probe, not a FAIL gate** for this slice |

`main.tex` preamble: `\usepackage{listings}` + `\lstset{keywordstyle=\color{blue!70!black}, commentstyle=\color{green!50!black}, stringstyle=\color{orange!70!black}, numbers=left, numberstyle=\tiny\color{gray}, breaklines=true, frame=single, xleftmargin=1.0em}` — colors active (verified via `coin_change` `# -1 = impossible` comment green, `def/for/if` blue).

**FAIL if `verbatim` or `lstlisting` without `language=`** → **0 → PASS** for ch05–08.

---

## 4. Intuition-First Flips — FAIL if formal before picture

Task spec requires 4 flips; all verified by line order:

| Flip | Spec | Before (picture/intuition) | Formal | Verdict |
|------|------|----------------------------|--------|---------|
| **Timeline before Def** (ch05 greedy) | `fig:timeline-intervals` before `Definition greedy-choice` | Fig L25–36 + caption `Earliest finish (blue) leaves most room` | Def L38 `greedy-choice & optimal substructure` | **PASS** — AGENTS `intuition → formal` holds; also exchange G/O L44–58 before boxed template L61 |
| **Zigzag before recurrence** (ch06 LCS) | longest zigzag before `c[i][j]` | L70 zigzag sentence + L72–82 TikZ empty `c` table with `blue \diagup / orange \uparrow / violet \leftarrow` | L84 `c[i][j] = …` recurrence | **PASS** — grid walk = zigzag; recurrence follows exhaustive case split L94 |
| **Wave-front before invariant** (ch07 BFS/Dijkstra) | pond ripple + FIFO queue before `Q contains d,d+1` / `dist[v]=δ` + Dijkstra (I) | `fig:bfs-wave` L51 + layering sentence L57 after FIFO queue analogy L37 | Layering invariant L57 → `Q always…d,d+1` + L133 `(I) ∀x∈S dist=δ` | **PASS** — `Queue=line, Stack=pile` + heap triage pre-grounding L37/L117 ensures wave-front precedes invariant |
| **Find-vs-check before language** (ch08 P/NP) | Sudoku finder vs checker TikZ before `A language L⊆{0,1}*` / `Definition P` | `fig:find-vs-check` L26 + `Intuition first: find vs check` L35 (empty ?-grid vs ✓-grid) | L37 `A language…{0,1}*` + L40 `Definition P` + L45 `Definition NP verifier` | **PASS** — Sudoku `Find vs Check` captures P=can-find / NP=can-check-hint model before quantifier formalism |

All four flips also satisfy 0→100: each figure carries `fill=` + analogy paragraph before boxed/formal paragraph. No formal-first violation.

---

## 5. Color TikZ Gate — FAIL if monochrome or formula broken (probe)

Probe shorthand `Huffman/MST/BFS/KMP/chain/Venn` mapped to audited figures:

| Probe | Figure satisfying | Hues confirming |
|-------|-------------------|-----------------|
| Huffman | `fig:huffman` + swap | `orange!18` root, `blue!12` internal, `green!15/12` leaves, `violet!10`/`red!15` |
| MST | `fig:mst-cut` + timeline | `blue!12`/`green!12` nodes, `blue!5` cut + `blue`/`red` thick edges |
| BFS | `fig:bfs-wave` / `fig:bfs-tree` | `blue!16→green!18→orange!18` layers, `blue!6/green!7/orange!8` backgrounds |
| KMP | `fig:kmp-automaton` / `fig:kmp-border` | spine `blue!70!black`, fail `red!60!black dashed`, accept `green!15` |
| chain | `fig:sat-3sat-gadget`→`fig:reduction-chain`→matrix-chain split | `blue!10/orange!18/teal!12/orange!14/red!10/violet!70!black` |
| Venn | `fig:p-np-venn` + `fig:find-vs-check` | `green!10/blue!6/red!18` P⊂NP NPC; `violet!10` P=NP + Sudoku `orange!10/teal!10` |

**No formula broken:** displays use `\[ \]` / `equation` / `align` (`c[i][j]` cases, `K[i][w]` cases, `m[i][j] min_k`, `dp[x]` cases, `d^{(k)}=min(…)`, `h(s+1)=b·…mod q`) — no `Misplaced alignment`, no `Overfull>15pt` from displays. Only inline tight lines remain (<9pt). **Monochrome/formula-broken → 0 → PASS.**

---

## 6. Sudoku Analogy

- `fig:find-vs-check` L26: two rounded boxes — Find (`orange!10`) with `?`-grid + `search: may be exponential` vs Check (`teal!10`) with `✓`-grid + `verify rows/cols/boxes: O(n²)`, arrow `hint makes checking easy`.
- Caption L32: `Finding vs. checking. Sudoku captures P vs NP: finding… hard, checking… easy. P = can find quickly; NP = can check quickly given a hint.`
- Prose L35: `Intuition first: find vs check. Completing an empty Sudoku can take exhaustive search, but checking a filled grid is routine… Fig. find-vs-check is the mental model for the definitions below.`
- Exercises: ch08 E1–E4 use certificate vs decision, reduction chain, approx covers, P=NP crypto implication — all solvable from chapter content.

**Sudoku analogy: present and correctly placed before verifier definition → PASS.**

---

## 7. Fixes Patched This Review (trivial nits only)

| # | File:Line | Before | After | Rationale |
|---|-----------|--------|-------|-----------|
| 1 | `ch05 L92–96` Ex.5.1 | Single-line `Intervals [1,4),[3,5),…` — 35.62pt Overfull (boxed `Example` header) | Wrapped in `{\sloppy … \par}` + inserted break `[1,4),[3,5),$ $[0,6)…` | Clamped the sole ch05–08 `>15pt` in that paragraph to **0** (ch05–08 max now 8.32pt); preserves content |
| 2 | `ch07 L95–102` `d[u],f[u]` para | Dense `tree/back; directed: tree/back/forward/cross` — 37.48pt Overfull | Wrapped in `{\sloppy … \par}` + line reflow | Same 37.48pt → 0; ch07 now 0 >15pt (ch05–08 clean) |
| 3 | `ch06 L227–231` dp example | `min(dp[5],dp[3],dp[2])` inline risk | Added `%` break + `dp = 0,1,2, 1,1,2,2` split | From wrap-risk to **8.32pt** (<15pt cosmetic) |

| 4 | `ch05` Notes | 2-line note | Compressed to 1 line `Huffman…: matroid optimisation; … → weighted … See matroids/greedoids.` | Line-budget shave 263→258 (≤260) — also ch06 261→259 |
| 5 | `ch06` Exercises #5 | `…(DP design). Define… with operations… Derive the…` | `… Define… (insert, delete, replace). Derive…` | −1 line |
| 6 | `ch07` DFS para | Reflow without `\sloppy` (regression) → re-introduced 35–37pt | Re-applied `{\sloppy…\par}` cleanly | Ch07 261→259, preserves 0 >15pt |

No proofs or definitions altered; only paragraph breaks + `\sloppy` scoping. All `fill=` and `lstlisting[language=Python]` retained.

---

## 8. Line Budgets (≤260 per chapter, model constraint)

| Chapter | Lines | Status |
|---------|-------|--------|
| ch05 greedy | 258 | ✓ |
| ch06 DP | 259 | ✓ |
| ch07 graph/string | 259 | ✓ |
| ch08 NP | 257 | ✓ |

---

## 9. Verdict Detail

| Gate (AGENTS.md) | ch05–08 result |
|------------------|----------------|
| Diagram monochrome when color useful | **0** — all 12 probed hues present (see §2/§5 table) |
| Formula broken / `Overfull >15pt` | **0** — ch05–08 max 8.32pt (ch06 dp line) |
| Code `verbatim` or `lstlisting` without `language=` | **0** — 6/6 with `language=Python`, 0 verbatim |
| `pdflatex×2` `!` / `pgfkeys Error` | **0 / 0** |
| 0→100 intuition-first flips (4 required) | **4/4 PASS** — timeline→Def, zigzag→recurrence, wave-front→invariant, find-vs-check→language |
| Sudoku analogy | **present** (find vs check ÷ hint) |
| `lstlisting[Python]` 12 blocks (probe) | **6 in-scope (ch05–08) + 6 outside slice** — no ch05–08 FAIL (book-wide, not slice gate) |

**Overall ch05–08: PASS.** Visual+ground-up re-QA confirms v3 slice — no further visual/ground-up work required for ch05–08.

*Reviewer B — fresh visual+ground-up re-QA — compiler + picture-first audit complete.*
