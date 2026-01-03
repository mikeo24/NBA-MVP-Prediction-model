# NBA MVP Prediction Pipeline

### A Two-Stage Machine Learning Approach to Identifying and Ranking MVP Candidates

## Overview

This project builds an end-to-end machine learning pipeline to predict NBA Most Valuable Player (MVP) outcomes using historical **(1991-2025)** player statistics. Rather than treating MVP voting as a single prediction task, the project mirrors the real-world voting process by decomposing it into two stages:

**1. Identifying MVP-caliber players** (classification)

**2. Ranking those elite players by expected vote share** (regression)

This approach addresses the extreme class imbalance and zero-inflation inherent in MVP data.

---

### Problem Framing

MVP voting presents two major modeling challenges:

> **- Rarity**: Only one MVP exists per season, making positive labels extremely scarce.

> **- Zero-inflation**: The vast majority of players receive zero MVP vote share.

Modeling MVP vote share directly for all players leads to unstable predictions dominated by zeros. To solve this, the problem is framed as a two-stage decision process:

> **- Stage 1: Who belongs in the MVP conversation?**

> **- Stage 2: Among those players, how strong is each candidate relative to others?**

---

# Modeling Approach
## Stage 1: MVP Classification (Binary)

- **Model:** XGBoost Classifier  
- **Target:** `MVP_binary` (1 = MVP winner, 0 = non-winner)  
- **Objective:** Maximize recall to ensure real MVPs are not missed  

This stage acts as a very **precise filter**, narrowing thousands of players down to a small, meaningful MVP candidate set.

## Stage 2: MVP Vote Share Prediction (Continuous)

- **Model:** Gradient Boosting Regressor  
- **Target:** `Share` (percentage of MVP votes)  
- **Objective:** Rank MVP-caliber players by expected vote share  

This stage reflects how MVP voting works in practice: voters compare a small group of standout players rather than the entire league.


---

##  Data Pipeline

### 1. Web Scraping  
- Historical NBA player statistics  
- MVP voting data from Basketball Reference  

### 2. Data Cleaning & Feature Engineering  
- Advanced performance metrics (TS%, USG%, per-36 stats, efficiency metrics)  
- Player-level and season-level normalization  
- Construction of binary and continuous targets  

### 3. Train / Validation / Test Split  
- Strict separation to prevent data leakage  
- Test set used **only once** for final evaluation  
- Supports future-season inference  

### 4. Model Training & Hyperparameter Tuning  
- Recall-optimized evaluation for MVP detection  
- Controlled complexity for stability and generalization  
- Randomized and grid-based search strategies  

Cross-validated recall optimization for classification

---

## Key Insights

- MVP voting is driven primarily by **offensive volume, usage, and star role**
- Team success contributes, but individual dominance matters more
- Modeling MVP as a single regression problem performs poorly due to extreme zero inflation
- A two-stage approach significantly improves interpretability and performance.


---

## Future Applications

- Rank MVP candidates for unseen seasons (e.g. 2026)
- Generate MVP probability leaderboards by season
- Extend framework to other awards (All-NBA, DPOY, MIP)


## Repository Structure

### Notebooks
- **MVPS_Webscraping_and_Predictions.ipynb**  
  Web scraping, historical data collection, and end-to-end pipeline setup.

- **data_cleaning_mvp.ipynb**  
  Data cleaning, feature engineering, and construction of MVP-relevant metrics.

- **Predict_MVP.ipynb**  
  Final modeling, evaluation, and MVP predictions using classification and regression models.

### Exports
- **HTML files (.html)**  
  Exported notebook versions for easy viewing without running code.

### Documentation
- **README.md**  
  Project overview, methodology, modeling decisions, and key results.



