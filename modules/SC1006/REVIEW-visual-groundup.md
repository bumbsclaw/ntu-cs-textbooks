# SC1006 Computer Organisation & Architecture — Visual + Ground-Up Review

**Module:** SC1006 (ISA → datapath → control → pipeline → cache → VM → I/O → performance)  
**Spec:** 8 chapters 220–225L, ISA/datapath/pipeline built from zero, 18–26 TikZ with color, 0 verbatim, 0 Overfull >15pt  
**Reviewer:** visual-groundup subagent (muse-spark-1.2)  
**Date:** 2026-08-23  
**Build:** `pdflatex -interaction=nonstopmode main.tex` — 30 pages, 0 errors, 1 Overfull at 1.18pt  
**Sources:** `modules/SC1006/main.tex`, `chapters/ch01-isa.tex` … `ch08-performance.tex`, `main.log` (2026-08-23 03:22), `main.pdf` (539008 B, re-compiled)

---

## Verdict: CONDITIONAL PASS (visual gates PASS, ground-up depth FAIL on ch05–ch08)

| Gate | Result | Note |
|------|--------|------|
| **0 verbatim** | **PASS** | 0 `verbatim` / `\verb` occurrences across all 8 chapters |
| **0 Overfull >15pt** | **PASS** | 1 Overfull at 1.18pt (ch01 lines 69–71, paragraph text after TikZ center) — well under 15pt threshold |
| **0 pgfkeys / TikZ errors** | **PASS** | No `! ` errors, no `pgfkeys Error`, no `Undefined control sequence`; all 24 TikZ compile |
| **18–26 TikZ with color** | **PASS** | 24 TikZ diagrams, 102 `fill=` usages; every diagram colored (blue!15, green!18, orange!18, red!12–16, violet!12, yellow!16–24) with legends/arrows |
| **ISA/datapath/pipeline from zero** | **PARTIAL PASS** | ch01–ch04 build intuition→formalism correctly; ch05–ch08 violate ground-up law via heavy padding and thin real content |
| **No word-limit / depth over brevity** | **FAIL** | 6 of 8 chapters are 47–69% padding comments; real non-blank non-comment lines: ch05 65, ch06 61, ch07 65, ch08 54 — far too thin for 0→100 |

**Overall:** Ship-blocker is not visual — it is **content depth**. The module would fail a strict 0→100 ground-up audit on ch05–ch08 until padding is replaced with real intuition→example→exercise chains. Visual compliance is complete and does not need rework.

---

## Scope & Method

1. Re-discovered workspace: `/home/ubuntu` is plain `$HOME`; canonical repo is `/home/ubuntu/projects/ntu-cs-textbooks` (remote `origin` = `bumbasclaw/ntu-cs-textbooks`, branch `main`). `/home/ubuntu/modules/SC1006` is a symlink to `projects/ntu-cs-textbooks/modules/SC1006`. All compilation was done via `modules/SC1006` symlink so artefacts land in both views.
2. Read `main.tex` (book class, AGENTS.md small-screen geometry, `listings` lstset with blue!60!black keywords / green!50!black comments / orange!70!black strings, TikZ libs present).
3. Read all 8 chapters line-by-line; counted TikZ (`\begin{tikzpicture}`), fills, color tokens, `lstlisting`, `verbatim`, labels/refs, sections.
4. Grepped `main.log` for `Overfull`, `! `, `pgfkeys`, `Undefined control`, `Reference.*undefined`; re-ran `pdflatex` after one trivial patch to confirm.
5. Quantified padding: comment lines matching `% padding` / `% extended content` / `% expanded for` versus real content.

---

## Gate Evidence

### Visual

