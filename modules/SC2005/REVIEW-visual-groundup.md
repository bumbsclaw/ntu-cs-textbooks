# Visual + Ground-Up QA — SC2005 Operating Systems (ch01–08) — Reviewer C

Date: 2026-08-23 · Reviewer: Visual QA (muse-spark-1.2-contributor)
Scope: `chapters/ch01-intro.tex` · `ch02-processes.tex` · `ch03-scheduling.tex` · `ch04-synchronization.tex` · `ch05-deadlocks.tex` · `ch06-memory.tex` · `ch07-virtual-memory.tex` · `ch08-filesec.tex` · `main.tex`
Baseline: 36p / 610 KB / 0 `! ` / 0 pgfkeys Error / 0 Overfull>15pt · Build: `pdflatex -interaction=nonstopmode main.tex` ×2 → exit 0
Line budget: 205 / 201 / 204 / 206 / 202 / 203 / 202 / 206 (all ≤260)

---

## Verdict: PASS

All visual-QA gates pass. No `verbatim`, all `lstlisting` carry `language=C`, all 24 TikZ figures carry colour fills where pedagogically useful (2 patched this review), max Overfull 5.1pt (<15pt), zero-prior and intuition→formal satisfied for scheduling/sync/deadlocks/paging.

---

## Compile Check

| Check | Result |
|-------|--------|
| `pdflatex` exit 0 (×2) | PASS |
| `grep "^! "` | 0 |
| `grep "pgfkeys.*Error\|Package pgf Error"` | 0 |
| `grep "Token not allowed"` (hyperref) | 0 |
| `Overfull \hbox >15pt` | 0 (max 5.11pt at `ch03:186--188` — exercise math line, not a display) |
| `multiply defined` label | 0 |
| `pdfinfo Pages` | 36 |
| `du -k main.pdf` | 596 KB (609773 bytes) |

Second pass confirms no new overfulls introduced by patches. Remaining 5.1pt is an inline-math exercise line (`For bursts $P_1{=}8, P_2{=}4, P_3{=}2$…`) — hyphenation artefact, not a formula overflow or layout failure; no action required at this gate.

---

## Code Highlighting Audit — FAIL if plain verbatim

| Chapter | `lstlisting` blocks | `language=` | `verbatim`/`minted` | Verdict |
|---------|---------------------|-------------|----------------------|---------|
| ch01 intro | 1: copy-file (POSIX `open/read/write`) | `language=C` | 0 | **PASS** — captioned, `main.tex` `\lstset` provides `keywordstyle blue!70!black`, `comment green!50!black`, `string orange!70!black`, `numbers left` |
| ch02 processes | 3: fork–exec–wait · pthreads parallel sum · exercise `fork()/x++` | `language=C` ×3 (exercise block also `language=C`) | 0 | **PASS** — all three carry `language=C`; 6 boundary lines for the two captioned + 2 for exercise |
| ch03 scheduling | 1: FCFS vs SJF wait sketch | `language=C` | 0 | **PASS** |
| ch04 synchronization | 4: Peterson · CAS spinlock · bounded-buffer (sem) · monitor+bcond (pthreads) | `language=C` ×4 | 0 | **PASS** |
| ch05 deadlocks | 1: ordered chopstick acquisition | `language=C` | 0 | **PASS** |
| ch06 memory | 1: two-level page-table walk | `language=C` | 0 | **PASS** |
| ch07 virtual memory | 1: LRU fault simulation | `language=C` | 0 | **PASS** |
| ch08 filesec | 1: UNIX permission check (`stat`) | `language=C` | 0 | **PASS** |

Totals: `grep -rn lstlisting chapters/` → 13 blocks (26 boundary lines counting `\begin`+`\end`), **all carry `language=C`**; `grep -rn verbatim` → 0. Gate requires 0 verbatim and ≥8 `lstlisting[C]` with `language=` — satisfied (13/8). No patch needed.

---

