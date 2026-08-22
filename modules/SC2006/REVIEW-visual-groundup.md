# Visual + Ground-Up QA — SC2006 Software Engineering

**Date:** 2026-08-23 SGT
**Scope:** `modules/SC2006/main.tex` + `chapters/ch01-sdlc.tex` · `ch02-requirements.tex` · `ch03-uml.tex` · `ch04-design-principles.tex` · `ch05-implementation-vcs.tex` · `ch06-testing.tex` · `ch07-maintenance.tex` · `ch08-agile.tex`
**Worktree:** `projects/ntu-cs-textbooks` (SC2006 untracked — `git status` shows `?? modules/SC2006/`; audited as worktree)
**Verdict: PASS** — all quantitative gates pass; content is ground-up SUFFICIENT with no blocking gaps. Two trivial editorial nits patched (see §5).

---

## 1. Quantitative Gates

| Gate | Requirement | Measured | Result |
|------|-------------|----------|--------|
| Pages | 48p | `pdfinfo main.pdf` → **48 pages** (668913 B) | ✅ PASS |
| TikZ figures | 26, all with color | `grep begin{tikzpicture}` → **26** (3+3+4+3+3+2+4+4) | ✅ PASS |
| TikZ color | fills + colored nodes/edges | distinct `fill=<hue>!` → **34 distinct fills**; every figure uses `fill=` + colored arrows/nodes | ✅ PASS |
| `verbatim` | 0 | `grep begin{verbatim}` → **0** | ✅ PASS |
| `lstlisting[Java/Python]` | ≥8 with `language=` + highlighted | `grep begin{lstlisting}` → **16** (6 Java + 10 Python), all with `language=Java` or `language=Python` and `lstset` colors | ✅ PASS |
| `pdflatex` errors | 0 `! ` | `grep ^! main.log` → **0** | ✅ PASS |
| `pgfkeys` errors | 0 | only `pgfkeys.code.tex` load lines — **0 errors** | ✅ PASS |
| Overfull \hbox >15pt | 0 | `grep Overfull main.log` → **0** lines | ✅ PASS |
| Overfull <15pt | cosmetic only | 0 lines total; previous SC2001 2–10pt cosmetics do not recur here — clean | ✅ PASS |
| `hyperref` warnings | 0 | `grep hyperref Warning` → 0 | ✅ PASS |
| Build | `pdflatex` exit 0 | exit 0, second pass stable | ✅ PASS |

**TikZ color detail (all 26 figures use fills):**

| Ch | Figures | Fill hues used |
|----|---------|----------------|
| 01 | 3 — SDLC cycle, waterfall, spiral | blue!20/green!20/orange!20/violet!20/red!15/teal!20/yellow!10; blue!15/green!15/orange!15/violet!15/red!12; blue!5/blue!3/blue!2/green!18/orange!18/violet!15/teal!15 |
| 02 | 3 — FURPS+ hexagon, RE process, use-case | blue!16/green!16/orange!16/violet!16/red!12/teal!14/blue!10/green!14/orange!14/violet!14/red!12/yellow!15/blue!4/orange!16/green!15/violet!15 |
| 03 | 4 — class, sequence, state-machine, activity | blue!14/green!14/orange!14/violet!14/gray!20; blue!12/green!14/orange!14/violet!14/yellow!18; green!15/orange!15/violet!15/red!12/gray!12/black; green!14/orange!18/blue!12/violet!14/teal!12/black!10 |
| 04 | 3 — coupling contrast, DIP, Observer | red!14/green!14/blue!12; red!12/green!14/blue!12/orange!14; blue!14/green!14/orange!14/violet!14 |
| 05 | 3 — Git DAG, Git Flow, CI pipeline | blue!14/green!14/orange!14/violet!14/yellow!15; blue!15/green!15/orange!15/violet!15/red!12; blue!14/green!14/orange!14/violet!14/red!12 |
| 06 | 2 — testing pyramid, TDD loop | green!16/orange!16/violet!15/red!12/blue!8; red!14/green!14/blue!14 |
| 07 | 4 — maintenance mix, smell→fix, traceability, legacy loop | red!14/orange!14/green!14/blue!14; red!10/green!14; blue!14/green!14/orange!14/violet!14; green!14/orange!14/blue!14 |
| 08 | 4 — Scrum flow, board, CI/CD pipeline, retros | blue!14/green!14/orange!14/violet!14/red!12/teal!14; blue!10/orange!14/violet!12/green!14/yellow!18/blue!10/green!10; blue!14/green!14/orange!14/violet!14/red!12; green!14/orange!14/blue!14 |

