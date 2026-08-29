# SC4064 GPU Programming — Module Outline

> **Code:** SC4064 (3 AU, MPE) · **Prereq:** SC4050 Parallel Computing (or SC1006 + SC2005) · **Lineage:** SC1006 → SC2005 → SC4050 → SC4064 · **Sem:** Y3/Y4 MPE · **Model:** muse-spark-1.2-contributor only (retry on 500/503, no fallback)

## Module Overview

SC4064 is the GPU-centric MPE that turns a parallel-computing student into a CUDA programmer. Where SC1006 explains *what* a processor does (ISA, pipeline, cache) and SC4050 teaches *parallel thinking* (threads, speedup, Amdahl, shared vs distributed memory), SC4064 asks *how to harness thousands of GPU cores for real speed*: write kernels, master the memory hierarchy, hide latency, and call high-performance libraries. 0→100 ground-up: every chapter opens with intuition (factory assembly line, laundry pipeline, library-desk cache) → formalism (grid/block/thread, SIMT, coalescing) → worked numbers (occupancy, bandwidth, Roofline) → runnable CUDA C++.

Assumes only SC1006 (datapath/cache) + SC2005 (threads/scheduling) + SC4050 intuition (parallel speedup); CUDA, SIMT, and GPU memory are defined on first use — no prior GPGPU assumed. Complements SC3050 (advanced arch/GPU as accelerator) and SC4001 (GPU for deep learning) with hands-on optimisation.

Position: SC1006 → SC2005 → SC4050 → **SC4064** (GPU leaf). MPE 3 AU, needs ≥4× SC4xxx; complements HPC/AI specialisation (15 AU).

## Chapter Plan (8 chapters, ~200–260 lines each)

**Ch1 — Heterogeneous Foundations:** CPU latency vs GPU throughput; when GPUs win (data-parallel, high arithmetic intensity); heterogeneous system (host/device, PCIe, unified memory); first `vectorAdd` kernel.
LOs: (a) contrast latency vs throughput cores; (b) place workloads on throughput spectrum; (c) compile & run a 1-thread → N-thread kernel and explain host/device split.

**Ch2 — CUDA Model I: Grids, Blocks & Threads:** kernel launch `<<<grid,block>>>`, threadIdx/blockIdx/blockDim/gridDim, 1-D/2-D/3-D indexing, bounds checks, mapping data → threads.
LOs: (a) map array/matrix elements to thread hierarchy; (b) compute grid size with ceiling division; (c) write correct indexed kernels without races.

**Ch3 — CUDA Model II: Warps, SIMT & Divergence:** warp = 32 threads, SIMT vs SIMD, warp scheduler, divergence/convergence, `__syncwarp`, independent thread scheduling (Volta+), occupancy vs latency hiding.
LOs: (a) trace warp execution under `if/else` divergence; (b) compute achieved vs theoretical occupancy; (c) refactor branchy code to reduce divergence.

**Ch4 — Memory Hierarchy & Coalescing:** global/shared/constant/texture, L1/L2, registers, coalesced vs strided access, shared-memory tiling, bank conflicts, unified memory & prefetch.
LOs: (a) diagram GPU memory pyramid with scope/lifetime; (b) analyse access pattern for coalescing; (c) tile matrix multiply in shared memory and quantify reuse.

**Ch5 — Synchronization & Concurrency:** `__syncthreads`, `__syncthreads` pitfalls, atomics, warp shuffles, streams/events, overlapping copy & compute (`cudaMemcpyAsync`), graphs.
LOs: (a) place barriers to avoid races without deadlock; (b) use atomics/shuffles for reductions; (c) overlap H2D/compute/D2H with 2+ streams and verify via timeline.

**Ch6 — Performance Optimisation & Profiling:** Roofline for GPUs, occupancy calculator, instruction & memory throughput, bank-conflict & partition camping, Nsight Systems/Compute workflow, optimisation checklist.
LOs: (a) place kernel on Roofline (compute vs bandwidth bound); (b) drive Nsight to find limiter (occupancy, bandwidth, divergence); (c) apply 3+ optimisations and report speedup.

