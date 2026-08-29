# SC4022 Network Science — Outline

**Code:** SC4022 (MPE 3 AU) · **Prereqs:** SC2001 Algorithm Design & Analysis + MH1812 Discrete Mathematics + SC2000 Probability & Statistics (SC2203 helpful) · **Position:** MPE elective, data & systems bridge · **Approach:** 0→100 ground-up, intuition→formalism, small-screen geometry 1.3/1.2 setstretch 1.20, color TikZ + lstlisting[Python]

## Module Overview
SC4022 studies the structure, formation, and behaviour of complex networks—social, biological, and technological. It assumes zero network-science background and builds from graph fundamentals (Ch 1) through measurement (Ch 2–3), generative models (Ch 4–5), dynamical processes (Ch 6), and robustness (Ch 7), culminating in real-world applications (Ch 8). 0→100 flow is **structure → model → dynamics**: first what networks *are*, then how they *form*, then what *happens on them*. Each chapter uses `lstlisting` with Python (NetworkX) and proves key results from first principles.

## Chapter Plan (8 chapters, 4–5 LOs each)

### Ch 1 — Network Foundations & Graph Models
- define graphs, directed/weighted/bipartite variants, adjacency and incidence representations;
- explain degree, path, component, and diameter intuition before formalism;
- classify canonical graph models (lattice, tree, complete, bipartite) and their properties;
- compute clustering coefficient and average path length on small examples;
- represent and manipulate graphs in code (adjacency list vs matrix trade-offs).

### Ch 2 — Centrality Measures
- motivate importance ranking: why degree alone is insufficient;
- define degree, closeness, betweenness, eigenvector and PageRank centralities;
- compute each measure on small hand-worked graphs and rank nodes;
- prove PageRank as stationary distribution of a random walk with teleportation;
- compare centrality correlations and choose the right measure for a task.

### Ch 3 — Community Detection
- define community/modularity intuition: dense inside, sparse outside;
- formulate modularity Q and the Louvain/Leiden greedy optimisation;
- apply spectral partitioning and label-propagation on toy networks;
- evaluate partitions: NMI, adjusted Rand, conductance, coverage;
- detect overlapping communities and hierarchical structure.

### Ch 4 — Random Graphs: ER, Configuration & Small-World
- construct Erdos-Renyi G(n,p) and G(n,M) and derive degree distribution (Poisson);
- explain phase transitions: emergence of giant component at p=1/n;
- build configuration model to match arbitrary degree sequences;
- generate Watts-Strogatz small-world via rewiring: high clustering + short paths;
- test real networks against null models (when is structure significant?).

### Ch 5 — Scale-Free Networks & Preferential Attachment
- characterise heavy-tailed degree distributions and power laws (log-log, MLE);
- derive Barabasi-Albert model: growth + preferential attachment → P(k) ~ k^{-3};
- simulate BA and measure hubs, exponent, and age-degree correlation;
- contrast BA with fitness, copying, and configuration alternatives;
- detect scale-free claims critically: Clauset-Shalizi-Newman tests.

### Ch 6 — Dynamics & Spreading: SIR on Networks
- model epidemics and information spread: SI, SIS, SIR on graphs;
- derive epidemic threshold via spectral radius (λ_c = 1/ρ(A)) and mean-field;
- simulate SIR on ER vs scale-free vs small-world and compare outbreaks;
- analyse influence maximisation and immunisation strategies (targeted vs random);
- extend to threshold models, cascading failures, and opinion dynamics.

### Ch 7 — Network Robustness & Resilience
- define robustness: connectivity under node/edge removal (random vs targeted);
- quantify percolation thresholds and size of giant component after attack;
- analyse error tolerance of scale-free vs fragility under hub removal;
- design resilient networks: onion structure, redundancy, and modular hardening;
- evaluate recovery: cascading failures and interdependent networks.

### Ch 8 — Applications: Social, Biological & Technological Networks
- map social networks: friendship, collaboration, influence and homophily;
- analyse biological networks: PPI, metabolic, neural, and ecological webs;
- dissect technological networks: WWW, Internet AS-graph, power grids, transport;
- synthesise cross-domain lessons: universal vs domain-specific patterns;
- conduct a capstone mini-project: collect, analyse, and report on a real dataset.

## TikZ Diagram Plan (2–3 per chapter, color where useful)

