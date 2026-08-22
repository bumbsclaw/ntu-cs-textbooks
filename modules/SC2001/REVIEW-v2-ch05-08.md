# Visual QA Review v2 — SC2001 ch05–08 (Greedy · DP · Graph/String · NP) — Reviewer B

Date: 2026-08-23 · Reviewer: Visual QA Reviewer B (muse-spark-1.2-contributor)
Scope: `chapters/ch05-greedy.tex`, `ch06-dynamic-programming.tex`, `ch07-graph-string.tex`, `ch08-np-completeness.tex`, `main.tex`
Baseline: 45p / ~860 KB / 0 `! ` / 0 hyperref Token / 0 Overfull>15pt · Build: `pdflatex -interaction=nonstopmode main.tex` ×2 → exit 0
Line budget: ch05 220 / ch06 233 / ch07 214 / ch08 212 (all ≤260)

---

## Verdict: PASS

All visual-QA gates pass after 2 trivial patches (ch05 fills). No `verbatim` code, no monochrome-when-colour-useful diagram, no formula overflow >15pt, no `texorpdfstring` omission. Exercises solvable from chapter content; 0→100 flow intact.

---

## Compile Check

| Check | Result |
|-------|--------|
| `pdflatex` exit 0 (×2) | PASS |
| `grep "^! "` | 0 |
| `grep "pgfkeys.*Error\|Package pgf Error"` | 0 |
| `grep "Token not allowed"` (hyperref) | 0 |
| `Overfull \hbox >15pt` | 0 (max 2.64pt at lines 326–327; 2.07pt at 176–182) |
| `multiply defined` label | 0 (ch06 `sec:coin-change-dp` distinct from ch05) |
| `pdfinfo Pages` | 45 |
| `du -k main.pdf` | 860 KB (≈880 KB baseline; within rounding/compression variance) |

Previous 10.14pt overfull at old log lines 17–18 no longer present; remaining overfulls are <3pt (hyphenation, not formula wrap).

---

## Code Highlighting Audit — FAIL if plain verbatim

| Chapter | `lstlisting` blocks | `language=` | `verbatim`/`minted` | Verdict |
|---------|---------------------|-------------|----------------------|---------|
| ch05 greedy | 4 blocks → 8 boundary lines (`\begin`+`\end` ×4) : EarliestFinish (6 lines), Huffman (7), Kruskal (5), Prim (6) | `language=Python` on all 4 | 0 | **PASS** — `main.tex` `\lstset` provides `keywordstyle blue!70!black`, `comment green!50!black`, `string orange!70!black`, `numbers left` |
| ch06 DP | 2 blocks → 4 boundary lines : fib memo+tab (12 lines), coin_change (9 lines) | `language=Python` on both | 0 | **PASS** — same global `lstset`; uses `#` comments and `def` keywords which highlight |
| ch07 graph-string | 0 `lstlisting` (pseudocode via `quote`+`\ttfamily\scriptsize` for BFS/DFS/Dijkstra/Bellman-Ford) | N/A — not code-highlighting gate | 0 | **PASS** — no `verbatim`; `quote` pseudocode is intentional and wraps (see Formulas) |
| ch08 NP | 0 `lstlisting` (no code samples; reductions described formally) | N/A | 0 | **PASS** — no code to highlight; no `verbatim` |

Criterion: every code block uses `\begin{lstlisting}[language=Python]` (or `C`/`Java`); plain `verbatim` count must be 0 — satisfied across all 4 chapters.

---

## Diagram Colour-Fill Audit — FAIL if lines-only when colour useful

| Figure | Required cue | Fills found | Verdict |
|--------|--------------|-------------|---------|
| ch05 `fig:huffman` (Huffman tree) | internal vs leaf distinction; greedy pair at depth | **PATCHED**: root `fill=orange!18`, internal `fill=blue!12`, leaves `fill=green!15/12`; edges `thick` | **PASS** — was monochrome (all `draw` circles, plain `stealth` edges); now gradient depth cue |
| ch05 `fig:mst-cut` (cut S={a,c}) | cut region vs crossing edges | **PATCHED**: nodes `fill=blue!12/green!12`, cut rectangle `fill=blue!5`; plus existing `ultra thick blue / red very thick` edge weights | **PASS** — was lines-only nodes; now filled |
| ch06 LCS table (p. ABC/ACB) | match cells, base row/col | `fill=gray!10` base, `fill=blue!10` matches, red backtrack arrows | **PASS** |
| ch06 Knapsack table W=5 | optimum cells, backtrack | `fill=gray!10` base, `fill=blue!10` optima, `red` backtrack arrows | **PASS** |
| ch06 Matrix-chain tree (A1A2)A3 | optimal subtree | `fill=blue!10` root, `fill=gray!10` leaves | **PASS** |
| ch07 `fig:bfs-tree` (BFS layers) | BFS layer colours + tree vs non-tree | nodes `fill=blue!18` (L0), `fill=green!18` (L1), `fill=orange!18` (L2); background `fill=blue!6/green!7/orange!8`; edges `blue!60!black / green!55!black / orange!75!black dashed` | **PASS** — full palette: `blue!/green!/orange!` fills |
| ch07 `fig:kmp-automaton` (KMP P=abab) | spine vs failure links | states `fill=blue!12/blue!8/green!15` (accept); `spine` style `blue!70!black`, `fail` style `dashed red!60!black` | **PASS** — `blue!/red!/green!` fills |
| ch08 `fig:reduction-chain` (SAT→VC) | reduction gradient | boxes `fill=blue!12/teal!12/orange!14/red!10`; arrows `blue!60!black/teal!60!black/orange!70!black/violet!70!black dashed` | **PASS** — gradient `blue!/orange!/red!/violet!` |
| ch08 `fig:p-np-venn` (P vs NP) | P inside NP, NPC core | left: `fill=green!10` (NP) `fill=blue!6` (P) `fill=red!18` (NPC); right: `fill=violet!10` (P=NP) `fill=blue!8` `fill=red!14`; strokes `green!55!black/blue!55!black/violet!60!black` | **PASS** — `green!/blue!/red!/violet!` fills |

