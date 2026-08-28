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
| 3 - Batch expansion (next cores) | DONE | SC1004 43p 683KB + SC1005 37p 609KB + SC1006 71p 788KB (thickened 1893L 0 padding) — QA deleg_578cc33b PASS×2 + CONDITIONAL→thickened deleg_8af99f8e PASS 03:42 SGT |
| 4 - Batch expansion (phase 4) | DONE | SC1008 43p 636KB + SC2000 40p 712KB + SC2002 44p 695KB — 3×8 ch 200-260L 0 ! drafts done deleg_b572680a 15m42s — QA FIXED 2026-08-28 14:40 SGT (SC2000 40p 0 ! 10.6pt max, SC2002 44p 0 ! resizebox fix + sloppy) — 0 ! 0 pgfkeys 0 fails>15 — PASS |
| 5 - Batch expansion (phase 5) | DONE | SC2203 42p 740KB + SC2008 50p 757KB + SC2207 45p 670KB — 3×8 ch 1620/1665/1641L 2-3 TikZ/color, lstlisting — 0 ! 0 >15 PASS 2026-08-28 15:01 SGT deleg_1aa6462b (1184s/939s/1211s) |
| 6 - Batch expansion (phase 6) | DONE | SC3099 46p 688KB + MH1812 45p 676KB + SC3000 46p 827KB — 3×8 ch 1710/2078/1762L 2-4 TikZ/color, lstlisting — 0 ! 0 >15 PASS 2026-08-28 15:24 SGT deleg_62e8848f (1324s/1070s/1031s) |
| 7 - Batch expansion (phase 7) | DONE | SC3010 51p 791KB + SC3020 48p 738KB + SC4001 46p 702KB — 3×8 ch 1673/1746/1621L 24/20/18 TikZ/color, lstlisting — 0 ! 0 >15 PASS 2026-08-28 15:47 SGT deleg_9702d10b (886s/690s/316s→fixed) |
| 8 - Batch expansion (phase 8) | DONE | SC4002 47p 868KB + SC4012 46p 750KB + SC4051 45p 626KB — 3×8 ch 1964/1649/1707L 24/20/18 TikZ/color, lstlisting — 0 ! 0 >15 PASS 2026-08-28 16:30 SGT deleg_6018dfda (952s/539s fix/501s) |
| 9 - Remaining MPE/BDE | IN_PROGRESS (Phase 9 dispatched) | queued: SC4040/SC4055/BDE — autonomous until ALL DONE |
| 10 - Final QA fleet | PENDING | cross-module prereq/notation + latexmk batch + release tag |

