# DSA 210 – Spotify Music Analysis
**Ayşe Gülcan Yörük** | Spring 2026

## Project Overview
This project analyzes personal Spotify listening history combined with audio features (energy, valence, danceability, tempo, acousticness, etc.) to uncover patterns in music preferences.

## Data Source
- Personal Spotify Extended Streaming History (private, excluded via `.gitignore`)
- Spotify Web API audio features
- 1,558 play events | 1,535 unique tracks | 921 unique artists | April 2025 – April 2026

## Milestone 1 – Data Collection, EDA & Hypothesis Tests

`milestone1.ipynb` covers data loading & cleaning, exploratory data analysis, and hypothesis testing.

| Hypothesis | Test | p-value | Result |
|---|---|---|---|
| H1: High-energy songs played more | Mann-Whitney (one-tailed) | 0.8707 | Not rejected |
| H2: Higher valence in summer | Mann-Whitney (two-tailed) | 0.8250 | Not rejected |
| H3: Acoustic → lower tempo | Mann-Whitney (one-tailed) | <0.0001 | **Rejected** |
| H4: Energy & danceability correlated | Spearman ρ (one-tailed) | <0.0001 | **Rejected** |

## Milestone 2 – Machine Learning Methods

`milestone1.ipynb` was extended with machine learning methods to predict whether a track is frequently played based on Spotify audio features.

### ML Task
- Problem type: Binary classification
- Target variable: `frequently_played`
- Definition: Tracks with play count ≥ 2 are labeled as frequently played.

### Models Used
- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier

### Evaluation Metrics
- Accuracy
- Precision
- Recall
- F1-score

### Interpretation
The models were compared to evaluate whether audio features such as energy, valence, danceability, acousticness, and tempo can predict repeated listening behavior. Feature importance from the Random Forest model was also used to understand which audio features were most influential.

## How to Reproduce
```bash
pip install pandas numpy matplotlib seaborn scipy jupyter
jupyter notebook milestone1.ipynb
```