All inspected TikZ figures contain `fill=` with `blue!/green!/orange!/red!/violet!`; no figure is lines-only when colour is pedagogically useful.

---

## Formulas & Pseudocode Wrapping

| Item | Check | Result |
|------|-------|--------|
| ch07 BFS quote (L33–41) | `\ttfamily\scriptsize` + `\\` breaks; layering invariant paragraph | wraps, no Overfull>15pt |
| ch07 DFS-Visit quote (L75–79) | same `quote` env | wraps |
| ch07 Dijkstra quote (L93–101) | `Relax`/`ExtractMin`/`DecreaseKey` with `\\` | wraps |
| ch07 Bellman-Ford `\textbf{for}` (L115) | single-line `\ttfamily\small` loop | wraps (0.20pt overfull only) |
| ch07 Floyd display `d^{(k)}[i,j]=min(...)` (L128–131) | `\[ ... \]` with `\begin{cases}` | no overflow |
| ch07 Rabin-Karp `h(s+1)=...` (L184–186) | `\[ ... \]` | no overflow |
| ch07 `Naïve \texorpdfstring{$\Theta((n-m+1)m)$}{...} Scan` (L142) | `texorpdfstring` present | no hyperref warning |
| ch08 all `\mathsf` sections (L23, L58, L122, L177) | `\texorpdfstring{$\mathsf{P}$...}{P...}` | 4/4 present; 0 `Token not allowed` |
| ch08 clause-splitting display (L78–80) | `\[ (l1∨... )... \]` | fits width |
| Max Overfull | 2.64pt (ch07 prose, not display) | PASS (<15pt) |

---

## Issues by Chapter (post-patch)

### ch05 Greedy — PASS (patched)
Exchange / cut-property / Huffman sibling proofs correct. Patches add depth fills to Huffman tree and node fills to MST-cut; TypeScript `lstlisting[language=Python]` on all 4 algorithms confirmed (8 boundary lines). Minor nit: sibling-lemma sentence "cannot both be reversed" still slightly terse — acceptable; not patched to keep line budget.

### ch06 DP — PASS
LCS/knapsack/matrix-chain/coin-change recurrences and complexities correct. 2 `lstlisting[language=Python]` blocks (4 boundary lines) verified. Tables and trees carry `blue!/gray!/red!` fills. No issues blocking; `sec:coin-change-dp` label distinct.

### ch07 Graph/String — PASS
BFS/DFS/Dijkstra/Bellman-Ford/Floyd/KMP/Rabin-Karp correct. BFS layer fills (`blue!/green!/orange!`) and KMP spine/fail (`blue!/red!+green!` accept) satisfy gradient requirement. Pseudocode in `quote` wraps; `texorpdfstring` on Naïve heading present.

### ch08 NP-Completeness — PASS
P/NP/coNP/verifier/reduction/NPC definitions + Cook-Levin statement + SAT→3SAT→Clique→VC chain correct; reduction chain gradient and Venn fills use full `blue!/teal!/orange!/red!/violet!/green!` palette. All 4 `\mathsf` titles wrapped with `texorpdfstring`.

### main.tex — PASS
`book` class, `xcolor`, `tikz` libs (`arrows.meta,positioning,calc,shapes,shapes.geometric,decorations.pathreplacing,fit,backgrounds,trees,automata`), `listings`+`hyperref` correctly configured. Includes ch01–ch08 in order.

---

## Fixes Applied (this review)

- `chapters/ch05-greedy.tex` `fig:huffman` — added `fill=orange!18` (root), `fill=blue!12` (internal), `fill=green!15/12` (leaves), `thick` edges; was monochrome lines-only.
- `chapters/ch05-greedy.tex` `fig:mst-cut` — added `fill=blue!12` (a,b), `fill=green!12` (c,d), `fill=blue!5` cut rectangle, `thick` node style; was unfilled circles + bare dashed cut.

No `verbatim` introduced; no `Overfull>15pt` introduced; both figures now pass colour-fill gate.

## Fixes Recommended (not blocking)

- None required for PASS. Optional: polish ch05 sibling-lemma wording one sentence if churn allows; ch07 Floyd in-place sentence could add "since `d[i][k]`/`d[k][j]` unchanged by iteration k" — already correct and concise.

---

*Reviewer B — visual QA, pdflatex-grep verified, colour-fill and language= gate enforced. FAIL would have triggered on any plain verbatim or unfilled diagram; none remain.*
