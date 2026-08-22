# NTU BSc Computer Science - Textbook Build Progress

**Repo:** bumbsclaw/ntu-cs-textbooks (to be created)
**Started:** 2026-08-23
**Model for fleets:** muse-spark-1.2-contribution
**Exemplar module:** SC2001 Algorithm Design and Analysis
**Workflow:** outline -> adversarial review -> exemplar fleet -> batch expansion -> final QA -> LaTeX PDF

## Phases
| Phase | Status | Notes |
|-------|--------|-------|
| 0 - Curriculum deep research and outline | DONE | outline committed 44c9533; verified 135 AU (17+16+47+35+20) |
| 0a - Adversarial review of outline | DONE (FAIL→FIXED) | 2026-08-23 01:05 SGT — verdict FAIL BLOCKING (SC2000 title, Core double-count, College Core 27→16 bucket, MPE 35/36 invariant). Review: docs/curriculum-outline-review.md. Trivial fixes patched in outline (SC2000→Prob&Stats, SC1003 deduped from Core, HW0288/SC2203/SC2008 prereq nuances, MPE Highest Distinction, bucket footnotes). Non-blocking TODOs (SC4023 verification, graph detail) logged in review §Recommended Fixes. |
| 1 - Exemplar fleet (SC2001) | DONE | fleet deleg_adace572+deleg_bc8aad5d+deleg_dd84bab0 DONE 01:22 SGT — 8/8 chapters (1859 lines, 16 TikZ) ch01 375 ch02 217 ch03 210 ch04 201 ch05 220 ch06 233 ch07 200 ch08 203; main.pdf 46p 824KB compiles 0 pgf errors (automata patched). QA fleet deleg_68d71dca DONE 01:28 SGT — PASS (conditional) ch01-04 + PASS WITH MINOR FIXES ch05-08; 2 trivial patches auto-applied (ch04 Master ref + strip lemma, ch06 coin-change label + matrix-chain arithmetic) |
| 2 - Batch expansion (3 cores) | READY | queued: SC1007 (Data Structures extension), SC2005 (Operating Systems), SC2006 (Software Engineering) chunked writers — awaiting push |
| 3 - Final QA fleet | PENDING | |
| 4 - LaTeX PDF render | PENDING | latexmk + push |

## Module Tracker
| Code | Title | AU | Type | Outline | Draft | Adversarial | QA | PDF |
|------|-------|----|------|---------|-------|-------------|----|-----|
| SC2001 | Algorithm Design and Analysis | 3 | Core | DONE (ab1d8cd) | DONE 8/8 (1859 lines, 16 TikZ) 01:22 SGT | DONE PASS ch01-04 (REVIEW-ch01-04.md) + PASS ch05-08 (REVIEW-ch05-08.md) 01:28 SGT | DONE | DONE 46p main.pdf (843KB, 2× pdflatex pass) |

## Research Log
- 2026-08-23: Phase 0 kicked off. Sources: ntu.edu.sg/ccds official, public forums (Reddit r/NTU). Private GDrives excluded per policy.
- 2026-08-23 01:05 SGT: Phase 0a adversarial review completed — FAIL BLOCKING → patched. Sources live-checked: CCDS curriculum page (135 AU), AY2024-25 CSC study plan PDF (pdftotext), NTUMods 17 mods (SC1003..SC2207, HW0288, MH1812, SC3000/3010/4001, CC0001). Findings: SC2000 title error (Introduction to Databases → Probability & Statistics), College Core 27 AU vs 16 AU bucket mismatch, Programme Core double-count SC1003, MPE 35/36 AU invariant unclarified. Review file: docs/curriculum-outline-review.md. Outline patched for blocking items; Phase 1 unblocked.
- 2026-08-23 01:28 SGT: Phase 1 QA DONE — Reviewer A (ch01-04) PASS conditional + Reviewer B (ch05-08) PASS WITH MINOR FIXES. Fixes auto-patched: ch04 Master ref Ch2->Ch3 + strip lemma 6->8 squares, ch06 duplicate label sec:coin-change + matrix-chain arithmetic. main.pdf 46p final (843KB) 0 pgf errors.

## Resume Instructions
- Read this file first on restart.
- Check last completed phase above.
- Continue from first PENDING row.
