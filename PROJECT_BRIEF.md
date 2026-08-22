# NTU CS Textbooks — Master Brief (autonomous overnight build)
> Last updated: 2026-08-23 02:12 SGT — Bowen asleep, Hermes to run autonomously until ALL modules complete.
> Resume anchor: `progress.md` (read first on crash). Repo: `bumbsclaw/ntu-cs-textbooks` @ `019c7a2`. Model: `muse-spark-1.2-contribution` via `opencode-go` (ox-alpha-free ONLY, no fallback, max_tokens≈3000, ≤260 lines/chapter to stay under 30s 500/503 flap).

## User intent (verbatim direction history)
1. Deep research NTU Bachelors in Computer Science curriculum — official NTU sources (ntu.edu.sg/ccds, AY2024-25 study plan PDF `2024-2025--studyplan-csc.pdf`, CCDS curriculum page 135 AU table) + public student forums (Reddit r/NTU, NTUMods) + student-shared drives **excluded** (private/auth + copyright). Include ALL electives and ALL "choose A or B" branches.
2. Organize into clear outline — done `docs/curriculum-outline.md` + adversarial review `docs/curriculum-outline-review.md` (FAIL→FIXED).
3. Spawn fleets of subagents (all on `muse-spark-1.2-contribution` — one fleet per module — writer + diagrammer + adversarial reviewer per module) to build end-to-end 0→100 LaTeX textbooks per module. Max diagrams, helpful only.
4. QA: adversarial QA per module (must be very critical) + one final QA fleet before PDF render. No delivery without PASS.
5. Render LaTeX → PDF (`pdflatex ×2`, `latexmk` toolchain). Save to `~/projects/ntu-cs-textbooks/`, `modules/<CODE>/main.tex + chapters/*.tex + main.pdf`, commit + push routinely to new GitHub repo `bumbsclaw/ntu-cs-textbooks`. Track `progress.md` for crash-resume.
6. Visual refinement (Bowen 01:31 SGT): diagrams MUST use color where useful (fills blue!12 etc), code blocks MUST be syntax-highlighted (`lstlisting[language=Python/C]` + `lstset` colors), QA MUST compile-check diagrams+formulas (grep `!`, `pgfkeys`, `Overfull>15pt`, `hyperref Warning`) and FAIL if broken. Saved to memory + `AGENTS.md`.
7. Small-screen tuning (Bowen 02:06 SGT): narrow margins top/bottom 1.3cm left/right 1.2cm includeheadfoot, `setstretch 1.20`, `parskip 0.70em`, `itemsep 0.45em`, TikZ scales 0.70-0.78, float seps tightened — maximize reading area on phones. Saved to `AGENTS.md` + memory.
8. 02:12 SGT: Bowen to bed — after Phase 2, Hermes is final quality gate, adversarial QA must run, then autonomously proceed phase-by-phase until ALL modules FULLY COMPLETE. Keep working through night. Save this brief so memory persists across crashes.

## Curriculum truth (adversarially verified)
- **Total 135 AU**: ICC+CSL 17 + College Core 16 + Programme Core 47 + MPE 35 + BDE 20 =135. PDF alternative buckets: Core 47 + MPE 35 + ICC 17 + F-Core 15 + BDE 21 =135 (bucket boundary, total invariant). Degree Audit authoritative.
- **Programme Core 47 AU (15 courses)**: SC1004(4), SC1005(3), MH1812(3), SC1006(3), SC1007(3), SC1008(3), SC2000 Probability & Statistics(3,Nil), SC2002(3), SC2001(3), SC2005(3), SC2203(3), SC2006(3), SC2008(3), SC2207(3), SC3099 Capstone(4). SC1003 is F-Core (not Core). Prereqs verified via NTUMods.
- **College Core / F-Core**: SC1003(3)+HW0288(2)+SC3920 Internship(10) (+1 rounding) =16/15 boundary; SC4079 FYP(8) counted as MPE.
- **MPE 35 AU (FYP path) / 36 AU (non-FYP)**: 9 courses SC3xxx/SC4xxx incl. ≥4 SC4xxx; FYP 27+8=35 vs non-FYP 12×3=36 (total 136 unless BDE adjusted). Highest Distinction requires FYP. Specialisation =15 AU in focus area.
- **All choose A-or-B enumerated**: FYP vs +3 MPE, specialisation, second-major/double-degree paths (25-31 AU replacing BDE).
- **Full MPE catalogue + prereq graph** in `docs/curriculum-outline.md`.

