# Part III — Machine Learning for Prediction

> **Task**: Predict whether a newspaper headline **explicitly** contains the feminine pronoun **“她”** under strict **leakage control**.  
> **Data size**: n = **20,177** headlines; **positive share = 0.9218%**.

---

## TL;DR

- **Leakage control**: remove “她/她们” *before* feature extraction so models must rely on context/outlet/period.  
- **Features**: char **2–3-gram TF-IDF** on the **masked title** + **One-Hot** for `Newspaper Title` + **One-Hot** for **year-bin** (≤1919, 1920–24, 1925–29, 1930–33, 1934–37, ≥1938).  
- **Split**: **GroupShuffleSplit by year (80/20)**.  
- **Models (≥3)**: Logistic Regression (saga), LinearSVC, Complement Naive Bayes (CNB).  
- **Metrics**: Accuracy, **Macro-F1**, ROC-AUC, **PR (AP/AUPRC)**.  
- **Headline results**: **CNB Macro-F1 = 0.606 (best)**; **LinearSVC ROC-AUC = 0.876 (best)**.

---

## Repository


