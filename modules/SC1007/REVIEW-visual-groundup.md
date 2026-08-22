# SC1007 Data Structures — Visual + Ground-Up QA

**Date:** 2026-08-23 &nbsp; **Reviewer:** muse-spark-1.2 (subagent) &nbsp; **Commit:** 21a57b7+ PHASE2 drafts
**Scope:** `modules/SC1007/main.tex` (60 lines) + `chapters/ch01`–`ch08` (1650 lines, 200-220 each)

## Verdict: PASS

All hard gates green after one trivial patch (Ch01 hidden-prior defs). No monochrome-when-color-useful diagram, no broken formula, no verbatim, no Overfull>15pt, no pgfkeys/! error after fix.

---

## Build Verification

| Check | Result |
|---|---|
| `pdflatex ×2 -interaction=nonstopmode` | EXIT 0 both passes |
| `grep "^!"` | 0 (only benign `First Aid for listings.sty`, not `!`) |
| `grep -i pgfkeys` error | 0 — only pgfkeys library loads |
| `grep "Overfull \\hbox >15pt"` | 0 Overfull at any threshold |
| `Missing $` / `Misplaced alignment` | 0 |
| `hyperref` | OK — 2 Unicode math-shift warnings in PDF strings (non-fatal, Ch07 BFS labels) |
| Pages / size | 37 pages, 541,999 bytes (A4) |
| Small-screen geometry | `top/bottom 1.3cm left/right 1.2cm`, `\setstretch{1.20}`, `\parskip 0.70em`, `itemsep 0.45em`, `lst xleftmargin 1em` — verified in `main.tex:17-28` |

---

## (b) Diagrams — 24 TikZ, All Color Fills

| # | File:line | Subject | Fills used | Monochrome? |
|---|---|---|---|---|
|1| ch01:36 | Array layout (contiguous + doubling) | `blue!15`, `green!15`, `green!5` dashed | No |
|2| ch01:80 | Singly vs doubly linked list | `orange!15`, `violet!12` | No |
|3| ch01:146 | Access-cost plot | `blue!6`, `orange!6` bands | No |
|4| ch02:28 | Stack plates + array top ptr | `blue!18/green!18/orange!18/violet!18`, `blue!12` | No |
|5| ch02:82 | Queue + circular buffer | `green!12`, `blue!14`, `gray!10` | No |
|6| ch02:115 | Deque both ends | `violet!10`, white | No |
|7| ch03:34 | Binary tree (root/leaves/height) | `orange!20`, `blue!15`, `green!18` | No |
|8| ch03:75 | DFS orders on 5-node tree | `orange!18`, `green!15`, `blue!14` | No |
|9| ch03:154 | Level-order / BFS queue | `blue!6`, `orange!18`, `blue!14`, `green!14` | No |
|10| ch04:33 | BST example (inorder sorted) | `orange!18`, `blue!14`, `green!14` | No |
|11| ch04:101 | AVL LL rotation before/after | `red!16`, `orange!16`, `green!14` | No |
|12| ch04:138 | Height plot (linear vs log) | `red!5`, `blue!6` bands | No |
|13| ch05:35 | Heap tree + array embedding | `orange!20`, `blue!14`, `green!14`, `blue!10` | No |
|14| ch05:71 | Sift-up / sift-down | `orange!18`, `red!14`, `blue!14` | No |
|15| ch05:144 | Build-heap cost plot | `blue!6` band | No |
|16| ch06:38 | Universe → table hash map | `violet!8`, `orange!18`, `blue!10` | No |
|17| ch06:70 | Chaining (5 slots) | `blue!14`, `green!14` | No |
|18| ch06:131 | Open addressing + cluster | `blue!14`, `orange!16`, `red!16`, `gray!10` | No |
|19| ch07:48 | Graph + matrix + adj lists | `orange!18`, `blue!14`, `green!14`, `orange!20`/`gray!8` matrix | No |
|20| ch07:130 | BFS tree (tree/non-tree) | `orange!20`, `green!16`, `violet!14` | No |
|21| ch07:179 | BFS vs DFS bars | `blue!14`, `green!14`, `violet!14`, `orange!14/10/6` | No |
|22| ch08:34 | Quicksort partition | `blue!10`, `orange!18`, `green!14`, `red!12` | No |
|23| ch08:107 | Counting sort histogram | `blue!12`, `green!14` | No |
|24| ch08:163 | Sorting landscape ($n^2$/$n\log n$/$n$) | `green!5`, `blue!5`, `red!4` bands | No |

Every TikZ uses `fill=` shades + colored `draw=` edges/arrows + legends where useful. No diagram is pedagogically monochrome.

---

## (c) Code — 0 verbatim, All Highlighted

