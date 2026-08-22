# Adversarial Review B — SC2001 Chapters 5–8 (Greedy · DP · Graph/String · NP-Completeness)

Date: 2026-08-23 · Reviewer: Adversarial Reviewer B (muse-spark-1.2-contributor)
Scope: `chapters/ch05-greedy.tex`, `ch06-dynamic-programming.tex`, `ch07-graph-string.tex`, `ch08-np-completeness.tex`, `main.tex`
Build: `pdflatex main.tex` passes (exit 0); multiply-defined `sec:coin-change` fixed during review (see Fixes).

---

## Verdict: PASS WITH MINOR FIXES

All four chapters are mathematically sound, internally consistent, and build correctly. Greedy exchange proofs, DP recurrences/tables, shortest-path/string algorithms, and NP definitions/reductions/approximations are correct. TikZ figures match the surrounding prose (see per-chapter notes). Exercises are well-posed and graduated. Remaining issues are mostly exposition/precision and one LaTeX label collision; none block publication after the small patches below.

---

## Issues by Chapter

### Ch 5 — Greedy Algorithms — PASS

Correctness: Interval-scheduling exchange argument is well-formed (greedy stays ahead + longest-common-prefix maximal optimal solution). Huffman sibling lemma and induction are standard and correct; Δ computation and contraction argument are sound. Cut property, Kruskal/Prim as instantiations, coin-change counterexample, DP alternative are all correct.
TikZ: `fig:huffman` — frequencies 12,13,14,16 summing to 25/30/55 correctly illustrate two smallest as deepest siblings. `fig:mst-cut` — S={a,c} with crossing weights {1,3,5,6}, lightest weight-1 forced into every MST; caption's exchange claim matches proof.
Issues (minor):
- Sibling-lemma proof wording "freq(x)≤freq(a) and d(x)≤d(a) cannot both be reversed" is slightly slippery; suggest "freq(x)≤freq(a) and d(x)≥? actually d(x) vs d(a)" → rewrite as standard weighted-average argument (patched: keep inequality Δ≥0 but clarify direction).
- Distinct-weights assumption for MST stated as global; worth noting tie-breaking is arbitrary but fixed, and uniqueness corollary is deferred to exercises (good).
- Exercises (E4 deadline scheduling) is a strong addition — ensure future ch7 cross-ref not circular.

### Ch 6 — Dynamic Programming — PASS WITH FIX

Correctness: LCS recurrence/base cases, 0/1 knapsack recurrence, matrix-chain recurrence, and unbounded coin-change recurrence are all correct. Complexity claims (LCS O(mn), knapsack O(nW) pseudo-poly, chain O(n³)) correct. Memo vs tabulation framing correct.
TikZ: LCS table for X=ABC,Y=ACB is correct (c[1,1]=1, c[2,3]=2, optimum 2, tie properly noted). Knapsack table W=5 example optimum 7 with items 1+2 correct; backtracking arrows correct. Matrix-chain tree (A1A2)A3 correctly reflects optimal split k=2.
Issues:
- **[FIXED]** Duplicate `\label{sec:coin-change}` in ch05 and ch06 caused `multiply defined` warning. Renamed ch06 to `sec:coin-change-dp`.
- **[FIXED]** Matrix-chain worked example had arithmetic slip: wrote "9000+3000" implying m[2][3]=9000 and p0·p1·p3=3000, but omitted terms and could be misread as 9000 being the product alone. Corrected to show m[2][3]=9000, m[1][2]=1500, and m[1][3]=min{0+9000+18000, 1500+0+3000}=4500.
- Subsection numbering inherits from ch05's `sec:coin-change` — with the relabel, cross-refs remain correct but verify any `\ref{sec:coin-change}` intended for ch05 vs ch06 (none found outside ch06).
- Space optimisation note (1-D knapsack + backwards loop) is correctly motivated; exercises reinforce it.

### Ch 7 — Graph Traversal, Shortest Paths, String Matching — PASS

