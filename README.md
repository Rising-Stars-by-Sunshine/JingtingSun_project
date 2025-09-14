Women and the Pronoun Ta in Republican-Era Newspapers (1911–1937)
Abstract

This project studies how Republican-era newspapers (1911–1937) framed women when the newly invented feminine pronoun Ta appeared explicitly in headlines, and whether that tone shifted with wartime mobilization and the expansion of new education and female creators. Using ~20,000 title-level records exported from the Shanghai Library National Periodical Index (NPI), we run sentiment analysis (SnowNLP), topic clustering (TF-IDF with KMeans), and a fixed-effects logistic model on the subset of headlines that explicitly use Ta. As noted below and in Figure 1, the design maps cleanly to the AI Triad (Data, Algorithms, Computing power) and yields both descriptive trends and controlled estimates.

System configuration (local + cloud)

Local: Python ≥ 3.10, Jupyter

Libraries: pandas, matplotlib, scikit-learn, statsmodels, snownlp

Cloud: Google Colab tested; requirements.txt provided

Research design and AI-Triad connections

We refer to Figure 1 when explaining the design.

Data — Structured export from Shanghai Library NPI (1911–1937). Records where the index flags Ta in the title or article text. We keep title-level metadata only (no full text). Dates normalized to YYYY-MM-DD; provenance preserved. About 20k rows support comparisons between the overall corpus and the subset with explicit Ta in the headline.

Algorithms —

Sentiment with SnowNLP (probability → positive / neutral / negative, with a small neutral band).

Topics via character 2–3-gram TF-IDF and KMeans to surface themes (war mobilization, schooling, creators) and compare mean sentiment by theme.

Regression using fixed-effects logistic on the she=1 subset (explicit Ta in title), controlling for newspaper and year, to assess differences across phases and topics.

Computing power — Dataset is modest; CPU suffices. GPU only if testing transformer robustness.

<a id="fig1"></a>

Conceptual flowchart (Figure 1)
flowchart TD
  A[Research question] --> B[Framing when Ta appears in headline]
  B --> C[Sentiment with SnowNLP]
  B --> D[Topics with TF-IDF and KMeans]
  B --> E[Logit on she subset with fixed effects]
  C --> F[Year and phase shares]
  D --> F[Cluster labels and mean sentiment]
  F --> G[Descriptive and controlled findings]


Figure 1. Conceptual flowchart linking the core research question to three analytic layers (sentiment, topics, regression) and showing how these produce both descriptive trends and controlled estimates. We cite Figure 1 in the sections above to explain the research design and its AI-Triad connections. In text, you can write: “see Figure 1
”.

Brief note on FAIR & CARE principles (how they apply here)

FAIR — Findable: Public GitHub repository with clear directories and dataset metadata.

FAIR — Accessible: Open formats (CSV/XLSX), versioned data subset and code; instructions for local and Colab runs.

FAIR — Interoperable: Standardized fields (e.g., date in YYYY-MM-DD), UTF-8 encoding; analysis with widely used Python libraries.

FAIR — Reusable: Data dictionary, preprocessing steps, and notebooks provided to enable replication and extension.

CARE — Collective Benefit: Findings inform research on gender representation and better media practices.

CARE — Authority to Control: Provenance from the Shanghai Library NPI is preserved and cited; custodianship acknowledged.

CARE — Responsibility: Interpretations situate results in period context; we avoid sensationalizing historical discourse.

CARE — Ethics: We present results as historical descriptions, encourage critical reading, and document limits of title-only metadata.
