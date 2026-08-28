# SC4023 AI for Software Engineering — Outline

**Code:** SC4023 (MPE 3 AU, variant SC5006) · **Prereqs:** SC2006 Software Engineering + SC3000 Artificial Intelligence (SC2001 helpful) · **Position:** MPE elective bridging SE process + AI methods · **Approach:** 0→100 ground-up, intuition→formalism, small-screen geometry 1.3/1.2 setstretch 1.20, color TikZ + lstlisting[Python/Java]

## Module Overview
SC4023 teaches *AI as an engineering partner* across the SDLC: from raw code and tests to AI-assisted generation, repair, and maintenance. It assumes zero AI-for-SE background and builds systematically: Ch 1–2 ground code/tests representations, Ch 3–5 apply modern AI (LLMs, embeddings, search) to generation/testing/repair, Ch 6–7 broaden to requirements/design/quality + evaluation/trust, Ch 8 synthesises an end-to-end AI-augmented pipeline. 0→100 flow is **code → tests → AI assistance**: first understand what code *means* (AST, representations), then how correctness is judged (tests, coverage), then how AI proposes, checks, and repairs code under human oversight. Each chapter useslstlisting with **Python** for AI/ML and **Java** for SE enterprise examples. All diagrams are color TikZ.

## Chapter Plan (8 chapters, 4–5 LOs each)

### Ch 1 — Foundations: Why AI for Software Engineering?
- define SE pain points (Boehm cost curve, defect leakage) and where AI helps vs. where it cannot;
- map the SDLC (SC2006 review) and locate AI insertion points per phase;
- distinguish automation vs. augmentation vs. autonomous generation and human-in-the-loop;
- classify AI-for-SE tasks (generation, completion, summarisation, repair, test, review);
- set up the 0→100 flow: code→tests→AI, and tool chain (Python, datasets, evaluation harness).
### Ch 2 — Code as Data: Representations, ASTs & Embeddings
- parse code into tokens, ASTs, CFGs/DFGs and explain why raw text is insufficient;
- build bag-of-tokens / sequence / graph encodings and compare trade-offs;
- train/use code embeddings (Code2Vec, CodeBERT intuition) and probe what they capture;
- apply embeddings to clone detection, code search, and similarity tasks;
- critique representation limits (aliasing, semantics vs. syntax).
### Ch 3 — Large Language Models for Code Generation
- explain LLM pretraining (next-token) → code finetuning → instruction tuning (SC3000 recap, 0→100);
- prompt strategies: zero/few-shot, chain-of-thought, retrieval-augmented generation for code;
- use and evaluate Copilot/Code Llama/StarCoder-style completion on HumanEval/MBPP intuition;
- detect hallucinations, insecure idioms, and license leakage in generated code;
- enforce guardrails: constrained decoding, post-generation static checks.
### Ch 4 — AI-Assisted Testing: Generation, Selection & Oracles
- recall testing pyramid & coverage (SC2006) and where AI complements human tests;
- generate unit tests with LLMs (prompt→assert) and search-based methods (EvoSuite intuition);
- select/minimise/prioritise tests using coverage and mutation signals;
- synthesise oracles and property-based tests; handle flaky-test detection;
- evaluate generated suites: line/branch/mutation score vs. false confidence.
### Ch 5 — Program Repair, Bug Detection & Static Analysis
- taxonomy: defect detection vs. fault localisation (spectrum-based) vs. automated repair;
- combine static analysis/AST patterns with learned detectors for vulnerability finding;
- generate patches via NMT/LLM and template-based repair; rank candidates by test+spec;
- apply generate-and-validate vs. correct-by-construction and discuss overfitting to tests;
- measure repair success: plausible vs. correct patches, Defects4J-style benchmarks.
### Ch 6 — AI for Requirements, Design, Maintenance & Code Review
- mine requirements from NL (user stories, SRS) via NLP classification and traceability links;
- assist design: API recommendation, UML sketch-to-code, architecture smell detection;
- support maintenance: code summarisation, commit-message generation, refactoring suggestion;
- automate code review: learned review comments, style/lint + semantic feedback;
- manage tech debt & evolution: duplicate detection, dependency analysis, change-impact prediction.
### Ch 7 — Evaluation, Trust, Ethics & Human-in-the-Loop
- design benchmarks (HumanEval, SWE-Bench, Defects4J) and avoid leakage/contamination;
- quantify correctness, robustness, efficiency, and security of AI-generated artefacts;
- explain AI decisions: attention/provenance, counterexample explanations;
- address ethics: bias, IP/license, privacy of proprietary code, accountability;
- implement HITL workflows: accept/reject/edit loops, confidence thresholds, audit trails.
### Ch 8 — Studio: End-to-End AI-Augmented SDLC Capstone
- compose Ch 1–7 into a single pipeline: spec→generate→test→repair→review→ship;
- build an AI pair-programmer harness (IDE plugin + CI gate) for a sample Java/Python project;
- integrate coverage, mutation, and static-analysis gates that AI must pass;
- run a controlled experiment (with vs. without AI) on velocity and defect density;
- reflect on limits, cost, and adoption: when *not* to use AI for SE.

## TikZ Diagram Plan (2–3 per chapter, color where useful)

