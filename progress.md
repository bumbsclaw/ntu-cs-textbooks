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
| 1 - Exemplar fleet (SC2001) v2 RETRY | DONE | v3 02:40-03:07 SGT — PASS re-QA v3 (deleg_20b1d946 ch01-04 PASS + ch05-08 PASS) — 8 intuition patches (From-zero, Venn/arrow, timed-story, band-first, one-level tree, indicator 2-coin, timeline/zigzag/wave-front/Sudoku), 2070L (295/233/260/249/258/259/259/257), 53p 982KB 0 ! 0 pgfkeys, verified ×2 | v2 45p 880KB — v1 52p — superseded |
| 2 - Batch expansion (3 cores) | DONE | SC1007 37p 530KB + SC2005 36p 610KB + SC2006 48p 654KB — 3×8 ch 200-260L, color TikZ, lstlisting — QA deleg_85968bd2 PASS all (SC1007/05/06) 02:48 SGT; SC2001 v3 patches 8× consolidated (deleg_700ed6fe+1f4ced8f) pending final QA |
| 3 - Batch expansion (next cores) | IN_PROGRESS | SC1004 43p + SC1005 37p + SC1006 30p drafted (deleg_e3a8fcba 9m21s) — QA queued deleg_qa3 — 8×200-260L 0 !, color TikZ, small-screen |
| 4 - LaTeX PDF render | DONE (v2) | v2 45p main.pdf rendered 01:47 SGT, 0 errors, pushed |

## Module Tracker
| Code | Title | AU | Type | Outline | Draft | Adversarial | QA | PDF |
|------|-------|----|------|---------|-------|-------------|----|-----|
| SC2001 | Algorithm Design and Analysis | 3 | Core | DONE (ab1d8cd) | DONE v3 8/8 (2070L 294/233/260/249/258/259/259/257, 16+ TikZ color, intuitions) 03:07 SGT | DONE PASS v3 ch01-04 (REVIEW-v3-ch01-04.md) + PASS v3 ch05-08 (REVIEW-v3-ch05-08.md) | DONE | DONE v3 53p 982KB 0 ! small-screen |
| SC1007 | Data Structures & Algorithms | 3 | Core | DONE | DONE 8/8 (1650L, 24 TikZ color) 02:38 SGT | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) | DONE | DONE 37p 541KB |
| SC2005 | Operating Systems | 3 | Core | DONE | DONE 8/8 (1629L, 24 TikZ color) 02:25 SGT | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) | DONE | DONE 36p 610KB |
| SC2006 | Software Engineering | 3 | Core | DONE | DONE 8/8 (1616L, 26 TikZ color) 02:30 SGT | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) | DONE | DONE 48p 654KB |
| SC1004 | Linear Algebra for Computing | 4 | Core | pending | DONE 8/8 drafted (43p) — QA queued | pending | pending | pending |
| SC1005 | Digital Logic | 3 | Core | pending | DONE 8/8 drafted (37p) — QA queued | pending | pending | pending |
| SC1006 | Computer Organisation & Architecture | 3 | Core* | pending | DONE 8/8 drafted (30p) — QA queued | pending | pending | pending |

## Research Log
- 2026-08-23: Phase 0 kicked off. Sources: ntu.edu.sg/ccds official, public forums (Reddit r/NTU). Private GDrives excluded per policy.
- 2026-08-23 01:05 SGT: Phase 0a adversarial review completed — FAIL BLOCKING → patched. Sources live-checked: CCDS curriculum page (135 AU), AY2024-25 CSC study plan PDF (pdftotext), NTUMods 17 mods (SC1003..SC2207, HW0288, MH1812, SC3000/3010/4001, CC0001). Findings: SC2000 title error (Introduction to Databases → Probability & Statistics), College Core 27 AU vs 16 AU bucket mismatch, Programme Core double-count SC1003, MPE 35/36 AU invariant unclarified. Review file: docs/curriculum-outline-review.md. Outline patched for blocking items; Phase 1 unblocked.
- 2026-08-23 01:28 SGT: Phase 1 QA DONE v1 — Reviewer A PASS conditional + Reviewer B PASS WITH MINOR FIXES. Fixes auto-patched: ch04 Master ref + strip lemma, ch06 duplicate label + matrix-chain arithmetic. main.pdf 46p 843KB 0 pgf errors.
- 2026-08-23 01:44 SGT: Phase 1 v2 DONE — 6 verbatim→lstlisting (ch05/06), 11 TikZ colorized across 6 chapters, formula Overfull>15pt 3→0 + hyperref 30+→0. Visual QA deleg_621390a0 PASS both slices.
- 2026-08-23 03:07 SGT: SC2001 v3 DONE — re-QA PASS (deleg_20b1d946) both slices, 8 intuition blocks consolidated, 2070L 53p 0 !
- 2026-08-23 02:48 SGT: Phase 2 DONE — SC1007/05/06 QA deleg_85968bd2 PASS all 3 (24-26 TikZ, 0 verbatim, 0 !). SC2001 v3 8 patches consolidated (294/233/260/249/260/257/251/257L, 53p 982KB 0 !) pending re-QA. Phase 3 queued: remaining Programme Core + MPEs + BDE. AGENTS.md + memory updated per Bowen: color where useful + syntax-highlighted code + QA must compile-check diagrams+formulas.

## Resume Instructions
- Read this file first on restart.
- Check last completed phase above.
- Continue from first PENDING row.
