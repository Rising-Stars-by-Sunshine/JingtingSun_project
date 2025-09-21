# Republican-Era Newspapers (1911–1937) — Title-Level Dataset & Processed Outputs

**Source:** 上海图书馆《全国报刊索引》 (Shanghai Library – National Periodical Index, **NPI**)  
**Files:** `Newspapers_merged_sorted.xlsx` (raw title-level export) • `data/processed/titles_sentiment.csv` (processed, public)  

> **Scope disclaimer.** This repository redistributes **derived, title-level metadata only** (no full texts). All analyses speak to **headline framing** and must **not** be extrapolated to full-article arguments. Please respect NPI access terms.

---

## 📦 Contents

- `Newspapers_merged_sorted.xlsx` — merged and normalized title-level export (raw).
- `data/processed/titles_sentiment.csv` — **core processed table** released for reproducibility (schema below).
- `data/validation/` *(optional)* — human-coded validation set (e.g., `headlines_gold.tsv`) for SnowNLP threshold calibration and agreement checks.
- `part1/` — code to clean, score sentiment, create variables, and reproduce Part I figures/tables.
- `explanatory/` — Part II (literature mapping) assets; see its own `README.md`.

---

## 📘 Dataset Overview

This dataset is a structured export derived from the Shanghai Library’s National Periodical Index (NPI). We collected records dated **1911–1937** for which the index indicates that the character **“她”** appears **in the title** or **within the article text**. We retain only **bibliographic title-level metadata**. Dates are normalized to `YYYY-MM-DD`, and provenance is preserved.

The table contains approximately **20,000 rows** and supports reproducible exploratory analysis and title-level sentiment scoring that compare (i) the overall corpus of titles with (ii) the subset explicitly mentioning **“她”** in the headline.

> **Known caveats:** indexing noise, occasional missing library/author fields, and possible duplicates across issues. See **Quality notes** below.

---

## 🧭 Data Dictionary (`Newspapers_merged_sorted.xlsx`)

| column          | type   | description                                                   |
|-----------------|--------|---------------------------------------------------------------|
| `Title`         | string | Article title (headline)                                      |
| `Author`        | string | Author (if available)                                         |
| `Newspaper Title` | string | Newspaper/outlet name                                       |
| `Time`          | string | Issue date in `YYYY-MM-DD`                                    |
| `year`          | int    | Year extracted from `Time`                                    |
| `藏馆`            | string | Holding library (if any)                                     |
| `馆藏索取号`        | string | Call number (if any)                                        |
| `分类号`            | string | Classification (if any)                                     |
| `SourceFile`    | string | Relative path to the source TXT used during merging           |
| `FileNumber`    | int    | Index extracted from filename (expected range **1–404**)      |
| `RowInFile`     | int    | Order of the record within its original TXT                   |

---

## 🧪 Processed Table (public): `data/processed/titles_sentiment.csv`

This is the **release artifact** used by the paper and figures. It is title-level only and contains derived variables aligned with **Table 1** in the manuscript.

| field               | type       | description                                                                 |
|---------------------|------------|-----------------------------------------------------------------------------|
| `paper_id`          | string     | Newspaper/outlet id (from `Newspaper Title`/`SourceFile`)                  |
| `date`              | date       | `YYYY-MM-DD`                                                                |
| `year`              | int        | extracted year                                                              |
| `phase_1931plus`    | {0,1}      | 1 if 1931–1937                                                              |
| `explicit_she_title`| {0,1}      | 1 if the **title** contains “她”                                            |
| `women_implicit`    | {0,1}      | women referenced without “她” (e.g., 妇女/女子/女工), excluding explicit-she titles |
| `education_topic`   | {0,1}      | education lexicon match (教育/学校/女校/师范/学生/课程/…)                     |
| `editorial`         | {0,1}      | editorial/opinion page (heuristic: tags/keywords)                          |
| `female_creator`    | {0,1}      | creator appears female (conservative cues; ambiguous=0)                     |
| `headline_len`      | int        | character count of the title                                               |
| `sentiment_score`   | float      | SnowNLP score in [0,1]                                                     |
| `sentiment_label`   | categorical| Positive (≥0.55), Neutral (0.45–0.55), Negative (≤0.45); **calibrated if validation provided** |
| `cluster_id`        | int / NA   | optional unsupervised topic id (if available)                              |

> **Reusability.** This single table is sufficient to regenerate our descriptive figures and regression tables without any full text.

---

## 🔁 Replicability

**Inputs.**
- NPI export filtered to **1911–1937** with query **“她”** in title/body; we only use **title-level** fields.

**Deterministic merge.**
- Raw TXT exports → `Newspapers_merged_sorted.xlsx`; dates normalized; provenance via `SourceFile`, `FileNumber (1–404)`, `RowInFile`.

**Environment.**
- See `requirements_part1.txt` and scripts in `part1/code/`.

**One-line run (example).**
```bash
# from repo root
pip install -r requirements_part1.txt
bash part1/run_part1.sh

