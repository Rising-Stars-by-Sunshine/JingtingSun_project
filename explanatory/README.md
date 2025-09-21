# Part II — Machine Learning for Explanation  
*Mapping the literature on women/“她” and Republican-era China*

> This folder contains the **explanatory ML** pipeline that organizes existing scholarship (OpenAlex) and motivates variables/hypotheses for the newspaper-headline study in **Part I**. The outputs here are **descriptive scaffolding**—they guide design and hypothesis generation rather than serve as evidence about historical newspapers.

---

## 🚀 What this does (with details)

- **Multilingual embeddings + clustering.** We encode titles/abstracts with a multilingual sentence model and run **K-means** to obtain coarse **topic clusters**. Cluster labels are created with **within-cluster TF-IDF top terms**; shares are computed as document proportions.  
- **2-D topic map.** We project embeddings to 2D via **Truncated SVD** (default; UMAP optional) to visualize topical neighborhoods. Each point is a paper; color = cluster; text labels = centroid top terms.  
- **Semantic kNN network (pruned).** We build a **k-nearest-neighbors graph** on embeddings (default `k=10`), **prune** to the top ~10% strongest similarities, detect **communities** (modularity), and highlight **bridging works** (high betweenness).  
- **Field dynamics & concepts.** We summarize **publications by year** and the most frequent **OpenAlex concepts** to show growth and disciplinary footprint.  
- **Preliminary tone by cluster (subset).** For a small subset of English/Chinese abstracts, we compute **sentiment by cluster** (for hypothesis generation only; not used as evidence on newspapers).  
- **Processed tables for reproducibility.** We ship clean CSVs (clusters, concepts, yearly counts, subset sentiment) so figures can be regenerated or audited without re-running model inference.

---

## 📁 What’s in this folder

### Notebooks / scripts
- `Explanation.ipynb` — end-to-end notebook (retrieval → embedding → clustering → figures).  
- `explanation.py` — script version with the same defaults (CLI flags for `--k`, `--prune_q`, `--umap`).

### Figures (with quick reading guides)
- **Topic map:** [`literature on women.png`](./literature%20on%20women.png)  
  *What to read:* spatial proximity ≈ semantic similarity; colors = clusters; labels = centroid keywords. Use this to see the **three main regions** (e.g., education / mobilization / authorship-visibility).
- **Semantic kNN (pruned):** [`knn network.png`](./knn%20network.png)  
  *What to read:* densely connected **communities** = topical subfields; **bridge nodes** often link education ↔ mobilization; edge thickness ≈ similarity strength (after pruning).
- **Publications by year:** [`publication by yr.png`](./publication%20by%20yr.png)  
  *What to read:* long-run field growth; use inflection points to motivate phase splits in Part I.
- **Top OpenAlex concepts:** [`Top OpenAlex Concepts.png`](./Top%20OpenAlex%20Concepts.png)  
  *What to read:* interdisciplinary footprint (linguistics/history/sociology/politics); use to justify mixed methods.
- **Mean sentiment by cluster (subset):** [`mean sentiment by cluster.png`](./mean%20sentiment%20by%20cluster.png)  
  *What to read:* **directional cues** (e.g., education clusters more positive; mobilization more heterogeneous). Treat as hypothesis-generating only.
- **Cluster shares (bar):** [`cluster shares.png`](./cluster%20shares.png)  
  *What to read:* relative prevalence of topical regions; aligns with Table `T_lit_topics_summary.csv`.
- **Appendix visuals:** co-authorship [`Co author network.png`](./Co%20author%20network.png), within-sample citations [`with sample citation network.png`](./with%20sample%20citation%20network.png), word cloud [`Word clouds.png`](./Word%20clouds.png).

### Processed tables (schemas)
- [`T_lit_topics_summary.csv`](./T_lit_topics_summary.csv)  
  **Columns:** `cluster_id (int)`, `top_terms (str; comma-separated)`, `share (float in [0,1])`.  
  **Use:** caption/labels for Fig. 1；report cluster prevalence in text.
- [`T_openalex_top_concepts.csv`](./T_openalex_top_concepts.csv)  
  **Columns:** `concept (str)`, `count (int)`.  
  **Use:** Fig. 4 bars; discuss interdisciplinarity.
- [`T_pub_counts_by_year.csv`](./T_pub_counts_by_year.csv)  
  **Columns:** `year (int)`, `count (int)`.  
  **Use:** Fig. 3; motivate phase split (e.g., pre-1931 vs. 1931–1937).
- [`T_mean_sent_by_cluster_subset.csv`](./T_mean_sent_by_cluster_subset.csv)  
  **Columns:** `cluster_id (int)`, `mean_sentiment (float −1..1 or 0..1)`, `n_scored (int)`.  
  **Use:** Fig. 5; **hypothesis cues** only (not used for newspaper claims).

### Raw retrieval
- `openalex_lit_women_ta_republican.csv` *(in this folder)* — titles, abstracts, concepts, authors, year, venue, etc.

---

## 🔧 Key parameters & defaults (tunable)
- **Embeddings:** `paraphrase-multilingual-MiniLM-L12-v2` (Sentence-Transformers).  
- **Clustering:** K-means, default `K` by silhouette (`--k` to override).  
- **Topic labels:** top TF-IDF terms within cluster (stopwords removed; bigrams enabled).  
- **2-D map:** Truncated SVD (default); `--umap` to switch to UMAP (`n_neighbors=30`, `min_dist=0.1`).  
- **kNN graph:** `k=10` neighbors; **prune** strongest edges to top **10%** by similarity (`--prune_q` to change).  
- **Sentiment (subset):** multilingual model on abstracts; **for direction only**.

---

## 🧭 How to use these outputs for Part I
- Use **cluster labels/shares** to define **topic flags** in headlines (e.g., education vs. mobilization) and to justify **interactions** with `explicit-“她”` and **phase** (pre-1931 vs. 1931–1937).  
- Use **bridging works** from the kNN graph to argue for **spillover** between education and mobilization frames.  
- Use **yearly counts** to motivate a **phase split** and to check whether research attention aligns with historical turning points.  
- Treat **subset sentiment** as **hypothesis-generating**; validate on headlines separately (Part I).

---

## ⚠️ Scope & caveats
- These visuals/tables summarize **secondary scholarship** (OpenAlex titles/abstracts), not newspapers.  
- Cluster shapes and networks are **sensitive** to embedding family, `K`, `k`, and pruning quantile; defaults are reported and can be changed via CLI flags.  
- OpenAlex concepts are **noisy proxies** for disciplines; use as context, not labels for headlines.


