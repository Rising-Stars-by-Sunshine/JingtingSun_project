# Part III — Machine Learning for Prediction

> **Task**: Predict whether a newspaper headline **explicitly** contains the feminine pronoun **“她”** under strict **leakage control**.  
> **Data size**: n = **20,177** headlines; **positive share = 0.9218%**.

---

## Methods

- **Leakage control**: remove “她/她们” *before* feature extraction so models must rely on context/outlet/period.  
- **Features**: char **2–3-gram TF-IDF** on the **masked title** + **One-Hot** for `Newspaper Title` + **One-Hot** for **year-bin** (≤1919, 1920–24, 1925–29, 1930–33, 1934–37, ≥1938).  
- **Split**: **GroupShuffleSplit by year (80/20)**.  
- **Models (≥3)**: Logistic Regression (saga), LinearSVC, Complement Naive Bayes (CNB).  
- **Metrics**: Accuracy, **Macro-F1**, ROC-AUC, **PR (AP/AUPRC)**.  
- **Headline results**: **CNB Macro-F1 = 0.606 (best)**; **LinearSVC ROC-AUC = 0.876 (best)**.

---

## Repository

This folder currently contains the notebook and the exported figures used in the Part III write-up. Below is a detailed inventory explaining what each file is, how it is produced, where it appears in the report, and how to cite it.

| Path / File | What it is | How it’s produced | Used in the write-up | Cite as |
|---|---|---|---|---|
| `prediction.ipynb` | Main notebook: data loading, leakage control (mask “她/她们”), feature engineering (TF-IDF + OHE), year-grouped split, model training/evaluation, plotting/export | Run the notebook (Run All or by section). Make sure to execute the cells that save figures. | End-to-end reproduction | “Source: this study (notebook: `prediction.ipynb`).” |
| `ConfusionMatrix(ComplementNB).png` | Confusion matrix for **Complement Naive Bayes** on the held-out test split | Saved by the evaluation/plotting cells in the notebook | **Figure X** (Confusion Matrix — ComplementNB) | “Figure X. Confusion matrix — ComplementNB. Source: this study; file: `ConfusionMatrix(ComplementNB).png`.” |
| `ConfusionMatrix(LinearSVC).png` | Confusion matrix for **LinearSVC** on the held-out test split | Saved by the notebook | **Figure X** (Confusion Matrix — LinearSVC) | “Figure X. Confusion matrix — LinearSVC. Source: this study; file: `ConfusionMatrix(LinearSVC).png`.” |
| `confusion matrix(LinearRegression).png` | Confusion matrix for **Logistic Regression (saga)** on the held-out test split | Saved by the notebook | **Figure X** (Confusion Matrix — Logistic Regression) | “Figure X. Confusion matrix — Logistic Regression (saga). Source: this study; file: `confusion matrix(LinearRegression).png`.” |
| `ROC.png` | ROC curves for the three models (includes AUC) | Saved by the notebook | **Figure X** (ROC curves) | “Figure X. ROC curves (3 models). Source: this study; file: `ROC.png`.” |
| `Precision recall.png` | Precision–Recall curves for the three models (legend shows AP/AUPRC) | Saved by the notebook | **Figure X** (PR curves) | “Figure X. Precision–Recall curves with AP. Source: this study; file: `Precision recall.png`.” |
| `README.md` | This documentation file | Edited manually | Repo landing page | — |

### File-name tips

- A few files contain **spaces** and **parentheses** (e.g., `confusion matrix(LinearRegression).png`, `Precision recall.png`).  
  When linking in Markdown, use **URL encoding**: space → `%20`, `(` → `%28`, `)` → `%29`. Examples:  
  - `![CM LogReg](confusion%20matrix%28LinearRegression%29.png)`  
  - `![PR](Precision%20recall.png)`
- Prefer simpler names if you want to avoid URL encoding (e.g., rename to `confusion_matrix_logreg.png`, `precision_recall.png`) and update links accordingly.

### How to regenerate / refresh the figures

1. Open `prediction.ipynb`.  
2. Run the sections through **training, evaluation, and plotting**.  
3. Confirm that the “save figures” cells write to the repo root (or to `figs/` if you reorganize).  
4. If you change filenames or paths, update links in `README.md` and captions in your paper.

### Optional, cleaner structure (recommended)

If you want a tidier layout, move data and figures into subfolders and update paths in the README and notebook:

