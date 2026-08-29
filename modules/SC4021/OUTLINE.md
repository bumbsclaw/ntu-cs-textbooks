# SC4021 Information Retrieval — Outline

**Code:** SC4021 (MPE 3 AU) · **Prereqs:** SC2001 Algorithm Design & Analysis + SC2207 Introduction to Databases (SC2000 Probability helpful) · **Position:** MPE elective bridging algorithms + data management + machine learning · **Approach:** 0→100 ground-up, intuition→formalism, small-screen geometry 1.3/1.2 setstretch 1.20, color TikZ + lstlisting[Python]

## Module Overview
SC4021 teaches *how to find the right document among millions*: from a user's vague need to a ranked list that satisfies it. It assumes zero IR background and builds systematically: Ch 1–2 ground what IR is and how Boolean/vector models differ, Ch 3–4 quantify term importance (TF-IDF) and make retrieval fast (inverted index), Ch 5 measures success rigorously (precision/recall/MAP/NDCG), Ch 6–8 improve and learn ranking (query expansion, links/PageRank, learning-to-rank & neural IR). 0→100 flow is **foundations → representation → efficiency → evaluation → improvement → learning**.

## Chapter Plan (8 chapters, 4–5 LOs each)

### Ch 1 — IR Foundations: From Need to Ranked List
- define information need vs query vs relevance and the IR pipeline (crawl→index→query→rank);
- contrast IR vs databases (exact match) vs data mining (pattern discovery);
- introduce collection, document, term, vocabulary and relevance judgments;
- describe the classic IR pipeline and the role of tokenization/normalization;
- scope a tiny IR task: Given 5 docs and a query, reason about relevance before any math.

### Ch 2 — Boolean Retrieval vs Vector Space Model
- construct Boolean retrieval (terms as sets, AND/OR/NOT, inverted sets) and its pros/limits;
- introduce the vector-space intuition: documents and queries as vectors in term-space;
- formalise cosine similarity and the term-document matrix;
- compare Boolean (exact) vs ranked retrieval and when each wins;
- work a 2-D vector example projecting queries onto documents.

### Ch 3 — Term Weighting: TF-IDF and Beyond
- explain why raw term frequency misleads and why rarity matters;
- derive TF variants (raw/log/double-norm), IDF = log(N/df), and TF-IDF product;
- normalise by document length and introduce sublinear TF / pivoted normalization intuition;
- contrast TF-IDF with BM25 preview (saturation + length penalties);
- compute TF-IDF by hand on a 3-doc corpus and rank a query.

### Ch 4 — The Inverted Index: Making Retrieval Fast
- define dictionary + postings, docIDs, term frequencies, positions;
- build a single-pass in-memory indexer (SPIMI intuition) and blocking/BSBI for large collections;
- handle phrase and proximity queries via positional postings;
- compress postings (gap encoding, variable-byte, gamma) and skip pointers for intersection speedup;
- analyse time/space: indexing O(T), query O(p log p), compression ratios.

### Ch 5 — Evaluation: Precision, Recall, MAP, NDCG
- define precision, recall, F-measure and the precision-recall curve / interpolated precision;
- introduce MAP: average precision per query then mean across queries;
- define graded relevance and NDCG with DCG discount log2 and ideal IDCG;
- discuss pooling, Cranfield/TREC methodology and significance testing intuition;
- compute P@k, AP, MAP, DCG, NDCG on a worked ranking and compare systems.

### Ch 6 — Query Expansion and Relevance Feedback
- motivate vocabulary mismatch (synonymy/polysemy) and why users underspecify queries;
- formalise Rocchio feedback: move query vector toward relevant, away from non-relevant centroids;
- distinguish pseudo-relevance feedback vs explicit feedback and risks (query drift);
- introduce thesaurus / WordNet and embedding-based expansion, plus query-term reweighting;
- evaluate expansion via before/after MAP and guard against drift with experiments.

### Ch 7 — Link Analysis: PageRank and HITS
- explain why content alone is insufficient: authority from links on the web;
- model the web as directed graph and introduce random surfer and teleportation;
- derive PageRank iteration PR = alpha*M*PR + (1-alpha)/N and power method convergence;
- contrast PageRank (global) vs HITS (hubs/authorities, query-dependent) with Kleinberg iteration;
- address spam, topic drift, and efficient computation on web-scale graphs.

### Ch 8 — Learning to Rank and Neural IR
- frame ranking as supervised learning: pointwise, pairwise, listwise losses;
- build features (TF-IDF, BM25, PageRank, proximity) and train LambdaMART intuition;
- introduce neural IR: dense retrieval, bi-encoders, cross-encoders, and late interaction (ColBERT);
- cover embeddings, ANN search (HNSW/IVF), and the sparse-dense hybrid;
- evaluate neural rankers with NDCG/MAP and discuss data, bias, and efficiency trade-offs.

## TikZ Diagram Plan (2–3 per chapter, color where useful)

