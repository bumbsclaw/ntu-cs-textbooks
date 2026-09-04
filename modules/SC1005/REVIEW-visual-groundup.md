# SC1005 Digital Logic — Visual + Ground-Up Review

**Date:** 2026-08-23  
**Reviewer:** subagent (visual+ground-up checklist)  
**Scope:** `modules/SC1005/main.tex` + `chapters/ch01`–`ch08` (8 chapters, ~200–210L each)  
**Pipeline:** binary/hex → gates → K-maps → combinational → sequential → FSM → registers → arithmetic → memory (gates/K-maps/flip-flops/FSM TikZ)

---

## Verdict: PASS (with trivial nits patched)

The textbook is **coherent, build-clean, and pedagogically sound** for a zero-prior audience. All automated gates pass after one paragraph reflow fix. No blocking issues.

| Gate (same as SC2001/SC1006) | Result | Detail |
|---|---|---|
| **0 `verbatim`** | ✅ PASS | `grep -rn verbatim chapters/*.tex` → 0 hits (0 in `main.tex` too) |
| **0 `lstlisting` (`verbatim`+`6` alias — actually `lstlisting` env)** | ✅ PASS | `grep \\begin{lstlisting}` → 0 in `*.tex`; 8 hits only in `.aux` counters (`\setcounter{lstlisting}{0}`) — no `lstlisting` environments used. No `\verb` either. `listings` package loaded in `main.tex` but unused (harmless; available for future code). |
| **0 Overfull > 15pt** | ✅ PASS | After patch: `grep Overfull main.log` → **0**. Before patch: 1× 4.66pt at ch01 L72–75 (well under 15pt threshold anyway). Reflowed and cleared. |
| **TikZ color (`blue!12`/`orange!16` etc)** | ✅ PASS | All 8 chapters use filled TikZ: counts `blue!` 50, `orange!` 28, `green!` 25, `red!` 32, `violet!` 11, `teal!` 28, `yellow!` 19. Every chapter has 6 `tikzpicture` envs (total 48 figures), each with `fill=…!` pastel palettes and semantic coloring (blue=weights/data, orange=second operand, red=carry, teal=feedback/clock, yellow=annotation). |
| **Build** | ✅ PASS | `pdflatex main.tex` → `Output written on main.pdf (37 pages, 608860 bytes)` — clean, no errors. `h`→`ht` warnings only (normal). |
| **Cross-refs** | ✅ PASS | 8 `\label{ch:…}` defined, 9 `\ref{ch:…}` uses all resolve. 23 `\label{fig:…}` defined; 2 `\ref{fig:…}` uses resolve. No undefined-ref warnings in log. |

---

## Ground-Up Checklist (zero-prior)

**Standard:** every abstraction introduced picture → words → definition, with no assumed digital background beyond school arithmetic.

