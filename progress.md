# NTU BSc Computer Science - Textbook Build Progress

**Repo:** bumbsclaw/ntu-cs-textbooks
**Started:** 2026-08-23
**Model for fleets:** muse-spark-1.2-contribution
**Exemplar module:** SC2001 Algorithm Design and Analysis
**Workflow:** outline -> adversarial review -> exemplar fleet -> batch expansion -> final QA -> LaTeX PDF

## Phases
| Phase | Status | Notes |
|-------|--------|-------|
| 0 - Curriculum deep research and outline | DONE | outline committed 44c9533; verified 135 AU (17+16+47+35+20) |
| 0a - Adversarial review of outline | DONE (FAIL→FIXED) | 2026-08-23 01:05 SGT — verdict FAIL BLOCKING (SC2000 title, Core double-count, College Core 27→16 bucket, MPE 35/36 invariant). Review: docs/curriculum-outline-review.md. Trivial fixes patched in outline (SC2000→Prob&Stats, SC1003 deduped from Core, HW0288/SC2203/SC2008 prereq nuances, MPE Highest Distinction, bucket footnotes). Non-blocking TODOs (SC4023 verification, graph detail) logged in review §Recommended Fixes. |
| 1 - Exemplar fleet (SC2001) v2 RETRY | DONE | v2 01:44 SGT — PASS v2 visual QA (deleg_621390a0): ch01-04 PASS + ch05-08 PASS. Fixes via deleg_518409bd: 6 verbatim→lstlisting[language=Python] (ch05 4, ch06 2), 11 TikZ colorized (ch01 RAM violet, ch02 bands+hierarchy, ch03 rectree+mastergeom, ch04 partition+strassen, ch07 BFS+KMP, ch08 chain+Venn), formula Overfull 3×42-47pt→0 + hyperref 30+→0. Final 45p 880KB 0 ! 0 pgfkeys, verified ×2 |
| 2 - Batch expansion (3 cores) | IN_PROGRESS | dispatched 02:16 SGT — SC1007 + SC2005 + SC2006 in parallel (muse-spark-1.2, chunked 200-260 lines, color TikZ + lstlisting + visual QA) — fleet deleg_phase2 |
| 3 - Final QA fleet | PENDING | |
| 4 - LaTeX PDF render | DONE (v2) | v2 45p main.pdf rendered 01:47 SGT, 0 errors, pushed |

## Module Tracker
| Code | Title | AU | Type | Outline | Draft | Adversarial | QA | PDF |
|------|-------|----|------|---------|-------|-------------|----|-----|
| SC2001 | Algorithm Design and Analysis | 3 | Core | DONE (ab1d8cd) | DONE v2 8/8 (1859→~1870 lines, 16 TikZ color) 01:44 SGT | DONE PASS v2 ch01-04 + PASS v2 ch05-08 01:47 SGT | DONE | DONE v2 52p 885KB (small-screen 1.2/1.3cm, stretch 1.20) |
| SC1007 | Data Structures & Algorithms | 3 | Core | pending | IN_PROGRESS | pending | pending | pending |
| SC2005 | Operating Systems | 3 | Core | pending | IN_PROGRESS | pending | pending | pending |
| SC2006 | Software Engineering | 3 | Core | pending | IN_PROGRESS | pending | pending | pending |

## Research Log
- 2026-08-23: Phase 0 kicked off. Sources: ntu.edu.sg/ccds official, public forums (Reddit r/NTU). Private GDrives excluded per policy.
- 2026-08-23 01:05 SGT: Phase 0a adversarial review completed — FAIL BLOCKING → patched. Sources live-checked: CCDS curriculum page (135 AU), AY2024-25 CSC study plan PDF (pdftotext), NTUMods 17 mods (SC1003..SC2207, HW0288, MH1812, SC3000/3010/4001, CC0001). Findings: SC2000 title error (Introduction to Databases → Probability & Statistics), College Core 27 AU vs 16 AU bucket mismatch, Programme Core double-count SC1003, MPE 35/36 AU invariant unclarified. Review file: docs/curriculum-outline-review.md. Outline patched for blocking items; Phase 1 unblocked.
- 2026-08-23 01:28 SGT: Phase 1 QA DONE v1 — Reviewer A PASS conditional + Reviewer B PASS WITH MINOR FIXES. Fixes auto-patched: ch04 Master ref + strip lemma, ch06 duplicate label + matrix-chain arithmetic. main.pdf 46p 843KB 0 pgf errors.
- 2026-08-23 01:44 SGT: Phase 1 v2 DONE — 6 verbatim→lstlisting (ch05/06), 11 TikZ colorized across 6 chapters, formula Overfull>15pt 3→0 + hyperref 30+→0. Visual QA deleg_621390a0 PASS both slices. AGENTS.md + memory updated per Bowen: color where useful + syntax-highlighted code + QA must compile-check diagrams+formulas.

## Resume Instructions
- Read this file first on restart.
- Check last completed phase above.
- Continue from first PENDING row.
