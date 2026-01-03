# NBA MVP Prediction Pipeline

### A Two-Stage Machine Learning Approach to Identifying and Ranking MVP Candidates

## Overview

This project builds an end-to-end machine learning pipeline to predict NBA Most Valuable Player (MVP) outcomes using historical player statistics. Rather than treating MVP voting as a single prediction task, the project mirrors the real-world voting process by decomposing it into two stages:
**1. Identifying MVP-caliber players** (classification)
**2. Ranking those elite players by expected vote share** (regression)

This approach addresses the extreme class imbalance and zero-inflation inherent in MVP data.

### Problem Framing

MVP voting presents two major modeling challenges:

> **- Rarity**: Only one MVP exists per season, making positive labels extremely scarce.

> **- Zero-inflation**: The vast majority of players receive zero MVP vote share.

Modeling MVP vote share directly for all players leads to unstable predictions dominated by zeros. To solve this, the problem is framed as a two-stage decision process:

> **- Stage 1: Who belongs in the MVP conversation?**

> **- Stage 2: Among those players, how strong is each candidate relative to others?**

# Modeling Approach
## Stage 1: MVP Classification (Binary)

**Model:** XGBoost Classifier

**Target:** `mvp_binary` (1 = received MVP votes, 0 = did not)

**Objective:** Maximize recall **(TP)** to avoid missing true MVP candidates

This stage acts as a very **precise filter**, narrowing thousands of players down to a small, meaningful MVP candidate set.



