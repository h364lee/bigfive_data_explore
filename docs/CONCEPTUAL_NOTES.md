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

## Internal Consistency
- how consistently the items within each trait measure the same underlying construct: internal consistency reliability
### Cronbach's Alpha (α)
- Estimates the reliability of a scale (the degree to which all items in a set measure the same latent trait)
- Example: if a person scores high on one Extraversion item, they should score high on the others - α quantifies how consistently this holds.
- Common interpretation: 
    - α ≥ .90 → Excellent
    - .80 ≤ α < .90 → Good
    - .70 ≤ α < .80 → Acceptable
    - .60 ≤ α < .70 → Questionable
    - α < .60 → Poor
### Item-Total Correlation
- How well each item correlates with the sum of the remaining items: way to check item quality
- Common interpretation: 
    - r ≥ .30 → Acceptable
    - r < .30 → Consider reviewing the item (it may be poorly worded or unrelated)

# Exploratory Factor Analysis
## Suitability for Factor Analysis
You want to confirm that your items form patterns of correlations — EFA only works when there are shared underlying dimensions. If these tests fail, EFA is not meaningful.
### KMO
- Kaiser-Meyer-Olkin statistic test: checks whether your variables share enough common variance to justify factor analysis.
    - KMO > .60: Acceptable
    - KMO > .80: Meritorious
### Bartlett's test
- Checks whether the correaltion matrix significantly differs from an identity matrix (i.e., not just noise)
    - p < .05: data are suitable for EFA

## Determining Number of Factors
Trying to discover how many psychological traits are hiding beneath the surface of my item data. Each trait is called a *latent factor*: an invisible psychological trait that causes patterns in item responses (e.g., You can’t measure "Extraversion" directly — but if someone agrees with “I enjoy parties,” “I am talkative,” and “I seek excitement,” you infer a common cause: Extraversion.)
### Scree plot
- Shows how much variance is explained by each potential factor
- The first few peaks are tall = strong factors
- The line 'elbows' and flattens = weak/noise
- Keep the factors before the elbow
### Parallel analysis
- Real data is compared to randomly shuffled data
- If my factor has a bigger eigenvalue than the random one, it is probably meaningful

## Factor Loadings
- Correlation between an item and a latent trait (Analogy: Factor loading = how strongly a light bulb (item) glows when a switch (factor) is turned on.)
- A loading of .80 means the item strongly reflects that trait.
- A loading of .20 means the item barely reflects that trait.
- Items can "cross-load" on multiple traits, which may mean they’re ambiguous.

## Rotation (Oblimin vs. Varimax)
Factor analysis starts with a mathematical solution, but it's often messy — many items might load a little bit on multiple factors.

Rotation cleans up the solution to make the patterns clearer.
Varimax = forces traits to be uncorrelated (orthogonal)
Oblimin = allows traits to correlate (recommended for Big Five)

Analogy: Imagine rotating a spotlight over a stage so it shines directly on clusters of people (items). Rotation helps you reorient the axes so items load more clearly on single traits.
## Maximum Likelihood Estimation 
- The method used to 'fit' the factors to your data (mathematical best guess for what the latent factors are).
- ML (Maximum Likelihood) tries to find the factor structure that makes the observed data most probable.