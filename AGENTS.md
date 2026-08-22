# NTU CS Textbooks — Project Instructions (AGENTS.md)
> Last updated: 2026-08-23 (Bowen 0→100 ground-up + visual-qa + small-screen)

## 0→100 ground-up content law (MUST-pass)
- **Assume ZERO bachelor's knowledge.** Every module starts from first principles (sets, logic, what a computer does). Do not assume discrete math, data structures, or programming maturity — define everything on first use, add intuition before formalism, then formalize.
- **Intuition first, then rigor.** Each concept: why it exists (intuition / picture / analogy) → formal definition → worked example → proof/sketch → exercise. Never jump straight to formalism.
- **No word limit.** Be as long as needed; not verbose/redundant, but do not compress to save space. Depth over brevity.

## Build quality invariants (MUST-pass before any commit)
- **Diagrams:** TikZ figures MUST use color where useful — fills (blue!15, green!20, orange!15, violet!10), colored nodes/edges, legend. Monochrome only when pedagogy demands. Each TikZ must compile (0 pgfkeys errors) and be labeled.
- **Formulas:** Every display/inline math must render correctly — test via `pdflatex -interaction=nonstopmode main.tex` and grep for `! `, `Overfull \hbox >15pt`, `Missing $`, `Misplaced alignment`. Use `align`/`equation` environments, break long formulas, no raw `$...$` wrapping across lines.
- **Code blocks:** NEVER plain `verbatim` for code. Use `listings` with language + syntax highlighting: `\begin{lstlisting}[language=Python]` or `C`, `Java`. Preamble must define lst colors (keyword blue!60!black, comment green!50!black, string orange!60!black, numbers gray). Use `lstset` with `language=` per block.
- **QA gate:** Adversarial reviewer MUST compile the full book (`pdflatex` ×2), check tikz/formula rendering visually (grep + page-count), and FAIL the module if any diagram is monochrome when color is useful, any formula overflows, or any code block lacks highlighting.

## Repo & workflow
- Branch `main`, remote `origin` = github.com/bumbsclaw/ntu-cs-textbooks. Commit routinely (outline → chapters → QA → pdf).
- `progress.md` is crash-resume checkpoint — first `PENDING` row is next task.
- Modules under `modules/<CODE>/` with `main.tex` (book class) + `chapters/*.tex` + `main.pdf` (tracked). `.gitignore` ignores *.aux/log/out/toc only — PDFs are tracked via `git add -f`.
- Model for fleets: `muse-spark-1.2-contribution` via opencode-go (ox-alpha-free ONLY, no fallback). Keep generations ≤260 lines / ~3000 tokens to stay under 30s 500/503 flap.

## Small-screen layout (Bowen 2026-08-23)
- Geometry: narrow margins (top/bottom ~1.3cm, left/right ~1.2cm, includeheadfoot) to maximize text area on phones. Spacing: \setstretch{1.20}, \parskip 0.70em, list itemsep 0.45em — airier than default. Float seps reduced for phone scroll.
- Keep lstlisting xleftmargin ~1em so code blocks breathe on narrow widths. Verify pdf still compiles with no Overfull>15pt on phone-width text.