| Chapter | Zero-prior Framing | Intuition → Formal | Notes |
|---|---|---|---|
| **ch01 Numbers** | ✅ Explicit `\fbox` From-zero banner: "We assume only school arithmetic." Opens with *why two voltages?* (noise immunity) before any positional math. Bits as switches in `LOW≈0V / HIGH≈VDD`, byte as storage atom. | ✅ LSB/MSB, weights via 8 colored boxes (blue!12 … yellow!18) → numeric example `10110101₂=181` → formal positional definition with radix `r`. | Strongest opening in the set. |
| **ch02 Boolean & K-maps** | ✅ From-zero banner: "We define propositions, connectives, axioms before any algebra." | ✅ Venn (blue/orange overlap) → Huntington axioms/De Morgan → SOP/POS → K-map as *Gray-order adjacency you can see*. Quad `y'`+pair `xz'` walked before formal prime/essential defs. | Gate-color family (blue AND, orange OR, green NOT, violet NAND) consistent. |
| **ch03 Combinational** | ✅ Banner: "We define combinational vs sequential … from truth tables. No sequential knowledge assumed." Design flow 1→4 (table→SOP→gates→hazard) made explicit. | ✅ HA truth table → `S=a⊕b, Co=ab` → FA from 2×HA+OR → RCA chain → then MUX/decoder as truth-table realizations. Hazards derived from K-map adjacency, not asserted. | Critical-path delay noted early and tied to later Ch07/04 timing. |
| **ch04 Sequential** | ✅ Banner: "We assume only gates (Ch2–3). We add one idea—feedback." Bistable from two inverters first, then SR → D → master-slave → edge-triggered. | ✅ Cross-coupled NOR with teal feedback wire (color = memory) → truth table beside figure → level-sensitive vs edge-triggered timing sketch → `t_su/t_h/t_cq` inequalities only after intuition. | SR→D→master-slave progression is the cleanest zero-prior path; metastability + 2-flop synchronizer included. |
| **ch05 FSM** | ✅ Banner: "We define state, transition, output … from word problems." 5-tuple `(S,I,O,δ,λ)` introduced before Moore/Mealy split. | ✅ Block diagrams (Moore vs Mealy red input arrow is the *only* difference) → 101 detector state graph with "last i bits matched" invariant → synthesis 5-step recipe → encoding tradeoffs. | Mealy glitch vs Moore latency called out with the "register the Mealy output" pattern — addresses a classic lab surprise. |
| **ch06 Registers/Counters** | ✅ Banner: "We assume D/JK (Ch04) and FSM ideas (Ch05). Each circuit derived from what next-state do we want?" | ✅ Register as `n` DFFs sharing CLK (picture) → `D_eff = LD·D + LD'·Q` → shift as `Q_i→D_{i+1}` → ripple vs synchronous toggle equations `T_i=∧_{j<i}Q_j`. | Johnson/ring self-correction, mod-m don't-cares handled. |
| **ch07 Arithmetic** | ✅ Banner: "We assume adders and two's complement (Ch01–03). Each faster circuit motivated by delay of previous." | ✅ Ripple O(n) pain → `g/p/c_{i+1}=g_i+p_i c_i` intuition → CLA unrolling → group G/P → carry-select/prefix as tradeoffs. Array multiplier grid → shift-add → Booth as "run of 1s" recoding. | `V = c_n⊕c_{n-1}` derived, not just stated; flags C/Z/N/V tied to branch logic. |
| **ch08 Memory** | ✅ Banner: "We build up from latch/register (Ch06) to arrays, then any truth table → memory lookup → FPGA." | ✅ `2^n×m` matrix picture (row dec + array + sense amps) → 6T vs 1T1C cell comparison → PLA (sparse terms) vs ROM (full table) figure → FPGA as "LUTs are tiny ROMs + interconnect". | Hierarchy/locality and ECC/Flash wear properly scoped as preview for architecture course. |

**Overall ground-up coherence:** The 8-chapter dependency graph is acyclic and honest — no forward references except as explicit previews ("preview for computer arithmetic courses", "full treatment in SC1007/SC2002"). The `From zero:` banners are present in every chapter, and the picture→words→definition order is respected.

---

## Visual Checklist (TikZ color)

- **Palette compliance:** Every `tikzpicture` uses pastel fills (`blue!10–14`, `orange!14–18`, `green!12–16`, `red!12–16`, `violet!12–14`, `teal!14`, `yellow!12–18`). No raw primary fills, no unstyled monochrome diagrams.
- **Semantic color discipline:** Blue = data/weights/state, orange = second operand / slave / column decode, green = control/OR planes, red = carry/borrow/flag path, teal = feedback/clock/interconnect, yellow = annotation/callout. Consistent across chapters.
- **Figure density:** 48 TikZ figures (6/chapter) — well above the informal "≥4 per chapter" bar. Covers: binary weights, hex grouping, number wheel, Venn, gates, K-map, HA/FA/RCA, MUX, SR/D latch timing, master-slave/DFF symbol, Moore/Mealy blocks, sequence detector, FSM datapath, register, shift register, ripple vs sync counter, CLA dataflow, array multiplier, ALU, memory org, PLA vs ROM, FPGA fabric.
- **Readability:** Rounded corners, `fill=…`, colored arrows with labels, scale 0.78–0.82 tuned for the 1.2 cm margins. No figure exceeds `\linewidth`; geometry `top1.3 bottom1.3 left1.2 right1.2` respected.

---

## Gaps & Non-Blocking Observations

No blocking gaps. Items below are **enhancement backlog** (none require immediate rewrite):

