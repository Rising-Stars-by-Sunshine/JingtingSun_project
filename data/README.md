# Dataset

**File:** `Newspapers_merged_sorted.xlsx`  
**Source:** 上海图书馆《全国报刊索引》 (Shanghai Library – National Periodical Index, NPI)

**Description、.**  
This dataset is a structured export derived from the Shanghai Library’s National Periodical Index (NPI). We collected all records dated **1911–1937** for which the index indicates the **character “她” appears either in the title or within the article text**, and we keep only the bibliographic **title-level metadata** (no full text). Fields are cleaned and normalized: dates are converted to `YYYY-MM-DD`, and the original file provenance is preserved. The table contains **~20k rows**, enabling reproducible EDA and sentiment analyses that compare the overall corpus of titles with the subset explicitly mentioning “她”. Known caveats include OCR/indexing noise, incomplete author/library fields, and potential duplicates across issues. Please refer to the root README for FAIR/CARE notes; reuse must respect the Shanghai Library/NPI access terms—this repository redistributes **derived metadata only** for academic purposes.

## Data Dictionary
| column           | type   | description                                                  |
|---               |---     |---                                                          |
| Title            | string | Article title                                               |
| Author           | string | Author (if available)                                       |
| Newspaper Title  | string | Newspaper name                                              |
| Time             | string | Issue date in `YYYY-MM-DD`                                  |
| year             | int    | Year extracted from `Time`                                  |
| 藏馆             | string | Holding library (if any)                                    |
| 馆藏索取号        | string | Call number (if any)                                        |
| 分类号            | string | Classification (if any)                                     |
| SourceFile       | string | Relative path to the source TXT used during merging         |
| FileNumber       | int    | Index extracted from filename (expected range **1–404**)    |
| RowInFile        | int    | Order of the record within its original TXT                 |

- ## Replicability & Reuse

**Replicability.**  
- **Input.** Export from the Shanghai Library **National Periodical Index (NPI)** filtered to **1911–1937** records where the character **“她”** occurs **in the title or within the article**; only title-level bibliographic metadata are used.  
- **Deterministic merge.** Raw TXT exports are merged into `Newspapers_merged_sorted.xlsx`; dates are normalized to `YYYY-MM-DD`, and provenance is preserved via `SourceFile`, `FileNumber (1–404)`, and `RowInFile` so ordering can be reproduced.  
- **Environment.** The notebooks/scripts in `code/` with `requirements.txt` reproduce cleaning and figures; outputs are deterministic (no randomness).

**Quality notes.**  
- The source is an **index database (not OCR)**, so **missingness is minimal**; some library/author fields may be blank in the original index and are kept as-is.  
- **Coverage & query scope.** The filter is the single character **“她”**; earlier or alternative forms of female reference (e.g., “伊”, “女子”, etc.) are **out of scope**, which may lead to omissions. Index coverage can also vary by newspaper and year.  
- **Duplicates & versions.** Identical titles can appear across issues/reprints; we keep all records and only remove **exact duplicates** on `(Title, Time, Newspaper Title)`.  
- **Date normalization.** Nonstandard source formats are standardized to `YYYY-MM-DD`; partially parseable cases retain original information in the table.

**Reuse.**  
- This repository redistributes **derived bibliographic metadata only** (no full texts) for **academic / non-commercial** use; please comply with **Shanghai Library/NPI** terms and **cite** both NPI and this repository.  
- Keep provenance fields when sharing derivatives; do not use the dataset for profiling or high-stakes decisions, and state the query scope and historical-language limitations when reporting results.