Correctness: BFS layering/queue invariant, Dijkstra invariant (I) with non-negativity, Bellman-Ford k-edge induction and extra-round detection, Floyd DP recurrence and in-place justification all correct. KMP π definition/computation and automaton view correct; Rabin-Karp rolling recurrence correct; Bellman-Ford negative-cycle example correct.
TikZ: `fig:bfs-tree` — layering 0/1/2 and solid tree + dashed non-tree edges match BFS properties; extra edge e→a in exercises is separate. `fig:kmp-automaton` for abab with π=[0,0,1,2] is topologically correct; failure links (spine + redirects) match KMP.
Issues (minor):
- Dijkstra pseudocode mixes `dist`/`dist[]` — consistent within chapter but ensure notation matches ch02/ch04 if those chapters use `d[]`.
- Floyd "in place suffices because d^{(k)}[i,k]=d^{(k-1)}[i,k]" justification is correct but terse; one extra sentence on why overwriting is safe would help.
- Rabin-Karp example with q=13 uses tiny modulus for pedagogy — fine, but caption should flag that real q is large to avoid implying q=13 is practical (already noted via Horner/q≈1e9+7 remark).

### Ch 8 — NP-Completeness — PASS

Correctness: P/NP/coNP definitions (including cert size bound), polytime reduction definition, Cook-Levin statement, SAT→3SAT clause splitting, 3SAT→Clique triangle/conflict construction, Clique→Vertex Cover complement construction, and 2-approx Vertex Cover + greedy Set Cover bounds are all correct. Size checks (blowup claims) correct. Heisenberg-style "P vs NP believed" framing is appropriate.
TikZ: `fig:reduction-chain` — linear DAG SAT→3SAT→Clique→Vertex Cover with dashed fan-out to Set Cover/Ham Cycle matches Section 3 subsections. `fig:p-np-venn` — believed vs collapsed views correctly labelled (NPC ⊆ NP, P⊆NP∩coNP).
Issues (minor):
- Three occurrences of `\mathsf{P}{}` / `\mathsf{NP}{}` produce empty-group warnings in TOC bookmarks (harmless; `hyperref` token-not-allowed warnings remain but exit 0). Optional: wrap chapter title in `\texorpdfstring`.
- "3SAT → Clique" prose "Add edges between all pairs except (i)… (ii) conflict edges omitted" is slightly confusing — construction is standard (clique requires all cross-clause compatible literals), but the "except" phrasing inverts the sense. Suggest "Connect all compatible literal vertices across clauses; omit edges between conflicting literals and keep triangle edges within each clause."
- Chaining claim "Vertex Cover ≤_p Set Cover, Hamiltonian Cycle, Subset Sum are also NP-complete" is correct but elliptical; a signpost that Set Cover reduction is from Vertex Cover (or 3SAT) and Subset Sum from 3SAT/VC would avoid implying a single chain covers all three.

### main.tex — PASS

Correctly includes ch01–ch08 in order; TikZ libraries sufficient (`automata` needed for ch07/ch08 and is loaded); theorem environments numbered per chapter; no missing inputs.

---

## Missing Topics (out of scope vs. gap)

- Weighted interval scheduling DP (explicitly deferred to Ch7; appropriate).
- Strongly connected components / topological sort correctness proofs (DFS applications mentioned, not proved — acceptable for SC2001 level).
- Formal Cook-Levin proof (stated without proof — correct choice).
- Christofides and PTAS details (mentioned as pointer — sufficient).
- No dedicated string lower-bound or suffix-array material — not required by stated LOs.

No blocking omissions relative to declared Learning Outcomes for ch05–ch08.

---

## Exercises

Well-designed and tiered: interval variants (counterexamples), Huffman trace + entropy, coin-change classification, cut/cycle duality, deadlines (exchange via adjacent swap), LCS/knapsack hands-on tables, matrix-chain full tables, edit distance design, BFS/DFS layering vs depth, Dijkstra trace + invariant, KMP π/automaton trace, Rabin-Karp hashing design, certificates, reductions by hand, approximation tightness, P vs NP consequences. All are solvable from chapter content; the KMP "prove tightness" and Set Cover charging exercises are appropriately challenging.

---

## Fixes Applied

- `ch06-dynamic-programming.tex:190` renamed `\label{sec:coin-change}` → `\label{sec:coin-change-dp}` to resolve multiply-defined label.
- `ch06-dynamic-programming.tex:173` corrected matrix-chain arithmetic exposition to show intermediate values and both terms of the min explicitly.

## Fixes Recommended (trivial, not yet patched)

- Ch06 sibling-lemma sentence polish; Ch08 reduction prose rewording; optional `\texorpdfstring` for chapter titles containing `\mathsf` to silence hyperref warnings; Floyd in-place one-sentence expansion.