All figures have `\caption`; chapter `\label{ch:*}` present. `lstset` preamble defines `keywordstyle=\color{blue!70!black}`, `commentstyle=\color{green!50!black}`, `stringstyle=\color{orange!70!black}`, breaklines, frame, numbers — inherited by all 16 listings.

---

## 2. Visual QA — Per-Chapter

### Ch01 SDLC — PASS
Cycle diagram uses 6 hue fills + `blue!55!black` arrows + `yellow!10` center badge. Waterfall uses per-phase fills (blue→green→orange→violet→red) + dashed costly-rework arc + yellow V-Model callout. Spiral uses concentric fills (blue!5/3/2) + 3 arc radii + quadrant badges. All labeled with captions; no monochrome.

### Ch02 Requirements — PASS
FURPS+ hexagon 6 fills + gray polygon edges. RE process 4 colored steps + dashed feedback arcs + yellow Management badge. Use-case diagram has blue!4 system boundary + orange!16 ellipses + green/violet actors. All intuitive — supports FURPS/SMART/MoSCoW text.

### Ch03 UML — PASS
Class diagram: blue/green/orange/violet fills per class + hollow-triangle inheritance + association-class diamond. Sequence: 4 colored lifelines + dashed returns + yellow `alt` fragment. State machine: green→orange→violet linear flow + red dashed cancel + gray arch/cancel. Activity: fork/join bars + colored action nodes + diamond decision. Only 4 figures but each dense; color essential and present.

### Ch04 Design Principles — PASS
Coupling contrast red (fragile, dense) vs green+blue interface (stable). DIP split red!12 (bad) vs green/blue/orange (good) with `<<interface>>`. Observer: blue/green/orange/violet class fills. All reinforce coupling/SOLID intuition before listing text.

### Ch05 Implementation & VCS — PASS
Git DAG: blue→green→orange/violet branches→green merge + yellow caption. Git Flow: 5 branch boxes distinct hues + solid/dashed arrow semantics. CI pipeline: 5 stage fills linear. Code listings (Java defensive, pip-tools, pre-commit, Makefile) all highlighted.

### Ch06 Testing — PASS
Pyramid: blue!8 triangle + green/orange/violet/red stacked layers + cost arrow. TDD loop: red→green→blue badges + dashed wrap-around. Listings (Java branch coverage, Python stubs/mocks, pytest-cov, mutation) highlighted. Pyramid shape prevents ice-cream anti-pattern visually.

### Ch07 Maintenance — PASS
4-way maintenance mix 2×2 grid with distinct red/orange/green/blue. Smell→fix bipartite mapping with solid primary / dashed alternative arrows. Traceability chain REQ→Design→Code→Test with `verifies`/`trace` labels. Legacy rescue loop green→orange→blue cycle.

### Ch08 Agile — PASS
Scrum flow 6-box loop with bend-back feedback. Board 4 columns + card fills (yellow user stories, blue bugs, green done). CI/CD 5-stage pipeline. Retrospective 3-question cycle. All reinforce text (roles/artefacts/events, DORA, WIP limits).

**Overall visual verdict: 0 monochrome-when-color-useful. Color is semantic (bad=red, good=green, abstraction=blue) and consistent across chapters.**

---

## 3. Ground-Up Audit (0→100: assume zero SE knowledge)

**Invariant:** assume no prior exposure to SE concepts; build from first principles — intuition → picture → definition → example → exercise. Check each SDLC/requirements/UML/SOLID/Git/testing/agile topic for assumed maturity.

