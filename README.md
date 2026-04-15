# DSA 210 – Spotify Music Analysis
**Ayşe Gülcan Yörük** | Spring 2026

## Project Overview
This project analyzes personal Spotify listening history combined with audio features (energy, valence, danceability, tempo, acousticness, etc.) to uncover patterns in music preferences.

## Dataset
- **Source**: Personal Spotify Extended Streaming History + Spotify Web API audio features
- **Records**: 1,558 play events | 1,535 unique tracks | 921 unique artists
- **Period**: April 2025 – April 2026
- Raw streaming data is excluded from this repository (`.gitignore`) as it contains private personal data.

## Milestone 1 – Data Collection, EDA & Hypothesis Tests
**File**: `milestone1.ipynb`

### Contents
1. Data loading & cleaning
2. Exploratory Data Analysis
   - Audio feature distributions
   - Correlation heatmap
   - Top artists & tracks
   - Monthly listening activity
   - Hourly & day-of-week patterns
   - Valence (mood) over time
   - Energy vs. Valence scatter
3. Hypothesis Tests (α = 0.05)

| Hypothesis | Test | p-value | Result |
|---|---|---|---|
| H1: High-energy songs played more | Mann-Whitney (one-tailed) | 0.8707 | Not rejected |
| H2: Higher valence in summer | Mann-Whitney (two-tailed) | 0.8250 | Not rejected |
| H3: Acoustic → lower tempo | Mann-Whitney (one-tailed) | <0.0001 | **Rejected** |
| H4: Energy & danceability correlated | Spearman ρ (one-tailed) | <0.0001 | **Rejected** |

## How to Reproduce
```bash
pip install pandas numpy matplotlib seaborn scipy jupyter
jupyter notebook milestone1.ipynb
```
