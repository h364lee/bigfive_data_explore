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
- Next step: group comparisons by gender and age bins in `02_group_comparison.ipynb` (Scaffolded).
- All code and EDA visuals reproducible via `notebooks/01_univariate_EDA.ipynb`.

## 2025-07-07
- Created continent grouping variable from country codes: North America (NA), South America (SA), Europe (EU), Asia (AS), Oceania (OC). Dropped NONE and Other for clear regional factors.
- Sampled 5,000 rows from the cleaned dataset (cleaned_bigfive_v1.csv).
- Verified group counts: all final continents have N > 100.
- Calculated mean, SD, and N for Openness, Conscientiousness, Extraversion, Agreeableness, and Neuroticism by continent.
- Ran one-way ANOVA for each trait:
    - Found significant differences for Openness, Conscientiousness, Agreeableness, and Neuroticism (all p < .001).
    - No significant differences for Extraversion.
- Ran Tukey HSD post-hoc tests for significant traits:
    - Found Asia consistently lower in Openness and Agreeableness.
    - North America significantly higher in Conscientiousness than Asia, Europe, and Oceania.
    - North America and Oceania higher in Neuroticism than Asia.- Created and reviewed boxplot: Openness by Continent matches ANOVA/Tukey pattern.
    - Next: Extend plots to other traits. Thinking weather I should do another group comparison (with multiple factors). 

## 2025-07-08
### part 1
- Completed R univariate EDA with descriptive table, Histograms + KDEs, and outlier boxplots with mean lines
- Matched Python flow.
### part 2
- Sampled the cleaned Big Five dataset (n = 5,000, same random seed = 42)
- Created continent groups matching my Python workflow:
    - North America, South America, Europe, Asia, Oceania
    - Countries not in these bins are assigned Other 
    - Filtered out NONE and low-n Other countries (e.g., minor African states, Russia, Turkey)
    - Verified group counts and listed remaining Other countries to check the logic
    - Ran one-way ANOVAs for each Big Five trait to test differences by continent
    - Ran Tukey HSD post-hoc tests for pairwise comparisons
    - Tidied the ANOVA + Tukey results using broom + knitr::kable for clean tables in Quarto
    - Wrote a reproducible loop to do ANOVA + Tukey for all traits at once
    - Reviewed the output:
        - Openness, Extraversion, Agreeableness, and Neuroticism showed consistent significant differences, mainly with Asia scoring lower than other region
        - Conscientiousness showed a small significant difference between South America and Asia
- Documented the interpretations for each trait as draft Results text.
- Tried how to display ANOVA and Tukey HSD results in knitr::kable format, but need to review it more tomorrow.

## 2025-07-13
- Group comparison in R (in qmd) with the whole dataset
- Created two sets of groups: continent groups and culture groups
- Ran ANOVA and TukeyHSD for the groups
- Blockers: too many groups and datapoints led to errors in R when run, and the plots with bad interpretibility. 
- Decided to move on to the next parts: Reliability analyses (Cronbach's alpha, item-total correlations), Correlation matrix and factor analyses, and cluster analysis. 

## 2025-07-14
- Reliability Analyses
- Subset item-level responses by trait 
- Calculated Cronbach's alpha for each trait using psych::alpha() with check.keys = TRUE for detecting reverse-coded items
- Identified reverse-scored items using auto-detection
- Created a summary table
- REALIZED THAT I USED UNADJUSTED SCORES FOR PREVIOUS ANALYSES... I knew there are reverse-coded items but assumed their scores had been adjusted in the dataset. Need to re-run these analyses with corrected trait scores -> very positive because I might find something interesting from the group comparison if I use the corrected scores.

## 2025-07-16
- annotated reliability analyses file (03_reliability_analysis)
- Recomputed alpha() with check.keys = TRUE to identify reverse-scored items
- Created a reverse_score() function and applied it to the reverse-scored items
- Comptuted trait-level scores with reverse-scored items
- Computed a Pearson correlation matrix using cor() and psych::corr.test()
- Tested for statistical significance of correlations (all p <.001) with sample size N = 602,587
- Visualized the correaltion matrix with ggcorrplot() and corrplot()
- Used inline R code to insert stats in line. 

## 2025-07-18
- Identified and reverse-coded items
- Exploratory Factor Analysis
    - Checked factorability with KMO and Bartlett's X2
    - Ran parallel analysis: suggested 10-factor solution
    - Estimated EFA models
        - 5-factor model (based on theory)
        - 10-factor model (data driven from parallel analysis)
    - Rotation method: maximum likelihood
    - MOre variance explained by the 10-factor model
    - Visualized factor structure