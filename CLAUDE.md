# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A dashboard for visualizing student academic performance predictions. The repository currently holds pre-computed ML results exported from a Python analysis pipeline; the dashboard frontend is not yet built.

## Data

`dashboard_data.json` is the single source of truth consumed by the dashboard. It contains four sections:

- **`dataset_info`** — 666 records split 80/20 stratified across 4 classes: `Average`, `Excellent`, `Good`, `Vg`
- **`model_results`** — accuracy scores for Random Forest (best at 57.5%), KNN, Logistic Regression, and Gradient Boosting
- **`feature_importance`** — 38 one-hot-encoded features ranked by Random Forest importance; top predictors are caste category, study time, and prior board exam percentages
- **`confusion_matrix`** — 4×4 matrix for the best model, labels in alphabetical order: `["Average", "Excellent", "Good", "Vg"]`

## Architecture Notes

The features in `feature_importance` are one-hot encoded from categorical originals (e.g. `Caste_ST`, `Father_occupation_OTHERS`, `coaching_WA`). Any feature display logic should group or label them by their original category rather than showing raw encoded names.

Class label `"Vg"` means "Very Good" — treat it as the second-highest tier when ordering performance levels (Average → Good → Vg → Excellent).