## Diagram Colour-Fill Audit — 24 TikZ, FAIL if lines-only when colour useful

Target: every pedagogical diagram uses fills (`blue!12` etc) for state/type distinction, plus a legend or labelled fills. Misses are lines-only boxes/arrows where colour would carry meaning.

| # | Figure | Required cue | Fills found | Verdict |
|---|--------|--------------|-------------|---------|
| 1 | ch01 `fig:os-layers` (user→kernel→hw layers) | privilege layers distinct | `blue!15` (app) · `green!15` (libs) · `orange!18` (kernel) · `violet!12` (hw); edges `blue!60!black` / `red!60!black dashed` | **PASS** |
| 2 | ch01 `fig:syscall-path` (trap→dispatch→return) | user vs kernel mode zones | `blue!12` (user nodes) · `orange!16` (kernel nodes); `fit` dashed kernel-mode box | **PASS** |
| 3 | ch01 `fig:interrupt` (5-stage pipeline) | pipeline stages distinct | `blue!12` · `orange!15` · `green!14` · `violet!12` · `blue!10`; staged left→right→return | **PASS** |
| 4 | ch02 `fig:proc-states` (5-state model) | state colours; dispatch vs I/O vs exit edges distinct | `blue!12/green!14/orange!18/violet!12/gray!18`; edges `blue!60!black/red!60!black/green!50!black` | **PASS** |
| 5 | ch02 `fig:fork-tree` (process tree) | parent vs children vs grandchild | `blue!13/green!14/orange!14/violet!12`; `COW` label; `blue!60!black/green!50!black` edges | **PASS** |
| 6 | ch02 `fig:threads` (threads sharing addr space) | per-thread private vs shared | `blue!12` (addr space) · `green!14/orange!15` (threads) · `violet!12` (shared); dashed sharing edges | **PASS** |
| 7 | ch03 `fig:gantt` (FCFS/SJF/RR Gantts) | job colours consistent across three Gantts | FCFS+SJF: `blue!16(P1)/green!16(P2)/orange!16(P3)`; RR: `blue!12/green!12/orange!12` slices | **PASS** |
| 8 | ch03 `fig:rr-intuition` (queue-length vs time) | RR vs FCFS queue bands + legend | **PATCHED**: `blue!6` canvas · `red!5` FCFS band · `white`/`blue!12`/`red!10` labels · `blue!14/red!12` legend swatches; was lines-only axes + two unfilled labels | **PASS** — now carries fills + legend |
| 9 | ch03 `fig:mlfq` (Q0→Q1→Q2 demote/boost) | priority levels + demote vs boost fibres | `blue!14/green!14/orange!15` queues; `blue!60!black` demote · `red!60!black dashed` boost | **PASS** |
| 10 | ch04 `fig:peterson` (4-node flow) | intend → spin → CS → release | `blue!12/orange!15/green!14/violet!12`; `blue!60!black/green!50!black/red!60!black` edges + spin loop | **PASS** |
| 11 | ch04 `fig:semaphore` (wait→CS→signal) | wait vs CS vs signal zones; invariant | `blue!12/green!14/orange!15`; `blue!60!black` + `red!60!black dashed` next-waiter; `fit` invariant box | **PASS** |
| 12 | ch04 `fig:monitor` (cond-var pattern) | enter → predicate → work/wait → exit | `blue!12/orange!15/green!14/violet!12/gray!14`; `green!50!black` true · `red!60!black` false · dashed wait→check | **PASS** |
| 13 | ch05 `fig:rag-cycle` (2-process deadlock cycle) | process vs resource node types; request vs holds | `blue!14` circles (P) · `orange!16` rects (R); `blue!60!black` requests · `red!60!black` holds | **PASS** |
| 14 | ch05 `fig:rag-3cycle` (3-process cycle) | three-way wait ring | `blue!12` circles · `green!14` rects; mixed red/blue edges | **PASS** |
| 15 | ch05 `fig:banker` (Banker flow) | request→tentative→safety→grant/deny | `blue!12/orange!15/green!14/violet!12/red!14`; `blue!60!black/green!50!black/red!60!black` outcomes | **PASS** |
| 16 | ch06 `fig:contiguous` (memory map + holes) | OS vs processes vs holes | `blue!14/green!14/orange!14/violet!12/gray!14`; `red!60!black` fragmentation arrow; `white` caption | **PASS** |
| 17 | ch06 `fig:paging` (VA→PT→PA→RAM) | VA vs PT vs PA vs RAM stages | `blue!12/orange!16/green!14/violet!12`; `blue!60!black` lookups + `red!60!black dashed` offset passthrough | **PASS** |
| 18 | ch06 `fig:segpage` (seg→PT→frame) | segmentation + paging legs | `blue!12/orange!15/green!14/violet!12`; staged `blue!60!black` arrows | **PASS** |
| 19 | ch07 `fig:demand-paging` (valid? → fast vs fault) | valid vs fault paths; disk stage | `blue!12/orange!15/green!14/red!14/violet!12`; `blue!60!black/green!50!black/red!60!black` fast-vs-fault | **PASS** |
| 20 | ch07 `fig:clock` (circular hand sweep) | frames + R bits + hand + sweep | `blue!12` frames (A–D) with `R=0/1`; `red!60!black` hand · `green!50!black` sweep arc | **PASS** |
| 21 | ch07 `fig:belady` (faults vs frames) | LRU monotonic vs FIFO Belady bump | **PATCHED**: `blue!6` canvas · `blue!12/red!12/orange!12` curve labels · `blue!14/red!12` legend swatches; was lines-only 4.5 cm of axes + two unfilled labels; `blue!60!black` (LRU) vs `red!60!black dashed` (FIFO) · `orange!70!black` anomaly arrow retained | **PASS** — now `blue!/red!/orange!` fills + legend |
| 22 | ch08 `fig:inode` (direct+indirect chain) | inode vs direct vs indirect levels | `blue!13` inode · `green!13/10` data · `orange!14/10` indirect · `violet!12` double-indirect; `blue!60!black/orange!70!black/violet!70!black` pointer edges | **PASS** |
| 23 | ch08 `fig:fat` (FAT walk) | FAT entries + file chains | `blue!12`(free) · `green!14/10`(File A chain) · `orange!14`(free) · `violet!12/10`(File B chain); chain labels `blue!60!black/violet!60!black` | **PASS** |
| 24 | ch08 `fig:disk-sched` (SCAN vs C-SCAN) | request dots + sweep fibres | `blue!60!black` request dots; `green!50!black` SCAN →→reverse dashed · `orange!70!black` C-SCAN always-→ | **PASS** — schematic sweep figure; fills on dots + sweep labels suffice |

