# Data Version Log

## 2025-07-04
**Raw file**: data/raw/bigfive_raw.csv (1M rows from Kaggle)

**Cleaned v1**: data/cleaned/cleaned_bigfive_v1.csv  
- Filters: dropped rows with testelapse < 20 sec, introelapse = 0, item entries outside of 1-5, rows with multiple IP counts, and rows with any missing values in the 50 questions.
- Added mean trait scores (E, N, A, C, O) (just a trial)
- Date locked: 2025-07-04
- Local only, not tracked in Git

To reproduce:
Run `notebooks/00_data_cleaning.ipynb` with raw CSV in `data/raw/`
## 2025-07-05

- Finalized Emotional Stability → Neuroticism reversal at item level.
- Added new NRT1–NRT10 items and recomputed Neuroticism mean.
- Verified trait distributions with histograms (sample n=1,000).
- Cleaned version: cleaned_bigfive_v1.csv (local only).

