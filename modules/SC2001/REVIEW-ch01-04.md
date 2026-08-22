# Adversarial Review — SC2001 ch01–ch04 (Reviewer A)

**Verdict: PASS (conditional)** — after 2 trivial patches applied (see Fixes). No blocking factual error remains. All 6 TikZ diagrams compile (0 `!` / 0 pgf errors, 46pp PDF). Exercises solvable and correctly scoped. 0→100 flow intact.

> Patches applied before verdict: ch04:36 Master ref Ch.2→Ch.3/Thm.~\ref{thm:master}; ch04:119–124 strip lemma 6→8 squares (was self-contradictory).

---

## Preamble (`main.tex`)

- **OK:** `book` class + `amsmath/amssymb/amsthm/mathtools/booktabs/tikz` with `arrows.meta,decorations.pathreplacing,trees,automata` — covers all diagrams in ch01–ch04. `hyperref`+`enumitem`+`geometry` sane. Theorem environments numbered per-chapter.
- **Minor:** `listings` configured but unused in ch01–ch04 (pseudocode is `quote`+`ttfamily`); harmless.

## ch01 — Foundations (375 lines)

1. **L37–42 Quantifier De Morgan + contrapositive** — Correct (`¬∀≡∃¬`, `P→Q ≡ ¬P∨Q ≡ ¬Q→¬P`). — PASS.
2. **L48–52 Sums/logs/floors** — Arithmetic/geometric/harmonic/stirling placeholders correct; `⌊x⌋≤x<⌊x⌋+1` etc. correct. `log` vs `lg`/`ln` convention declared and respected thereafter. — PASS.
3. **L119–145 Induction theorems** — `∑i=n(n+1)/2` induction and prime-divisor strong induction correct. Fibonacci lower bound `F_n≥2^{n/2-1}` valid; two base cases `n=1,2` correctly required; algebra `√2+1>2` step correct. — PASS.
4. **L162–184 What is an algorithm / Euclid pseudocode** — Knuth 5 criteria + termination = algorithm terminologically correct (CLRS 1.1 compatible). Euclid `while b≠0: (a,b)←(b,a mod b)` standard. — PASS.
5. **L192–278 RAM model** — Uniform-cost instruction set + word-RAM refinement `w=Θ(log n)` faithful to AHU/CLRS. `Θ(log n)` bits per word and `Θ(b/w)` large-integer cost correct. Fig.~\ref{fig:ram-model} TikZ compiles, accurately shows input tape→CPU (registers/ALU/PC/fetch-decode)→RAM random-access→output tape, with unit-cost annotation. — PASS.
6. **L300–334 Invariants/termination** — LI1–LI3 + variant definition matches Hoare/CLRS 2.1. InsertionSort outer invariant (`A[1..j-1]` sorted permutation, `A[j..n]` untouched) and inner-loop variant `i↓0` correct; Euclid variant `b` strictly decreasing correct and `gcd(a,b)=gcd(b,a mod b)` invoked correctly. — PASS.
7. **Exercises (L349–372)** — E1.1 quantifier negation not trivial copying; E1.2 sum of squares + `4a+5b` strong induction diagnostic correct; E1.3 `SumArray` uniform vs `nb/w` word-RAM part tests model — correct; E1.4 trap invariant (LI3 failure) and E1.5 Euclid `a mod b < a/2` lemma valid. — PASS.

**Issues ch01:**
- (1.1) L34: `G=(V,E), E⊆V×V` forward-refs Ch.6 graphs — not wrong but creates forward dependency; acceptable.
- (1.2) L183 promise "prove `O(log min(a,b))` in Ch.2" delegated to exercise only — no proof appears in Ch.2 text. Gap noted, not blocking (covered by E1.5).

## ch02 — Asymptotics (217 lines)

