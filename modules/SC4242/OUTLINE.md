# SC4242 Compiler Techniques — Textbook Outline (0→100, 3 AU, MPE)

**Module:** SC4242 Compiler Techniques (Software/Theory MPE, 3 AU)  
**Prerequisites:** SC1007 Data Structures & Algorithms → SC2203 Automata, Computability & Complexity → SC4242  
**Co-requisites:** SC2001 (Algorithm Analysis) helpful; SC1008 (C/C++) for runtime labs  
**Position:** MPE-6..9 eligible (SC4xxx), specialisation track: Systems / Theory

## Prerequisite Graph
```
SC1003 --→ SC1007 --→ SC2001 --→ SC2203 --→ SC4242
  |          |          |          |
  +--→ SC1008            +--→ SC2207   +--→ SC2002 (OOP for visitor patterns)
SC1005 --→ SC1006 --→ SC2005 (OS memories) --┘
         MH1812 --→ SC2001 (proofs, induction)
```
SC2203 provides regular languages, NFA→DFA, CFGs, decidability — reused in Ch.2–3.
SC1007 provides trees, graphs, hash tables — reused for symbol tables, CFGs, dataflow.
SC1008 provides C/assembly intuition for Ch.7.

## Learning Outcomes (module-level)
After SC4242 you will be able to (1) trace a program through all compiler phases with
concrete IRs, (2) build a lexer from regexes via NFA→DFA→minimisation, (3) implement
LL(1)/LR parsers and construct ASTs, (4) type-check with inference and report errors,
(5) lower to 3AC/SSA and reason about dominance, (6) apply dataflow optimisations and
prove preservation, (7) allocate registers via graph colouring and emit correct assembly,
(8) explain JIT, GC, and incremental compilation trade-offs.

## Chapter Plan (8 chapters, 200–260 lines each)

| Ch | Title | Core intuition → formal → example | TikZ (colour) | Code (lstlisting) |
|----|-------|------------------------------------|---------------|-------------------|
| 1 | Compiler Overview & Phases | source→target as pipeline; phases, passes, drivers | pipeline conveyor (fills blue/green/orange + legend); pass-vs-phase Venn | driver dispatch in Python |
| 2 | Lexical Analysis: Regex → NFA → DFA | why lexing; regex syntax, Thompson NFA, subset DFA, minimisation, maximal munch | Thompson fragments; subset lattice with Eclosure; DFA minim table | regex→NFA Thompson; lexer loop |
| 3 | Parsing: Grammars, LL & LR, ASTs | ambiguity intuition; CFG, derivations, FIRST/FOLLOW, LL(1), LR(0)/SLR/LALR, AST build | FIRST/FOLLOW table visualisation; LL parse stack steps; LR shift-reduce & AST | recursive-descent LL(1); LR table driver |
| 4 | Semantic Analysis & Type Systems | name binding vs typing; scopes, symbol tables, type rules, inference (Hindley–Milner sketch) | scope tree + symbol table stack; typing derivation tree; unification steps | symbol table with scopes; Hindley–Milner W sketch |
| 5 | Intermediate Representations: 3AC & SSA | why IR; 3AC, basic blocks, CFG, SSA, dominance, phi placement | CFG before/after SSA; dominator tree; phi insertion at frontier | 3AC printer; SSA construction (Cytron) |
| 6 | Optimisation: Dataflow, Inlining, Loops | when optimising pays; dataflow lattice, reaching defs, liveness, DCE, CSE, inlining, LICM/unrolling | dataflow equations on CFG; liveness lattice; loop nest + unrolling | liveness fixed-point; loop unroller |
| 7 | Register Allocation & Code Generation | infinite virtual → k physical; liveness intervals, interference graph, colouring, spilling, instruction selection | interference graph colouring (4-col); linear-scan intervals; tiling tree | graph-colour allocator; MIPS/ARM emitter |
| 8 | Advanced Topics: JIT, GC, Incremental | ahead-of-time limits; JIT tiers & deopt, GC (mark-sweep, copying, generational), incremental & LSP | JIT tier pyramid; heap with mark-sweep vs copying; incremental build DAG | baseline JIT stub; write-barrier snippet |

### Chapter Details (intuition → formal → example)