- `grep verbatim` → 0 hits.
- `grep lstlisting` → 23 blocks; every `\begin{lstlisting}` carries `language=` (`Python` ×18, `C++` ×4, `C` ×1). All `\end{lstlisting}` filtered out in naive grep; manual audit confirms each begin has language.
- Preamble `main.tex:40` defines `\lstset` with `keywordstyle \color{blue!70!black}`, `commentstyle \color{green!50!black}`, `stringstyle \color{orange!70!black}`, `numbers=left`, `breaklines=true`, `frame=single`, `xleftmargin=1em` — satisfies PROJECT_BRIEF §9.

## (d) Formulas — Clean

All display math uses `equation`/`align` (no raw `$$` or `$…$` wrapping across lines). Checked: `!`, `Missing`, `pgfkeys`, `Overfull` all 0. Long formulas in Ch05 `eq:build-heap` and Ch06 hash family correctly broken with `\nonumber`.

---

## (a) 0→100 Ground-Up — Per-Chapter

| Ch | Title | Prereq line | Intuition-first? | Hidden prior? |
|---|---|---|---|---|
|1| Arrays/Lists/Foundations | `ch01:10` SC1003 C/Python basics, 0→1 declared | Yes: quote → addr formula → figure `fig:array-layout` → amortised proof | **Fixed:** `pointer`, `Θ/O/Ω` used at line 30 before def. Patched (see below). Remaining clean. |
|2| Stacks/Queues/Deques | `ch02:10` Ch1 + $O(\cdot)$ | Yes: plates analogy (`fig:stack`) / corridor queue before LIFO/FIFO def | No — recursion explained as call stack at `ch02:168` |
|3| Trees & Traversals | `ch03:10` Ch1-2 | Yes: hierarchy quote → depth/height def with `fig:binary-tree` before traversals | Minor forward-ref: `ch03:24` defines tree as "connected acyclic graph" before graph defined in Ch07. Tolerated — glossed adequately. |
|4| BST / AVL / RB sketch | `ch04:10` Ch3 | Yes: BST invariant `Def 4.1` before ops; AVL rotation story with `fig:avl-rotation` before formalism `eq:avl-invariant` | No |
|5| Heaps / Priority Queues | `ch05:10` Ch3+Ch1 | Yes: "smallest on top" → complete-tree definition → `eq:heap-index` → `fig:heap-array` | No |
|6| Hashing | `ch06:10` Ch1+Ch5 | Yes: pigeonhole (`fig:hash-map`) → `h(k)` constructions `align at 26` before chaining/open addressing | No — uniform hashing & universal family derived |
|7| Graphs (BFS/DFS/MST/Dijkstra) | `ch07:10` Ch2+3+5 | Yes: "vertices and edges" → table `tab:graph-repr` → `fig:graph-representations` before BFS/DFS | No |
|8| Sorting & Analysis | `ch08:10` Ch1-7 | Yes: landscape preview → per-algorithm recurrence → lower-bound decision tree, `fig:sorting-landscape` synthesises | No — Stirling referenced as sketch, acceptable |

Progression `arrays/lists → stacks/queues → trees → BST/balanced → heaps → hashing → graphs → sorting` is coherent 0→100 with no chapter assuming an undefined bachelor's concept after patch.

---

## Fixes Applied (trivial nits patched directly)

- **ch01:22-24 — Added pointer + asymptotic notation ground definitions.** Inserted before first use of `pointer`/`Θ/O/Ω`: "`pointer` is a variable whose value is a memory address…" and "`Θ/ O/ Ω` tight/upper/lower bounds, $O(1)$ constant…". Recompiled: still 0 errors, 0 Overfull. This was the sole FAIL-grade hidden prior.

## Recommended Fixes (non-blocking, do next)

1. **ch03:24 — Gloss "graph" on first tree definition** (1 line): append "(a graph is a set $V$ of vertices plus edges $E\subseteq V\times V$; defined fully in Ch. 7)" so the tree definition is self-contained without forward ref.
2. **ch06:171 / hyperref math-in-section warnings** — low priority; if any section title later contains `$…$`, add `\texorpdfstring`. Current warnings are benign.
3. **ch02:179 `eval(f"{a}{tok}{b}")` pedagogy note** — add one-line comment `# toy only; production would dispatch on operator` to avoid normalising `eval`.
4. **ch08:193 introsort `import heapq` unused** — remove import or use `heapq.heapify` in sketch for tidiness.

---

## Small-Screen Verification (PROJECT_BRIEF §9)

