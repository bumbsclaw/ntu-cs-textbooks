# Audit — SC2001 Ch01–04 Ground-Up Gaps (0→100: Zero Bachelor Prior)

**Repo:** `ntu-cs-textbooks` @ `9b1ad10` · **Date:** 2026-08-23 SGT
**Invariant:** 0→100 — assume *no* discrete math / data structures / programming; intuition + picture before formalism; thorough not verbose.
**Scope:** `ch01-foundations.tex` (378L), `ch02-asymptotics.tex` (221L), `ch03-recurrences.tex` (220L), `ch04-divide-conquer.tex` (220L)
**Method:** Read openings, first definitions, first examples per chapter; flag assumptions vs. first-principles buildup.

## Verdict Summary

| Ch | Title | Verdict | Severity |
|----|-------|---------|----------|
| 01 | Foundations | **NEEDS EXPANSION** | High — "refresher" framing contradicts 0→100 |
| 02 | Asymptotics | **NEEDS EXPANSION** | Medium-High — formalism precedes picture; calculus/probability assumed |
| 03 | Recurrences | **NEEDS EXPANSION** | High — Master/Akra-Bazzi machinery has steep prior slope |
| 04 | Divide & Conquer | **NEEDS EXPANSION** | Medium — QuickSort expectation + Strassen algebra assume maturity |

> None of ch01–04 is SUFFICIENT as-is for a literal zero-prior reader. Ch02 is closest after the band figure; ch01 and ch03 need the most added scaffolding.

---

## Ch01 — Foundations (ch01-foundations.tex)

**Verdict: NEEDS EXPANSION**

### (a) Assumed bachelor's knowledge without first-principles buildup

- **L11, L27:** "assume the maturity of MH1812/SC1007 … This is not a substitute for MH1812, but a compact reference" — directly violates 0→100. Reader with no sets/proofs/induction is told to skim.
- **L30–34 Sets/Functions/Relations:** Injective/surjective/bijective (L32), reflexive/symmetric/transitive/antisymmetric + equivalence/partial order, graph `G=(V,E)⊆V×V` with "assume familiarity with paths, cycles, trees from SC1007" — all delivered as notation dump, no construction from examples.
- **L36–42 Logic & quantifiers:** `¬,∧,∨,⇒,⇔`, `∀/∃`, De Morgan `¬∀≡∃¬` given as facts; no prior on proposition vs. predicate, no everyday-language bridge.
- **L44–53 Sums/Products/Logs:** "We use freely:" then arithmetic/geometric/harmonic (`γ≈0.5772`), `log₂ vs ln vs lg`, change-of-base `Θ(log_b n)`, floors/ceilings, `n! ≤ nⁿ` — assumes Σ-notation fluency, log fluency, factorial asymptotics.
- **L63–104, L106–156 Proof techniques & induction:** Weak/strong/structural induction stated as proof schemas; structural induction on `Leaf/Node(L,x,R)` (L150) assumes ADTs/trees.
- **L159–184 What is an algorithm + Euclid:** "effectiveness," program vs. algorithm, 1-indexed pseudocode, `a mod b` — assumes programming maturity; Euclid presented before loop-invariant machinery that proves it.

### (b) Formalism precedes intuition / picture

