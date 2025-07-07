# CONCEPTUAL_NOTES.md

## Kernel Density Estimation (KDE)
- KDE estimates the probability density function (PDF) of a sample.
- Smooths data using a kernel function (often Gaussian).
- Good for big samples, but shows *sample shape*, not population truth.
- Use `kde=True` in seaborn histplot to overlay KDE on histogram.

## Reverse Scoring
- Needed when a scale direction is flipped.
- Example: Emotional Stability → Neuroticism.
- Formula: If scale is 1–5 → new = 6 - old.

## Difference: Histogram vs. Density Plot
- Histogram = discrete bin counts.
- KDE = continuous estimate.
- Overlaying both is common.

## How to organize imports and settings
- Imports & global plot settings = once, at top
- Specific settings (like figsize, palette, ax options) → do those in the plot code block, because they’re plot-specific.

## ANOVA Recap
### One-way ANOVA
- Tests one categorical factor (i.e., DV: continuous; IV: categorical)
- Example: "Does mean Openness differ across continents?"
### Two-way ANOVA (factorial)
- Tests two categorical factors and their interaction on continuous DV (i.e., DV: continuous; IVs: categorical)
- Example: "Does mean Openness differ by continent and by gender? Is there an interaction?
### Repeated Measures ANOVA
- Tests means across repeated measures on the same subject (within-subject design)
- Example: "Did mean Openness scores change over 3 time points for each participant?"
### Mixed ANOVA
- Combines between- and within-subject factors
- Example: "Does a training program (group) change test scores over time (within)?"

## Tukey's HSD
- A post-hoc test used after finding a significant ANOVA result
- ANOVA tells that at least one group mean differs, but not which groups differ.
- Tukey's HSD (Honest Significant Difference) does all pairwise comparisons, while controlling the familywise error rate (adjusted p-values)
### Confidence Interval in Tukey
- For each pairwise comparison:
    - The mean difference is your estimate of how much the two group means differ.
    - The confidence interval (lower, upper) shows the range where you expect the true mean difference to fall with 95% confidence.
    - If the CI includes zero, you cannot reject the null hypothesis for that pair because zero difference is plausible.
- If CI includes zero, 0 difference is possible. Thus, if your reject column says True but your CI includes zero, you should distrust the reject flag.
- This can happen due to rounding in printed output (the real CI might barely miss zero by 0.0001)