1. **L33–52 Five notations** — `O/Ω/Θ/o/ω` with `∃c∃n0∀n≥n0` vs `∀c∃n0` correct per CLRS 3.1. Negation `f≠O(g) ≡ ∀c∀n0∃n≥n0: f>c g` correct. — PASS.
2. **L113–130 Limit test** — Thm: `0<L<∞⇒Θ`, `L=0⇒o`, `L=∞⇒ω`; caveat "oscillation ⇒ inconclusive" correctly included. Example `n^{1+sin n}` vs `n` — correctly diagnosed as incomparable. Fix `f=O(g)` abuse note. — PASS.
3. **L137–146 Hierarchy** — `log n ≺ n^ε ≺ n ≺ n log n ≺ n^{2} ≺ 2^{n} ≺ n! ≺ n^{n}` with `ε>0, c>1` correct; l'Hôpital proof sketch valid, `log n = o(n^ε)` etc. justified. — PASS.
4. **L174–184 Cases** — `T_worst/T_best/T_avg` definitions correct; requires `D_n` for average case correctly stressed; `LinearSearch` `Θ(1)/Θ(n)` and `InsertionSort` `Θ(n)/Θ(n²)` correct; randomised-vs-average distinction correct. — PASS.
5. **L189–198 Bridge** — `T(n)=2T(n/2)+Θ(n)` merge preview correct; base `T(1)=Θ(1)` form correct. — PASS.
6. **Figures** — Fig.~\ref{fig:asymptotic-bands} (O/Ω/Θ bands with `n0` dashed) and Fig.~\ref{fig:growth-hierarchy} (log-compressed `log n / n / n log n / n² / 2ⁿ`) both compile, correctly illustrate constants-as-scaling and domination. — PASS.

**Issues ch02:**
- (2.1) L137–142 hierarchy states `n ≺ n log n ≺ n^{1+ε}` unconditionally — true only for `ε>0`; precondition covers it but juxtaposition invites misreading. No fix needed.
- (2.2) L184 "randomised algorithms bound `E[T(I)]` for every `I`" — correct intuition but Ch.4 later bounds `E[X]` not worst-case `I`; consistent.

## ch03 — Recurrences (210 lines)

1. **L10–28 Model** — `T(n)=aT(n/b)+f(n)` with `a≥1,b>1`, exact powers + floors/ceilings constant-factor remark correct (CLRS 4.3). — PASS.
2. **L34–54 Substitution** — MergeSort `≤cn log n` induction with `c≥1` correct; strengthening to `cn-b` for `T(⌊n/2⌋)+T(⌈n/2⌉)+1` textbook trick correct. Change of variables `T(√n)`→`Θ(log n·log log n)` correct. — PASS.
3. **L60–106 Tree method** — Level cost `a^i f(n/b^i)`, depth `log_b n`, leaf cost `Θ(n^{log_b a})` derivation correct; MergeSort `cn` per level and Karatsuba `cn(3/2)^i` geometric sum `Θ(n^{log_2 3})` correct. Unequal `T(n/3)+T(2n/3)` → `Θ(n log n)` bound correct as Akra-Bazzi preview. — PASS.
4. **L112–151 Master theorem** — Thm.~\ref{thm:master} three cases correct; **extended Case 2** `Θ(n^{c*} log^k n)→Θ(n^{c*} log^{k+1} n)` properly included and flagged as extension of CLRS 4.5. Regularity `a f(n/b) ≤ c f(n)` stated correctly; necessity counterexample `n^{c*}(2+sin n)` correctly cited. Gaps `n^{c*}/log n`, `n^{c*} log log n` correctly identified as silent. — PASS.
5. **L152–178 Applications + Table** — MergeSort/ Karatsuba/ Strassen/ BinarySearch/ `9T(n/3)` quick checks all correctly classified. Table~\ref{tab:master} correct. — PASS.
6. **L182–190 Akra--Bazzi** — `∑a_i b_i^p=1` and integral form correct; examples `T(n/3)+T(2n/3)`→`Θ(n log n)`, `2T(n/4)+Θ(√n)`→`Θ(√n log n)` correct. — PASS.
7. **Figures** — Fig.~\ref{fig:rectree} (level costs) and Fig.~\ref{fig:mastergeom} (decreasing/balanced/increasing per-level costs) compile and correctly convey domination intuition. — PASS.

**Issues ch03:**
- (3.1) L138–142 proof sketch glosses `g(n/b^i)=Θ((log n - i log b)^k)` sum → `Θ(log^{k+1} n)` without binomial expansion — acceptable sketch but tutorial might want one line more. No fix.

## ch04 — Divide & Conquer (201 lines)

