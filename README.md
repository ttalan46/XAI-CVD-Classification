# Title

Beyond Internal Validation: An Explainable Machine Learning Approach to Cardiovascular Risk Prediction with Cross-Domain Generalizability

---

## Repository Description

This repository contains the full codebase used in the study, including preprocessing, model training, hyperparameter optimization, calibration, and explainability analyses.

---

## Python Version

Python 3.11

---

## Technical Declarations and Reproducibility

To support reproducibility, the following experimental settings were used throughout the study:

### Random Seed Configuration

A fixed random seed (`random_state = 42`) was used across data splitting, model training, and resampling procedures to ensure reproducibility of results.

---

### Hyperparameter Optimization (Optuna)

Tree-based ensemble models (XGBoost, LightGBM, CatBoost) were optimized using Optuna (LightGBM: 50 trials, XGBoost: 50 trials, CatBoost: 30 trials). The search space included:

n_estimators: [300, 1500]
learning_rate: [0.01, 0.1] (log scale)
max_depth: [3, 8]
subsample: [0.6, 1.0]
colsample_bytree: [0.6, 1.0]
reg_alpha, reg_lambda: [1e-8, 1.0] (log scale)

---

### Final Model Configuration

The final selected model used the following hyperparameters:

* Learning rate: 0.03–0.05
* Maximum depth: 6
* Subsample ratio: 0.8
* Early stopping was applied during training for stability

---

### Resampling Strategy

Synthetic Minority Over-sampling Technique (SMOTE) (k_neighbors=3, random_state=42) was applied within each cross-validation fold as a pipeline component to prevent data leakage.
---

### Calibration and Uncertainty Quantification

Model probabilities were calibrated using isotonic regression applied on a held-out calibration set (15% of training data).
Additionally, split conformal prediction was applied with α = 0.15 to provide uncertainty-aware predictions with empirical coverage on unseen data.

---

## Environment and Setup

To reproduce the results, install dependencies using:

```bash
pip install -r requirements.txt
```

---

## Notes

All experiments were conducted using standard scientific Python libraries. Exact reproducibility may vary slightly depending on hardware and library versions.