| Ch | Topic | Ground-up verdict | Gaps asked → how the chapter answers |
|----|-------|-------------------|--------------------------------------|
| 01 | SDLC & process models | **SUFFICIENT** | Starts with "100-line script vs 50-person banking system" intuition (L4), defines SE formally only after motivation, enumerates 6 phases in plain language, introduces each model (waterfall/V/iterative/spiral) with strengths/weaknesses + when-to-choose table, UP 4 phases, CMMI tailoring, STARS case study. No assumed SDLC knowledge; Boehm 100× cost curve cited with context. |
| 02 | Requirements (FR/NFR, FURPS+, prioritisation, use cases/stories, SRS/traceability) | **SUFFICIENT** | Defines requirement from zero (L8–10), FR vs NFR vs domain with exam-system example (L20), FURPS+ figure before checklist, SMART/INVEST, 5-step RE process with stakeholder list (L60), MoSCoW+Kano negotiation, 5 classic pitfalls, use-case diagram with `include`/`extend`, user-story format + Gherkin listing, elicitation comparison table, SRS/traceability blast-radius. |
| 03 | UML (class/sequence/state/activity, package) | **SUFFICIENT** | Motivates "why model" before notation (L14), model vs diagram definition, visibility/relationship/multiplicity bullets before class figure, inheritance vs association-class heuristics, sequence lifeline/message types defined before diagram, state guard/action syntax before figure, activity fork/join semantics distinguished from flowcharts, package/component lollipop notation, 60-second readability remark. |
| 04 | Design principles & patterns (coupling/cohesion, SOLID, GRASP, GoF) | **SUFFICIENT** | Two-metric framing (coupling/cohesion) before SOLID, each SOLID principle in one paragraph with single-sentence example anchored to figure, DIP before/after diagram makes abstraction concrete, Singleton/Factory/Observer/Strategy each with captioned Java listing + caution (Singleton→DI) or selection guide, GRASP as assignment heuristic, package metrics (Ca/Ce/I/D) stated but not over-proved. Assumes basic OO (class/interface) but ch03 already built it — acceptable dependency. |
| 05 | Implementation & VCS (standards, defensive, Git, workflows, builds, review, CI) | **SUFFICIENT** | "Design documents do not run" hook (L4), 4-practice list before any Git, VCS defined as DAG + 5 bullet core concepts (repo/commit/branch/remote/staging), Git DAG figure ties to definitions, Git Flow branches enumerated then contrasted with GitHub Flow + trunk + feature flags, build reproducibility (lock files/containers), merge-conflict markers shown, PR size rule (<400 lines), CI 5-stage pipeline figure, semver + ADRs. Zero → can `git clone && make bootstrap`. |
| 06 | Testing (levels, black/white box, TDD, doubles, coverage, mutation, CI) | **SUFFICIENT** | Verification vs validation opening (L11), pyramid figure before level definitions (intuition-first), black-box (equivalence/boundary/decision) vs white-box (statement⊂branch⊂path) with Java `isEligible` listing, TDD red→green→refactor loop figure before benefits/costs, 5 test doubles defined (dummy/stub/spy/mock/fake) with stub-vs-mock listing, coverage listing + "necessary not sufficient" then mutation section as effectiveness answer, CI 10-minute gate, security/performance/BDD. |
| 07 | Maintenance, refactoring, debt, legacy | **SUFFICIENT** | "60% cost after release" hook, 4 maintenance types defined before Lehman laws, refactoring definition ("not rewriting"), 8 smell table + bipartite fix map figure, strangler-fig vs big-bang, tech-debt financial analogy with prudent/reckless distinction + 15–20% allocation, metrics (McCabe ≤10, duplication <3%), sprout/wrap/characterisation strategies, traceability impact figure, docs-as-code/bus-factor, estimating with spike card. |
| 08 | Agile, Scrum, CI/CD, DevOps | **SUFFICIENT** | Agile values before framework ("not no process"), Scrum roles/artefacts/events in one list + 2 figures before estimation, Kanban WIP limits + Lean 7 principles, CI/CD definitions (integration vs delivery vs deployment) + pipeline figure, deployment strategies (rolling/blue-green/canary), CALMS + DORA 4 metrics quantified (elite <1h), scaling (SAFe/LeSS/Nexus) + hybrid regulated-domain note, feature-flag listing for trunk, one-experiment retrospective figure. |

**Cross-chapter ground-up notes:**
- **Prerequisite threading is honest:** Ch01 builds SDLC vocabulary that Ch02 (RE process loop), Ch03 (UML modelling), Ch04 (design reasoning), Ch05 (Git collaboration), Ch06 (testing against requirements), Ch07 (maintenance cycle), Ch08 (agile as modern synthesis) each reuse explicitly. No "as known from MH1812/SC1007" leakage (unlike SC2001 v1). The one forward assumption — basic programming fluency for reading Java/Python snippets — is acceptable for an SE module (code is the object of study) and is mitigated by defensive-programming and Gherkin listings that read as pseudocode.
- **Intuition-first ordering holds throughout:** Every chapter leads with a motivating contrast or question, then shows a colored figure, then formalizes (FURPS+ before taxonomy, pyramid before test levels, cycle before phase list, TDD figure before cycle description, debt analogy before backlog percentage). This is the AGENTS.md "intuition → picture → formalism" law.
- **Depth without verbosity:** Each chapter is ~200 lines (1616 total) + 48 pages, matching the 8-ch × 6-page budget; exercises (5 per chapter, 40 total) require synthesis (draw traceability, sketch cost curve, design CI pipeline) not recall.