- **Ch1:** (1) Graph types gallery: undirected/directed/weighted/bipartite (4 panels, blue!12/green!14/orange!14/violet!10); (2) Path & component illustration on 8-node graph (blue component fill, red path highlight); (3) Adjacency matrix vs list side-by-side (yellow!10 matrix, teal!10 list)
- **Ch2:** (1) Star vs bridge: degree vs betweenness contrast (hub blue!15, bridge orange!16); (2) Eigenvector centrality iteration converging (bar chart sequence, violet gradient); (3) PageRank random-walk with teleportation (green!14 nodes, dashed teleport edges)
- **Ch3:** (1) Two-community network with/without correct partition (blue/green clusters, red cut edges); (2) Modularity landscape Q vs partition (curve with optimum, orange!14 peak); (3) Spectral embedding 1-D layout (nodes on line, blue→red communities)
- **Ch4:** (1) ER giant-component emergence S-curves for n=20,100,500 (blue/green/orange); (2) Configuration model stub-matching (stubs yellow!14, matched green!14); (3) Watts-Strogatz rewiring lattice→random (blue lattice, red rewired edges, clustering vs path trade-off)
- **Ch5:** (1) Power-law vs Poisson degree distribution log-log (red power-law line, blue Poisson curve); (2) BA growth animation 4 steps (new node green, preferential edges violet); (3) Hub-and-spoke scale-free with degree-rank plot (hub red!18, leaves blue!12)
- **Ch6:** (1) SIR curves S/I/R over time on chain vs star network (blue/green/red time series); (2) Epidemic threshold vs spectral radius diagram (infected fraction, λ_c vertical); (3) Immunisation comparison random vs hub-targeted (green shield vs red target, bar chart outcome)
- **Ch7:** (1) Random vs targeted removal effect on scale-free (giant component size vs f, blue random slow, red targeted cliff); (2) Percolation lattice with occupied fraction p and spanning cluster (green occupied, yellow cluster); (3) Onion robust vs fragile topology contrast (concentric blue!14 vs hub red!14)
- **Ch8:** (1) Three-domain montage: social/bio/tech icons as networks (blue/green/orange panels); (2) Bipartite projection: authors→papers→co-authorship (yellow→green→blue pipeline); (3) Capstone workflow: collect→clean→measure→visualise→report (pipeline with fills per chapter)

## lstlisting Language Plan

- **Python (primary, all chapters):** NetworkX for creation/measure/layout, NumPy/SciPy for distributions and spectra, Matplotlib conceptual snippets, simulation loops for ER/BA/SIR. Every block `language=Python`.
- **Python secondary snippets (Ch 1,4,6,8):** adjacency matrix via NumPy, configuration-model stub code, SIR Gillespie-style simulation, real-data loading (Karate club, Les Miserables, power grid).
- Every code block uses `\begin{lstlisting}[language=Python]` (never verbatim); caption + line numbers; xleftmargin 1em for small-screen.

## Exercise Themes (per chapter, 5 items)

- Ch1: hand-draw graph, count edges via handshake lemma, compare matrix vs list memory, compute clustering, BFS diameter.
- Ch2: rank by 3 centralities on 6-node graph, trace PageRank iteration, prove eigenvector exists (Perron-Frobenius intuition), correlation test.
- Ch3: compute modularity by hand, run Louvain step, spectral cut on 8 nodes, NMI of two partitions, overlapping extension.
- Ch4: generate G(n,p) and estimate GC threshold, configuration-model degree check, WS clustering vs p sweep, null-model hypothesis test.
- Ch5: fit power-law slope on log-log, simulate BA(n=500) and test k^{-3}, age-degree plot, Clauset test critique, fitness-model variant.
- Ch6: threshold on 3 topologies, mean-field SIR equations, SIS steady-state, influence maximisation greedy, threshold cascade demo.
- Ch7: GC vs f for random/targeted, percolation p_c on 2D lattice, onion construction gain, interdependent cascade, redundancy budget.
- Ch8: karate-club full analysis report, PPI hub biological meaning, WWW bow-tie description, bipartite projection task, capstone dataset paper.

## Prereq Graph Note (how it builds on SC2001 + MH1812 + SC2000)

**SC2001 → SC4022:** graph concepts (BFS/DFS, shortest path, MST), algorithm analysis for community Louvain and centrality costs, complexity of NP-hard partitioning.
**MH1812 → SC4022:** sets, combinatorics, graph theory foundations, proof techniques for phase transitions and power-law derivations; logic for modularity formalism.
**SC2000 → SC4022:** random variables, distributions (Poisson, power-law), expectation, MLE, hypothesis testing—essential for ER analysis, BA derivation, and Clauset tests.
**Graph:** `SC1003→SC1007→SC2001 ─┐` + `MH1812 ─┤→ SC4022 → {capstone/research}` and `SC2000 ─┘`; SC2203 automata helpful but not required. SC4022 is MPE-leaf, not a prereq for other cores.

## 0→100 Flow Summary

Foundations (Ch 1: what a network is) → Measurement (Ch 2–3: who matters, what groups exist) → Formation (Ch 4–5: how networks arise randomly vs by rich-get-richer) → Behaviour (Ch 6–7: what happens on networks, how they break) → Reality (Ch 8: what real networks reveal). No prior network science assumed; every formal notion (modularity, giant component, preferential attachment, epidemic threshold) is introduced via intuition→definition→example→exercise.
