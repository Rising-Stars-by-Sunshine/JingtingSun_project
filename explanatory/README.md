# Part II — Machine Learning for Explanation  
*Mapping the literature on women/“她” and Republican-era China*

> This folder contains the **explanatory ML** pipeline that structures existing scholarship (OpenAlex) and motivates variables/hypotheses for the newspaper-headline study in **Part I**.

---

## 🚀 What this does
- Build **multilingual sentence embeddings** for titles/abstracts and **cluster** them.  
- Render a **2-D topic map** and a **pruned semantic kNN network** (communities + **bridging works**).  
- Summarize **publication trends** and **OpenAlex concepts**.  
- Compute **preliminary sentiment by cluster** on a subset (*hypothesis-generating only*).  
- Export **processed tables** for reproducibility (cluster labels/shares, concepts, years, sentiment).

> Figures/tables here are **descriptive scaffolding** for Part I — not direct evidence about newspapers.

---

## 📁 What’s in this folder

- Notebook / script  
  - `Explanation.ipynb`  
  - `explanation.py`
- Figures  
  - **Topic map:** [`literature on women.png`](./literature%20on%20women.png)  
  - **Semantic kNN (pruned):** [`knn network.png`](./knn%20network.png)  
  - **Publications by year:** [`publication by yr.png`](./publication%20by%20yr.png)  
  - **Top OpenAlex concepts:** [`Top OpenAlex Concepts.png`](./Top%20OpenAlex%20Concepts.png)  
  - **Mean sentiment by cluster (subset):** [`mean sentiment by cluster.png`](./mean%20sentiment%20by%20cluster.png)  
  - **Cluster shares (bar):** [`cluster shares.png`](./cluster%20shares.png)  
  - **Co-authorship (appendix):** [`Co author network.png`](./Co%20author%20network.png)  
  - **Within-sample citations (appendix):** [`with sample citation network.png`](./with%20sample%20citation%20network.png)  
  - **Word cloud (appendix):** [`Word clouds.png`](./Word%20clouds.png)
- Processed tables  
  - [`T_lit_topics_summary.csv`](./T_lit_topics_summary.csv) — `cluster_id, top_terms, share`  
  - [`T_openalex_top_concepts.csv`](./T_openalex_top_concepts.csv) — `concept, count`  
  - [`T_pub_counts_by_year.csv`](./T_pub_counts_by_year.csv) — `year, count`  
  - [`T_mean_sent_by_cluster_subset.csv`](./T_mean_sent_by_cluster_subset.csv) — `cluster_id, mean_sentiment, n_scored`
- Raw retrieval  
  - `openalex_lit_women_ta_republican.csv` *(in this folder)*


