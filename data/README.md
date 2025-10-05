# data/ README

## Purpose (≈130 words)
These datasets support a headline-level study of whether the **1937** full-scale war shifted the *tone* of newspaper titles that explicitly use the feminine pronoun **“她.”** The unit of analysis is the **headline title** (no article body). We provide two cleaned, chronologically sorted title tables (1911–1937 and 1938–1949) plus a derived table with sentiment outputs used to build the analysis panel for DiD and event-study models with newspaper and year fixed effects. Where upstream sources have access restrictions, we follow a “derived-data only” policy and share normalized titles/metadata and model outputs rather than raw scans. These files are consumed directly by notebooks in `code/explanation/` (sentiment calibration, figures) and `code/prediction/` (DiD/event-study), enabling reproducibility without redistributing proprietary content.

## Origin and Source
Titles/metadata come from **Republican-era newspaper indexes**, primarily the Shanghai Library National Periodical Index (1911–1949). Sentiment variables are **derived** using calibrated classifiers (e.g., SnowNLP / SentProp) via our preprocessing scripts. Please respect the original repositories’ terms; raw scans are **not** included.

---

## Dataset overview
| File | Years | What it contains | How it was produced |
|---|---|---|---|
| `1911-1937_merged_sorted.xlsx` | 1911–1937 | Cleaned, de-duplicated titles + standardized newspaper names; basic flags | Merged index exports → Unicode/punctuation normalization → newspaper name canonicalization → drop exact/near-duplicates → compute flags → chronological sort |
| `1938-1949_merged_sorted.xlsx` | 1938–1949 | Same schema as above for the late period | Same pipeline; cut at 1938 to align with 1937 shock windows |
| `final_sentiment_sentprop.xlsx` | 1911–1949 | Titles joined with sentiment scores/classes and analysis helpers | Left-join early & late tables → run SnowNLP/SentProp → calibrate thresholds → map to classes; add modeling variables (`post1937`, interactions) |

> Paths in notebooks assume these live in `data/processed/` (adjust if needed).

---

## Variable dictionaries (by dataset)

### A) `1911-1937_merged_sorted.xlsx`
Core columns
| Variable | Type | Description |
|---|---|---|
| `id` | string | Unique row identifier. |
| `year` | int | Publication year (1911–1937). |
| `paper` | string | Standardized newspaper/source name. |
| `title` | string | Headline title (normalized; article body not included). |
| `has_ta` | int/bool | 1 if the title explicitly contains **“她”**, else 0. |
| `woman_kw` | int/bool | 1 if the title mentions women without “她” (e.g., 女子/妇女/女性/女校/女工), else 0. |
| `len_chars` | int | Title length in Chinese characters (used as control). |
| `source_index` | string | Upstream index tag (e.g., NPI). |
| `notes` | string | Manual fixes / OCR remarks (optional). |

How created
- Merge index exports; normalize Unicode and punctuation.
- Canonicalize newspaper names; parse and validate year.
- Drop duplicates via (`paper`, `year`, `title`) and fuzzy match on trimmed titles.
- Compute `has_ta`, `woman_kw` via regex lists; compute `len_chars`.
- Sort by year and write to Excel.

---

### B) `1938-1949_merged_sorted.xlsx`
Core columns (same schema; different year range)
| Variable | Type | Description |
|---|---|---|
| `id` | string | Unique row identifier. |
| `year` | int | Publication year (1938–1949). |
| `paper` | string | Standardized newspaper/source name. |
| `title` | string | Headline title (normalized). |
| `has_ta` | int/bool | 1 if **“她”** appears, else 0. |
| `woman_kw` | int/bool | Women-related keywords without “她.” |
| `len_chars` | int | Title length. |
| `source_index` | string | Upstream index tag. |
| `notes` | string | Optional curation notes. |

How created
- Same pipeline as dataset A, applied to the post-1937 period.

---

### C) `final_sentiment_sentprop.xlsx`
What it adds
- Sentiment scores and classes from calibrated models; modeling helpers for DiD/event-study.

Core & derived columns
| Variable | Type | Description |
|---|---|---|
| `id`, `year`, `paper`, `title`, `has_ta`, `woman_kw`, `len_chars` | — | Carried over from A/B. |
| `snownlp_prob` | float | SnowNLP polarity probability (0–1). |
| `sentprop_score` | float | SentProp score (0–1) or standardized z-score. |
| `sent_score` | float | Harmonized sentiment score used in plots/tables (e.g., average or calibrated transform). |
| `sent_class` | string | Sentiment class mapped from `sent_score`: `Positive` / `Neutral` / `Negative`. Default thresholds: **≥0.55 → Positive; ≤0.45 → Negative; otherwise Neutral**. |
| `post1937` | int/bool | 1 if `year ≥ 1937`, else 0. |
| `phase` | string | Period label: `pre1937`, `1937_1945`, `post1945` (if created). |
| `ta_x_post` | int | Interaction `has_ta * post1937` for DiD. |
| `paper_fe`, `year_fe` | string/int | Encoded fixed-effect labels for modeling tables (optional). |

How created
- Concatenate A & B → left-join model outputs by `id` (fallback key: `paper`+`year`+`title`).
- Calibrate thresholds against a manually checked validation set; map to `sent_class`.
- Add `post1937` and interactions; write analysis-ready Excel.

---

## Usage notes
- Load with `pandas.read_excel()`; enforce dtypes as above.
- Keep restricted raw sources outside the repo (e.g., `data/raw/`, git-ignored).
- If you regenerate features, keep the same schemas so notebooks run unchanged.

## License & Ethics
Derived tables are released for educational use under the repository license. Do not redistribute upstream copyrighted materials; cite original indexes if you reuse these derivatives.


