# Ground-Up Audit — SC2001 ch05–08 (Greedy · DP · Graph/String · NP)

Date: 2026-08-23 · Auditor: muse-spark-1.2-contributor
Scope: `chapters/ch05-greedy.tex` (220 L), `ch06-dynamic-programming.tex` (233 L), `ch07-graph-string.tex` (214 L), `ch08-np-completeness.tex` (212 L)
Lens: 0→100 ground-up law — assume ZERO bachelor's knowledge; every term defined on first use; intuition/picture/analogy → formal definition → worked example → proof → exercise. Checklist: (a) hidden bachelor's assumptions, (b) intuition-before-formalism gaps, (c) expansion suggestions with line refs.
Build context: `main.pdf` 45p compiles clean; this audit is content/pedagogy only.

---

## Verdict Summary

| Chapter | Verdict | Rationale |
|---------|---------|-----------|
| ch05 Greedy | **CONDITIONAL PASS — needs 4 intuition blocks** | Correct but 4 formal definitions precede picture; exchange template and Huffman swap assume proof maturity |
| ch06 DP | **PASS with 3 small gaps** | Best 0→100 flow of the four; only recurrence-first ordering and backward-loop rationale need patches |
| ch07 Graph/String | **NEEDS PATCH — 5 intuition gaps** | Highest density of hidden DS assumptions (adj list, heap, mod arithmetic, border); invariants stated before wave picture |
| ch08 NP | **NEEDS PATCH — 4 intuition gaps** | Formal-language / quantifier front-load before find-vs-check analogy; reductions need gadget-first ordering |

No chapter is mathematically wrong. Gaps are pedagogical: a true Year-1 (no discrete math / DS / number theory) reader would stumble at the flagged lines before the formalism.

---

## ch05 — Greedy Algorithms

### (a) Hidden bachelor's assumptions