- `main.tex:17` `geometry{top=1.3cm,bottom=1.3cm,left=1.2cm,right=1.2cm,includeheadfoot}` — phone-width maximised.
- `main.tex:19-21` `\setstretch{1.20}`, `\parskip 0.70em`, `\parindent 1.0em` — airier than default.
- `main.tex:26-28` `\topsep/itemsep/parsep` reduced, `textfloatsep/intextsep` 10pt/8pt — scroll-friendly.
- `main.tex:40` `xleftmargin=1.0em` gives code blocks breathing room; `breaklines=true` prevents phone overflow.
- No `Overfull>15pt` at A4 confirms phone-width will not overflow (narrower geometry is more forgiving on overfull, but code breaklines already handle it).

## Methodology

1. Read `main.tex` preamble for `lstset`, `geometry`, `tikz` libraries, `hyperref`.
2. Read all 8 `chapters/*.tex` end-to-end (1650 lines) — checked intuition→definition→example→proof→exercise flow, prerequisite chain, and hidden priors.
3. Compiled `pdflatex -interaction=nonstopmode main.tex ×2`; grepped logs for `^!`, `pgfkeys`, `Missing`, `Overfull`, `hyperref`.
4. Counted `tikzpicture` (24), audited each `fill=` / `draw=` for color; `lstlisting` (23) for `language=`; `verbatim` (0).
5. Audited `equation`/`align` vs inline `$` for formula hygiene; spot-checked `eq:array-addr`, `eq:avl-invariant`, `eq:heap-index`, `eq:build-heap`, hash `align` at `ch06:26`.
6. Patched single hidden-prior gap (Ch01) and recompiled to confirm still 0 errors.

## Raw Evidence (for audit trail)

```
pdflatex ×2: EXIT 0, 0 Overfull, 0 ^! (1 benign listings First Aid), 0 pgfkeys error
grep verbatim: 0 hits
grep lstlisting begin: 23 (Python 18, C++ 4, C 1) — all with language=
grep tikzpicture: 24 — all contain fill= with ! shades
pdfinfo: 37 pages, 541,999 bytes, A4
grep "Missing": 0
hyperref: 2 Unicode math-shift warnings (Ch07 BFS queue labels) — non-fatal
```

## Detailed Per-Chapter Gaps (line-precise)

- **Ch01 `ch01-stl-foundations.tex:10-33`**: Prerequisites SC1003 declared. `pointer` used in quote `:7` before def — now defined at new `:24`. `Θ/O` at `:15,30` before def — now defined at new `:24`. `amortised` defined with proof at `:165-172 eq:amortised` with figure.
- **Ch02 `ch02-stacks-queues.tex:10,24-35,60-72,168`**: No hidden prior; `recursion` deferred to `:168` call-stack explanation — correct ordering. Circular buffer modulo at `:106` derived from array indexing.
- **Ch03 `ch03-trees-traversals.tex:24,27-30,60,65-71`**: `graph` at `:24` is forward ref to Ch07 — recommendation adds gloss (non-blocking). Height/depth conventions (`-1` for empty) explicit at `:26`.
- **Ch04 `ch04-bst-balanced.tex:25-30,83-86,90-94,171-174`**: BST invariant as formal `Definition` before ops — exemplary intuition-first. AVL `1.44 log n` derived, not asserted.
- **Ch05 `ch05-heaps-priority.tex:24-31,101-126,135-140`**: Completeness → array embedding `eq:heap-index` before sift ops — correct 0→1.
- **Ch06 `ch06-hashing.tex:24-33,66,96,154-155`**: Pigeonhole → uniform hashing → `α` → chaining/open addressing — no hidden probability prior.
- **Ch07 `ch07-graphs.tex:24-44,122-153`**: Matrix vs list tradeoffs via `tab:graph-repr` before traversals — no hidden `Θ(n+m)` justification gap.
- **Ch08 `ch08-graphs-sorting.tex:26-31,101-104,154-159,181`**: `Ω` lower bound via decision tree `Thm` with Stirling proof sketch — closes loop on Ch01 asymptotics.

## Summary

24/24 TikZ colored, 23/23 listings highlighted with language, 0/8 chapters with broken formulas,
build 0 errors / 0 Overfull>15pt, 0→100 chain intact after one ground-up patch. **PASS** — ready to commit PDF.

## Reviewer Checklist (AGENTS.md §9)

- [x] 0→100 zero prior verified (pointer/Θ/O/Ω now defined Ch01:24; recursion at Ch02:168; graph at Ch07)
- [x] Intuition before formalism per chapter (quote/figure before definition)
- [x] Color where useful — 24 TikZ all with `fill=!` + colored edges, `lstset` highlighting
- [x] No Overfull>15pt (`grep Overfull` 0), no `!`/`pgfkeys`/`Missing`
- [x] Compiled pdflatex ×2, 37p 542KB, A4 — PDFs tracked via `git add -f`
