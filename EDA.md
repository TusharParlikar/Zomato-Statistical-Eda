# Zomato EDA — Paper Reproduction Guide

Companion to Day 1 (Statistics + EDA). Reproduce a real, published paper's numbers using today's skills, then extend into modelling once that's covered.

## The Paper

| | |
|---|---|
| **Title** | Machine Learning-Driven Statistical Analysis of Indian Restaurants: Insights from the Zomato Dataset |
| **Authors** | Ayushi Vaidhy, Deepak Batham, Rachit Jain, Amit Kumar Manjhwar |
| **Affiliation** | Madhav Institute of Technology & Science, Gwalior + Prestige Institute of Management & Research, Gwalior |
| **Venue** | Facta Universitatis, Series: Electronics and Energetics, Vol. 38, No. 2 (June 2025), pp. 355–374 |
| **DOI** | [10.2298/FUEE2502355V](https://doi.org/10.2298/FUEE2502355V) |
| **Full text (open access PDF)** | [Link](https://casopisi.junis.ni.ac.rs/index.php/FUElectEnerg/article/download/13158/5693) |

**Why this paper:** same restaurant/rating domain as your Zomato Bangalore project, open access, and it reports hard numbers for 7 different models — real targets to hit rather than eyeballing whether your charts look similar.

**What it does:** pulls ~2.12 lakh (211,944) Zomato India restaurant records across 26 columns — cost, rating, votes, cuisine, location, delivery/takeaway flags — cleans it, runs EDA to surface market patterns (top chains, what drives rating, price-vs-rating relationship), then benchmarks Linear Regression, Decision Tree, Random Forest, KNN, Gradient Boosting, XGBoost, and LASSO predicting `aggregate_rating`. Tree-based models dominate; plain Linear Regression and LASSO lag badly because the relationship isn't linear.

## The Dataset

The paper says its data came from Kaggle but doesn't link the specific file — a real gap in the paper itself. The closest match by row count (2 lakh+) and columns:

**[Zomato India Restaurants (2 Lakh+ restaurants data)](https://www.kaggle.com/datasets/ngokulakannan/zomato-india-restaurants2-lakh-restaurants-data/)**

- [ ] Download it and confirm the columns roughly match the paper's Table 1: `res_id`, `name`, `establishment`, `city`, `locality`, `cuisines`, `average_cost_for_two`, `price_range`, `aggregate_rating`, `votes`, `delivery`, `takeaway`, `opentable_support`, plus lat/long, zipcode, currency, highlights, rating_text, photo_count
- [ ] If it doesn't line up exactly, that's fine — say so in your write-up and treat the paper as a methodology template rather than a byte-for-byte target

You already have **[himanshupoddar/zomato-bangalore-restaurants](https://www.kaggle.com/datasets/himanshupoddar/zomato-bangalore-restaurants)** loaded for the Day 1 project — keep it open. Once the paper's pipeline is rebuilt on the India-wide set, rerunning it on your Bangalore-only set is a free bonus round (last section below).

## Scope: today vs. later

| Phase | Paper section | Skill it uses | Timing |
|---|---|---|---|
| Cleaning | §3.2 | duplicates, missing data | Day 1 |
| EDA | §4 | univariate / bivariate / multivariate, outliers | Day 1 |
| Statistical validation | *(paper skips this — your addition)* | correlation, p-values, hypothesis testing | Day 1 |
| Linear Regression baseline | §5.1 | correlation → regression bridge | Day 1 |
| Tree / ensemble / boosting comparison | §5.2–§6 | classifiers & regressors | Once you've covered those algorithms |

## Results Tracker

Fill in "Your result" as you go. Exact numbers won't match — different dataset vintage, different random split — you're checking the ballpark and the ranking (trees > boosting > KNN > linear), not decimal-perfect replication.

| Model | Paper's Accuracy (R²) | Paper's MAE | Your Accuracy | Your MAE |
|---|---|---|---|---|
| Linear Regression | 63.51% | 199.23 | | |
| Decision Tree | 97.71% | 22.89 | | |
| Random Forest | 97.86% | 27.00 | | |
| KNN (k=7) | 81.31% | 90.36 | | |
| Gradient Boosting | 79.63% | 138.40 | | |
| XGBoost | 89.48% | 107.31 | | |
| LASSO | 63.51% | 198.79 | | |

## Phase 1 — Environment & Data

- [ ] Set up Python with pandas, numpy, matplotlib, seaborn, scipy (Colab is fine — it's what the paper used)
- [ ] Download the dataset, load it, run `.info()` and `.describe()`
- [ ] Record the raw row count (paper started at 211,944)

## Phase 2 — Cleaning (mirrors the paper's §3.2)

- [ ] Drop duplicate rows on `res_id`
- [ ] Strip the square brackets around `establishment` values; blanks → `'NA'`
- [ ] Impute missing `address` / `timings` with placeholder text; missing `opentable_support` → `0`
- [ ] Check your post-cleaning row count against the paper's ~195,000 retained — close is fine, exact isn't expected
- [ ] For every column you imputed, label it MCAR, MAR, or MNAR and justify in one line — the paper skips this, so it's where your write-up goes deeper

## Phase 3 — EDA (mirrors §4 — your main deliverable against the paper)

- [ ] Top 10 restaurant chains by outlet count (paper's finding: Domino's Pizza led)
- [ ] Top 10 chains by average rating (paper's finding: ABs-Absolute Barbecues led)
- [ ] Top 5 establishment types by count (paper's finding: Quick Bites most common)
- [ ] Boxplot: price range vs. aggregate rating
- [ ] Univariate: cost, rating, and votes distributions — note skew, and whether `votes` looks like skewed count data rather than the more symmetric shape of `rating`
- [ ] Bivariate: does `delivery` / `takeaway` / `opentable_support` status shift the rating distribution? (direct analogue of your Bangalore project's online-order / table-booking question)
- [ ] Multivariate: cost × cuisine × rating, or city × establishment type × rating
- [ ] Outlier pass on `votes` and `average_cost_for_two` — IQR or Z-score, decide keep / cap / drop, justify it
- [ ] Sanity-check your city and cuisine findings against the paper's: Bangalore highest restaurant count, Gurgaon highest-rated (avg 3.83), Hyderabad most votes, North Indian top cuisine, most restaurants in the 3–4 rating band, typical cost ₹250–800

## Phase 4 — Statistical Validation (your addition — the paper reports patterns, never tests them)

- [ ] Pearson correlation + p-value: cost vs. rating
- [ ] Independent t-test: rating for `delivery` = 1 vs. `delivery` = 0
- [ ] One-way ANOVA: rating across establishment types or top cuisines
- [ ] Write one line per test — what you tested, the p-value, what you can and can't conclude
- [ ] Flag it explicitly: the paper states higher average cost correlates with a higher likelihood of a higher rating — even a significant p-value here is correlation, not causation. Say so in your summary.

## Phase 5 — Baseline Model (§5.1 — the correlation-to-regression bridge)

- [ ] Pick the paper's feature set: cost, votes, price_range, plus cuisine / location encodings
- [ ] Fit Linear Regression predicting `aggregate_rating`, 90/10 train/test split (matches the paper)
- [ ] Record R² and MAE in the tracker above
- [ ] One paragraph: why does plain linear regression underperform here? (Paper's own read: the cost/votes/rating relationship isn't linear — exactly why the tree models crush it next.)

## Phase 6 — Full Model Comparison (once you've covered these algorithms)

| Model | Paper's tuned hyperparameters |
|---|---|
| Decision Tree | max_depth=15, min_samples_split=4 |
| Random Forest | n_estimators=150, max_depth=20, min_samples_split=5 |
| KNN | k=7 |
| Gradient Boosting | learning_rate=0.05, n_estimators=100, max_depth=4 |
| XGBoost | learning_rate=0.1, n_estimators=150, max_depth=6 |
| LASSO | alpha=0.01 |

- [ ] Train each with the paper's hyperparameters as your starting point
- [ ] Fill in the rest of the results tracker
- [ ] Write up which model won for you, and whether the ranking matches the paper's (trees on top, linear models at the bottom)

## Bonus — Tie Back to Day 1

- [ ] Rerun Phases 2–5 on your Bangalore-only dataset
- [ ] One paragraph: what changes going from all-India to Bangalore-only? Do the same features still drive rating?