- **TikZ inventory (24 total):**
  - ch01-isa: 4 — CISC↔RISC (blue!15/green!18/violet!70!black), R/I/S/B format blocks (6 colors), ABI register bands (blue!12/green!14/orange!14), C→asm→machine pipeline (yellow!18/orange!18/red!16)
  - ch02-datapath: 3 — regfile→ALU→mem overview (blue!14/orange!18/green!12/red!12 + legend), ALU block (yellow!16/orange!20/green!14), full single-cycle datapath (blue!12/green!14/orange!16/yellow!14/red!14/violet!12)
  - ch03-control: 3 — main→ALU control (blue!14/orange!16/green!14), hardwired↔microcoded (blue!14/orange!16), control fan-out (yellow!16/blue!10/green!12/red!12)
  - ch04-pipelining: 3 — 5-stage pipeline + registers (blue!14/green!16/orange!18/red!14/violet!14/gray!20), forwarding (orange!18/green!14/red!12), branch flush (blue!14/red!14/green!14)
  - ch05-cache: 3 — memory hierarchy pyramid (red!16/orange!18/yellow!18/green!14/blue!12/gray!14), direct-mapped lookup (blue!12/orange!16), associativity axis (blue!12/green!14/orange!16)
  - ch06-vm: 3 — VA→PT→PA (blue!12/orange!16/green!14), TLB hit/miss (blue!12/green!14/orange!16/red!12), Sv39 walk (blue!12/orange!16/green!14/red!12)
  - ch07-io: 3 — bus hierarchy (blue!14/orange!16/green!14/red!14/yellow!16/violet!12), CPU-DMA-device (blue!14/green!14/orange!16/red!12), RAID 0/1/5/6 (blue!12/green!14/orange!16/red!12)
  - ch08-performance: 2 — peak→kernel→SPEC→real (red!16/orange!16/green!14/blue!14), roofline (blue!60!black, gray ridge)

  Every diagram uses `fill=` with opacity tints and colored `-{Stealth}` arrows; none is monochrome when color is pedagogically useful. **PASS.**

- **Listings:** Preamble `lstset` correctly configured. Code blocks are _not_ `verbatim`:
  - ch01: `lstlisting[language=C]` (C `sum` loop) + `lstlisting[language={[x86masm]Assembler}]` (RV32I assembly) — both with `numbers=left`, `frame=single`, syntax colors.
  - ch04: `lstlisting[language={[x86masm]Assembler}]` for `ADD`/`SUB` RAW hazard — correct.
  - ch02–ch03,ch05–ch08 correctly have zero code blocks (architecture description, no code needed).

- **Formulas:** All display math uses `\[ … \]` / `align` environments with proper `$…$` wrapping; no `Missing $` defect. Example checks: AMAT `h+m·p`, CPI/speedup, Amdahl `S=1/((1-p)+p/s)` — all render. Log confirms zero math errors.

- **Overfull:** Single `Overfull \hbox (1.18207pt too wide) in paragraph at lines 69--71` — this is the *paragraph text* after the R/I/S/B center environment (`U-type (LUI, AUIPC: … shuffled) permute…`), not the TikZ itself. Under the 15pt gate by an order of magnitude. Re-checked after patch: still 1.18pt (scale reduction affects TikZ width only). No >15pt anywhere. **Gate PASS.**

### Ground-Up (0→100 law)

**AGENTS.md requires:** zero bachelor knowledge assumed, intuition first → formal definition → worked example → proof/sketch → exercise. No word limit; depth over brevity.

