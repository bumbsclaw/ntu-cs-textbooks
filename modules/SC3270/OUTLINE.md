# SC3270 Reasoning About Programs — Outline

**Code:** SC3270 (MPE 3 AU) · **Prereqs:** SC1007 Data Structures & Algorithms + SC2001 Algorithm Design & Analysis (MH1812 Discrete Mathematics helpful) · **Position:** MPE elective, theory/software track · **Approach:** 0→100 ground-up, intuition→formalism, small-screen geometry 1.3/1.2 setstretch 1.20, color TikZ + lstlisting[Python/C/Java]

## Module Overview
SC3270 teaches *how to prove programs correct*. Starting from zero logic background it builds a complete verification stack: Ch 1–2 introduce specifications and Hoare triples, Ch 3–5 develop the core technique of invariants and loop proofs plus termination, Ch 6 formalises backward reasoning via weakest preconditions, Ch 7 scales to heap-manipulating programs with separation logic, Ch 8 synthesises correctness-by-construction and refinement. The 0→100 flow is **specify → prove → scale → build**: first say what correct means, then prove straight-line code, then conquer loops and non-termination, then mechanise reasoning backwards, then handle pointers, then construct correct programs from scratch. Every chapter uses lstlisting with Python (executable specs), C (pointer/heap snippets) or Java (contracts/JML style). All diagrams are color TikZ.

## Chapter Plan (8 chapters, 4–5 LOs each)

### Ch 1 — What Does Correct Mean? Programs as Logic
- define program state, assertion, specification as set of allowed behaviours;
- distinguish testing (finite sampling) from proof (all paths) with soundness intuition;
- introduce Hoare triple `{P} C {Q}` informally and explain partial vs total correctness;
- illustrate with absolute value and max; show why informal argument fails on aliasing.

### Ch 2 — Hoare Logic: The Proof System
- present Hoare axioms: assignment, skip, sequencing, conditional, consequence;
- build proof trees for straight-line programs; explain compositionality;
- prove soundness intuition and discuss completeness (Cook relative completeness);
- contrast Hoare logic with operational semantics; introduce proof outline notation.

### Ch 3 — Preconditions and Postconditions: Writing Contracts
- formalise contract as `requires/ensures`; relate to Hoare triple slots;
- craft strong vs weak preconditions; show precondition strengthening, postcondition weakening;
- specify real functions (binary search pre: sorted) and detect vacuous specs;
- translate informal requirements to formal assertions with quantifiers; introduce JML-style syntax.

### Ch 4 — Invariants: What Stays True
- define invariant as property preserved by every step; distinguish loop vs data invariant;
- discover invariants via intuition: what the loop has achieved so far + what remains;
- prove invariant preservation and use invariant + negated guard ⇒ postcondition pattern;
- illustrate on sum, counting, linear search; show invariant too weak / too strong pitfalls.

### Ch 5 — Verifying Loops: Putting Invariants to Work
- state full Hoare while-rule with invariant annotation; build verification conditions;
- verify classic loops: summation, search, partition, Euclid GCD, Dutch flag sketch;
- handle nested loops and invariant conjunction; show where auxiliary variables help;
- mechanise VC generation: from annotated program to logical implications.

### Ch 6 — Termination: Proving Programs Stop
- distinguish partial vs total correctness; introduce variant (ranking function) and well-founded order;
- prove termination of while-loops via decreasing natural-number variant;
- handle tricky termination: lexicographic variants, Ackermann sketch, non-termination counterexample;
- relate termination to halting problem limits; show total-correctness Hoare rule.

### Ch 7 — Weakest Preconditions: Reasoning Backwards
- define `wp(C,Q)` as weakest assertion guaranteeing `Q` after `C`; Dijkstra's calculus;
- compute `wp` for assignment (substitution), sequence, conditional, loop (approximation);
- show `wp` vs `sp` duality; use `wp` for systematic correctness derivation and VC generation;
- automate `wp` with substitution; connect to symbolic execution and modern verifiers (Dafny intuition).

### Ch 8 — Separation Logic and Correctness by Construction
- motivate heap: why Hoare logic stumbles on aliasing; introduce `*` separating conjunction and emp;
- specify heap programs: `{x↦_} [x]:=3 {x↦3}`, list segment `ls`, frame rule;
- apply stepwise refinement: from spec to code via law-driven development; Morgan/Dijkstra style;
- construct correct program (e.g., in-place list reversal, binary search) by calculation, not post-hoc proof.

## TikZ Diagram Plan (2–3 per chapter, color where useful)

