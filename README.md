# DSA 210 - Spotify Music Analysis

Ayse Gulcan Yoruk | DSA 210 Introduction to Data Science | Spring 2026

## Project Overview

This project analyzes personal Spotify listening history together with Spotify audio features such as energy, valence, danceability, tempo, acousticness, loudness, and speechiness. Milestone 1 focuses on exploratory data analysis and hypothesis testing. Milestone 2 focuses on machine learning tasks that are better matched to the available audio-feature data.

## Dataset

The dataset is based on:

- Personal Spotify Extended Streaming History
- Spotify Web API audio features

The private data file is expected to be named:

```text
gulcan_spotify_formatted.json
```

This file is excluded from GitHub through `.gitignore` because it contains personal listening history. To reproduce the notebooks, place the private JSON file in the repository root before running the code.

Dataset summary:

- 1,558 play events
- 1,535 unique tracks
- 921 unique artists
- Date range: April 2025 to April 2026

## Repository Structure

```text
.
|-- milestone1.ipynb
|-- milestone2.ipynb
|-- images/
|-- requirements.txt
|-- README.md
`-- .gitignore
```

The report/LaTeX folder was removed for now. The current focus is working code, reliable ML results, and generated figures.

## Milestone 1

`milestone1.ipynb` contains data loading, data cleaning, exploratory data analysis, visualizations, and hypothesis testing.

Main Milestone 1 analyses include:

- Audio feature distributions
- Correlation heatmap
- Top artists and tracks
- Monthly and hourly listening activity
- Valence trend over time
- Energy-valence scatter analysis
- Listening activity by day of week

Hypothesis test summary:

| Hypothesis | Test | p-value | Result |
|---|---:|---:|---|
| High-energy songs are played more frequently | Mann-Whitney U | 0.8707 | Not rejected |
| Valence is higher in summer than winter | Mann-Whitney U | 0.8250 | Not rejected |
| Acoustic songs have lower tempo | Mann-Whitney U | <0.0001 | Rejected |
| Energy and danceability are positively correlated | Spearman correlation | <0.0001 | Rejected |

## Milestone 2 Research Questions

The original repeated-listening classification target was removed because almost all track-artist pairs appeared exactly once. Daytime/nighttime classification was also tested, but audio features produced near-random AUC values. The final Milestone 2 tasks are therefore:

### Classification Question

Can Spotify audio features predict whether a song is high-energy or low-energy?

Target:

```text
high_energy = 1 if energy >= median(energy)
high_energy = 0 if energy < median(energy)
```

Important leakage rule:

```text
energy is removed from the predictor features.
```

### Regression Question

Can Spotify audio features predict a song's acousticness score?

Target:

```text
acousticness
```

Important leakage rule:

```text
acousticness is removed from the predictor features.
```

## Milestone 2 Pipeline

`milestone2.ipynb` includes:

- Missing-value checks
- Target construction
- Leakage checks
- Audio-only feature engineering
- Numeric imputation and scaling
- One-hot encoding for `key` and `mode`
- sklearn `Pipeline` and `ColumnTransformer`
- Cross-validated hyperparameter tuning
- Backward feature-selection audit with `SequentialFeatureSelector`
- Classification model comparison
- Regression model comparison
- Final figures saved to `images/`

## Models Tested

Classification models:

- Logistic Regression
- Gaussian Naive Bayes
- Decision Tree
- Random Forest
- Extra Trees
- Support Vector Machine
- Gradient Boosting
- Hist Gradient Boosting

Regression models:

- Ridge Regression
- Decision Tree Regressor
- Random Forest Regressor
- Extra Trees Regressor
- Support Vector Regressor
- Gradient Boosting Regressor
- Hist Gradient Boosting Regressor

## Current Milestone 2 Results

### Classification Results

Best model:

```text
Extra Trees Classifier
```

Held-out test results:

```text
F1-score:          0.904
Accuracy:          0.904
Precision:         0.899
Recall:            0.910
Balanced accuracy: 0.904
ROC-AUC:           0.969
```

Interpretation:

The model can classify high-energy vs low-energy songs very well using other audio features such as loudness, acousticness, tempo, danceability, valence, key, and mode. This result is strong and passes the 0.6 F1 threshold.

### Regression Results

Best model:

```text
Support Vector Regressor
```

Held-out test results:

```text
R2:   0.678
MAE:  0.158
RMSE: 0.212
```

Interpretation:

The model can predict acousticness reasonably well from the remaining audio features. The result passes the 0.6 R2 threshold and is much stronger than the earlier valence-regression attempt, which did not pass the threshold.

## Generated Milestone 2 Figures

The current Milestone 2 notebook writes these figures to `images/`:

- `m2_audio_feature_correlation_heatmap.png`
- `m2_classification_confusion_matrix.png`
- `m2_classification_roc_curve.png`
- `m2_classification_model_comparison.png`
- `m2_classification_feature_importance.png`
- `m2_regression_predicted_vs_actual.png`
- `m2_regression_residuals.png`
- `m2_regression_model_comparison.png`

## How to Run

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the notebooks:

```bash
jupyter notebook milestone1.ipynb
jupyter notebook milestone2.ipynb
```

Before running, make sure `gulcan_spotify_formatted.json` is in the repository root.

## Reproducibility

The Milestone 2 workflow uses `RANDOM_STATE = 42`, fixed train/test splits, sklearn `Pipeline`, and `ColumnTransformer`. Preprocessing steps are fit inside cross-validation folds to reduce train-test leakage.

No private raw data is committed to GitHub. Model results should be regenerated locally using the private JSON file.

## Academic Integrity and AI Assistance

AI assistance was used for repository organization, preprocessing design, machine learning pipeline structure, documentation, and code review. AI was not used to fabricate data, model scores, or findings.
