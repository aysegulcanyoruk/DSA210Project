# DSA 210 - Spotify Music Analysis

Ayse Gulcan Yoruk | DSA 210 Introduction to Data Science | Spring 2026

## Project Overview

This project analyzes personal Spotify listening history together with Spotify audio features such as energy, valence, danceability, tempo, acousticness, loudness, and speechiness. The project combines exploratory data analysis, hypothesis testing, and traditional machine learning methods to study listening patterns and repeated track plays.

## Motivation

Music listening behavior can reflect personal preferences, routines, mood, and repeated engagement with specific songs or artists. This project uses Spotify listening records to explore whether audio characteristics are related to listening behavior and whether they can help predict whether a track is played repeatedly.

## Dataset

The dataset is based on:

- Personal Spotify Extended Streaming History
- Spotify Web API audio features

The private data file is expected to be named:

```text
gulcan_spotify_formatted.json
```

This file is excluded from GitHub through `.gitignore` because it contains personal listening history. To reproduce the notebooks, place the private JSON file in the repository root before running the code.

Milestone 1 outputs report:

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
|-- reports/
|   |-- figures/
|   `-- final_report/
|       `-- main.tex
|-- requirements.txt
|-- README.md
`-- .gitignore
```

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

## Milestone 2

`milestone2.ipynb` adds a reproducible preprocessing and machine learning workflow.

The machine learning task is binary classification:

- Target variable: `frequently_played`
- Positive class: tracks with play count greater than or equal to 2
- Negative class: tracks with play count equal to 1

The notebook includes:

- Data understanding and missing value checks
- Numeric skewness analysis
- `log1p` transform for strongly skewed positive numeric variables
- Scaling inside sklearn pipelines
- Binary categorical handling
- One-hot encoding for non-binary categorical variables
- Text cleaning and optional lemmatization/TF-IDF preparation
- Date/time feature engineering for auditability
- Leakage-risk review before modeling
- Stratified train/test split
- Cross-validated hyperparameter tuning
- Confusion matrices and classification reports
- Model comparison table
- Random Forest feature importance

Models compared:

- Logistic Regression
- Gaussian Naive Bayes
- Decision Tree
- Random Forest
- Support Vector Machine
- Gradient Boosting
- AdaBoost

## Reports and Figures

Milestone 1 figures are available in `images/` and copied into `reports/figures/` for report use.

The Milestone 2 notebook generates additional outputs in `reports/figures/` after it is run with the private data file, including:

- `target_distribution.png`
- `confusion_matrix_logistic_regression.png`
- `model_comparison.png`
- `feature_importance_random_forest.png`

The final report scaffold is located at:

```text
reports/final_report/main.tex
```

The LaTeX report uses IEEE two-column format and includes red TODO notes for results that must be filled in only after rerunning the notebook with the private data.

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

The Milestone 2 workflow uses `RANDOM_STATE = 42`, a fixed stratified train/test split, sklearn `Pipeline`, and `ColumnTransformer`. Preprocessing steps are fit inside cross-validation folds to reduce train-test leakage.

No private raw data is committed to GitHub. Model results should be regenerated locally using the private JSON file.

## Academic Integrity and AI Assistance

AI assistance was used for repository organization, preprocessing design, machine learning pipeline structure, documentation, and the LaTeX report scaffold. AI was not used to fabricate data, model scores, or findings. Any unverified or incomplete report items are marked as red TODO notes in the LaTeX file.
