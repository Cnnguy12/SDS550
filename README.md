# California Housing Dataset Analysis

Exploratory and inferential statistical analysis of the [California Housing dataset](https://scikit-learn.org/stable/datasets/real_world.html#california-housing-dataset).

**Selected Variable:** `AveRooms` (average number of rooms per household)
**Target Variable:** `MedHouseVal` (median house value)

## Overview

This project explores the relationship between household room count and median house value across 20,640 California census block groups (1990 census data, as distributed via `sklearn.datasets.fetch_california_housing`). The analysis moves from univariate description through transformation, categorization, and hypothesis testing:

1. **Load and inspect** the dataset (9 variables, 20,640 observations)
2. **Descriptive statistics** for `AveRooms` (mean, median, std, quartiles)
3. **Distribution visualization** via histograms at two bin resolutions (30 and 100 bins)
4. **Categorization** of `AveRooms` into four meaningful bins (Small / Medium / Large / Very Large) based on quartile cut points, with a frequency table and pie chart
5. **Log transformation** of `AveRooms`, with a `normaltest` check for whether the transform improves normality
6. **Relationship analysis** between `AveRooms` and `MedHouseVal`:
   - IQR-based outlier detection and removal on both variables
   - Log transformation of the cleaned data
   - Graphical analysis (box plots by category, correlation heatmap)
7. **Statistical testing** — a one-way ANOVA testing whether mean `MedHouseVal` differs across the four room-count categories, preceded by Shapiro-Wilk normality checks and Levene's test for homogeneity of variance on each group

## Key Findings

- `AveRooms` is heavily right-skewed (mean 5.43 vs. median 5.23, max of ~142 rooms), driven by a small number of extreme outliers
- Most households fall in the **Medium (4–6 rooms)** category (~60%), followed by **Large (6–8 rooms)** at ~23%
- After IQR-based outlier removal, ~93% of observations were retained for the relationship analysis
- Room-count group assumptions were violated for classical ANOVA (Shapiro-Wilk rejected normality in every group; Levene's test found unequal variances), but the **one-way ANOVA still found a statistically significant difference in mean house value across room categories** (F = 563.34, p < 0.001), leading to rejection of the null hypothesis that all categories share the same mean house value

## Repository Structure

```
.
├── SDS550-CaliforniaHousing.ipynb   # Main analysis notebook (code + output)
├── requirements.txt                 # Python dependencies
├── README.md
└── .gitignore
```

## Getting Started

```bash
git clone https://github.com/Cnnguy12/SDS550.git
cd SDS550
pip install -r requirements.txt
jupyter notebook SDS550-CaliforniaHousing.ipynb
```

The dataset is fetched automatically at runtime via `sklearn.datasets.fetch_california_housing`, so no separate data download is required.

## Tools

- Python (pandas, NumPy)
- scipy.stats (Pearson/Spearman correlation, normality tests, one-way ANOVA, Levene's test, Shapiro-Wilk)
- scikit-learn (dataset loader)
- matplotlib / seaborn (visualization)
