# SC4024 Data Visualisation — Outline

**Code:** SC4024 (MPE 3 AU) · **Prereqs:** SC1007 Data Structures & Algorithms → SC2007/SC2001 Algorithm Design → SC3020 Data Analytics & Mining → SC4024 · **Also:** SC2000 Probability & Statistics, SC1004 Linear Algebra · **Position:** MPE capstone, graphics & analytics bridge · **Approach:** 0→100 ground-up, intuition→formalism, small-screen geometry 1.3/1.2 setstretch 1.20, color TikZ + lstlisting

## Module Overview
SC4024 teaches how to turn data into pictures that humans can reason with. It assumes zero visualisation background and builds from human perception (Ch 1) through data models and encodings (Ch 2), design and colour (Ch 3), statistical and interactive charts (Ch 4), network layouts (Ch 5), scientific volumes (Ch 6), cognition and evaluation (Ch 7), to production tools and narrative (Ch 8). 0→100 flow is **see → encode → design → interact → scale → evaluate → tell**. Every chapter uses `lstlisting` with Python/Altair/D3/Vega-Lite snippets and proves or motivates each principle from first principles.

## Chapter Plan (8 chapters, 4–5 LOs each)

### Ch 1 — Visualisation Foundations & Perception
- define visualisation: mapping data → visual variables, Anscombe and why pictures matter;
- explain human visual system: retina, pre-attentive processing, Weber–Fechner and Stevens laws;
- classify visualisation goals: exploratory, explanatory, presentational; Munzner nested model;
- compare effectiveness rankings of visual channels (Mackinlay) on small examples;
- implement a first scatter/heat example in Python and critique it.

### Ch 2 — Data Types & Visual Encodings
- taxonomy: nominal, ordinal, quantitative, temporal, spatial, relational; dataset types;
- define marks (point, line, area) and channels (position, length, angle, colour, size);
- apply expressiveness & effectiveness: choose channel for data type, avoid mismatch;
- encode tables, networks, fields, geometry; handle missing and uncertain data;
- build encodings in code: Altair/Vega-Lite channel bindings and scale transforms.

### Ch 3 — Design Principles & Colour Theory
- principles: data-ink ratio, chartjunk, lie factor, data density, figure–ground, Gestalt;
- formulate colour spaces: RGB, HSL, Lab/Luv, HCL; perceptual uniformity;
- design palettes: sequential, diverging, qualitative; ColorBrewer and accessibility (CVD);
- apply Gestalt laws (proximity, similarity, continuity) to layout and grouping;
- critique and redesign a flawed chart: colour, annotation, and hierarchy fixes.

### Ch 4 — Statistical Charts & Interaction
- survey statistical charts: histogram, boxplot, violin, scatterplot matrix, parallel coordinates;
- derive binning, KDE, and quantile logic; link to SC2000 distributions;
- design interaction: Shneiderman mantra, brushing, linking, filtering, zoom, details-on-demand;
- implement linked views and dynamic queries (Altair selections, D3 brushes);
- evaluate interaction latency and visual scalability trade-offs.

### Ch 5 — Graph & Network Visualisation
- layout families: force-directed, layered (Sugiyama), circular, hive, matrix vs node-link;
- define aesthetics: crossings, bends, symmetry, angular resolution, edge bundling;
- apply hierarchy and tree visualisation: treemap, sunburst, icicle; large-graph sampling;
- analyse multivariate networks: attribute encoding on nodes/edges, adjacency matrix ordering;
- implement a force layout and a matrix view in D3 and compare readability.

### Ch 6 — Volume & Scientific Visualisation
- scalar fields: isosurface (marching cubes), direct volume rendering, transfer functions;
- vector fields: glyphs, streamlines, LIC; tensor ellipsoids and topology;
- map projections and scientific domains: medical (CT/MRI), flow, geospatial, time-varying;
- optimise via acceleration: octrees, GPU ray casting, level-of-detail;
- build a volume ray-marcher sketch and an isosurface extraction demo in Python.

### Ch 7 — Perceptual, Cognitive & Evaluation
- perception deeper: pre-attentive pop-out, change blindness, attention, working memory;
- cognition: mental models, chunking, cognitive load, dual-process reasoning with charts;
- design controlled studies: hypothesis, variables, tasks (Cleveland–McGill, Heer–Bostock);
- measure: accuracy, time, preference, insight; statistics: t-test, ANOVA, effect size;
- run a mini evaluation: compare two encodings and report with confidence intervals.

### Ch 8 — Tools & Storytelling (D3, Vega-Lite, Narrative)
- survey stack: D3.js (low-level), Vega-Lite (grammar), Tableau, Python (Matplotlib/Altair/Plotly);
- compose Vega-Lite specs: data, transform, mark, encoding, view composition (layer/concat/facet);
- script D3 data joins, scales, axes, transitions; contrast declarative vs imperative;
- craft narrative: story points, annotating, sequencing, scrollytelling, dashboard rhetoric;
- deliver a capstone story: dataset → sketches → interactive narrative → presentation.

## TikZ Diagram Plan (2–3 per chapter, color where useful)