## Module Tracker
| Code | Title | AU | Type | Outline | Draft | Adversarial | QA | PDF |
|------|-------|----|------|---------|-------|-------------|----|-----|
| SC2001 | Algorithm Design and Analysis | 3 | Core | DONE (ab1d8cd) | DONE v3 8/8 (2070L 294/233/260/249/258/259/259/257, 16+ TikZ color, intuitions) 03:07 SGT | DONE PASS v3 ch01-04 (REVIEW-v3-ch01-04.md) + PASS v3 ch05-08 (REVIEW-v3-ch05-08.md) | DONE | DONE v3 53p 982KB 0 ! small-screen |
| SC1007 | Data Structures & Algorithms | 3 | Core | DONE | DONE 8/8 (1650L, 24 TikZ color) 02:38 SGT | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) | DONE | DONE 37p 541KB |
| SC2005 | Operating Systems | 3 | Core | DONE | DONE 8/8 (1629L, 24 TikZ color) 02:25 SGT | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) | DONE | DONE 36p 610KB |
| SC2006 | Software Engineering | 3 | Core | DONE | DONE 8/8 (1616L, 26 TikZ color) 02:30 SGT | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) | DONE | DONE 48p 654KB |
| SC1004 | Linear Algebra for Computing | 4 | Core | DONE | DONE 8/8 (1637L, 23 TikZ color) 43p 683KB | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) | DONE | DONE 43p 683KB 0 ! |
| SC1005 | Digital Logic | 3 | Core | DONE | DONE 8/8 (1619L, 48 TikZ) 37p 609KB | DONE PASS visual+ground-up (REVIEW-visual-groundup.md) — 5.1pt max | DONE | DONE 37p 609KB 0 ! |
| SC1006 | Computer Organisation & Architecture | 3 | Core* | DONE | DONE 8/8 (1893L 225/256/260/202/256/262/221/211, 24 TikZ color) 71p 788KB | DONE PASS thickened ch02/03/04/05/06/07/08 (deleg_8af99f8e) 0 padding 0 ! | DONE | DONE 71p 788KB 0 ! |
| SC1008 | C/C++ Programming | 3 | Core | DONE | DONE 8/8 (43p 635KB 1704L, 24 TikZ color, 110 lstlisting) — FIXED 14:31 SGT 0 ! | DONE PASS 14:40 SGT (0 !, 0 >15) | DONE | DONE 43p 635KB 0 ! |
| SC2000 | Probability & Statistics for Computing | 3 | Core | DONE | DONE 8/8 (40p 712KB 1673L, 20 TikZ color, 24 lstlisting) — FIXED ch02 41pt→10.6pt max 14:31 SGT 0 ! | DONE PASS 14:40 SGT (0 !, 10.6pt max) | DONE | DONE 40p 712KB 0 ! |
| SC2002 | Object-Oriented Design & Programming | 3 | Core | DONE | DONE 8/8 (44p 695KB 1654L, 28 TikZ color, 56 lstlisting) — FIXED ch04 resizebox 222→0 + ch07 sloppy 30→0 14:39 SGT 0 ! | DONE PASS 14:40 SGT (0 !, 0 >15) | DONE | DONE 44p 695KB 0 ! |
| SC2203 | Automata, Computability & Complexity | 3 | Core | DONE | DONE 8/8 (42p 740KB 1620L 25 TikZ color, 26 lstlisting) 15:01 SGT | DONE PASS 15:01 SGT (0 !, 12.27 max) | DONE | DONE 42p 740KB 0 ! |
| SC2008 | Computer Network | 3 | Core | DONE | DONE 8/8 (50p 757KB 1665L 26 TikZ color, 46 lstlisting) 14:56 SGT | DONE PASS 15:02 SGT (0 !, 12.82 max) | DONE | DONE 50p 757KB 0 ! |
| SC2207 | Introduction to Databases | 3 | Core | DONE | DONE 8/8 (45p 670KB 1641L 24 TikZ color, 44 lstlisting) 15:01 SGT | DONE PASS 15:02 SGT (0 !, 9.41 max) | DONE | DONE 45p 670KB 0 ! |
| SC3099 | Capstone Project | 4 | Core | DONE | DONE 8/8 (46p 688KB 1710L 24 TikZ color) 15:24 SGT | DONE PASS 15:24 SGT (0 !, 14.91 max) | DONE | DONE 46p 688KB 0 ! |
| MH1812 | Discrete Mathematics | 3 | Core* | DONE | DONE 8/8 (45p 676KB 2078L 24 TikZ color) 15:20 SGT | DONE PASS 15:24 SGT (0 !, 0 max) | DONE | DONE 45p 676KB 0 ! |
| SC3000 | Artificial Intelligence | 3 | MPE | DONE | DONE 8/8 (46p 827KB 1762L 20 TikZ color) 15:19 SGT | DONE PASS 15:24 SGT (0 !, 0 max) | DONE | DONE 46p 827KB 0 ! |
| SC3010 | Computer Security | 3 | MPE | DONE | DONE 8/8 (51p 791KB 1673L 24 TikZ color) 15:41 SGT | DONE PASS 15:47 SGT (0 !, 0.67 max) | DONE | DONE 51p 791KB 0 ! |
| SC3020 | Data Analytics & Mining | 3 | MPE | DONE | DONE 8/8 (48p 738KB 1746L 20 TikZ color) 15:37 SGT | DONE PASS 15:47 SGT (0 !, 3.01 max) | DONE | DONE 48p 738KB 0 ! |
| SC4001 | Neural Networks & Deep Learning | 3 | MPE | DONE | DONE 8/8 (46p 702KB 1621L 18 TikZ color) 15:47 SGT — fixed \end{chapter}+snake+47pt+ch08 TikZ 72→0 | DONE PASS 15:47 SGT (0 !, 2.54 max) | DONE | DONE 46p 702KB 0 ! |
| SC4002 | Natural Language Processing | 3 | MPE | DONE | DONE 8/8 (47p 868KB 1964L 24 TikZ color) 16:04 SGT | DONE PASS 16:30 SGT (0 !, 12.72 max) | DONE | DONE 47p 868KB 0 ! |
| SC4012 | Software Security | 3 | MPE | DONE | DONE 8/8 (46p 750KB 1649L 20 TikZ color) 16:30 SGT — fixed \item bracket+9 overfull 83→11 | DONE PASS 16:30 SGT (0 !, 11.31 max) | DONE | DONE 46p 750KB 0 ! |
| SC4051 | Distributed Systems | 3 | MPE | DONE | DONE 8/8 (45p 626KB 1707L 18 TikZ color) 15:56 SGT | DONE PASS 16:30 SGT (0 !, 0 max) | DONE | DONE 45p 626KB 0 ! |

