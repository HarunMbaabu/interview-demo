# MoPhones Interview Case Study Deliverables

This repository contains two executive-facing outputs for the MoPhones credit-risk case study:

1. **Jupyter Notebook**: `MoPhones_Case_Study.ipynb`  
   - Structured analysis flow (business context → cleaning → feature engineering → portfolio health → credit × NPS → recommendations).
2. **Slide Deck (12-slide format)**: `MoPhones_Executive_Deck.md`  
   - Executive-ready storyline aligned to the requested slide structure.

---

## Contents

- `MoPhones_Case_Study.ipynb` — Primary analytical notebook.
- `MoPhones_Executive_Deck.md` — Slide-by-slide deck narrative (max 12 slides).
- `Credit Data - *.csv` — Snapshot credit performance extracts.
- `NPS Data.xlsx` — Customer NPS response data.
- `Credit Data Definitions.xlsx` — Supplemental data dictionary reference.

---

## Quick Start

### 1) Recommended Python environment

Use Python 3.10+ and install:

```bash
pip install pandas matplotlib seaborn openpyxl
```

### 2) Run notebook

Open and run all cells in:

```bash
jupyter notebook MoPhones_Case_Study.ipynb
```

---

## Important Assumptions (documented in notebook)

- `DATE` is used as snapshot date for portfolio trends.
- Default proxy is defined as:
  - `days_past_due >= 90`, or
  - account status in `{FPD, FMD, PAR 30, Write Off}`.
- Requested DOB/income/duration fields were not present in delivered extracts, so a proxy segmentation using available fields is applied and explicitly called out.

---

## Deliverable Intent

These materials are designed for high-stakes interview presentation quality:

- Business-grade interpretation (not just descriptive analytics)
- Clear assumptions and data limitations
- Decision-oriented recommendations for credit and collections strategy

