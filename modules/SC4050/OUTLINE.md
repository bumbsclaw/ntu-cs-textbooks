# SC4050 Parallel Computing — Module Outline

> **Code:** SC4050 (3 AU, MPE) · **Prereq:** SC2001 (NTUMods) · **Pedagogical lineage:** SC1006 pipeline + SC2005 threads (SC1007 via SC2001) · **Type:** Major Prescribed Elective (≥4× SC4xxx) · **Model:** muse-spark-1.2-contributor only

## Module Overview

SC4050 turns a correct sequential program into a *fast* parallel one. Where SC1006 builds a pipelined datapath and SC2005 creates threads that share memory, SC4050 asks how to *decompose* work, *map* it to cores/nodes/GPUs, and *reason* about speedup and cost. 0→100 ground-up: every chapter opens with intuition (kitchen brigade, highway lanes, Amdahl's ceiling), then formalism, worked numbers (speedup, efficiency, isoefficiency), and runnable C/OpenMP/MPI snippets. Assumes only SC1006 ch04 pipeline + SC2005 ch02 threads + SC2001 divide-and-conquer; all parallelism metrics re-derived on first use.

Position in curriculum: NTUMods lists SC2001 as sole formal prereq; pedagogically SC4050 builds on SC1006 pipeline/throughput and SC2005 threads/synchronization, then feeds SC4064 GPU Programming and SC4051 Distributed Systems. Mirrors the official 4-component syllabus: foundations → architectures → algorithm patterns → programming & performance.

## Chapter Plan (8 chapters, ~200–260 lines each)

**Ch1 — Foundations: Concurrency vs Parallelism, Decomposition:** concurrency/parallelism, task vs data decomposition, granularity, dependencies (Bernstein), performance metrics (speedup, efficiency, cost, overhead).
Outcomes: (a) distinguish concurrency/parallelism; (b) decompose a problem by task/data/domain; (c) compute speedup/efficiency/cost and identify overhead sources.

**Ch2 — Parallel Architectures & Execution Models:** Flynn (SISD/SIMD/MIMD), shared-memory UMA/NUMA vs distributed-memory, multicore/cache coherence (MESI recall from SC3050/SC1006), interconnects, hardware impact on performance.
Outcomes: (a) classify architecture by Flynn/memory model; (b) explain coherence/false-sharing cost; (c) predict locality/bandwidth bottlenecks.

**Ch3 — Performance Laws & Scalability:** Amdahl's law (fixed-size), Gustafson (scaled), isoefficiency, Amdahl ceiling with serial fraction, weak vs strong scaling, Roofline model.
Outcomes: (a) apply Amdahl/Gustafson to bound speedup; (b) plot strong/weak scaling and diagnose saturation; (c) place a kernel on Roofline (compute vs memory bound).

**Ch4 — Shared-Memory Programming with OpenMP:** pthreads recap → OpenMP fork-join, `parallel for`, `sections`/`task`, data scoping (`private`/`shared`/`reduction`), synchronization (`critical`/`atomic`/`barrier`), false sharing, scheduling (`static`/`dynamic`/`guided`).
Outcomes: (a) parallelise a loop with correct scoping; (b) choose schedule and measure imbalance; (c) fix races and false sharing.

**Ch5 — Distributed-Memory Programming with MPI:** rank/communicator, point-to-point (`Send`/`Recv`, blocking vs non-blocking), collective (`Bcast`/`Scatter`/`Gather`/`Reduce`/`Allreduce`), domain decomposition, halo exchange, communication cost (latency vs bandwidth).
Outcomes: (a) write blocking/non-blocking point-to-point; (b) select collective for a pattern; (c) model communication overhead for 1D/2D decomposition.

**Ch6 — Synchronization, Consistency & Load Balancing:** races/locks/semaphores recap, barriers, memory consistency (SC vs weak), load imbalance, static vs dynamic balancing, work-stealing, deadlock/livelock in parallel context.
Outcomes: (a) walk a race to a barrier/lock fix; (b) reason about fence placement under weak consistency; (c) compare static partition vs work-stealing via Gantt.

**Ch7 — Parallel Algorithm Design Patterns:** divide-and-conquer (parallel merge-sort), pipeline, task parallelism, data-parallel/stencil, master-worker, bag-of-tasks, isoefficiency-driven design, case studies (matrix multiply, prefix sum).
Outcomes: (a) design a divide-and-conquer parallel algorithm; (b) map pipeline/stencil to OpenMP/MPI; (c) analyse isoefficiency and scalability.

**Ch8 — Heterogeneous & GPU Computing, Performance Engineering:** CPU vs GPU (SIMT warps, coalescing, shared memory), CUDA/OpenACC offload, heterogeneous scheduling, communication-computation overlap, profiling (`perf`, `nvprof`), capstone mini-app.
Outcomes: (a) contrast CPU thread vs GPU warp execution; (b) optimise coalescing/shared-memory tiling; (c) overlap comm/comp and profile a scaling study.

## TikZ Diagram Plan (2–3 per chapter, colour fills blue!15/green!20/orange!15/violet!10/red!12, legend, labelled)

- **Ch1:** (a) concurrency vs parallelism Venn/timeline (blue!15 interleaved vs green!15 simultaneous); (b) task vs data decomposition tree vs grid (orange/violet); (c) speedup vs p ideal vs overhead gap (red dashed overhead).
- **Ch2:** (a) UMA/NUMA vs distributed cluster side-by-side (blue!12 shared bus vs green!12 network); (b) cache-coherence MESI snoop with private L1s (orange!15); (c) interconnect crossbar vs mesh hop-count (violet!10).
- **Ch3:** (a) Amdahl ceiling curves by serial fraction f; (b) Gustafson scaled-speedup lines; (c) Roofline ridge with compute/memory-bound kernels (green/red dots).
- **Ch4:** (a) OpenMP fork-join with master→team→join (blue→green→blue); (b) `parallel for` worksharing chunk distribution static vs dynamic (striped); (c) race → critical/atomic fix timeline (red→green).
- **Ch5:** (a) MPI ranks + communicator ring/grid (blue!15 nodes); (b) point-to-point vs collective (Bcast/Reduce) arrows (orange!15 collective fan); (c) 2D domain decomposition with halo exchange (violet ghost cells).
- **Ch6:** (a) barrier/lock busy-wait timeline Gantt (red stall vs green balanced); (b) false-sharing cache-line ping-pong (two cores, red invalidations); (c) work-stealing deque per worker with steal arrows.
- **Ch7:** (a) parallel divide-and-conquer recursion tree with spawn/sync (blue→green leaves); (b) pipeline stages with throughput fill (orange!15); (c) stencil 5-point with halo communication (violet halo band).
- **Ch8:** (a) CPU core vs GPU SM/warp diagram (blue CPU vs green GPU SM); (b) heterogeneous offload timeline CPU→GPU→CPU with overlap (orange overlap band); (c) strong vs weak scaling plot with ideal diagonal (red vs green).

## lstlisting Plan (listings with language=, colours keyword blue!60!black, comment green!50!black, string orange!60!black, numbers gray, xleftmargin 1em)

- **Ch1:** `C` — sequential vs parallel timing harness; `Python` — speedup/efficiency calculator and overhead plot.
- **Ch2:** `C` — false-sharing microbenchmark (padded vs unpadded, `perf` cache-miss); `Python` — UMA vs NUMA bandwidth model.
- **Ch3:** `Python` — Amdahl/Gustafson sweep plotter; `C` — Roofline ridge calculator (flops/byte).
- **Ch4:** `C` — OpenMP `parallel for` + `reduction` + `schedule(static/dynamic)` + `critical`/`atomic` (compile with `-fopenmp`); `C` — task parallelism via `omp task`.
- **Ch5:** `C` — MPI `MPI_Send`/`Recv` ping-pong + `MPI_Bcast`/`Reduce`/`Allreduce` + non-blocking `Isend`/`Irecv`/`Wait`; 2D halo exchange skeleton.
- **Ch6:** `C` — barrier (`omp barrier` + `MPI_Barrier`) + work-stealing queue skeleton (pthreads + deque); `Python` — load-imbalance Gantt simulator.
- **Ch7:** `C` — parallel merge-sort (OpenMP tasks) + stencil `for` with halo; `Python` — isoefficiency solver.
- **Ch8:** `C` — CUDA kernel `__global__` matmul (coalesced vs naive) + OpenMP target offload; `Python` — strong/weak scaling profiler plot.

## Exercise Themes (per chapter, exam-style + hands-on)

- **Ch1:** decompose word-count / matrix-vector by task/data; compute speedup/efficiency/cost; Bernstein dependency check.
- **Ch2:** classify Flynn cases; MESI walk for 2-core trace; NUMA locality placement and false-sharing fix.
- **Ch3:** Amdahl bound with f=5%/1%; Gustafson scaled prediction; Roofline placement and ridge analysis; isoefficiency derivation.
- **Ch4:** fix `private`/`reduction` bugs; compare `static` vs `dynamic` on irregular loop; measure speedup vs threads (`OMP_NUM_THREADS`).
- **Ch5:** write `Send`/`Recv` vs `Bcast`/`Reduce` equivalence; time blocking vs `Isend`/`Irecv` overlap; 1D vs 2D decomposition comm volume.
- **Ch6:** Gantt-trace imbalance and rebalance; fence placement litmus; work-stealing steal-count simulation.
- **Ch7:** parallel prefix-sum / merge-sort span analysis; pipeline throughput calc; stencil halo width vs comm trade-off.
- **Ch8:** coalescing vs strided CUDA timing; overlap comm/comp with `MPI_Isend` + compute; mini-app weak/strong scaling report with profiling.

## Prerequisite Graph

```
SC1005 → SC1006 (ISA, datapath, pipeline, cache, perf) ─┐
SC1003 → SC1007 → SC2001 (D&C, recurrences, big-O) ─────┤→ SC4050 → SC4064
SC1006 + SC1007 → SC2005 (processes, threads, sync) ────┘        ↘ SC4051
SC3050 (coherence/MESI, optional deepening) ──────────────────────→ SC4050 Ch2/Ch6
```

Formal prereq per NTUMods: SC2001 only; SC1006/SC2005 are pedagogical lineage (pipeline throughput + threads/sync) verified via SC1006 ch04 and SC2005 ch02.

## Build Invariants & Pedagogy

Book class `11pt a4paper`, geometry `1.3/1.2cm includeheadfoot`, `setstretch 1.20`, `parskip 0.70em`, TikZ `scale 0.82–0.88`, `lstset` coloured above, `hyperref` links, `pdflatex×2` → `grep -c "! " 0`, `pgfkeys 0`, `Overfull>15pt 0`. 0→100 law: intuition→picture→formal→worked example→proof sketch→exercise; no word limit, depth over brevity; small-screen verified.

Sources: NTUMods SC4050 description (4-component syllabus: foundations, architectures, algorithm patterns, programming & performance; prereq SC2001, mutually exclusive CE4011/CZ4011) extracted 2026-08-28 via `ntumods.com/mods/SC4050` SSR props; CCDS 135 AU map; SC1006 ch04 pipeline + SC2005 ch02 threads for lineage; SC3050 coherence + SC4051/SC4064 adjacency for HPC track.