1. **Simulatable code listings — intentionally absent, acceptable**  
   No `lstlisting`/`verbatim` environments by design. The spec's "0 verbatim / 0 lstlisting" is a *style* gate (avoid monospace dumps) — this book passes and uses prose + math instead. If evaluators expect HDL snippets (e.g., `always @(posedge clk)` for FSM in Ch05), they would need `lstlisting` with `breaklines` — currently none. Recommendation: keep current gate-passing style; add an optional appendix with 2–3 short Verilog sketches if a future rubric requires runnable code.

2. **Worked K-map could show wrap-around group explicitly**  
   Ch02 K-map describes wrap but the violet dashed rectangle `(0,0)→(1.20,1.10)` only hints at the `(4,6)` wrap adjacency. A curved arrow around the map edge would make wrapping visceral. Low priority — caption already states it.

3. **Ch03 7-segment decoder example is text-only**  
   Example says "K-maps for each segment share product terms" but no figure. A small 2-panel 7-seg + per-segment K-map montage would repay the visual promise. Optional.

4. **`listings` package loaded but unused**  
   `main.tex` loads `listings` + `\lstset` yet no chapter uses it. Harmless (no warnings), but either remove or add a comment `% reserved for optional HDL appendix` to avoid confusion.

5. **Ch08 DRAM timing diagram text-only**  
   `t_AA`, `t_AS`, `t_DS`, `R̄ĀS̄/C̄ĀS̄` are described in prose. A 4-trace timing figure (CLK/Addr/WE/Data) would mirror Ch04's timing sketch quality. Optional.

6. **Exercises: Ch05 Q4 table placeholder**  
   `E5.4` says "A FSM has 6 states with given table (provide)." Parenthetical is an author note — needs either an inline table or "see tutorial sheet." Minor editorial.

7. **No end-of-book summary / concept map**  
   Each chapter has Notes/Exercises but there is no capstone page tying `numbers → gates → combinational → sequential → FSM → datapath → arithmetic → memory → FPGA` into one system picture. A single TikZ system-stack figure would close the loop.

---

## Fixes Applied (trivial nits — patched directly)

| # | File | Line(s) | Before → After | Reason |
|---|---|---|---|---|
| 1 | `ch02-boolean.tex` | 92 | ``$m_5=\bar x y\bar? $ no---with order $x\,y\,z$, $m_5=x'\cdot y\cdot z'$? Check: binary $101=5$.`` → ``(order $x\,y\,z$): binary $101=5$ gives $m_5 = x\cdot \bar y\cdot z$ (variable complemented when its bit is $0$).`` | Remove editorial doubt fragment; give correct `m₅ = x·ȳ·z` for `101` with stated literal convention. |
| 2 | `ch02-boolean.tex` | 161–171 | Removed 3 dead draws (`blue!60!black`, `green!60!black`, `orange!70!black` placeholders) + 2 editorial comments (`% placeholder for 0,4`, `% Single extra…`, `% Actually show…`) | Dead code + author TODO left in TikZ — final figure already redrawn in red/violet. |
| 3 | `ch01-numbers.tex` | 72–74 | Reflowed ``Since $16=2^4$, group bits… $(1011 0110)_2 = (B6)_{16}$, and $(3F)…`` → ``Since $16=2^4$, group bits in fours.\nFor example, $(1011 0110)_2=(B6)_{16}$ and $(3F)_{16}=(0011 1111)_2$.`` | Fix sole `Overfull \hbox (4.66pt)` paragraph; also tightened spacing around `=`. Rebuild → 0 Overfull. |
| 4 | `ch01-numbers.tex` | 172 | ``result&1&0&0&0&1 % 17 - need 5 bits? Actually …`` → ``result&1&0&0&0&1`` | Remove inline author question from `tabular` source. |

Rebuilt after patches: `pdflatex main.pdf` **37 pages, 608860 bytes, 0 Overfull, 0 errors**.

---

## Not Patched (deferred — outside trivial-nit scope)

- Items 1–7 in **Gaps** above require editorial decisions (add figures/HDL appendix vs keep gate-clean). Left for module owner.
- No `\label`/`\ref` renumbering needed; no content rewrites.

---

## Reproduce

```bash
cd /home/ubuntu/projects/modules/SC1005
grep -rn "verbatim" chapters/ main.tex        # → 0
grep -rn "begin{lstlisting}" chapters/ main.tex # → 0 (only \setcounter in .aux)
grep -c "Overfull" main.log                    # → 0 after patch
pdflatex -interaction=nonstopmode main.tex     # → Output written on main.pdf (37 pages)
```