- **L30–35:** Formal set/function/relation definitions first; no Venn diagram, no arrow-diagram for functions, no picture of relation as directed graph before the taxonomy.
- **L37–42:** Quantifier De Morgan laws as symbolic equivalences before any "for every … there exists …" story or picture.
- **L44–53:** Formula list before any motivating sum (e.g., handshake count, doubling) that shows *why* we need closed forms.
- **L303–313 Loop invariant (LI1)–(LI3):** Formal predicate + three numbered obligations before the "boundary picture" (what's done / remains / boundary). The intuition sentence "Think of I as IH travelling around the loop" (L311) comes *after* the definition.

### (c) Expansion suggestions (with line refs)

1. **L11 + L27 — Rewrite prerequisite framing:** Replace "refresher / not a substitute" box with "From zero: we build sets, functions, logic, and induction here; no MH1812/SC1007 needed" and gate later chapters on it. (1 paragraph, remove SC1007 pointer.)
2. **L30–34 — Insert pictures before definitions:** Add 2 TikZ figures *before* L30: (i) Venn + element dots for `∈,⊆,|S|`, (ii) arrow diagram domain→codomain for injective vs. non-injective. Define relation properties each with a 2–3-node digraph example after.
3. **L36–42 — Quantifiers intuition-first:** Prepend Everyday example ("Every student passed …" already in E1.1) → picture of domain dots all satisfying P vs. one counterexample → then formal `∀/∃` and De Morgan as "swap and flip."
4. **L44–53 — Derive, don't list:** For each bullet add 3-line derivation/intuition box: pairing for `n(n+1)/2` (Gauss picture), geometric as binary-tree leaves, harmonic as "coupon/stack of blocks" with integral test sketch, log base-change via ruler analogy, floors as "off-by-one ≤1" number-line figure.
5. **L303–342 — Flip invariant order:** Move "Recipe" (L339) and a concrete array-barrier TikZ (sorted prefix | unsorted suffix) *before* Def L303; state invariant in words first ("first j-1 slots already sorted"), then formalize (LI1)–(LI3) and variant.

---

## Ch02 — Asymptotics (ch02-asymptotics.tex)

**Verdict: NEEDS EXPANSION**

### (a) Assumed bachelor's knowledge

- **L25–28 Why asymptotics:** `T(n)=Σ cost_i·count_i(n)` and "eventually non-negative" `∃n₀∀n≥n₀` assume RAM cost model + quantifier maturity from ch01.
- **L33–55 Five notations:** `∃c∃n₀∀n≥n₀` vs. `∀c∃n₀∀n≥n₀` gap (L53–55) assumes logic maturity; `f=O(g)` as set abuse (L54) assumes set membership comfort.
- **L109–131 Limit method:** L'Hôpital, `lim f/g ∈ ℝ∪{∞}`, oscillation example `n^{1+sin n}` (L128) assume calculus (limits, continuity, trig oscillation) not built from zero.
- **L134–146 Hierarchy:** `ε>0, c>1` hierarchy (L138–141) and sketch "apply l'Hôpital k times + transitivity of o" (L145) assume real analysis.
- **L180–188 Best/worst/average:** `𝔼_{I∼D_n}[T(I)]`, "distribution D_n (often uniform)" (L184) and randomised vs. average-case distinction (L188) assume probability (expectation, uniform distribution) not defined.

### (b) Formalism precedes intuition / picture

- **L33–51 → Fig L57–104:** Five `∃c∃n₀∀n≥n₀` definitions appear *before* the band figure that makes them intuitive. Text says "Fig. visualises" after the fact (L106).
- **L113–121 Limit test theorem:** Formal `L = lim f/g` trichotomy stated before any `f/g → 3` walk-through with numbers; picture of ratio tending to constant/0/∞ comes only as abstract bands.
- **L134–146 Hierarchy:** Theorem + algebraic sketch before Fig L148–173; the schematic log-scale figure is labelled "schematic: vertical compressed" (L169) — useful only after the definitions, not as the lead intuition.

### (c) Expansion suggestions

1. **L23–28 — Motivate with two timed programs:** Before L25, add 1-paragraph story + table: same task on two laptops gives `3n²+5n` vs. `100n` timings; plot shows shape wins → then introduce `∃n₀∀n≥n₀` in words ("after some cutoff n₀, always below").
2. **L33–56 — Picture first, quantifiers second:** Move Fig L57–104 to *before* Def L33; introduce each notation by pointing at the band ("O = stays under a scaled copy after n₀") then write the formal `∃c∃n₀∀n≥n₀` as translation. Add `o/ω` panel or dashed "for every c" narrowing bands.
3. **L109–131 — Build limit intuition without calculus prerequisite:** Prepend 5-line box: "if f/g settles near 3, f is Theta(g); if f/g→0, f is tiny vs g" with numeric table `n=10,100,1000` for `3n²+5n` vs `n²`; introduce l'Hôpital as optional calculus shortcut with forward pointer, not as the definition.
4. **L180–188 — Define expectation from zero:** Insert 6-line box before L180: discrete uniform distribution as "pick one of N inputs equally likely," expectation as average `(1/N)Σ T(I)`, indicator `X=1 if event else 0`; then define `T_worst/T_avg` and note "average needs a stated D_n."

---

## Ch03 — Recurrences (ch03-recurrences.tex)

**Verdict: NEEDS EXPANSION**

### (a) Assumed bachelor's knowledge

- **L10–14 General form:** `T(n)=aT(n/b)+f(n)`, `a≥1, b>1`, "n exact power of b; floors change bounds by constant factor via domain-transformation" (L14) — assumes recurrence fluency + analytic hand-waving.
- **L30–44 Substitution:** "Guess bound, verify by induction" with `T(n)≤cn log n` algebra (L35–37) and hypothesis-strengthening `cn-b` trick (L41–43) assumes induction algebra + inequality manipulation.
- **L48–53 Change of variables:** `m=log n, S(m)=T(2^m)` reduction to MergeSort (L49–51) assumes comfortable substitution/reindexing.
- **L58–64, L98–103 Tree sum:** `T(n)=Σ a^i f(n/b^i)+Θ(n^{log_b a})` (L61–62), depth `L=log_b n`, geometric-series dominance arguments (L98–102) assume Σ notation + geometric series + log identities.
- **L116–159 Master theorem:** `c⋆=log_b a`, three cases with `∃ε>0` polynomial gap + regularity `af(n/b)≤cf(n)` (L121) and "gaps" `n^{c⋆}/log n`, `n^{c⋆} log log n` (L157) — heavy formalism; regularity counterexample `n^{c⋆}(2+sin n)` (L155) assumes oscillation insight.
- **L190–200 Akra-Bazzi:** `Σ a_i b_i^p=1` + integral `Θ(n^p(1+∫ f(u)/u^{p+1} du))` (L192–195) assumes real analysis (integral, existence/uniqueness of p) — stated without proof, but still assumed as quotable tool.

### (b) Formalism precedes intuition / picture

- **L10–18 → Fig L65–91:** General recurrence equation and exact-power remark appear ~50 lines before the recursion-tree figure that explains them; the "what's happening" story (expand one level, count cost per level) should come first.
- **L30–38 Substitution examples:** Inequality chain `2c(n/2)log(n/2)+n = cn log n - cn + n ≤ cn log n` shown before any tree-derived guess story; reader sees verification without learning where the guess came from (trees are next section, L55).
- **L116–129 Master theorem → Fig L127–146:** Three-case theorem stated formally (L118–122) and only then "Figure gives geometric intuition" (L125) — the per-level cost picture (decreasing/balanced/increasing) should precede the case statement.

### (c) Expansion suggestions

1. **L10–18 — Start with a one-level expansion picture:** Before Eq L11, draw `T(n)` as root cost `f(n)` with `a` children `T(n/b)`; show one expansion step concretely for MergeSort `2T(n/2)+n`; then state the general form as shorthand and defer the exact-power/floor remark to a boxed "Floors at most ×2" proof sketch with ruler figure.
2. **L30–44 — Bridge trees→substitution:** Add 2-sentence bridge at L32: "We never guess blindly — next section's tree tells us `cn log n`; here we verify it." For L41 strengthening, add line-by-line inequality picture: show `cn+1` overshoot then `cn-b` absorption with `b≥1` as "subtract to pay the +1."
3. **L112–160 — Flip Master order + add worked gap:** Place Fig L127–146 *before* Thm L116 with walk-through "if level costs shrink, leaves win (Case 1); if flat, multiply by depth (Case 2)" then state cases; add 4-line box at L157 showing `f=n^{c⋆}/log n` with numeric `n=1024` gap between `n^{c⋆-ε}` and `n^{c⋆}` to make "no ε separates them" concrete.
4. **L190–200 — Akra-Bazzi intuition box:** Prepend 3-line picture: unequal splits as lopsided tree + integral as continuous tree sum; flag "you may quote it; check `0<b_i<1`, `h_i=O(n/log²n)`" checklist TikZ before the formula, so formalism lands on intuition.

---

## Ch04 — Divide & Conquer (ch04-divide-conquer.tex)

**Verdict: NEEDS EXPANSION**

### (a) Assumed bachelor's knowledge

- **L10 Prerequisites line:** "basic probability (linearity of expectation, indicator variables)" — assumes a full probability module not built in ch01–03.
- **L26–38 D&C paradigm:** Recurrence `T(n)=aT(n/b)+f(n)` + Master classification restated (L34–36) assumes ch02–03 mastery; "cheap combine relative to shrinking" is stated not shown.
- **L44–61 MergeSort:** Array `A[p..r]`, `q=⌊(p+r)/2⌋`, auxiliary array, induction on `n=r-p+1` (L50) assumes imperative arrays + recursion maturity; optimality pointer "lower bound in Ch.8" assumes decision-tree model not yet built.
- **L64–113 QuickSort + Randomised analysis:** Lomuto invariant (L67), double sum `E[X]=ΣΣ 2/(j-i+1)` → `2(n+1)H_n-4n ∼2n ln n` (L105–109) assumes expectation linearity, harmonic numbers `H_n`, `ln` vs `log₂`, double-sum reindexing `k=j-i`; symmetry argument "first pivot among Z_ij equally likely" (L99–100) is subtle without prior.
- **L116–138 Closest pair:** Euclidean `‖·‖₂`, `δ×2δ` rectangle, diagonal `δ/√2<δ`, `δ×2δ` strip + "at most 8 squares side δ/2" packing (L127) assumes planar geometry; presorting trick "passing y-order through recursion" (L134) assumes algorithmic refinement maturity.
- **L141–206 Strassen:** Block matrix `[[A11,A12],[A21,A22]]`, 7 products `M₁…M₇` + 18 additions `Θ(n²)` (L152–158), recombination formulas (L158) assume linear-algebra matrix multiplication definition; recurrence `T(n)=7T(n/2)+Θ(n²)` solution via `log₂7≈2.807` (L202) assumes ch03.

### (b) Formalism precedes intuition / picture

- **L26–38 Paradigm:** Numbered D&C steps as labelled paragraphs + equation (L32–35) + Master restatement (L36) before any concrete "split a problem, draw the recursion tree" figure; MergeSort is the first picture but comes a page later.
- **L97–112 Randomised QuickSort expectation:** Indicator `X_ij` definition and probability `2/(j-i+1)` stated, then double sum evaluation — the "random pivot as random permutation, comparisons as interval events" picture is described in one sentence (L99) rather than shown; linearity of expectation used before being pictured as "average of 0/1 dots."
- **L123–128 Strip sparsity lemma:** Lemma (L123) + 8-squares proof (L127) appear before a plane figure of the strip/rectangle/squares; reader must reconstruct geometry from text.
- **L152–158 Strassen formulas:** Seven `M_k` linear combinations listed as algebra (L153–156) before Fig L160–196; the "why these 7 suffice" intuition (deriving `ad+bc` from three products) is never pictured — formulas precede the block-matrix figure that could motivate them.

### (c) Expansion suggestions

1. **L10 — Remove or build probability prerequisite:** Either add a 1-page micro-primer before L64 (indicator `X∈{0,1}`, `E[X]=Pr[X=1]`, linearity `E[ΣX]=ΣE[X]` with 2-coin example) or move randomised QuickSort to after that primer; reference it explicitly at L10.
2. **L26–38 — Lead with a picture before the recurrence:** Insert a 2-level D&C tree TikZ (root problem size n → a children size n/b → combine cost f(n)) *before* L32; state recurrence as "cost = children + combine" caption; defer Master restatement to a margin box "solved in Ch.3."
3. **L97–112 — Picture the indicator argument:** Add strip diagram of sorted line `z1 … zn` with interval `Z_ij` highlighted and "first pivot in interval wins" dots; show double sum as triangle of `1/(k+1)` terms with harmonic sum `H_n` shaded, before the algebra.
4. **L123–135 — Figure before lemma:** Move a strip figure (dividing line `x=m`, `δ`-strip, one `δ×2δ` rectangle subdivided into 8 `δ/2` squares with at most one dot per square) to *before* L123; state lemma as caption "why only 7 successors" then give the 2-sentence proof.
5. **L141–158 — Derive Strassen, don't list:** Before L152, add 4-line intuition: Karatsuba analogy "4 products → 3 via ` (a+b)(c+d)` trick" then show block analog; annotate each `M_k` as "which quadrant sum/difference" on the block figure so recombination `C11=M1+M4-M5+M7` reads as picture, not just algebra.

---

## Priority Expansion Order (highest drag first)

1. **Ch01 framing + pictures (1 day, highest leverage):** Rewrite L11/L27 prerequisite box and insert 3 TikZ (Venn/arrow/number-line) — unblocks all later "as built in Ch.1" claims. Without this, every downstream chapter inherits the prior.
2. **Ch03 tree-first reorder (half day):** Move recursion-tree figure before Eq. L11 and Master geometry before Thm L116. Pure reordering + 2 captions; largest formalism-first fix for the steepest chapter.
3. **Ch02 band-first + expectation box (half day):** Move asymptotic-band figure before Def L33 and add the `E[X]` micro-primer that Ch04 also needs. Bridges Ch02→Ch04 probability gap in one insert.
4. **Ch04 probability primer + strip/strassen figures (1 day):** Indicator/linearity box before L97, strip 8-squares figure before Lemma L123, and Strassen block derivation before formula list. Turns the most calculation-heavy chapter from algebra-first to picture-first.

Each item is 8–20 lines + one TikZ; total ~80 lines added across four chapters, well within the small-screen budget.

## Cross-Chapter Notes (drag on ground-up goal)

- **Prerequisite leakage:** Ch01 L11/L27/L34 sets tone that "refresher, not substitute" — this leaks through ch02–04 prerequisites. Fixing ch01's framing (Priority 1 above) cascades: ch02 L10 and ch04 L10 can then honestly say "as built in Ch.1" instead of "as assumed from MH1812."
- **Small-screen budget:** Each suggestion above is 3–8 lines + one TikZ; ~30 lines per chapter keeps the 52p budget while satisfying "thorough not verbose." Priority order above minimises added pages by reordering before adding.
- **Intuition-first ordering rule applied:** Move every band/tree/strip/block-matrix figure ½ page earlier and add a 2–3-sentence story before the definition/theorem that it illustrates — this single mechanical change fixes most (b) items without adding pages.
- **Verification checklist for 0→100:** After expansion, re-read each chapter opening asking (i) "would a reader with only high-school algebra follow this paragraph without a prior course?" and (ii) "is there a picture/story before each formal definition?" — fail either and the chapter remains NEEDS EXPANSION.

**Overall:** ch01–04 are well-structured and visually strong (color TikZ, lst conventions) but currently second-course texts with a refresher, not 0→100 ground-up texts. The gaps are fixable with targeted intuition-first inserts and prerequisite reframing as above — see priority order for the cheapest path to SUFFICIENT.

**Effort estimate:** 3 days for all four chapters to reach SUFFICIENT; Ch01 alone is 1 day and unlocks the other three.

*Lines cited against `modules/SC2001/chapters/chXX*.tex` at `9b1ad10`; figures/tables cited by label where line numbers shift with edits.*