**Ch7 — Libraries & Multi-GPU Patterns:** cuBLAS/cuFFT/Thrust/cuDNN, cooperative groups, stencil/halo, sparse (cuSPARSE), reduction/scan primitives, single → multi-GPU (NCCL, peer copy).
LOs: (a) replace hand kernel with Thrust/cuBLAS and compare; (b) implement tiled stencil with halo exchange; (c) sketch multi-GPU decomposition and reason about scaling.

**Ch8 — Applications & Future:** deep-learning training/inference (GEMM, Tensor Cores, mixed precision), graphics/compute interop, scientific HPC case study (e.g., n-body), power/perf, Grace-Hopper & beyond.
LOs: (a) map DL operator to Tensor Core tile; (b) end-to-end profile a mini-app (e.g., image blur or matmul) and argue bottleneck; (c) discuss precision vs throughput and future heterogeneity.

## TikZ Diagram Plan (2–3 per chapter, colour fills blue!15/green!20/orange!15/violet!10/red!12, legend, labelled)

- **Ch1:** (a) CPU (few big cores, blue!15) vs GPU (many small cores, green!20) throughput vs latency; (b) host-device system with PCIe (orange!15 arrow) + unified memory; (c) speedup vs data-parallel fraction (Amdahl/Gustafson) with GPU ceiling.
- **Ch2:** (a) grid→block→thread hierarchy 3-level (blue!15 grid, green!20 blocks, orange!15 threads) with 2-D example; (b) thread-index math `tid = blockIdx*blockDim+threadIdx` with colour mapping; (c) launch config ceiling-division diagram.
- **Ch3:** (a) warp of 32 threads (4×8 grid, 2 warps coloured differently) + SIMT lane diagram; (b) divergence fork/join timeline (green converged, red divergent, violet reconvergence); (c) occupancy vs block-size bar (active warps/SM, red limit).
- **Ch4:** (a) memory pyramid registers→shared→L1/L2→global→host (blue→green→orange→violet) with bandwidth labels; (b) coalesced (green!15 aligned) vs strided (red!12 scattered) global access; (c) shared-memory tiling for matMul (halo + bank-conflict colour conflict red).
- **Ch5:** (a) `__syncthreads` barrier timeline (threads arrive→wait→release, violet!10); (b) streams timeline H2D→kernel→D2H overlapped (3 colours blue/green/orange); (c) atomics vs shuffle reduction tree comparison.
- **Ch6:** (a) GPU Roofline (ridge point, green compute-bound, orange bandwidth-bound, kernel dot); (b) Nsight timeline (kernel, memcpy, occupancy gauge blue→red); (c) optimisation checklist flowchart (divergence→coalescing→shared→occupancy).
- **Ch7:** (a) library stack Thrust/cuBLAS→CUDA runtime→driver (layered blue!12/green!14/orange!12); (b) stencil halo exchange (neighbour blocks with orange halo); (c) multi-GPU ring with NCCL (2–4 GPUs, violet all-reduce arrows).
- **Ch8:** (a) Tensor Core 4×4×4 tile (blue A, green B, orange C, yellow accumulator); (b) end-to-end app pipeline (preprocess→GPU kernel→postprocess) with power/perf annotation; (c) mixed-precision throughput vs accuracy trade-off curve.

## lstlisting Plan (listings with language=C++ / CUDA C++, colours keyword blue!60!black, comment green!50!black, string orange!60!black, numbers gray, xleftmargin 1em)

