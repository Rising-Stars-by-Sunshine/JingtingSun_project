Part II — Machine Learning for Explanation

Mapping the literature on women/“她” and Republican-era China

This folder documents the explanatory ML pipeline used to structure the existing scholarship (OpenAlex) and to motivate variables/hypotheses for the newspaper headline study in Part I.

What this does

Build multilingual sentence embeddings for titles/abstracts and cluster them.

Render a 2-D topic map and a pruned semantic kNN network (communities + bridging works).

Summarize publication trends and OpenAlex concepts.

Compute preliminary sentiment by cluster on a subset (hypothesis-generating only).

Export processed tables for reproducibility (cluster labels/shares, concepts, years, sentiment).

These figures/tables are descriptive scaffolding for Part I (they are not evidence about newspapers).

Folder layout (relative to repo root)
explanatory/
  README.md                # this file
  figs/                    # figures produced by the pipeline
data/
  raw/openalex_lit_women_ta_republican.csv
  processed/
    T_lit_topics_summary.csv
    T_openalex_top_concepts.csv
    T_pub_counts_by_year.csv
    T_mean_sent_by_cluster_subset.csv
code/
  01_embed_and_cluster.py
  02_topic_map_svd.py
  03_semantic_knn_network.py
  04_field_dynamics_and_concepts.py
  05_sentiment_subset.py


If your filenames differ, keep the structure but adjust names in the scripts.

Quick start

Environment

python -V     # >= 3.10 recommended
pip install -r requirements.txt


Minimal requirements.txt:

pandas>=2.0
numpy>=1.24
scikit-learn>=1.3
matplotlib>=3.7
networkx>=3.1
tqdm>=4.66
requests>=2.31
sentence-transformers>=2.2
umap-learn>=0.5   # optional; we default to SVD so this is not required


Data
Place the OpenAlex retrieval at:

data/raw/openalex_lit_women_ta_republican.csv


(Contains titles, abstracts, concepts, authors, year, etc.)

Run the pipeline

python code/01_embed_and_cluster.py
python code/02_topic_map_svd.py
python code/03_semantic_knn_network.py
python code/04_field_dynamics_and_concepts.py
python code/05_sentiment_subset.py

Outputs
Figures (saved to explanatory/figs/)

Fig. 1 fig1_topic_map_svd.png — Topic map (SVD-2D; colors = clusters; centroid labels = top TF-IDF terms)

Fig. 2 fig2_semantic_knn_pruned.png — Semantic kNN (pruned to top ~10% similarities; communities + high-betweenness “bridges”)

Fig. 3 fig3_publications_by_year.png — Publications by year (optionally with 3-year moving average)

Fig. 4 fig4_top_openalex_concepts.png — Most frequent OpenAlex concepts

Fig. 5 fig5_mean_sentiment_by_cluster.png — Preliminary sentiment by cluster (subset)

Processed tables (saved to data/processed/)

T_lit_topics_summary.csv — cluster_id, top_terms, share

T_openalex_top_concepts.csv — concept, count

T_pub_counts_by_year.csv — year, count

T_mean_sent_by_cluster_subset.csv — cluster_id, mean_sentiment, n_scored

These are the files you can cite/ship for reproducibility in the paper.

Parameters (defaults)

Embeddings: paraphrase-multilingual-MiniLM-L12-v2 (Sentence-Transformers)

Clustering: K-means with K chosen by silhouette (override via --k)

Topic labels: top TF-IDF terms within cluster (stopwords removed)

2-D map: Truncated SVD (UMAP optional)

Semantic graph: kNN on embeddings (k=10), prune edges to top 10% similarities (--prune_q to change), communities by modularity; label top betweenness nodes

Sentiment: multilingual model on a subset (scores in [−1,1]); descriptive only

How this informs Part I

Fig. 1 + Table 1 (from T_lit_topics_summary.csv) show three stable regions—education, crisis mobilization, authorship/visibility—which directly motivate headline-level flags (education page, editorial page, female creator, explicit-“她”).

Fig. 2 identifies bridging works linking education and mobilization → motivates a phase split (1911–1930 vs. 1931–1937) and interactions such as explicit-“她” × education / explicit-“她” × post-1931.

Figs. 3–4 provide context (field growth; interdisciplinary footprint) that justifies mirroring those domains in the headline taxonomy.

Fig. 5 offers hypothesis cues about tone differences (education more positive; mobilization more heterogeneous), to be validated on headlines.

Limitations

Scope: This maps secondary scholarship (OpenAlex titles/abstracts), not newspapers; use to design & contextualize Part I, not to infer historical sentiment.

Model sensitivity: Clusters/graphs vary with the embedding family, K, k, and pruning quantile. We report parameters and include hooks for sensitivity checks.

Concept noise: OpenAlex concepts are noisy disciplinary proxies—contextual only.

Sentiment subset: Preliminary, model-based, trained on modern language; treat as hypothesis-generating and validate with manual coding on headlines.

Citation

Women and the Pronoun “她” in Republican-Era Newspapers (1911–1937): Part II — Machine Learning for Explanation.
Code and processed data available in this repository (see explanatory/ and data/processed/).

Please additionally cite OpenAlex and the Sentence-Transformers model you use.