- **Ch1:** (1) IR pipeline crawl→index→query→rank→evaluate (blue→green→orange→violet→teal, legend); (2) DB vs IR vs mining Venn with query types (three fills); (3) Relevance judgment matrix docs×queries (green relevant, red non-rel, grey unjudged)
- **Ch2:** (1) Boolean sets Venn for AND/OR/NOT (blue/green/violet fills); (2) 2-D vector space docs+query with cosine angle (blue docs, red query, dashed projection); (3) Term-document matrix heatmap (blue intensity = weight)
- **Ch3:** (1) TF log curve and IDF decay 1/df (blue TF, orange IDF); (2) 3-doc TF-IDF bar chart per term (grouped bars blue/green/orange); (3) BM25 saturation vs TF curve (teal saturation, red linear for contrast)
- **Ch4:** (1) Inverted index table dictionary→postings with docIDs+freq+positions (blue dict, green postings); (2) SPIMI/BSBI block-merge diagram (orange blocks→violet merged index); (3) Gap+VB compression and skip pointer illustration (yellow gaps, teal skip arrows)
- **Ch5:** (1) Precision-recall curve with interpolated steps (blue curve, red interpolation, grey area); (2) MAP vs NDCG ranking comparison before/after (paired bars); (3) Pooling/TREC judgment funnel (yellow pool, green judged, violet evaluated)
- **Ch6:** (1) Rocchio vector move in 2-D (blue relevant centroid, red non-rel, green new query arrow); (2) Pseudo-RF loop query→top-k→extract→expand→rerank (circular fills); (3) Embedding expansion neighbours around query term (violet query, blue synonyms scatter)
- **Ch7:** (1) Web graph 5 nodes with PageRank scores sized by rank (blue nodes, orange edges, green scores); (2) Random surfer teleport diagram with alpha damping (teal surf, red teleport dashed); (3) HITS hub/auth bipartite iteration (blue hubs→green auths, iterative arrows)
- **Ch8:** (1) LTR feature pipeline query+doc→features→model→ranked list (blue→green→orange→violet); (2) Bi-encoder vs cross-encoder architecture (dual towers vs joint, blue/green/yellow); (3) ANN index dense search with HNSW graph and hybrid sparse+dense fusion (teal HNSW, orange sparse, violet fused)

## lstlisting Language Plan

- **Python (primary, all chapters):** tokenization, TF-IDF computation, cosine similarity, SPIMI-style indexer, positional intersection, precision/recall/MAP/NDCG calculation, Rocchio update, PageRank power iteration, pairwise/listwise toy ranker, bi-encoder cosine with numpy/sklearn, BM25 scoring. Shared lstset highlights (keyword blue!60!black, comment green!50!black, string orange!60!black).
- **Java (secondary, Ch 4 & Ch 7):** Lucene-style indexer snippet (Analyzer, IndexWriter) and web-graph PageRank skeleton to show production IR stacks bridging SC2207→SC4021; still uses listings with language=Java.
- Every code block uses `\begin{lstlisting}[language=Python]` or `[language=Java]` (never verbatim); caption + line numbers; xleftmargin 1em for small-screen.

## Exercise Themes (per chapter, 5 items)

- Ch1: information need vs query examples, IR vs DB vs mining table, Cranfield collection exercise, tokenization choices.
- Ch2: Boolean set operations by hand, cosine by hand on 2-D, term-doc matrix construction, ranked vs Boolean trade-off essay.
- Ch3: compute TF/IDF/TF-IDF, log vs raw TF comparison, length normalization effect, BM25 intuition calculation.
- Ch4: build postings for tiny corpus, intersect with skip pointers, positional phrase query, VB gap encode/decode.
- Ch5: P@k / recall / F1, draw PR curve + interpolated, compute AP/MAP, compute DCG/NDCG graded.
- Ch6: Rocchio numeric update, pseudo-RF term selection, drift analysis, embedding neighbour expansion.
- Ch7: PageRank 3-node by iteration, damping effect, HITS one iteration, spam resistance discussion.
- Ch8: LTR feature design, pairwise loss intuition, bi-encoder vs cross-encoder pros/cons, ANN recall/latency trade-off.

## Prereq Graph Note (how it builds on SC2001 + SC2207)

**SC2001 → SC4021:** reuses asymptotic analysis for index/query time (inverted index intersection O(p), skip optimization), hashing for dictionary, sorting/merging for BSBI/SPIMI, graph algorithms for PageRank/HITS power iteration and convergence analysis. Students without SC2001 would lack the vocabulary for `O(T log T)` indexing and `O(log N)` dictionary ops that SC4021 relies on.
**SC2207 → SC4021:** reuses relational vs inverted thinking, B-trees/hashing vs dictionary structures, SQL exact-match vs IR ranked retrieval, and normalization concepts repurposed as document-length normalization. SC4021 generalizes SC2207's exact lookup into best-match ranking.
**Graph:** `SC1003→SC1007→SC2001 ─┐` + `SC1007→SC2207 ─┤→ SC4021 → {SC3020/SC4002/SC4023}`; auxiliary `SC2000` supports evaluation statistics. SC4021 is MPE-leaf, not a prereq for other cores.

## 0→100 Flow Summary

Foundations (Ch 1: what IR is, pipeline, relevance) → Representation (Ch 2–3: Boolean→vector, TF-IDF weighting) → Efficiency (Ch 4: inverted index, compression, phrase search) → Judgment (Ch 5: precision/recall/MAP/NDCG, Cranfield) → Improvement (Ch 6: feedback & expansion) → Authority & Learning (Ch 7: PageRank/HITS, Ch 8: LTR & neural dense retrieval). No prior IR assumed; every formal notion (cosine, IDF, postings, AP, Rocchio, PageRank, bi-encoder) is introduced via intuition→definition→example→exercise before use.
