# SC3050 Advanced Computer Architecture — Module Outline

> **Code:** SC3050 (3 AU, MPE) · **Prereq:** SC1006 (SC1005 via SC1006) · **Lineage:** SC1006 → SC3050 (SC2005/SC2008 recommended) · **Sem:** Y3 MPE · **Model:** muse-spark-1.2-contributor only (retry on 500/503, no fallback)

## Module Overview

SC3050 goes beyond SC1006 Computer Organisation & Architecture. Where SC1006 builds a *correct* 5-stage RISC-V datapath (single-cycle, pipelined, cached, virtual), SC3050 asks *how to make it fast, parallel, and scalable*: deep and superscalar pipelines, hazard elimination, branch prediction, memory-hierarchy optimisation, coherence/consistency for multicores, bus/interconnect design, and power-aware SoC/GPU futures.

0→100 ground-up: every chapter opens with intuition/picture (why the bottleneck exists — e.g., laundry pipeline, cache as library desk, branch as fork in road), then formalism, worked numbers (Iron Law, AMAT, MESI traces), and a runnable snippet. Assumes *only* SC1006 (ISA, datapath, cache basics, Iron Law/AMAT); OS/virtual-memory details re-derived on first use — no leakage assumed.

Position in curriculum: SC1006 is the sole formal prereq per 2024 MPE sheet (SC2005/SC2008 listed as recommended in older sheets). SC3050 is the systems-performance hinge between SC1006 foundations and SC4051 Distributed Systems / SC402X accelerators.

## Chapter Plan (8 chapters, ~200–260 lines each)

**Ch1 — Foundations & ISA Revisited:** RISC vs CISC vs VLIW spectrum; compiler-ISA contract; performance Iron Law (IC×CPI×Tclk), Amdahl/Gustafson, cost/power walls.
Outcomes: (a) classify ISAs on code-size/CPI/decoder cost; (b) apply Iron Law to compare designs; (c) compute speedup bounds and argue fixed vs scaled scaling.

**Ch2 — Advanced Pipelining & Hazards:** 5-stage review → deep pipelines; structural/data/control hazards; forwarding truth table, load-use bubble, precise exceptions, register overhead.
Outcomes: (a) draw pipeline timing tables; (b) resolve RAW with forward/stall logic; (c) compute pipelined speedup with imbalance and overhead.

**Ch3 — Superscalar & Out-of-Order Execution:** dual/4-way issue; Tomasulo reservation stations, CDB, register renaming, ROB for in-order commit and speculation.
Outcomes: (a) schedule a window on superscalar/OoO; (b) explain renaming eliminating WAR/WAW; (c) trace ROB commit and precise interrupt recovery.

**Ch4 — Branch Prediction & Speculation:** 1-bit/2-bit saturating counters, correlating/tournament predictors, BTB, return-address stack; speculation recovery, Spectre intuition.
Outcomes: (a) simulate 2-bit predictor accuracy on a trace; (b) size BTB vs hit-rate; (c) quantify misprediction penalty and flush cost.

**Ch5 — Memory Hierarchy Optimisations:** AMAT revisited; six cache optimisations (larger blocks, associativity, victim, prefetch, non-blocking, critical-word-first); TLB/Sv39 walk, huge pages; DRAM bandwidth wall.
Outcomes: (a) compute multi-level AMAT; (b) choose block/assoc/prefetch trade-offs; (c) explain TLB miss walk cost and huge-page benefit.

**Ch6 — Cache Coherence & Consistency:** private caches → coherence problem; snooping MESI/MOESI, bus vs directory (full/bit-vector/limited), false sharing; sequential vs weak, fences.
Outcomes: (a) walk MESI transitions for a 2-core trace; (b) contrast snoop vs directory scaling; (c) place fences for a weak model.

**Ch7 — Interconnects, Buses & I/O:** bus hierarchy (memory/PCIe/USB), arbitration (daisy-chain, central, distributed), interrupts vs polling, DMA, MMIO ordering; topologies (crossbar, mesh, torus).
Outcomes: (a) arbitrate a grant sequence; (b) compare polling/interrupt/DMA overhead; (c) evaluate topology latency/bisection bandwidth.

**Ch8 — Parallel Architectures & Future:** multicore SMP/NUMA, SMT vs fine-grain MT, SIMD/GPU warps, SoC/chiplets, power (DVFS, dark silicon), DSA; Roofline & warehouse-scale preview.
Outcomes: (a) contrast TLP flavours; (b) place kernels on Roofline; (c) argue power vs performance for SoC/GPU/DSA.

## TikZ Diagram Plan (2–3 per chapter, colour fills blue!15/green!20/orange!15/violet!10/red!12, legend, labelled)

