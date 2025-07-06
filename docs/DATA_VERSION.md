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
- Created new NRT1–NRT10 items (reverse-coded from EST1–EST10).
- Recomputed Neuroticism mean from the new NRT items.
- Confirmed all trait means match expected scale direction (higher = more of trait).
- Verified trait distributions with histograms (sample n=1,000, random_state=12).
- Added KDE (density estimate) overlays for all traits.
- Checked for outliers with individual boxplots and multi-panel boxplots (1-row and 2-row layouts).
- Added mean lines to boxplots for comparison with median.
- Ran basic numeric summaries: mean, median, SD, min, max.
- Confirmed all trait values fall within 1–5 range with normal minor outliers, no impossible values found.
- Cleaned version remains: `cleaned_bigfive_v1.csv` (local only).
- Decided to rename jupyter notebook `01_EDA.ipynb` to `01_univariate_EDA` to better organize notebooks.
- Next step: group comparisons by gender and age bins in `02_group_comparison.ipynb`.
- All code and EDA visuals reproducible via `notebooks/01_univariate_EDA.ipynb`.

