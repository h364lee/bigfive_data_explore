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