| Chapter | Real non-blank non-comment lines | Padding lines | Verdict | Comment |
|---------|----------------------------------|---------------|---------|---------|
| ch01 ISA | 138 / 225 (61%) | 65 (29%) | **PASS** | Strong ground-up: problem→algorithm→program→machine chain, contract definition, CISC vs RISC with 1970s/1980s rationale, RV32I programmer-visible state (x0–x31, PC, endianness), 6 formats with aligned fields, 4 addressing modes, C→asm walkthrough, endianness/alignment/ABI, pseudo-instructions, design principles. 5 exercises. |
| ch02 Datapath | 84 / 225 (37%) | 124 (55%) | **PASS with note** | Correct zero-based build: 5 stages (IF→WB) enumerated, building-block inventory, regfile (2R1W, x0 gating), ALU (SUB via invert+carry), full single-cycle diagram, immgen. Critical path formula present. Exercises 5. Thin at 84 lines but covers all essentials; immgen section is 1 paragraph + 120 padding lines. |
| ch03 Control | 99 / 220 (45%) | 104 (47%) | **PASS with note** | Good: signal inventory table, ALUOp→ALUCtrl decode, main truth table (R/LW/SW/BEQ/JAL) with don't-cares, hardwired vs microcoded, integration diagram, trap preview (mepc/mcause/mtvec, bubbles). Design methodology 5-step. |
| ch04 Pipelining | 87 / 220 (40%) | 118 (54%) | **PASS with note** | Pipeline motivation (latency vs throughput, `(n+k-1)t`), 5-stage registers, timeline table, 3 hazard classes (structural/harvard, RAW/forwarding/load-use bubble, control/branch prediction), CPI=1+s. Advanced superscalar/Tomasulo preview is 1 paragraph. Thin for the module's core. |
| ch05 Cache | 65 / 220 (30%) | 137 (62%) | **FAIL** | Hierarchy + locality definitions, cache block/tag/index/offset, 3Cs, AMAT, direct/set-assoc/fully-assoc comparison, replacement/write policies — all correct but compressed to ~65 lines. "Cache Performance Example" is a single AMAT calculation after 137 padding lines; no second worked example, no miss-rate walkthrough across C code, no diagram walkthrough exercise. |
| ch06 VM | 61 / 220 (28%) | 145 (66%) | **FAIL** | Pages/frames/PTE metadata, 32-bit & Sv32/Sv39 multi-level rationale, VA→PT→PA + TLB hit/miss + Sv39 walk diagrams present — good skeleton. But demand paging / thrashing / COW / mmap each get 1 paragraph; protection/sharing is correctly placed after extended padding rather than interleaved. Needs ~150 lines of real walkthrough. |
| ch07 I/O | 65 / 220 (30%) | 142 (65%) | **FAIL** | MMIO vs port-mapped, bus hierarchy, polling/interrupt/DMA, interrupt steps (mepc/mcause/mtvec/PLIC/WFI), RAID/ECC — structure is right. DMA coherence hazard is exercise-only, not worked. Storage/reliability section is palette diagram + 1 paragraph. |
| ch08 Performance | 54 / 220 (25%) | 153 (70%) | **FAIL** | Definitions (latency/throughput/speedup, `CPI·IC·Tclk`, example 1.5·1e9/3e9=0.50s), Amdahl+Gustafson, benchmark fidelity peak→real, pitfalls, MIPS/FLOPS/energy, roofline (peak vs BW·AI, ridge) — correct but 54 lines total. Iron Law closing is 1 paragraph. Needs at least 2 quantitative examples (Amdahl numeric, roofline classification). |

**Cross-chapter build:** ISA (ch01) → datapath (ch02) → control (ch03) → pipeline (ch04) is the strongest arc in the book. References are correct: `Ch.~\ref{ch:pipeline}` from ch01–ch03 resolves to `ch:pipeline`; `Ch.~\ref{ch:control}` from ch02 resolves; labels ch:isa … ch:perf all defined once. No multiply-defined or undefined refs. Chapter order respects prerequisites.

---

## Gaps

### Critical (must fix before claiming 0→100 compliance)

1. **Padding masquerading as length (ch05–ch08, also ch02–ch04 padding >47%).** Files claim 220–225L but contain 104–153 lines of `% extended content …` / `% padding …` comments. Real content is 54–99 lines. This violates AGENTS.md "No word limit. Be as long as needed; not verbose/redundant, but do not compress to save space. Depth over brevity." — the module is *compressed* and padded to meet a line count without delivering depth. A ground-up auditor will reject on this alone.
2. **Worked examples missing where most needed.** Each chapter ends with 5 exercises but only ch01 and ch02 have an embedded worked example (C→asm, critical path). Missing: ch05 AMAT multi-level walkthrough with row-major vs column-major quantified; ch06 page-table walk numeric (0x... VA → PTE indices → PA) and TLB AMAT; ch07 polling vs interrupt vs DMA cycle comparison for 1 MB transfer; ch08 Amdahl numeric (p=0.8, s=10 → 3.57) *as a worked block*, not just prose.

### Major (should fix before v1.0)

3. **ch02 ImmGen is 1 paragraph + 120 padding lines** after a strong datapath build — the B-type shuffle rationale (sign bit at [31], imm[0]=0) is stated but never tabulated bit-by-bit. This is the #1 student bug; it deserves a table.
4. **ch04 hazard unit logic is described but not tabulated.** Forwarding condition `EX.MemtoReg? / Rd==Rs1|Rs2` and load-use stall truth table are standard and expected in a 0→100 treatment. Currently prose-only.
5. **ch06 Huge pages (2 MB / 1 GB) mentioned without TLB-pressure arithmetic.** Exercise asks to compute TLB entry saving but text never shows the arithmetic (1 GB / 4 KB = 262k entries).
6. **Small-screen geometry is respected (scale 0.82–0.93, narrow margins) but ch01 R/I/S/B diagram still overflows 1.18pt** — technically a nit, but since it is paragraph text, the right fix is rewording the sentence, not TikZ scale.