Count: `grep -rn "begin{tikzpicture}" chapters/` → 24. `grep -c "fill=" chapters/*.tex` post-patch: ch01 11 · ch02 13 · ch03 20 · ch04 12 · ch05 11 · ch06 14 · ch07 12 · ch08 15 (was 6 in ch07 pre-patch, 15 in ch03 pre-patch). All 24 carry `fill=` with `blue!/green!/orange!/violet!/red!` tints; no monochrome-when-colour-useful remains.

---

## Zero-Prior (processes as programs in execution, not assumed)

Gate: first mention of process, PCB, thread, burst, semaphore, deadlock, page, fault, thrashing must be defined in-text on first use, not assumed from prerequisite. Verdict by chapter:

| Chapter | New abstractions | Defined ground-up? | Gaps |
|---------|-----------------|--------------------|------|
| ch01 intro | OS / kernel / dual-mode / privileged instruction / system call / trap / interrupt / DMA / storage hierarchy | **Yes** — `Definition: Kernel`, mode-bit model, `privileged instruction → trap` explicitly; storage hierarchy enumerated before caching/paging are invoked; OS structures (monolithic/layered/µkernel/modular) sketched with examples (Linux, Mach, seL4) | None blocking. DMA gloss is brief; acceptable at intro scope. |
| ch02 processes | program vs process / address space (text/data/heap/stack) / PCB / 5-state model / context switch / fork+COW / exec / wait / zombie vs orphan / thread / user vs kernel threads / IPC | **Yes** — `program is passive … process is active` paragraph is the canonical zero-prior opening; PCB contents listed; 5-state diagram preceded by text definition; `fork` return-value contract (0 vs PID vs −1) stated; COW explained with sharing-then-copy; threads `PC+regs+stack` vs shared `text/data/heap/files` made explicit | None blocking. Recommend term "COW" expanded once more in ch02 remark (already done). |
| ch03 scheduling | CPU vs I/O bursts / criteria (util/throughput/turnaround/waiting/response/fairness) / FCFS/SJF/SRTF/RR/Priority/aging/starvation/convoy/quantum/MLFQ/multicore/RT/CFS | **Yes** — `Definition: Burst` + exponential intuition; each classical algorithm gets a paragraph of mechanics before Gantt; MLFQ rules enumerated as 4 bullets before the figure; `Little's Law L=λW` introduced as a Remark tying queue length to wait | Minor nit: "SRTF is preemptive SJF" stated without a one-line preemption definition repeat — mitigated because preemptive vs nonpreemptive defined two paragraphs earlier; no patch. |
| ch04 synchronization | race / critical section + 3 requirements (mutual excl / progress / bounded wait) / Peterson / TSL-CAS-fetchAdd / semaphore vs mutex / blocking vs spinning / producer–consumer / monitor+cond-var / spurious wakeups | **Yes** — `count++ = load–inc–store` lost-update intuition before formalism; 3 CS requirements as enumerated definition; Peterson shared variables `flag[2]+turn` declared before code; hardware atomics glossed as "each completes atomically in hardware"; semaphore `S≥0` invariant boxed | Peterson "sequentially consistent" caveat correctly flagged. Exercise 4.2 cross-refs ch05 deadlock when mutex-before-count ordering is swapped — intentional forward link. |
| ch05 deadlocks | resource type/instance / request→use→release / deadlock / Coffman 4 conditions / RAG + request/assignment edges / cycle⇔deadlock nuance / prevention vs avoidance / safe state / Banker's / detection vs ostrich / dining philosophers | **Yes** — `Theorem: Coffman conditions` with 4 labelled items; RAG node/edge vocabulary defined before the two cycle figures; multi-instance nuance ("cycle necessary not sufficient") stated; safe-state search procedure laid out before Banker figure; ostrich labelled explicitly | See Gaps below on Banker's worked example brevity. |
| ch06 memory | logical vs physical / MMU / binding times (compile/load/exec) / contiguous+base/limit / external fragmentation / compaction / first/best/worst-fit / paging+frames / offset / internal fragmentation / TLB+hit-rate formula / multi-level tables / segmentation vs paging / segmented-paging / R/W/X bits / COW phrased via PTE bits | **Yes** — logical→physical translation framed before relocation vs paging; external fragmentation picture before allocation strategies; paging `f×PAGE_SIZE+d` formula immediately after page/frame definition; TLB effective-time derived with numbers; `Remark: internal vs external` contrasts both fragmentations | None blocking. Huge-pages remark correctly contrasts TLB pressure vs internal fragmentation. |
| ch07 virtual memory | demand paging / valid+dirty+ref bits / page fault / fault service time / COW vs mmap / FIFO/OPT/LRU/Clock+reference bit / Belady anomaly + stack-algorithm intuition / working set W(t,Δ) / thrashing / global vs local replacement / prepaging | **Yes** — demand-paging flow figure is preceded by valid/dirty/retinal bit definitions and "find free frame or evict → read from disk → restart instruction" lifecycle; each replacement policy gets a one-line mechanism; Belady Remark gives stack `M(k)⊆M(k+1)` intuition; `W(t,Δ)` formally defined before thrashing cures | None blocking. |
| ch08 filesec | file attributes / allocation (contiguous/linked/FAT/indexed-inode + direct/indirect) / directory→inode mapping / journaling+replay / bitmap vs free-list / disk seek+rotation / FCFS/SSTF/SCAN/C-SCAN/LOOK / polling vs interrupt vs DMA / buffering+page cache / ACL vs capability / threat model | **Yes** — each allocation method gets trade-offs in the same list that introduces it; journaling `write-ahead log → checkpoint → replay` lifecycle stated; disk schedulers each get one-line discipline + starvation note; ACL vs capability as two bullet definitions; SSD Remark contrasts seek vs wear-level/parallelism | None blocking. |