**Ch.1 Compiler Overview & Phases (3 AU anchor).** Intuition: compiler = translator + optimiser;
bridging human language to machine. Formal: phases (lex→parse→sem→IR→opt→codegen),
front/middle/back-end, passes, driver. Example: `a=b+c*2` through all IRs to MIPS.
Ends with pipeline trade-off exercise (single- vs multi-pass).

**Ch.2 Lexical Analysis.** Intuition: scanning as pattern matching. Formal: alphabet,
regex operators, Thompson construction, ε-closure, subset construction, Hopcroft
minimisation, maximal-munch + priority. Example: keywords vs identifiers DFA; lexing
`if (x<=10)` with token stream. Exercise: build DFA for `0x[0-9a-f]+`.

**Ch.3 Parsing.** Intuition: structure from linear tokens. Formal: CFG, derivations,
sentential forms, ambiguity, FIRST/FOLLOW, LL(1) table, LR(0) items, SLR/LALR, AST vs
parse tree, error recovery (panic mode). Example: expression grammar `E→E+T|T` factored
to LL(1) and SLR table walkthrough. Exercise: prove dangling-else ambiguity.

**Ch.4 Semantic Analysis & Type Systems.** Intuition: meaning beyond syntax.
Formal: scope (lexical vs dynamic), symbol table (stack/hash + chaining), type
judgements `Γ ⊢ e : τ`, inference rules, unification, Hindley–Milner `W`, coercions.
Example: let-polymorphism derivation for `let id=λx.x in id 3`. Exercise: implement shadowing.

**Ch.5 Intermediate Representations.** Intuition: portable stepping-stone.
Formal: 3-address code, quads, basic blocks, CFG, SSA def-use, dominance/dominator
tree, dominance frontier, φ-placement (Cytron), mem2reg. Example: factorial lowering
to 3AC then SSA with φ at loop header. Exercise: compute dominance frontier.

**Ch.6 Optimisation.** Intuition: preserve semantics, cut cost. Formal: dataflow
framework (lattice, transfer, meet, fixed-point), reaching defs, liveness, available
exprs, constant prop/folding, CSE, DCE, inlining heuristics, loop invariants, LICM,
unrolling, strength reduction. Example: liveness on factorial CFG → DCE + LICM.

**Ch.7 Register Allocation & Code Generation.** Intuition: k colours for n variables.
Formal: liveness intervals, interference graph, graph colouring (Chaitin-Briggs),
coalescing, spill cost, linear scan, instruction selection (tiling, maximal munch),
calling convention. Example: 4-colour allocation walkthrough with spill. Exercise: linear scan.

**Ch.8 Advanced Topics: JIT, GC, Incremental.** Intuition: compile late, manage memory
automatically, rebuild little. Formal: interpreter→baseline JIT→optimising JIT,
OSR/deoptimisation, inline caches, GC roots, mark-sweep/compact/copying/generational,
write barriers, tri-colour invariant, incremental build DAG, LSP. Example: tiered JIT
trace for hot loop + minor GC. Exercise: design write barrier.


## Pedagogy Invariants (per AGENTS.md)
- **0→100 ground-up:** Ch.1 defines alphabet, token, grammar, AST from zero; no SC2203 assumed without recap.
- **Intuition→formal→example→exercise:** every section opens with picture/analogy, then definition/theorem, then worked example, then 5 exercises.
- **Visuals:** 2–3 colour TikZ per chapter (fills blue!15/green!20/orange!15/violet!10 + legends).
- **Code:** 1–2 `lstlisting` per chapter with `language=` and colour highlighting; zero `verbatim`.
- **QA gate:** pdflatex×2, grep `^!` / `pgfkeys` / `Overfull>15`, target 40–55 pages, geometry top=1.3 bottom=1.3 left=1.2 right=1.2 includeheadfoot, setstretch 1.20, parskip 0.70em.

## Cross-Module Links
- SC2203 Ch.2–4 (regular languages, CFGs) → SC4242 Ch.2–3 (lexer/parser theory realised).
- SC1007 trees/graphs → SC4242 Ch.3–7 (ASTs, CFGs, interference graphs, dominators via Lengauer–Tarjan).
- SC2005 (memory, processes) → Ch.8 (GC, code cache, OS interaction).
- SC4023/SE electives → Ch.8 (tooling: LSP, build systems).