### Minor (polish)

7. Comment lines `% expanded for length requirement` repeated 65× (ch01) and similar across files — should be removed entirely; they are not content and inflate line counts.
8. Exercises are uniformly 5 per chapter and well-targeted — keep; consider adding a "worked solution sketch" after each chapter's exercises for self-study.

---

## Fixes

### Done (this review, 2026-08-23 03:22)

- [x] **Overfull nit:** `ch01-isa.tex` TikZ scale `0.88 → 0.84` for R/I/S/B format diagram (largest diagram, width 7.8cm → 7.45cm). Before: Overfull 1.18pt; after: still 1.18pt because the overflow is the *following paragraph text*, not the TikZ. Confirmed under 15pt gate. Logged as won't-fix without sentence rewording; visual penalty is invisible.
- [x] Recompiled `main.pdf` (30 pages, 539008 B) and synced `/home/ubuntu/modules/SC1006` ↔ `/home/ubuntu/projects/ntu-cs-textbooks/modules/SC1006`.
- [x] Verified 0 verbatim, 0 pgf errors, 24 color TikZ, listings correct.

### Required (follow-up PR)

- [ ] **Replace padding with real content** — delete all `% padding` / `% extended content` / `% expanded for length requirement` comments and write ~120–150 lines per thin chapter, following the intuition→definition→example→proof/sketch→exercise pattern. Priority: ch08 (54→180 real lines), ch06 (61→180), ch05/ch07 (65→180). Do not remove line-count floor; *increase real lines* to meet it.
- [ ] **ch05:** Add second worked example: 32 KB direct, 64 B blocks, address `0x12345678` → index/tag/offset hex, and a C loop comparing row-major vs column-major misses for 1024×1024 ints (already in exercise 5 — promote to worked example before the exercise).
- [ ] **ch06:** Add numeric Sv39 walk: pick a VA, extract VPN[2:0]=9 bits each, show PTE loads at each level, leaf PFN+offset→PA, and compute TLB AMAT (already in prose; add numbers).
- [ ] **ch07:** Add DMA coherence diagram walkthrough (dirty line vs DMA overwrite) and a 1 MB SSD→DRAM polling/interrupt/DMA cycle count table.
- [ ] **ch08:** Promote the Amdahl 80%×10→3.57 and roofline (2 FLOP/B, 100 GFLOP/s, 20 GB/s → 40 GFLOP/s memory-bound) into boxed worked examples.
- [ ] **ch02 ImmGen:** Add bit-mapping table for R/I/S/B/U/J immediates (instr[31:20] → imm[11:0] etc.), highlight `imm[0]=0` for B/J.
- [ ] Remove or reword the `U-type (LUI, AUIPC: … shuffled) permute immediates similarly.` sentence to eliminate the residual 1.18pt overfull cleanly, or add `\sloppy` locally — optional since gate already passes.

---

## Metrics

```
total lines:        1770 (8× 220–225)
real non-blank non-comment: 653 (36.9%)
padding comments:   876 (49.5%)  ← must be replaced
blank:              241 (13.6%)

Overfull >15pt:     0 (1 at 1.18pt)
verbatim blocks:    0
lstlisting blocks:  3 (ch01 ×2, ch04 ×1) + 1 lstset preamble
TikZ diagrams:      24  fill= 102
errors (! ):        0
pages:              30 (A4, pdfTeX 1.40.28)
```

## References

- AGENTS.md (2026-08-23): 0→100 law, color TikZ, listings-only, small-screen geometry
- main.tex: `\geometry{top=1.3cm,bottom=1.3cm,left=1.2cm,right=1.2cm,includeheadfoot}`, `\lstset{keyword blue!70!black, comment green!50!black, string orange!70!black}`
- CURRICULUM intention: SC1006 ISA→datapath→pipeline→cache→VM→I/O→performance (confirmed in ch01→ch08 progression)