- **L10 prerequisites:** "priority queues and Union-Find (Ch.3)" assumes heap + DSU semantics. A zero-knowledge reader has not internalised `extractMin` cost or `Find`/`Union` with path compression. Used later at L83–88, L140–154 without re-definition.
- **L47 half-open `[s_i,f_i)`:** interval notation and "compatible = non-overlapping" assumes set/interval literacy. No ground definition of `∩ = ∅`.
- **L58 proof technique:** "maximise longest common prefix with G" is the maximal-counterexample method — assumes comfort with proof by extremal choice / induction on prefix length (bachelor's proof maturity).
- **L77 prefix code:** "no codeword is prefix of another" assumes binary-tree coding model; depth `d_T(c)` used at L78 without defining tree depth via root distance.
- **L125 distinct weights:** "ties broken arbitrarily" assumes understanding that MST uniqueness then follows; tie-breaking as total order not explained.
- **L132 cycle argument:** "unique cycle C must cross cut in another edge" assumes tree+edge = cycle and cut parity — graph-theory lemma not proved or pictured.

### (b) Intuition-before-formalism gaps

- **L29–31 Def. greedy-choice/optimal substructure** appears before any picture or example. Violates intuition→formalism. Should follow a timeline picture.
- **L33–41 Exchange template (boxed)** is abstract before student has seen one concrete exchange (interval instance L67 comes 25 lines later).
- **L103–108 Sibling lemma Δ = (freq(a)-freq(x))(d(a)-d(x)) ≥ 0** — algebra presented as "cannot both be reversed" without numeric swap demo or tree-redraw sequence.
- **L129 Cut property stated as definition** before showing a cut drawing; fig `fig:mst-cut` is 30 lines later.

### (c) Expansion suggestions (line refs + what to add)

1. **Insert before L29 (new §0 intuition, ~10 lines):** `Intuition block: Greedy as "never regret" — analogy: making change with largest coin, then counterexample preview; picture: timeline of intervals stacked, scanning left→right.` Grounds Def. L29.
2. **Insert before L36 (exchange picture, ~8 lines):** `Two-row diagram: G's choices on top, O's below, highlight first divergence r, arrow showing swap o_r → g_r. Caption: "make O look more like G without hurting it."` Precedes boxed template L36.
3. **Expand L106–108 proof (add 6 lines + mini-table):** `Swap walkthrough with numbers: T has a at depth 3 (freq 14) and x at depth 2 (freq 12); swapping saves (14-12)*(3-2)=2. Then state general Δ. Add 2-step tree sketch before/after swap.` Replaces terse "cannot both be reversed".
4. **Insert before L129 (cut picture first, ~7 lines):** `Move conceptual fig:mst-cut intuition paragraph ahead of Def.: "draw S={a,c} as dashed bubble, list 4 crossing edges with weights 1,3,5,6 — which must any MST take?" Then define cut property formally.` Swaps L129↔L158 order pedagogically (keep figure placement, add forward ref).
5. **Annotate L140–154 (2 lines each):** `After Kruskal line "Find(u)!=Find(v)" add parenthetical: "(Find = are u,v already connected? Union = merge components)". After Prim PQ add: "(PQ key = cheapest edge leaving settled set S)".`

**Patch plan ch05 — 4 new paragraphs + 2 annotations = ~31 lines, keeps ≤260 (220+31=251).** Verdict becomes PASS after.

---

## ch06 — Dynamic Programming

### (a) Hidden assumptions

- **L15 longest simple path lacks optimal substructure:** assumes reader knows "simple = no vertex repeated" and why global vertex-reuse forbids local optimality — graph path maturity.
- **L35–42 memo vs tabulation:** assumes dictionary/array, recursion stack, cache locality vocabulary.
- **L163 `pqr` cost:** assumes matrix multiplication cost `p×q` by `q×r` costs `pqr` scalar multiplications — linear-algebra prior.

### (b) Intuition-before-formalism gaps

- **L68–78 LCS recurrence before grid picture:** recurrence `c[i][j]` is defined at L72, but the grid-walk intuition (diagonal = match, up/left = skip) only appears at L86 TikZ. Should be reversed.
- **L121–129 Knapsack recurrence** before backpack-packing analogy; table L137 follows recurrence rather than motivating it.
- **L157 backward loop rationale:** "iterated backwards" stated without showing why forward loop reuses an item twice (unbounded vs 0/1). Needs 1-D array trace picture.
- **L168 matrix-chain `m[i][j]`** formal split `k` before parenthesization tree picture L176.

### (c) Expansion suggestions

1. **Insert before L68 (LCS grid intuition, ~9 lines):** `Picture-first: two strings as axes, grid cell (i,j)=prefix pair; arrow meanings: ↖ = take match, ↑/← = drop one char. Then derive recurrence as exhaustive case split. Relocate current L80 sentence "depends on three neighbours" into this block.`
2. **Insert before L121 (knapsack story, ~6 lines):** `Analogy: backpack weight limit W, items = souvenirs with weight/value; decision at each item = take or skip; remaining capacity shrinks. Then formalise K[i][w].`
3. **Expand L157 (backward-loop picture, ~7 lines + tiny table):** `Show 1-D array [0..5] forward bug: taking item 1 twice because dp[w] already updated in same i iteration. Contrast backward scan preserving previous row's values. Add 2-row trace for W=5 taking item (2,3).`
4. **Insert before L168 (matrix chain tree first, ~5 lines):** `Show 3 matrices A1·A2·A3 with two parenthesisations and costs 12000 vs 4500 (numbers from L173) as tree sketches, then ask "which split k gives min?" leading to min_k.`

**Patch plan ch06 — 3 intuition blocks + 1 annotation = ~27 lines (233+27=260 exactly).** Smallest patch set.

---

## ch07 — Graph Traversal, Shortest Paths, String Matching

### (a) Hidden assumptions

- **L26–27 adjacency list vs matrix:** assumes DS representation tradeoffs (`Θ(n²)` scan) without defining either. Bachelor's DS assumed.
- **L31 FIFO queue / L73 LIFO stack + recursion:** assumes queue/stack semantics; "recursion as stack" not unpacked for zero-knowledge.
- **L77 discovery/finish times + parenthesis theorem:** assumes DFS timestamp model; intervals `[d[u],f[u]]` nested/disjoint stated without picture.
- **L88 `w: E→ℝ`, `δ(s,v) = -∞` for negative cycle, `∞` for unreachable:** assumes real weights, extended reals, and negative-cycle semantics in one dense line.
- **L95 heap `ExtractMin/DecreaseKey`:** assumes binary-heap operations without prior definition (Ch2 heap assumed but not re-grounded).
- **L146 KMP border `π[q]` :** assumes longest proper border / prefix-suffix concept; highly non-trivial for first exposure.
- **L183 base-b mod q rolling hash:** assumes modular arithmetic, Horner's rule, base representation — number-theory prior.

### (b) Intuition-before-formalism gaps

- **L33 BFS pseudocode before wave picture:** code at L33, but layering/wave intuition at L43 comes after. Should show pond ripple first.
- **L43 layering invariant "Q contains at most two consecutive distances"** stated formally before explaining why FIFO enforces it.
- **L105–109 Dijkstra invariant (I)** is a two-quantifier statement before any "expanding frontier / settled vs frontier" picture.
- **L112 Bellman-Ford "n-1 rounds"** before explaining that any shortest simple path has ≤ n-1 edges (pigeonhole) — reason for n-1 not motivated.
- **L127 Floyd `d^{(k)}[i,j]`** double-index definition before illustrating "allow vertex k as intermediate" picture (k = new hub).
- **L148 π-while loop before border picture:** `while k>0 ∧ P[q]≠P[k+1] do k←π[k]` appears without first showing a failed partial match falling back along borders (e.g., `abab` example).

### (c) Expansion suggestions

1. **Insert before L29 (BFS wave analogy, ~8 lines):** `Picture: drop stone at s, circular waves = layers B0,B1,B2; queue = line of people in order waves were reached. Then define BFS as wave expansion. Keep fig:bfs-tree but add forward ref "see wave diagram Fig.".`
2. **Insert before L72 (DFS commitment analogy, ~6 lines):** `Analogy block: BFS = fair host (visits all neighbours equally), DFS = explorer who commits down one tunnel before backtracking; stack = pile of breadcrumbs. Then give iterative vs recursive views side-by-side.`
3. **Insert before L91 (Dijkstra picture, ~10 lines):** `Settled set S as growing safe zone; frontier edges as doorways with tentative distances; ExtractMin = closest doorway is safe because any alternative detour via negative? No, weights ≥0 so detour cannot be shorter — picture with triangle inequality. Then state invariant (I) as "S = proven, V\S = best via S".`
4. **Expand L112–118 (Bellman-Ford motivation, ~8 lines):** `Intuition: after 1 round you know 1-edge best, after 2 rounds 2-edge best, … After n-1 rounds any simple path exhausted; extra round = can still improve ⇒ cycle you can loop forever for profit (negative cycle as money loop). Tie to example L120 before code.`
5. **Insert before L126 (Floyd hub picture, ~6 lines):** `Diagram: k as new airport hub; either best path avoids hub (old value) or goes through hub (i→k + k→j). In-place safety sentence already at L132 — expand with "k-th row/column frozen" illustration.`
6. **Insert before L146 (KMP border picture, ~9 lines):** `Show pattern P=abab with borders: prefix "ab" = suffix "ab"; on mismatch at position 4, you don't restart at 0 but slide to longest border length π[3]=1. Draw prefix/suffix underbrace before giving π definition and while loop.`

**Patch plan ch07 — 6 intuition blocks = ~47 lines (214+47=261 → trim 1 line elsewhere, or place Floyd hub as 5-line note to stay ≤260).** Highest priority.

---

## ch08 — NP-Completeness

### (a) Hidden assumptions

- **L26 language `L ⊆ {0,1}*`:** assumes formal languages, binary encoding of instances, decision vs optimisation distinction — heavy for zero bachelor's (prerequisites line L11 insufficient).
- **L30 polynomial time `O(n^c)`:** assumes RAM/Turing model and asymptotic polynomial vs exponential gap already internalised.
- **L37 verifier quantifiers `∃c |c|≤p(|x|) ∧ V(x,c)=1`:** first-order logic with polynomial bound — assumes quantifier/ polynomial notation maturity; witness size bound motivation ("without bound every decidable language trivially in NP") relegated to comment L55.
- **L46 coNP complement:** assumes complement operation and duality; example UNSAT correctly shows "no"-certificate not obviously short.
- **L62 reduction `f` polynomial-time computable:** assumes function-computability + instance transformation idea; transitivity (L74) assumes composition knowledge.
- **L128 maximal matching:** matching defined in passing ("disjoint edges") but not as formal definition with picture; lower-bound argument assumes it instantly.
- **L138 pigeonhole "some set covers ≥ n/k":** assumes averaging argument.

### (b) Intuition-before-formalism gaps

- **L29 P definition before intuition:** formal `P` at L29, but grounding examples (sorting, BFS, Dijkstra are in P) at L34 come after. Find-vs-check analogy at L56 should precede both P and NP definitions (currently after).
- **L62 reduction before gadget picture:** reduction definition at L62, but reduction-chain intuition (translate Sudoku → SAT, hardness flows) appears only at Fig. `fig:reduction-chain` L101, 40 lines later.
- **L77 clause splitting formula before gadget:** algebraic split at L78 before example L83; reader sees `y_i` fresh variables without knowing gadget purpose (break long clause into 3-literal pieces while preserving satisfiability).
- **L88 Clique construction "Add edges between all pairs except…"** is inverted phrasing (lists omitted edges rather than included) — construction before drawing triangle-per-clause picture.
- **L132 maximal vs maximum matching** distinction stated in one line L135 ("No need to find maximum") without illustrating maximal-but-not-maximum example (path of length 3).

### (c) Expansion suggestions

1. **Insert before L26 (encoding + find vs check story, ~10 lines):** `Grounding block: every input is a binary string (encode graph as adjacency list, formula as bits); decision problem = yes/no question. Then find-vs-check analogy FIRST: P = you can FIND answer fast; NP = someone gives you a hint (certificate) you can CHECK fast (Sudoku hint, jigsaw). Then give verifier definition. Move L56 sentences up, keep formal quantifiers after.`
2. **Insert before L58 (reduction analogy, ~8 lines):** `Picture: two islands A and B, bridge f translates any A-puzzle into B-puzzle; if you can solve B, you solve A via bridge + one call. Label cost = polynomial. Then formalise A ≤_p B at L62. Add forward ref to chain fig.`
3. **Expand L77–85 (clause gadget first, ~7 lines):** `Before formula, draw original 4-literal clause as long OR, then gadget chain: (l1∨l2∨y1) ∧ (¬y1∨l3∨y2) ∧ … Show y's as switches that propagate truth; state invariant "y_i must be…". Then state size O(|x|) and satisfiability iff.`
4. **Rewrite L88–89 (Clique gadget picture first, ~6 lines + clarify):** `Reword to constructive: "Make triangle per clause (3 vertices per clause, fully connected). Then connect EVERY compatible literal across triangles; OMIT edge iff literals conflict (x vs ¬x)." Add tiny 2-clause example diagram before full 3m construction. Remove "except (i)…(ii)" inversion.`
5. **Expand L128–136 (matching picture, ~7 lines):** `Show path a—b—c—d: maximal matching {a-b} leaves edge c-d uncovered? Actually maximal means can't add more; illustrate {b-c} is maximal but not maximum on 4-vertex path. Then prove lower bound OPT ≥ |M| with picture of disjoint edges each needing distinct cover vertex.`
6. **Annotate L138 (charging, ~3 lines):** `After "shrinks geometrically" add: "If k sets suffice, average set covers n/k uncovered; best set does at least that well — pigeonhole." Then state H_n bound.`

**Patch plan ch08 — 5 intuition blocks + 1 rewrite = ~41 lines (212+41=253).**

---

## Global Patch Plan (propose, do NOT apply yet)

Order by pedagogical impact:

1. **ch07 #3 Dijkstra frontier picture (L91)** + **ch05 #2 exchange diagram (L36)** — highest leverage; both invariants currently formal-first.
2. **ch08 #1 find-vs-check before quantifiers (L26)** + **ch05 #1 greedy timeline (L29)** — establish intuition-first law.
3. **ch06 #1 LCS grid-first (L68)** + **ch07 #6 KMP border (L146)** — recurrence/automaton comprehension.
4. **ch07 #4 Bellman-Ford n-1 motivation (L112)** + **ch06 #3 backward loop (L157)** — prevent mechanical memorisation.
5. **ch08 #4–5 gadget clarification (L88, L128)** + **ch05 #3 Huffman swap numbers (L106)** — reduce "except" confusion and Δ tedium.

**Insertion mechanics:** All blocks are `> \begin{remark}[Intuition]` or `> \paragraph{Intuition.}` + `tikz`/`quote` as needed; no existing proof or theorem text deleted, only added before/after. Line counts above keep each chapter ≤260 after patches (ch07 needs 1-line trim elsewhere, e.g., shorten L133 remark).

**No file patched in this audit — plan only.** Next step (separate task) to implement blocks and re-verify `pdflatex` + colour-fill + `Overfull>15pt`.

---

*Auditor note: Compared to `REVIEW-v2-ch05-08.md` (visual QA PASS) and `REVIEW-ch05-08.md` (adversarial PASS), this ground-up audit does not contradict correctness or build gates; it adds the 0→100 lens that those reviews did not assess. Overlap with prior minor nits (sibling lemma wording L107, Clique phrasing L88, Floyd in-place L132) is intentional — this audit promotes them from "optional polish" to "required ground-up intuition block".*
