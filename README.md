# Women and the Pronoun "她" in Republican-Era Newspapers (1911–1937)

## Abstract
This project investigates how Republican-era newspapers (1911–1937) framed women when the newly invented feminine pronoun “她” appeared explicitly in headlines, and whether the tone of this representation shifted under wartime mobilization and the expansion of new education and female creators. The dataset consists of approximately 20,000 bibliographic records exported from the Shanghai Library’s National Periodical Index, cleaned and normalized for reproducibility. Using sentiment analysis (SnowNLP), topic clustering (TF-IDF + KMeans), and logistic regression with newspaper and year fixed effects, the study aims to uncover whether linguistic innovation reflected broader changes in women’s public representation during periods of social and political shock.  

---

## System Configuration
- **Local environment**: Python 3.10+, Jupyter Notebook  
- **Required libraries**: `pandas`, `matplotlib`, `scikit-learn`, `statsmodels`, `snownlp`  
- **Cloud environment**: Google Colab tested; repository designed for portability and reproducibility with `requirements.txt`  

---

## Research Design Flowchart

```mermaid
flowchart TD
    A[Core Research Question] --> B[Framing of women with Ta in headlines]
    B --> C[Sentiment analysis: SnowNLP<br>Positive / Neutral / Negative]
    B --> D[Topic clustering: TF-IDF + KMeans<br>Wartime, Education, Creators]
    B --> E[Regression analysis<br>Logit on she=1 subset with FE + clustered SE]
    C --> F[Descriptive statistics<br>Shares by year and historical phase]
    D --> F
    F --> G[Results: Descriptive trends, Topic differences, Regression evidence]