Overall zero-prior: **PASS**. The book honours "processes as programs in execution" (ch02 quote) and never assumes scheduling/sync/deadlock/paging vocabulary before defining it.

---

## Intuition → Formal

Gate: for scheduling · synchronization · deadlocks · paging each concept must appear as intuition/picture/analogy first, then formal definition or algorithm, then worked example or Gantt/trace, then proof or invariant where applicable.

| Topic | Intuition | Formal | Worked example / diagram | Proof / invariant | Verdict |
|-------|-----------|--------|--------------------------|-------------------|---------|
| Scheduling (ch03) | CPU vs I/O burst alternation; convoy effect; "short bursts dominate" exponential intuition; `RR keeps queue short` diagram; quantum-vs-overhead trade-off paragraph | Criteria as bullet definitions; `Definition: Burst`; MLFQ as 4-rule algorithm; CFS as virtual-runtime + RB-tree `O(log n)`; Little's Law `L=λW` as Remark | Gantt triple (FCFS vs SJF vs RR q=4) on fixed workload `(24,3,3)` with waiting-time arithmetic `W=(0,24,27) avg 17` vs `W=(0,3,6) avg 3`; MLFQ 3-level figure with `q=8/16/32 ms` + boost | SJF optimality proof assigned as Exercise 3.2 (with hint on simultaneous arrivals) — appropriate delegation; no in-text handwave | **PASS** — full intuition→formal→Gantt chain |
| Synchronization (ch04) | `count++ = load–inc–store` interleaving as race intuition; CS 3-requirement list as desiderata before any algorithm | Peterson algorithm with shared state declaration; hardware atomics (TSL/CAS) as atomic primitives; semaphore `wait/signal` semantics; monitor+`while(predicate) wait` discipline | Peterson flow figure (spin loop); CAS spinlock 2-line code; producer–consumer with `empty=N/full=0/mutex=1` 14-line solution; monitor `put/get` with `while(cnt==N/0) cond_wait` figure | Peterson 3-requirement satisfaction discussed; spurious-wakeup `while` invariant emphasized; ordering deadlock flagged and forward-linked to ch05 | **PASS** |
| Deadlocks (ch05) | "standstill" quote; RAG cycle pictures as visual deadlock; dining-philosophers 5-cycle as canonical story | `Theorem: Coffman conditions` 4-item formal; RAG formalism (process/resource nodes, request vs assignment edges); `Need = Max − Allocation` + safe-sequence search procedure | Two RAG figures (2-cycle and 3-cycle); `Example: Banker's safety check` with `Available=(3,3,2)` and safe sequence `⟨P1,P3,P4,P0,P2⟩`; ordered-lock 12-line `eat(i)` code preventing circular wait | Prevention table (break each condition) + avoidance safe-state invariant; `Remark: livelock vs deadlock vs starvation` contrasts three phenomena | **PASS** — minor gap noted below |
| Paging (ch06–ch07) | Contiguous allocation + external fragmentation picture motivates paging; "any free frame fits any page" vs "last page wastes PAGE_SIZE/2" contrast; TLB hit-rate example `t_eff = 86.6 ns` vs `160 ns`; demand-paging fast vs fault flow; faults-vs-frames curves (LRU monotonic vs FIFO bump) | `phys = f×PAGE_SIZE + d` (`d` preserved); TLB formula `t_eff = h·(t_TLB+t_mem)+(1−h)(t_TLB+2t_mem)`; two-level split `p1|p2|offset (10|10|12)`; demand-paging `t_eff=(1−p)t_mem + p·t_f`; `W(t,Δ)` definition; FIFO/LRU/OPT/Clock definitions | Contiguous memory map with holes (200 KB / 80 KB); paging VA→PT→PA diagram; segmented-paging `s|p|d` chain; demand-paging flow (valid? branch); Clock hand sweep (R bits); faults-vs-frames sketch; 2-level size `12 KB vs 4 MB (300×)` example; effective-access `p=10⁻⁴ → 900 ns (10×)` | Internal vs external fragmentation remark; Belady stack-property `M(k)⊆M(k+1)` remark; working-set `Δ` too-small vs too-large trade-off paragraph | **PASS** |