## Completed phases (commits)
- `44c9533` Phase 0 outline
- `ab1d8cd` Phase 0a FAIL→FIXED + review doc
- `685b806` ch01 + main.tex scaffold
- `9fd2ae9` partial marker
- `03851de` SC2001 8/8 v1 (1859 lines, 16 TikZ, 46p 843KB)
- `96988c1` v1 QA PASS
- `4ce05b9` AGENTS.md + progress v2 marker
- `59a6092` v2 color+highlight (45p 880KB, 0 !, visual QA PASS deleg_621390a0)
- `019c7a2` small-screen 52p 885KB (current HEAD, pushed)

## SC2001 exemplar spec (template for all modules)
- `main.tex`: `book` 11pt a4paper, `geometry` 1.3/1.2cm, `setstretch 1.20`, `lmodern`, `amsmath/amsthm`, `xcolor+tikz(automata, ...)`, `listings` with `lstset` colors, `hyperref`, `enumitem` tight lists.
- Chapters: `ch01 foundations 375` · `ch02 asympt 217` · `ch03 recurrences 210` · `ch04 D&C 201` · `ch05 greedy 220` · `ch06 DP 233` · `ch07 graph/string 200` · `ch08 NP 203` =1859→~1870 lines after v2 color pass. 16 TikZ (1+2+2+2+2+3+2+2) all colorized, 6 lstlisting blocks (ch05 4 + ch06 2) highlighted.
- QA: two reviewers per module (ch01-04 + ch05-08) must PASS with compile checks; patches auto-applied (ch04 Master ref + strip lemma 6→8, ch06 label, v2 ch05 fills). PDF 45-52p verified 0 ! 0 pgfkeys.

## Remaining work (autonomous overnight)
- **Phase 2 READY**: SC1007 Data Structures & Algorithms, SC2005 Operating Systems, SC2006 Software Engineering — each 8 chapters 0→100, chunked 200-260 lines, color+highlight+visual-QA, `main.pdf` per module.
- **Phase 3+**: All remaining Programme Core (SC1004, SC1005, SC1006, SC1008, SC2000, SC2002, SC2203, SC2008, SC2207, SC3099, MH1812) + MPE electives (SC3000, SC3010, SC4001 etc — 9 required + extras) + University/College Core overviews + BDE guide. Same methodology: deep-research → outline → write chunked → colorize+highlight+formula fix → QA visual → pdf → commit/push → update progress.md.
- **Final QA fleet**: cross-module consistency (prereq graph, notation, cross-refs), full `latexmk` batch, GitHub release tag.
- **Operator is final gate**: do not mark any module DONE without adversarial PASS; chunk to stay under 30s; commit routinely; update `progress.md` Module Tracker per chapter.

## Operational constraints (never forget)
- Provider `ox-alpha-free` ONLY (`clear model.fallback + fallback_model.model`), `max_tokens≈3000`, `muse-spark-1.2-contribution` for all fleets.
- `progress.md` is the only resume truth — first PENDING row is next. Branch `main`, remote `origin` bumbsclaw/ntu-cs-textbooks. PDFs tracked via `git add -f` (gitignore ignores aux/log only).
- After each module: `pdflatex ×2` verify, commit, push, update Module Tracker (Outline/Draft/Adversarial/QA/PDF).
- If crash: `cat progress.md && git log --oneline -3 && ls modules/<CODE>/chapters/` then continue from PENDING.