- **Ch1:** (1) State space: precondition blob blue!15 → program arrow → postcondition blob green!15 with illegal traces red!15 blocked (legend); (2) Testing vs proof: sample dots orange vs universal shading violet; (3) Hoare triple conveyor: P box → C machine → Q box
- **Ch2:** (1) Hoare proof tree: axioms as leaves green!12, rules as branches blue!10 culminating in triple; (2) Assignment axiom as substitution arrow yellow!12 → blue!12; (3) Sequence rule domino chain
- **Ch3:** (1) Contract strength lattice: stronger pre up, weaker post down, implication arrows blue!40; (2) Pre/post Venn: calls inside P green, outputs inside Q orange; (3) Requires/ensures badge on function box
- **Ch4:** (1) Invariant as loop fence: states before/during/after, invariant band blue!12 preserved; (2) Invariant discovery: done vs todo split (green!14 / orange!14); (3) Too-weak vs too-strong seesaw
- **Ch5:** (1) While-rule verification conditions as three implication arrows (init, preserve, exit); (2) Annotated GCD trace: states with invariant colour bar; (3) Nested loop invariant onion layers
- **Ch6:** (1) Variant descent staircase: natural numbers decreasing green → 0 red stop, infinite non-WF grey; (2) Lexicographic order grid; (3) Partial vs total correctness Venn
- **Ch7:** (1) wp as weakest set: Q pullback through C, wp innermost blue!15 vs arbitrary P orange; (2) wp computation pipeline backwards: Q → ... → P arrows; (3) Loop wp as limit of approximations
- **Ch8:** (1) Heap with separating `*`: two disjoint heaplets blue!12 + green!12 = combined violet!08; (2) Frame rule: local proof + untouched frame grey; (3) Refinement lattice: spec at top violet, steps down to code green, calculational arrows

## lstlisting Language Plan

- **Python (primary, Ch 1,2,4–7):** executable specs with `assert`, VC generation toy, `z3` sketch for wp, variant checking, loop invariant runtime monitor. Shared lstset highlights (keyword blue!60!black, comment green!50!black, string orange!60!black).
- **C (Ch 7–8, heap):** heap snippets with `malloc/free`, pointer alias examples, separation-logic annotated list code; shows why `x` and `y` aliasing breaks naive Hoare reasoning.
- **Java (secondary, Ch 3,8):** JML-style contracts `//@ requires ... ensures ...`, class invariants, refinement example with `ArrayList` vs array.
- Every code block uses `\begin{lstlisting}[language=Python]` or `[language=C]`/`[language=Java]` (never verbatim); caption + line numbers; xleftmargin 1em for small-screen.

## Exercise Themes (per chapter, 5 items)

- Ch1: formalise state, distinguish partial/total, write triples for max, find spec bug, testing vs proof counterexample.
- Ch2: apply assignment axiom, prove sequence, use consequence, build proof tree, show unsound rule breakage.
- Ch3: strengthen pre, weaken post, write sorted-array contract, spot vacuous truth, translate English to quantified assertion.
- Ch4: propose invariant for sum/search, show invariant too weak, too strong, invariant for counting positives.
- Ch5: verify while-sum, Euclid, linear search, nested loop, generate VCs from annotated code.
- Ch6: find variant for countdown, lexicographic for nested loops, prove non-termination, Ackermann variant, total correctness triple.
- Ch7: compute wp for assignments/sequence/conditional, wp vs Hoare connection, loop wp approximation, symbolic execution trace.
- Ch8: `*` vs `∧` heap example, apply frame rule, spec list reverse, stepwise refinement of binary search, compare Hoare vs separation.

## Prereq Graph Note (how it builds on SC1007 + SC2001)

**SC1007 → SC3270:** reuses imperative programs (arrays, lists, loops), recursion intuition, and informal invariant (loop invariant from sorting) as the *object* to be proven — SC3270 makes that intuition rigorous with Hoare rules. Students who skip SC1007 would lack the programming model that triples talk about.
**SC2001/MH1812 → SC3270:** reuses asymptotic reasoning as motivation for correctness alongside efficiency, and discrete math (propositional/predicate logic, induction, well-founded orders) as the *logic* in which assertions live — Ch 1 recaps logic from zero but leans on SC2001 maturity for quantifier fluency. Together: SC1007 supplies *what programs do*, SC2001/MH1812 supplies *how to argue*, SC3270 supplies *how to prove it airtight*.
**Graph:** `SC1003→SC1007→SC2001 ─┐→ SC3270 → {SC4040/SC4051/MH4511 advanced verification}` + `MH1812→SC3270`; SC3270 is MPE-leaf, not a prereq for other cores.

## 0→100 Flow Summary

Specify (Ch 1–3: what correctness means, Hoare triples, contracts) → Prove loops (Ch 4–5: invariants, verification conditions) → Ensure progress (Ch 6: termination, variants) → Mechanise (Ch 7: weakest preconditions, backward reasoning) → Scale & build (Ch 8: separation logic for heap, refinement for construction). No prior verification assumed beyond SC1007 loops and SC2001 logic maturity; every formal notion (Hoare rule, invariant, variant, wp, separating conjunction) is introduced via picture→definition→example→exercise.