- **Ch1:** (1) Visualisation pipeline: data→transform→visual mapping→view (blue!12/green!14/orange!14/violet!10); (2) Retina to cortex cartoon with pre-attentive pop-out grid (red target among blue distractors); (3) Mackinlay channel ranking bars (quantitative vs nominal, teal!14/blue!12)
- **Ch2:** (1) Data-type taxonomy tree: tables→networks→fields→geometry (fills per type); (2) Marks & channels gallery: point/line/area × position/colour/size (legend); (3) Expressiveness mismatch: nominal→length vs hue comparison (red error vs green correct)
- **Ch3:** (1) Gestalt laws demo: proximity/similarity/continuity panels (grey dots → coloured groups); (2) Colour spaces: RGB cube vs Lab uniformity strip (rainbow vs perceptually uniform); (3) Palette types: sequential/diverging/qualitative swatches with CVD simulation
- **Ch4:** (1) KDE vs histogram with bin-width slider effect (blue histogram, orange KDE, green rug); (2) Brushing & linking: scatterplot + histogram linked (brush yellow!16, linked highlight red!16); (3) Shneiderman mantra pipeline overview→zoom→details
- **Ch5:** (1) Force-directed vs matrix view of same 6-node graph (blue nodes, red force edges vs yellow matrix); (2) Treemap vs sunburst vs icicle for hierarchy (green/orange/violet fills); (3) Edge-bundling before/after (grey hairball → bundled teal)
- **Ch6:** (1) Volume rendering pipeline: scalar field→transfer function→ray casting→image (orange→violet gradient); (2) Marching cubes 2-D case table with isovalue interpolation (blue cells, red isoline); (3) Vector glyphs vs streamlines vs LIC on same field (arrow green, streamline blue, LIC texture)
- **Ch7:** (1) Pre-attentive search: colour vs conjunction (pop-out vs serial, red/blue targets); (2) Evaluation design: independent vs dependent variables, within/between subjects (teal/orange boxes); (3) Results forest plot with CI and effect size (blue points, red significance)
- **Ch8:** (1) Tool stack pyramid: D3→Vega→Vega-Lite→Tableau (granularity vs ease, blue→green gradient); (2) Vega-Lite spec anatomy: JSON blocks data→mark→encoding (yellow/blue/teal); (3) Story arc: Martini-glass narrative structure with annotation callouts

## lstlisting Language Plan

- **Python (primary, Ch 1–7):** Matplotlib, Altair/Vega-Lite via Python, NumPy, NetworkX, scikit-image for marching cubes sketch. Every block `language=Python`.
- **JavaScript/JSON (Ch 8 primary, Ch 4–5 secondary):** D3.js data joins and Vega-Lite JSON specs. Blocks use `language=JavaScript` or `language=Python` where Python generates Vega-Lite JSON; Vega-Lite JSON shown inside Python string or as JavaScript object literal.
- Every code block uses `\begin{lstlisting}[language=...]` (never verbatim); caption + line numbers; xleftmargin 1em.

## Exercise Themes (per chapter, 5 items)

- Ch1: reproduce Anscombe quartet, Stevens power-law fit, channel ranking experiment sketch, nested-model mapping, critique a misleading chart.
- Ch2: classify datasets by type, choose channels for 4 variables, fix expressiveness error, encode uncertainty with value-suppressing, Altair channel binding task.
- Ch3: compute data-ink ratio, design CVD-safe palette, apply Gestalt to redesign, lie-factor calculation, Lab interpolation vs RGB.
- Ch4: histogram bin-width selection (Sturges/Freedman), KDE bandwidth effect, implement brushing in Altair, design details-on-demand, SPLOM vs parallel coordinates trade-off.
- Ch5: draw force vs matrix for 8 nodes, count crossings in two layouts, build treemap vs sunburst, order matrix by barycentre, D3 force parameter tuning.
- Ch6: extract 2-D isocontour by hand, design transfer function for CT, trace streamline via Euler, compare glyph density, octree culling arithmetic.
- Ch7: change-blindness demo design, Cleveland–McGill replication plan, power analysis for study, analyse given accuracy/time data with CI, insight diary protocol.
- Ch8: write Vega-Lite spec for layered chart, D3 data-join update pattern, Tableau vs code trade-off memo, storyboard a dataset narrative, capstone dashboard critique.

## Prereq Graph Note (how it builds on SC1007→SC2007→SC3020→SC4024)

**SC1007 → SC2007/SC2001 → SC4024:** basic structures and algorithms for layout (BFS, force iteration, treemap recursion), complexity for scalability.
**SC2000 → SC4024:** distributions, KDE, quantiles, hypothesis testing for Ch 4 and Ch 7 evaluation.
**SC3020 → SC4024:** data mining context: SC3020 covers analysis; SC4024 covers communication—shared transforms, shared curiosity about structure in data.
**Graph:** `SC1007 → SC2007/SC2001 → SC2207/SC3020 → SC4024 → {FYP/capstone/visual analytics}` and `SC2000 + SC1004 → SC4024`; SC4024 is MPE-leaf, not a prereq for other cores.

## 0→100 Flow Summary

Perceive (Ch 1: how eyes and brain see) → Encode (Ch 2: what data types map to what marks) → Design (Ch 3: how to make it honest and beautiful) → Explore (Ch 4: how to interact with distributions) → Connect (Ch 5: how to show networks) → Render (Ch 6: how to show volumes and fields) → Validate (Ch 7: how to know it works) → Narrate (Ch 8: how to tell the story with tools). No prior visualisation assumed; every principle is introduced via intuition→definition→example→exercise.