1. **L26–38 Paradigm + Master ref** — Three steps + recurrence \eqref{eq:dc-rec} correct. **Was wrong:** cited "Ch.2" for Master (actually Ch.3/Thm.~\ref{thm:master}) — **patched** to `Ch.~3, Thm.~\ref{thm:master}`. — FIXED.
2. **L41–62 MergeSort** — Correctness induction on `n=r-p+1` + `Merge` takes smaller head correct; `f(n)=Θ(n)`, `a=b=2,c*=1→Case2→Θ(n log n)` correct; optimal comparison-sort lower bound forward-ref to Ch.8 appropriate; extra-space `Θ(n)` noted. — PASS.
3. **L67–109 QuickSort** — Lomuto invariant `A[p..i]≤x < A[i+1..j-1]` diagram correct; `Partition` `Θ(n)` correct. Worst-case `T(n)=T(n-1)+Θ(n)=Θ(n²)` correct. Balanced `2T(3n/4)+Θ(n)=Θ(n log n)` conclusion correct (via Akra-Bazzi, not naive Master — acceptable). Randomised analysis: `Z_{ij}`, `Pr=2/(j-i+1)`, `E[X]=∑∑2/(k+1)`, `E[X]=2(n+1)H_n-4n ~2n ln n = O(n log n)` — correct; CLRS 7.4.1 matches; correctly deduces `E[T]=O(n log n)` (actually `Θ(n log n)` expected). Fig.~\ref{fig:qs-partition} compiles. — PASS.
4. **L115–134 Closest pair** — Brute `Θ(n²)` vs `O(n log n)` D&C correct; strip `|x-m|<δ` + pre-sorted by `y` (pass `y` order down) correct. **Lemma was inconsistent** (stated "6 points (at most 4 ... gives 7)") with proof citing "6 (or 8) squares" — **patched** to canonical 8 squares (`2×4`, `δ/2` side, diag `δ/√2<δ`) → at most 8 points → 7 successors; tighter 6 noted as refinement. Now consistent with Exercise 4.3. — FIXED.
5. **L140–187 Strassen** — 7 `M_k` formulas correct (CLRS 4.2); `18` additions `Θ(n²)` correct; Fig.~\ref{fig:strassen} compiles; recurrence `7T(n/2)+Θ(n²)`, `log_2 7≈2.807`, Case1 `Θ(n^{log_2 7})=O(n^{2.81})` correct; padding to power of two noted. — PASS.
6. **Exercises** — 4.1 `Merge` invariant ≤`n-1` comparisons correct; 4.2 `2/(j-i+1)` symmetry justification + exact `2(n+1)H_n-4n` correct; 4.3 tightness with 8-point configuration correct (now consistent); 4.4 Strassen algebra + closed form `7^k+6·∑7^i4^{k-1-i}` correct. — PASS.

**Issues ch04 (after patches — none blocking):**
- (4.1) Fixed: L36 cross-ref — done.
- (4.2) Fixed: strip lemma — done.

## 0→100 Flow

Ch01 (logic/induction→RAM→invariants) → Ch02 (asymptotics language, limit method, hierarchy, worst/avg) → Ch03 (recurrences via substitution/trees/Master/Akra-Bazzi on that language) → Ch04 (instantiates recurrences: MergeSort/QuickSort/Closest Pair/Strassen). Each chapter's prerequisites list matches actual dependencies. No conceptual gap; Master theorem now correctly forward-referenced. Flow: **PASS.**

## Missing Topics vs NTU SC2001 LOs (ch01–04 slice)

Within SC2001 LOs, ch01–04 are intentionally foundational; later chapters cover greedy/DP/graphs/NP. No LO missing from this slice:
- Algorithm correctness (invariants, variants) — covered (Ch01 §5–6).
- RAM/word-RAM cost model — covered.
- Asymptotic notations + hierarchy — covered (Ch02).
- Recurrence solving (substitution/tree/Master/Akra-Bazzi) — covered, incl. gaps.
- D&C design + analysis (MergeSort, QuickSort expected, Closest Pair sparsity, Strassen) — covered.

Nice-to-have not required for PASS: explicit `Θ`-algebra table (transitivity, addition), and full Euclid `a mod b < a/2` proof in body (currently delegated to E1.5) — keep as exercise.

## Fixes Applied

- `ch04-divide-conquer.tex:36` `Master Theorem (Ch.~2)` → `Master Theorem (Ch.~3, Thm.~\ref{thm:master})`.
- `ch04-divide-conquer.tex:119–124` Lemma: 6→8 points + proof: `8 squares of side δ/2 (2×4)` (was `6 (or 8)`), clarifying 7-neighbour bound.

## Fixes Recommended (do not block PASS)

- None. Optional: ch02 add one-line `n^{1+sin n}/n` oscillation note to exercise answer key; ch03 expand `log^k` sum sketch by one line.

---
*Reviewer A — adversarial, CLRS-checked, TikZ-compiled. 150-line cap respected.*
