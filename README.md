# Women and the Pronoun “Ta” in Republican-Era Newspapers (1911–1937)

## Abstract
This project studies how Republican-era newspapers (1911–1937) framed women when the newly invented feminine pronoun “Ta” appeared explicitly in headlines, and whether that tone shifted with wartime mobilization and the expansion of new education and female creators. Using ~20,000 title-level records exported from the Shanghai Library National Periodical Index (NPI), we run sentiment analysis (SnowNLP), topic clustering (TF-IDF with KMeans), and a fixed-effects logistic model on the subset of headlines that explicitly use Ta. As outlined below and in **Figure 1**, the design maps to the **AI Triad** (Data, Algorithms, Computing power) and yields both descriptive trends and controlled estimates.

---

## System configuration (local + cloud)
- **Local:** Python ≥ 3.10, Jupyter Notebook
- **Libraries:** `pandas`, `matplotlib`, `scikit-learn`, `statsmodels`, `snownlp`
- **Cloud:** Google Colab tested; repo includes `requirements.txt` for portability

---

## Dataset note (what the table contains)
This dataset is a structured export derived from the **Shanghai Library’s National Periodical Index (NPI)**. We collected all records dated **1911–1937** for which the index indicates the character “她” appears either in the title or within the article text, and we keep **bibliographic title-level metadata only** (no full text). Fields are cleaned and normalized (dates in **YYYY-MM-DD**, provenance preserved). The table contains about **20,000 rows**, enabling reproducible EDA and sentiment analyses that compare the overall corpus of titles with the subset explicitly mentioning “她” in the headline.

---

## Research design and AI-Triad connections
We refer to **Figure 1** when explaining the design.

- **Data**  
  Structured NPI export (1911–1937), title-level metadata only; normalized dates and preserved provenance; comparisons between the full title corpus and the explicit-Ta subset.

- **Algorithms**  
  1) **Sentiment:** SnowNLP probability → positive / neutral / negative with a small neutral band.  
  2) **Topics:** character 2–3-gram **TF-IDF** + **KMeans** to surface themes (e.g., war mobilization, schooling, creators) and compare mean sentiment by theme.  
  3) **Regression:** **fixed-effects logistic** on the **explicit-Ta subset** (title contains Ta), holding newspaper and year constant, to assess shifts across historical phases and topic flags.

- **Computing power**  
  Dataset is modest; CPU suffices for all analyses. GPU is optional for transformer-based robustness checks.

mermaid flowchart TD A[Research question] --> B[Framing when Ta appears in headline] B --> C[Sentiment with SnowNLP] B --> D[Topics with TF-IDF and KMeans] B --> E[Logit on explicit-Ta subset (FE)] C --> F[Year and phase shares] D --> F[Cluster labels and mean sentiment] F --> G[Findings: descriptive and controlled]

*Figure 1. Conceptual flowchart of the research design. Source: authors’ visualization (Mermaid) based on Shanghai Library National Periodical Index, 1911–1937.*


## FAIR & CARE Principles

### FAIR
- **Findable**: Public GitHub repo with a clear directory structure and dataset metadata.
- **Accessible**: Open formats (CSV/XLSX), versioned code and data subset; instructions for local and Colab runs.
- **Interoperable**: Standardized fields (e.g., date in `YYYY-MM-DD`), UTF-8 text; analysis in common Python libraries.
- **Reusable**: Data dictionary, preprocessing steps, and notebooks enable replication and extension.

### CARE
- **Collective Benefit**: Results support research on gender representation and informed media practices.
- **Authority to Control**: Provenance from the Shanghai Library NPI is preserved and cited; we acknowledge custodianship.
- **Responsibility**: Interpretations contextualize period-specific biases; we avoid sensationalizing historical discourse.
- **Ethics**: We present findings as historical descriptions, encourage critical reading, and document limitations of title-only metadata.