Overall intuition→formal: **PASS** — each of the four gated topics follows the required arc without jumping straight to formalism.

---

## Gaps & Non-Blocking Recommendations

1. **Banker's worked trace is summary-only (ch05, `Example: Banker's safety check`).** The example states a safe sequence exists for the `Available=(3,3,2)` instance without showing the row-by-row Need-vs-Available walk that students need to replicate in exercises (Ex 5.3 asks them to verify step-by-step). With the line budget at 202/260 there is headroom; a one-sentence walk ("P1 needs (1,0,0) ≤ (3,3,2) → release …") or a small Need/Allocation sub-table would close the gap without breaking the 36p target. Left as a recommended follow-up, not a FAIL, because the algorithm procedure is fully specified above the example and Exercise 5.3 forces the student to do the walk.

2. **No other blocking gaps.** Page count, line budget, zero-prior, intuition→formal, and all visual/code/overfull gates satisfy PASS thresholds.

---

## Fixes Applied (this review)

- `chapters/ch03-scheduling.tex` `fig:rr-intuition` — added `fill=blue!6` canvas, `fill=red!5` FCFS band, `fill=white` / `fill=blue!12` / `fill=red!10` labelled fills, and two `fill=blue!14`/`fill=red!12` legend swatches; was a lines-only time-vs-queue sketch with two bare labels. Now carries `blue!/red!` fills and a legend; no Overfull introduced.

- `chapters/ch07-virtual-memory.tex` `fig:belady` — added `fill=blue!6` canvas, `fill=blue!12` (LRU) / `fill=red!12` (FIFO) / `fill=orange!12` (anomaly) label fills, and `fill=blue!14`/`fill=red!12` legend swatches; promoted `every node` from `font=\tiny` to `font=\scriptsize` for consistency with the other 22 `\scriptsize` figures; was lines-only fault curves with bare LRU/FIFO labels. Now carries `blue!/red!/orange!` fills and a legend.

No `verbatim` introduced; no `language=` removed; no new `Overfull>15pt` introduced; both figures now pass diagram colour-fill gate. Post-patch `pdflatex` ×2 → exit 0, 36p, max Overfull 5.1pt.

---

## Fixes Recommended (not blocking)

- None required for PASS. Optional: expand ch05 Banker's `Example` with one short trace table as noted in Gaps; ch03 exercise `$P_1{=}8$` line contributes the 5.1pt overfull — a `\,` or line-break after the first burst tuple would shave 3–4pt if strict 0-overfull polish is desired, but it is already <15pt and not a formula overflow.

---

*Reviewer C — visual + ground-up QA, pdflatex-grep verified, colour-fill (`blue!12` etc) and `language=C` gates enforced, zero-prior and intuition→formal audited for scheduling/sync/deadlocks/paging. FAIL would have triggered on any plain verbatim, any monochrome-when-colour-useful diagram, or any Overfull>15pt; none remain.*