- **Ch1:** (a) CISC→RISC→VLIW spectrum bar; (b) Iron Law triangle IC/CPI/Tclk → CPU time; (c) Amdahl vs Gustafson curves with ceiling.
- **Ch2:** (a) 5-stage pipeline with coloured IF/ID/EX/MEM/WB + pipeline registers; (b) forwarding mux/bypass (violet EX/MEM→ALU); (c) hazard timeline (load-use bubble).
- **Ch3:** (a) dual-issue superscalar width diagram; (b) Tomasulo RS + CDB + ROB block diagram; (c) renaming map table before/after.
- **Ch4:** (a) 2-bit saturating-counter FSM (4 states); (b) BTB+direction-predictor datapath; (c) misprediction flush vs select timeline.
- **Ch5:** (a) hierarchy pyramid CPU-L1-L2-LLC-DRAM with hit-time labels; (b) cache-opt trade-off axes; (c) Sv39 TLB+page-table walk (offset pass-through).
- **Ch6:** (a) MESI 4-state FSM; (b) snoop bus vs directory side-by-side; (c) coherence message chart (Rd/RdX/Inv/Ack).
- **Ch7:** (a) bus hierarchy with bridge; (b) arbitration waveform (request/grant); (c) mesh vs crossbar vs torus with hop-count.
- **Ch8:** (a) 4×4 multicore mesh with L2 slices; (b) SMT occupancy (1T vs 2T vs SMT); (c) heterogeneous SoC (CPU+GPU+NPU+NoC, power islands).

## lstlisting Plan (listings with language=, colours keyword blue!60!black, comment green!50!black, string orange!60!black, numbers gray, xleftmargin 1em)

- **Ch1:** `C` — Iron Law & Amdahl solver; `Python` — RISC-V encoding printer (hex → fields).
- **Ch2:** `[x86masm]Assembler` — RISC-V hazard sequence with forward annotation; `C` — 5-stage pipeline simulator (cycle table).
- **Ch3:** `Python` — Tomasulo trace (issue/execute/writeback); `C` — renaming demo (logical→physical map).
- **Ch4:** `Python` — 2-bit predictor on trace + accuracy report; `C` — BTB microbenchmark via `rdcycle`.
- **Ch5:** `C` — cache AMAT sweep (B, assoc, prefetch); `Python` — stride prefetcher plotter.
- **Ch6:** `Python` — MESI simulator (trace → states/bus txns); `C` — false-sharing demo (padded vs unpadded, `perf` timing).
- **Ch7:** `C` — MMIO poll vs interrupt latency (GPIO mock); `Python` — round-robin bus-arbiter simulator.
- **Ch8:** `Python` — Roofline calculator (ridge point); `C` — OpenMP/SIMD scaling (pthreads + intrinsics).

## Exercise Themes (per chapter, exam-style + hands-on)

- **Ch1:** Iron-Law back-of-envelope; RISC/CISC code-size vs CPI; Amdahl fixed vs Gustafson scaled bounds.
- **Ch2:** pipeline timing tables; forwarding truth-table hunts; load-use bubble counting; precise-exception handling.
- **Ch3:** dual-issue schedule under structural limits; Tomasulo CDB contention; ROB in-order commit trace.
- **Ch4:** 2-bit predictor walk on history string; BTB sizing vs miss-rate; speculation flush cost (cycles lost).
- **Ch5:** address 0x12345678 decomposition for varied geometries; multi-level AMAT; prefetch coverage vs pollution.
- **Ch6:** 2-core MESI interleaving; directory bit-vector vs full-map scaling; fence placement for store-buffer litmus.
- **Ch7:** arbitration grant latency; polling/interrupt/DMA cycle-steal; bisection bandwidth of mesh/torus.
- **Ch8:** Roofline placement (compute vs memory bound); SMT vs multicore throughput; DVFS ED/ED² energy-delay.

## Prerequisite Graph

```
MH1812 / SC1005 → SC1006 (ISA, datapath, control, pipeline, cache, VM, I/O, perf)
                               ↓
SC1006 ─┬─→ SC2005 (OS: threads, paging, TLB — reused in Ch5/6)
        ├─→ SC2008 (networks: topology/protocol intuition for Ch7)
        └─→ SC3050 (advanced pipeline → superscalar → branch → cache-opt → coherence → buses → parallel/SoC)
SC1007 / SC2001 ──→ algorithmic maturity only (big-O for cache vs compute trade-offs)
```

Formal prereq per 2024 MPE: SC1006 only; SC2005/SC2008 recommended not required — verified via curriculum-outline.md and NTUMods MPE sheet. Diagram uses SC1006 as hinge; Ch6 revisits VM invariants, Ch7 previews SC4051 consensus reasoning at hardware level.

## Build Invariants & Pedagogy

Book class `11pt a4paper`, geometry `1.3/1.2cm includeheadfoot`, `setstretch 1.20`, `parskip 0.70em`, TikZ `scale 0.82–0.88`, `lstset` coloured above, `hyperref` links, `pdflatex×2` → `grep -c "! " 0`, `pgfkeys 0`, `Overfull>15pt 0`. 0→100 law: intuition→picture→formal→worked example→proof sketch→exercise; no word limit, depth over brevity; small-screen verified.

Sources: NTUMods SC3050 description (CPU arch, ISA, pipeline/hazards, CISC/RISC/VLIW, ILP, cache/VM/MMU, superscalar/branching, multithreading, I/O/buses, arithmetic, multiprocessing/coherence, SoC/GPU/low-power), CCDS curriculum 135 AU map, SC1006 ch01–08 for continuity (ISAs, pipeline, cache, VM, I/O, perf).
