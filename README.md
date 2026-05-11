# Student Performance Dashboard

An interactive browser dashboard for exploring machine learning predictions of student academic performance on the Common Entrance Examination (CEE). Built to accompany a Jupyter notebook ML analysis pipeline.

## What the Models Predict

Models classify each student into one of four performance tiers based on demographic and academic background features:

| Class | Meaning | Count |
|-------|---------|------:|
| Average | Below-average performance | 157 |
| Good | Moderate performance | 210 |
| Vg | Very Good performance | 198 |
| Excellent | Top performance | 101 |
| **Total** | | **666** |

## Dataset

| Property | Value |
|----------|-------|
| Total records | 666 students |
| Train / test split | 532 / 134 (80/20 stratified) |
| Exam | Common Entrance Examination (CEE) |
| Performance classes | 4 (Average, Good, Vg, Excellent) |
| Chance baseline | 25% (random 4-class) |

**Features include:** caste/social category, gender, parental occupation (father and mother), medium of instruction, coaching type, Class X and XII percentage, Class X and XII board (CBSE, SEBA, AHSEC, etc.), and study time.

## Model Results

| Model | Test Accuracy |
|-------|:------------:|
| **Random Forest** | **57.5%** |
| Logistic Regression | 56.7% |
| KNN | 56.0% |
| Gradient Boosting | 50.8% |

All models substantially outperform the 25% chance baseline. Random Forest is used for the confusion matrix and feature importance visualizations.

**Top predictors (Random Forest):** caste category (ST, General, OBC), study time, and prior board exam percentages (Class XII and X).

## Running the Dashboard

Open `index.html` via a local HTTP server — browsers block `fetch()` on `file://` URLs:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

The dashboard is a single self-contained file (`index.html`) with no build step or dependencies beyond a CDN-loaded Chart.js.

**Three views:**

1. **Model Comparison** — horizontal bar chart of all model accuracies with the 25% chance baseline marked
2. **Confusion Matrix** — class-level prediction breakdown; diagonal (correct) shown in blue, errors in red, per-class recall below
3. **Feature Importance** — top 10 Random Forest predictors, color-coded by category (caste/social, academic history, other)

## Companion Notebook

This dashboard displays pre-computed results exported from `student_performance_analysis.ipynb`, a Jupyter notebook covering:

- Exploratory data analysis and class distribution
- Feature encoding (one-hot encoding of categorical variables)
- Model training: Random Forest, KNN, Logistic Regression, Gradient Boosting
- Evaluation: accuracy, confusion matrix, feature importances
- Export of results to `dashboard_data.json`
