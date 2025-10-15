# Framing Women with the Pronoun “她” in Republican-Era Newspapers (1911–1949)

> STAT 201: Machine Learning for Social Science · Duke Kunshan University (Autumn 2025)

## Abstract
During the Republican era, the feminine pronoun **“她”** entered mass print, making women newly visible. This project tests whether the **1937** full-scale war shifted the *tone* of headlines that explicitly use “她” toward greater positivity. Using 1911–1949 newspaper titles, I classify sentiment (positive/neutral/negative) and estimate difference-in-differences and event-study models with newspaper and year fixed effects and clustered standard errors. This is crucial to understanding whether rising visibility reflects genuinely improved portrayals or merely a lexical shift, with relevance to current debates on gender representation in news and fair NLP.  
**Results will be added to the poster and final report.**

---

## Authors and Roles
- **Jingting Sun** — research design; data collection & normalization; sentiment pipeline and calibration; DiD/event-study modeling; visualization; documentation; reproducibility setup.

---

## Disclaimer
This repository supports the final research proposal submitted to **STATS 201: Machine Learning for Social Science, instructed by Prof. Luyao Zhang at Duke Kunshan University in Autumn 2025**.

---

## Acknowledgments
Thanks to DKU professors and classmates for feedback, AIGC tools for drafting and code review, and open-source communities for libraries used in this project. Any errors are my own.

---

## Statement of Growth
This project strengthened my skills in (i) historical text preprocessing and metadata hygiene, (ii) sentiment modeling and threshold calibration, (iii) fixed-effects causal designs (DiD and event study) with proper clustering, and (iv) reproducible research practices—version-controlled code, environment pinning, and scripted figure exports.

---

## Table of Contents
- [Navigation Instructions](#navigation-instructions)  
- [System Configurations](#system-configurations)  
- [Embedded Media](#embedded-media)

---

## Navigation Instructions
- **Code (explanation / visualization):** see [`code/explanation/`](code/explanation/) for sentiment classification, calibration checks, and plotting scripts.  
- **Code (prediction / causal):** see [`code/prediction/`](code/prediction/) for DiD and event-study models with newspaper & year fixed effects (clustered by newspaper).  
- **Datasets & preprocessing:** descriptions and provenance in [`data/README.md`](data/README.md). Processed, analysis-ready tables live in `data/processed/`; raw sources (if access-restricted) are kept in `data/raw/` and are git-ignored.  
- **Figures:** exported images are stored in [`visualizations/`](visualizations/) and referenced by the poster/report.

---

## System Configurations
**Quickstart (create venv → install deps → smoke-test imports).**  
*macOS/Linux (bash/zsh):*
```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
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
---

## Media
- **Code (Demo):** see (https://duke.box.com/s/nsc40udbjrkofunm1ev50j005slziq4q) 


---