**Remaining minor gaps (non-blocking, tracked as future enhancements):**
- Ch04 GRASP "Pure Fabrication" and "Indirection" are named but only one sentence each — a one-line example per term would tighten zero-prior clarity (e.g., "Pure Fabrication: invent a `PaymentLogger` class when no domain class should own logging").
- Ch06 mutation testing could link back to the branch-coverage listing with a numbered annotation ("mutant at `>=` vs `>` survived because Test 2 missed the boundary") — currently two separate listings.
- Ch08 story-point Fibonacci and Little's Law are introduced quickly; a 2-line numeric example of Little's Law (`WIP 15 / throughput 3 per sprint → lead time 5 sprints`) is in the exercise but could be a worked inline box.

None of these fails the SUFFICIENT threshold; they are polish, not missing scaffolding.

---

## 4. Build & Formula QA

- All 26 `tikzpicture` environments compile (0 `!`, 0 `pgfkeys Error`). `scale=0.68–0.78` chosen to fit `a4paper` with narrow margins (top/bottom 1.3cm, left/right 1.2cm) — no figure exceeds text width.
- Display math is inline only (`$…$`, `$70\%$`, `$100×$`, `$C_e/(C_a+C_e)$`); no `align`/`equation` block overflows. `Overfull \hbox` clean (0 lines), so no formula break needed — inherits the small-screen geometry invariants from `main.tex` (`\setstretch{1.20}`, `\parskip 0.70em`, `\textfloatsep 10pt`).
- Code: 16 listings each with `language=` and caption; `\lstset` provides `breaklines=true` so narrow-phone widths will not overfull. The prior SC2001 risk (`verbatim` ban) does not recur here.

---

## 5. Fixes Applied This Review

| # | File:Line | Before | After | Rationale |
|---|-----------|--------|-------|-----------|
| 1 | `ch06:164–166` | `\section{Automation and Regression}` + paragraph repeating "Flaky tests … must be quarantined" (duplicate of §`Regression, Flaky Tests, and Test Doubles` L94) + "Test doubles—dummy, stub…" (duplicate of L96–104) | `\section{Automation and Regression Suite Curation}` + new paragraph: "As the suite grows, curate it: parallelise by shard, quarantine … (see § Regression above), promote E2E to nightly …" | Removed verbatim repetition (two sentences copied from L94/L96); section now advances to suite curation (sharding, nightly promotion) instead of restating earlier material. Builds on prior section via cross-ref. |
| 2 | `ch06:126` | `\section{Test Coverage and Quality}` + paragraph that pre-empted mutation ("Mutation testing … measures effectiveness …") — duplicated §`Mutation Testing and Test Quality` L148–150 | `\section{Measuring Coverage}` + trimmed paragraph ending "… but do not chase 100% at the expense of meaningful assertions. The next section shows how mutation testing measures whether tests actually detect faults." | Renamed to reflect that this section is measurement (`pytest --cov`), not quality judgement; forward pointer hands off to Mutation section instead of repeating its definition. Eliminates duplicate coverage→mutation sentence. |

Both patches are editorial (no new TikZ, no pagination change beyond 668878→668913 B). Build re-run: `pdflatex` exit 0, 48p, 0 Overfull, 0 `!`.

---

## 6. Gate Summary

| Gate | Result |
|------|--------|
| 26 TikZ color | **PASS** — 26/26 with `fill=` + colored edges/labels |
| 0 `verbatim`, ≥8 `lstlisting[Java/Python]` | **PASS** — 0 verbatim, 16 listings (6 Java, 10 Python) |
| 0 Overfull >15pt | **PASS** — 0 total Overfull |
| 0 `!` / `pgfkeys` errors | **PASS** |
| Ground-up (SDLC/requirements/UML/SOLID/Git/testing/agile) | **PASS — SUFFICIENT** across all 8 chapters (see §3) |
| Exercises | 40 (5 per chapter), synthesis-oriented |
| Trivial nits patched | 2 (ch06 section dedup, see §5) |

**Overall: PASS.** No blocking visual or ground-up issue. The module is shippable as a 0→100 text for readers with no prior SE exposure; the three minor polish items in §3 are optional enhancements.

*Reviewer — SC2006 visual+ground-up — compiler + line-by-line audit complete.*