## Research Log
- 2026-08-23: Phase 0 kicked off. Sources: ntu.edu.sg/ccds official, public forums (Reddit r/NTU). Private GDrives excluded per policy.
- 2026-08-23 01:05 SGT: Phase 0a adversarial review completed — FAIL BLOCKING → patched. Sources live-checked: CCDS curriculum page (135 AU), AY2024-25 CSC study plan PDF (pdftotext), NTUMods 17 mods (SC1003..SC2207, HW0288, MH1812, SC3000/3010/4001, CC0001). Findings: SC2000 title error (Introduction to Databases → Probability & Statistics), College Core 27 AU vs 16 AU bucket mismatch, Programme Core double-count SC1003, MPE 35/36 AU invariant unclarified. Review file: docs/curriculum-outline-review.md. Outline patched for blocking items; Phase 1 unblocked.
- 2026-08-23 01:28 SGT: Phase 1 QA DONE v1 — Reviewer A PASS conditional + Reviewer B PASS WITH MINOR FIXES. Fixes auto-patched: ch04 Master ref + strip lemma, ch06 duplicate label + matrix-chain arithmetic. main.pdf 46p 843KB 0 pgf errors.
- 2026-08-23 01:44 SGT: Phase 1 v2 DONE — 6 verbatim→lstlisting (ch05/06), 11 TikZ colorized across 6 chapters, formula Overfull>15pt 3→0 + hyperref 30+→0. Visual QA deleg_621390a0 PASS both slices.
- 2026-08-23 03:07 SGT: SC2001 v3 DONE — re-QA PASS (deleg_20b1d946) both slices, 8 intuition blocks consolidated, 2070L 53p 0 !
- 2026-08-23 03:22 SGT: QA deleg_578cc33b PASS SC1004(23 TikZ) + PASS SC1005(48 TikZ) | CONDITIONAL SC1006(visual PASS, depth FAIL 49% padding ch05-08 thin — thickening queued)
- 2026-08-23 03:42 SGT: SC1006 thickened — ch02 84→210 + ch03 99→200 + ch04 87→202 + ch05 65→204 + ch06 61→204 + ch07 65→221 + ch08 54→211 real lines (0 padding), 71p 788KB 0 ! PASS
- 2026-08-23 02:48 SGT: Phase 2 DONE — SC1007/05/06 QA deleg_85968bd2 PASS all 3 (24-26 TikZ, 0 verbatim, 0 !). SC2001 v3 8 patches consolidated (294/233/260/249/260/257/251/257L, 53p 982KB 0 !) pending re-QA. Phase 3 queued: remaining Programme Core + MPEs + BDE. AGENTS.md + memory updated per Bowen: color where useful + syntax-highlighted code + QA must compile-check diagrams+formulas.
- 2026-08-28 14:40 SGT: Phase 4 QA FIXED — SC1008 (43p 0 !), SC2000 (40p 0 !, 41pt→10.6), SC2002 (44p 0 !, 222pt→0 via resizebox, 30pt→0 via sloppy) — all PASS visual+ground-up, committed.
- 2026-08-28 15:02 SGT: Phase 5 DONE — SC2203 42p 1620L 0 ! 12.27 max, SC2008 50p 1665L 0 ! 12.82 max, SC2207 45p 1641L 0 ! 9.4 max — deleg_1aa6462b PASS, committed.
- 2026-08-28 15:25 SGT: Phase 6 DONE — SC3099 46p 1710L 0 ! 14.91 max, MH1812 45p 2078L 0 !, SC3000 46p 1762L 0 ! — deleg_62e8848f PASS, committed.
- 2026-08-28 15:47 SGT: Phase 7 DONE — SC3010 51p 1673L 0 ! 0.67 max, SC3020 48p 1746L 0 ! 3.01 max, SC4001 46p 1621L 0 ! 2.54 max — deleg_9702d10b 2 PASS + 1 fixed (72 !→0 via \end{chapter}+snake+ch08 TikZ) — committed.
- 2026-08-28 16:30 SGT: Phase 8 DONE — SC4002 47p 1964L 0 ! 12.72 max, SC4012 46p 1649L 0 ! 11.31 max (fixed 1 !+9 >15 via item bracket+sloppy), SC4051 45p 1707L 0 ! — deleg_6018dfda (952s/539s/501s) — committed.

## Resume Instructions
- Read this file first on restart.
- Check last completed phase above.
- Continue from first PENDING row.
