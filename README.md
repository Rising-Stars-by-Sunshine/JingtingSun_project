# Women and the Pronoun “她” in Republican-Era Newspapers (1911–1937)

## Abstract
This project studies how Republican-era newspapers (1911–1937) framed women when the newly invented feminine pronoun “她” appeared explicitly in headlines, and whether that tone shifted with wartime mobilization and the expansion of new education and female creators. Using ~20,000 title-level bibliographic records exported from the Shanghai Library’s National Periodical Index (NPI), we conduct sentiment analysis (SnowNLP), topic clustering (TF-IDF + KMeans), and fixed-effects logistic regression on the subset of headlines that explicitly use “她”. The aim is to provide a reproducible, quantitative account of gendered representation in historical media.

---

## System configuration (local + cloud)
- **Local**: Python ≥ 3.10, Jupyter
- **Key libraries**: `pandas`, `matplotlib`, `scikit-learn`, `statsmodels`, `snownlp`
- **Cloud**: Google Colab tested; repo includes `requirements.txt` for portability

---

## Research design and AI-Triad connections
Our research design has three analytic layers that map directly to the **AI Triad**—**Data, Algorithms, Computing power**—and are visualized in **Figure 1**.

- **Data**  
  Structured export from the **Shanghai Library NPI**. Records dated 1911–1937 where the index flags that “她” appears in the title or in the article text; we retain **title-level bibliographic metadata only** (no full text). Fields are cleaned and normalized (dates in YYYY-MM-DD; provenance preserved). The table has ~20k rows, enabling comparisons between the **overall corpus of titles** and the **subset with explicit “她” in the headline**.

- **Algorithms**  
  1) **Sentiment**: SnowNLP probability → positive / neutral / negative with a small neutral band.  
  2) **Topics**: character 2–3-gram **TF-IDF** + **KMeans** to surface themes (e.g., war mobilization, schooling, creators) and compare their average sentiment.  
  3) **Regression**: **fixed-effects logit** on the **she=1** subset to assess whether sentiment differs across historical phases and topics while holding newspaper and year constant.

- **Computing power**  
  Corpus size is modest; all analyses run efficiently on CPU. GPU is optional for any transformer-based robustness checks.

---

## Conceptual flowchart (Figure 1)

```mermaid
flowchart TD
    A[Research question] --> B[Women framing when she appears in headline]
    B --> C[Sentiment analysis with SnowNLP]
    B --> D[Topic clustering with TF-IDF and KMeans]
    B --> E[Fixed-effects logit on she subset]
    C --> F[Year and phase shares]
    D --> F[Cluster labels and mean sentiment]
    F --> G[Findings: trends, topic differences, controlled effects]
  Figure 1. Conceptual flowchart linking the core research question to the three analytic layers (sentiment, topics, regression) and showing how these produce descriptive and controlled findings. We refer to Figure 1 in the text above when explaining the research design and AI-Triad connections.

## FAIR & CARE principal

- **FAIR ** – Findable: Public GitHub repo with clear directory structure and dataset metadata.

- **FAIR ** – Accessible: Open formats (CSV/XLSX), versioned code and data subset; instructions for local and Colab runs.

- **FAIR ** – Interoperable: Standardized fields (e.g., date in YYYY-MM-DD), UTF-8 text; analysis in common Python libraries.

- **FAIR ** – Reusable: Data dictionary, preprocessing steps, and notebooks enable replication and extension.

- **CARE ** – Collective Benefit: Results support research on gender representation and informed media practices.

- **CARE ** – Authority to Control: Provenance from the Shanghai Library NPI is preserved and cited; we acknowledge custodianship.

- **CARE ** – Responsibility: Interpretations contextualize period-specific biases; we avoid sensationalizing historical discourse.

- **CARE ** – Ethics: We present findings as historical descriptions, encourage critical reading, and document limitations of title-only metadata.