- **Ch1:** `C++` — host/device split `vectorAdd<<<1,1>>>` → `<<<N/256,256>>>`, `cudaMalloc/cudaMemcpy` HelloWorld; `Python` — CPU vs GPU throughput back-of-envelope (ops/s).
- **Ch2:** `C++` — 1-D/2-D indexed kernels (vector add, matrix add) with ceiling division and bounds check; `C++` — 2-D image kernel (`threadIdx.x + blockIdx.x*blockDim.x`).
- **Ch3:** `C++` — divergence demo (`if (tid%2)`) before/after refactor; occupancy query via `cudaOccupancyMaxActiveBlocksPerMultiprocessor`.
- **Ch4:** `C++` — naive vs tiled `matMul` (shared `__shared__ float tile[16][16]`, `__syncthreads`), coalescing microbench.
- **Ch5:** `C++` — stream overlap (`cudaStreamCreate`, `cudaMemcpyAsync`, events timing), warp-shuffle reduction (`__shfl_down_sync`).
- **Ch6:** `C++` — Nsight-instrumented kernel + Roofline calculator; optimisation delta (coalesced + shared + unrolled) with `nvprof` timing.
- **Ch7:** `C++` — Thrust `transform/reduce` vs hand kernel, cuBLAS `cublasSgemm` call, cooperative-groups `this_thread_block().sync()`.
- **Ch8:** `C++` — Tensor Core WMMA `wmma::fragment` + mixed-precision `__half` demo; `Python` — PyTorch GPU timing harness for comparison.

## Exercise Themes (per chapter, exam-style + hands-on)

- **Ch1:** latency vs throughput classification; Amdahl for GPU offload; compile/run HelloWorld, vary N and time host→device.
- **Ch2:** hand-compute `tid` for 1-D/2-D launches; ceiling-division sizing; fix out-of-bounds bug; map 1024×1024 image to 16×16 blocks.
- **Ch3:** warp-divergence trace table; occupancy calculator (register/shared limits); refactor `if (threadIdx.x < 16)` to branchless.
- **Ch4:** coalescing analysis (stride 1 vs 32); bank-conflict detection (32-way shared); tile-size sweep for matMul and report bandwidth.
- **Ch5:** barrier placement (deadlock hunt); atomics vs shuffle correctness; 2-stream overlap schedule and event-measured speedup.
- **Ch6:** Roofline placement (is kernel bound?); Nsight Systems trace reading; 3-step optimisation lab (+2× speedup required).
- **Ch7:** Thrust vs hand performance; stencil halo correctness; 1→2 GPU scaling prediction vs NCCL measurement.
- **Ch8:** Tensor Core vs FP32 throughput math; end-to-end mini-app profiling report; precision-accuracy trade-off justification.

## Prerequisite Graph

```
SC1003 → SC1006 (ISA, datapath, cache, perf) ─┐
SC1005 → SC1006 ───────────────────────────────┤
SC1003 → SC1007 → SC2005 (threads, scheduling) ┤→ SC4050 (parallel concepts, speedup) → SC4064 (CUDA, memory, optimisation, libraries)
SC1006 + SC2005 ──→ SC3050 (arch complement)    │
SC2001/MH1812 ──→ algorithmic maturity only      ┘
```

Formal MPE prereq per 2024 sheet: SC4050 (or SC1006+SC2005 if SC4050 not taken) — 0→100 text re-derives thread/block intuition so SC4050 is *recommended* not strictly blocking. Ch1 revisits OS-thread vs GPU-thread; Ch4 revisits cache/AMAT.

## Build Invariants & Pedagogy

Book `11pt a4paper`, geometry `1.3/1.2cm includeheadfoot`, `setstretch 1.20`, `parskip 0.70em`, TikZ `scale 0.70–0.82`, `lstset` coloured above, `hyperref` links, `pdflatex×2` → `grep -c "! " 0`, `pgfkeys 0`, `Overfull>15pt 0`. 0→100: intuition→picture→formal→worked example→runnable CUDA→exercise; no word limit, depth over brevity; small-screen verified.

Sources: CCDS MPE catalogue (SC4050/SC4064 3 AU), NTUMods SC1006/SC2005/SC4050 prereq chain, SC3050 OU ch06/ch08 GPU complements, CUDA Toolkit docs (grid/block/warp, memory, streams, WMMA), SC4001 GPU-for-DL linkage.