- **Ch1:** (1) SDLC ring with AI insertion badges (blue!15 req, green!15 design, orange!15 impl/test, violet!15 deploy — legend); (2) Cost-of-defect exponential curve + AI shift-left arrow (red!12→green!12 fill); (3) Automation spectrum slider (manual→augmented→autonomous, teal gradient)
- **Ch2:** (1) Code→tokens→AST→graph pipeline (blue!12→green!14→orange!14→violet!12 boxes); (2) AST for `for` loop with coloured node types (keyword blue!15, id green!15, literal orange!15); (3) Embedding t-SNE cluster of clones (scatter, clone pairs linked violet)
- **Ch3:** (1) LLM code pipeline: pretrain→finetune→RLHF→prompt→generate (blue!12→teal!12→green!12→orange!12→violet!12); (2) Prompt template with retrieval augmentation (yellow!12 context box feeding blue prompt); (3) Pass@k evaluation funnel (samples→execute→pass, green/red bars)
- **Ch4:** (1) Testing pyramid with AI-assisted layer overlay (blue base + orange AI band, WIP limits grey); (2) Coverage heatmap: file×test matrix (green covered, red uncovered, grey flaky); (3) Mutation score lattice (killed/survived mutants, violet!10)
- **Ch5:** (1) Spectrum-based fault localisation spectrum (red suspicious→green clean, heat bar); (2) Generate-and-validate repair loop: bug→localise→generate→validate→rank (circular, 4 fills); (3) Plausible vs. correct Venn (blue plausible, green correct, overlap teal, red overfit)
- **Ch6:** (1) Req traceability bipartite: NL stories (blue!12) ↔ code/test artefacts (green!12) with learned links (orange dashed); (2) Code-review bot swimlane: author→bot→CI→human reviewer (4 lanes, fills); (3) Tech-debt treemap by module (orange intensity = debt)
- **Ch7:** (1) Benchmark leakage diagram: train/test overlap with contamination warning (red!15 forbidden zone); (2) Trust dashboard: correctness/robustness/security gauges (blue/green/red dials); (3) HITL loop with confidence gate (blue AI→amber threshold diamond→green human→teal audit log)
- **Ch8:** (1) End-to-end AI-SDLC pipeline board (backlog→AI-gen→test gate→repair→review→ship, Kanban fills per SC2006 ch08); (2) A/B experiment design: control vs. AI-augmented throughput/defect bars (blue vs. green); (3) Cost-benefit frontier: velocity vs. defect density Pareto (violet curve, dominated region grey)

## lstlisting Language Plan

- **Python (primary, Ch 2–5, 7–8):** tokenisation/AST via `ast`/`tree-sitter`, embeddings with `transformers`/`sentence-transformers`, LLM prompting via HuggingFace/OpenAI API, test generation & mutation with `pytest`, program-repair ranking, benchmark harness (HumanEval/SWE-Bench mini). Shared `lstset` highlights (keyword blue!60!black, comment green!50!black, string orange!60!black).
- **Java (secondary, Ch 1, 4–6, 8):** enterprise SE artefacts — JUnit 5 tests, EvoSuite-style generated tests, Defects4J bug snippets, review examples, CI pipeline snippets (Maven/Gradle). Demonstrates SC2006→SC4023 transfer (same Java DTOs tested in Ch 4, repaired in Ch 5, reviewed in Ch 6/8).
- Every code block uses `\begin{lstlisting}[language=Python]` or `[language=Java]` (never verbatim); caption + line numbers; xleftmargin 1em for small-screen.

## Exercise Themes (per chapter, 4–6 items)

- Ch1: SDLC mapping table, cost-curve calculation, classify AI-for-SE papers by task, tool-chain setup (clone repo, run harness).
- Ch2: hand-parse to AST, compare BoW vs. AST similarity on clones, probe embedding nearest neighbours, write tree-sitter query.
- Ch3: engineer 3 prompts for same spec (compare pass@1), detect insecure generation (SQL injection), RAG vs. no-RAG ablation, license audit.
- Ch4: generate JUnit/pytest suite with LLM, measure coverage & add missing branch, minimise suite, flaky-test quarantine drill.
- Ch5: localise bug via Tarantula/Ochiai on coverage matrix, rank 3 LLM patches (plausible vs. correct), static-analysis rule vs. learned detector.
- Ch6: link user stories to code (traceability matrix), summarise a Java class with LLM and critique, bot-review a PR diff, smell detection on God class.
- Ch7: design a decontaminated split, compute pass@k & mutation score, write model card & risk register, HITL threshold tuning.
- Ch8: capstone — ship a feature with AI pair-programmer under CI gates; A/B report on velocity/defects; reflection essay on when to disable AI.

## Prereq Graph Note (how it builds on SC2006 + SC3000)

**SC2006 → SC4023:** reuses SDLC, requirements/FURPS+, UML, design principles/SOLID, testing pyramid/coverage/TDD, maintenance/refactoring, and agile/CI/CD as the *substrate AI augments* — every AI technique is evaluated by whether it improves a classical SE activity. Students who skip SC2006 would lack the definition of "correctness" that AI is judged against.
**SC3000 → SC4023:** reuses agent/rationality framing (Ch 1), search & logic (Ch 2–5), and ML/learning fundamentals (perceptron→LLM intuition, train/test/overfitting, embeddings) as the *methods* — Chapter 3 explicitly recaps next-token pretraining before code-LLMs so non-SC3000 readers can follow, then deepens to code-specific finetuning. Together: SC2006 supplies *what to automate*, SC3000 supplies *how*, SC4023 is their intersection.
**Graph:** `SC1003→SC2002→SC2006 ─┐` + `SC3000 (with SC2001/MH1812 upstream) ─┤→ SC4023 → {SC4040/SC4051/MH4511 capstones}`; SC4023 is MPE-leaf, not a prereq for other cores.

## 0→100 Flow Summary

Code (Ch 1–2: what software is, how code is represented) → Tests (Ch 4 + parts of 1/5: how we know it works, coverage/oracles/mutation) → AI Assistance (Ch 3,5–8: how AI generates, tests, repairs, reviews, and ships under human oversight). No prior AI-for-SE assumed; every formal notion (AST, embedding, pass@k, spectrum localisation) is introduced via intuition→definition→example→exercise before use.
