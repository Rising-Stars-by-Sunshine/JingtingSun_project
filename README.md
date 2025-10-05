# Framing Women with the Pronoun “她” in Republican-Era Newspapers (1911–1949)

> STAT 201: Machine Learning for Social Science · Duke Kunshan University (Autumn 2025)

## Abstract
During the Republican era, the feminine pronoun **“她”** entered mass print, making women newly visible. This project tests whether the **1937** full-scale war shifted the *tone* of headlines that explicitly use “她” toward greater positivity. Using 1911–1949 newspaper titles, I classify sentiment (positive/neutral/negative) and estimate difference-in-differences and event-study models with newspaper and year fixed effects. This is crucial to understanding whether rising visibility meant better portrayals or merely a lexical shift, informing current debates on gender representation and fair NLP.  
**Results will be added to the poster and report.**

---

## Authors and Roles
- **Jingting Sun** — research design; data curation; sentiment pipeline; DiD/event-study; visualization; writing.

---

## Disclaimer
This repository supports the final research proposal submitted to **STATS 201: Machine Learning for Social Science, instructed by Prof. Luyao Zhang at Duke Kunshan University in Autumn 2025**.

---

## Acknowledgments
Professors, classmates, AIGC tools, and open-source communities that supported this work. Any errors are my own.

---

## Statement of Growth
I strengthened skills in text preprocessing, sentiment calibration, fixed-effects causal designs (DiD/event-study), and reproducible research (versioned code, environments, scripted figures).

---

## Table of Contents
- [Navigation Instructions](#navigation-instructions)  
- [System Configurations](#system-configurations)  
- [Embedded Media](#embedded-media)

---

## Navigation Instructions
- **Code (explanation/visualization):** [`code/explanation/`](code/explanation/) — sentiment classification, calibration checks, plots.  
- **Code (prediction/causal):** [`code/prediction/`](code/prediction/) — DiD and event-study with clustered SEs & fixed effects.  
- **Datasets & preprocessing:** see [`data/README.md`](data/README.md); processed tables in `data/processed/` (CSV/Parquet). Raw files (if restricted) remain in `data/raw/` and are git-ignored.  
- **Figures:** exported charts live in [`visualizations/`](visualizations/).

---

## System Configurations
**One-liner quickstart (creates venv → installs deps → smoke-test):**
```bash
python -m venv .venv && \
( source .venv/bin/activate || .\.venv\Scripts\activate ) && \
python -m pip install --upgrade pip && \
pip install -r requirements.txt && \
python - <<'PY'
import importlib
mods=["pandas","numpy","statsmodels","sklearn","matplotlib","pyarrow"]
[importlib.import_module(m) for m in mods]
print("Environment OK ✅")
PY

### CARE
- **Collective Benefit**: Results support research on gender representation and informed media practices.
- **Authority to Control**: Provenance from the Shanghai Library NPI is preserved and cited; we acknowledge custodianship.
- **Responsibility**: Interpretations contextualize period-specific biases; we avoid sensationalizing historical discourse.
- **Ethics**: We present findings as historical descriptions, encourage critical reading, and document limitations of title-only metadata.
