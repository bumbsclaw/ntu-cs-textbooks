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
| 1 - Exemplar fleet (SC2001) | IN_PROGRESS | fleet deleg_bd18a029 partial 01:15 SGT — ch1-foundations DONE (685b806); ch2-ch8 hit opencode-go 500/503 transient (max_tokens~3000 + retry per memory). Retry fleet deleg_e5f2 queued 01:16 SGT chunked (1 chapter per subagent, max_tokens 3000) on muse-spark-1.2-contribution |
| 2 - Batch expansion (3 cores) | PENDING | SC1007, SC2005, SC2006 etc |
| 3 - Final QA fleet | PENDING | |
| 4 - LaTeX PDF render | PENDING | latexmk + push |

## Module Tracker
| Code | Title | AU | Type | Outline | Draft | Adversarial | QA | PDF |
|------|-------|----|------|---------|-------|-------------|----|-----|
| SC2001 | Algorithm Design and Analysis | 3 | Core | DONE (ab1d8cd) | PARTIAL ch1 DONE (685b806), ch2-ch8 retrying | pending | pending | pending |

## Research Log
- 2026-08-23: Phase 0 kicked off. Sources: ntu.edu.sg/ccds official, public forums (Reddit r/NTU). Private GDrives excluded per policy.
- 2026-08-23 01:05 SGT: Phase 0a adversarial review completed — FAIL BLOCKING → patched. Sources live-checked: CCDS curriculum page (135 AU), AY2024-25 CSC study plan PDF (pdftotext), NTUMods 17 mods (SC1003..SC2207, HW0288, MH1812, SC3000/3010/4001, CC0001). Findings: SC2000 title error (Introduction to Databases → Probability & Statistics), College Core 27 AU vs 16 AU bucket mismatch, Programme Core double-count SC1003, MPE 35/36 AU invariant unclarified. Review file: docs/curriculum-outline-review.md. Outline patched for blocking items; Phase 1 unblocked.

## Resume Instructions
- Read this file first on restart.
- Check last completed phase above.
- Continue from first PENDING row.
