# Bayesian Uncertainty in Aqueous Solubility Prediction

This repository contains a reproducible analysis comparing **Ridge regression** and **Bayesian linear regression (BayesianRidge)** for aqueous solubility prediction, with a focus on **predictive uncertainty** rather than point-estimate performance alone.

The primary goal is to evaluate:
1. Whether Bayesian regression improves predictive accuracy relative to Ridge.
2. Whether Bayesian posterior predictive intervals are empirically calibrated under small-to-moderate data regimes.

---

## Overview

The core analysis is implemented in a single Jupyter notebook:

- `bayesian_uncertainty_solubility_prediction.ipynb`

The notebook performs:
- Bootstrap-based estimation of RMSE uncertainty with full model refitting.
- Comparative evaluation of Ridge and BayesianRidge point-prediction performance.
- Empirical coverage analysis of Bayesian predictive intervals across multiple train–test splits.
- Analysis of the relationship between predicted uncertainty and observed prediction error.

---

## Methodology Summary

### Point Prediction Evaluation
- Metric: Root Mean Squared Error (RMSE)
- Evaluation method: Nonparametric bootstrap
- Bootstrap details:
  - Resampling the full dataset with replacement
  - Randomized train–test splits within each bootstrap iteration (80% / 20%)
  - Full refitting of preprocessing (standardization) and model at each iteration
- Output: Mean RMSE and 95% bootstrap confidence intervals

### Uncertainty Evaluation (Bayesian Model Only)
- Predictive intervals derived from the Bayesian posterior predictive distribution
- Coverage evaluated via repeated random train–test splits (10 seeds)
- Coverage assessed at 90% and 95% nominal confidence levels
- One-sample t-tests used to assess consistency with nominal coverage

---

## Key Findings
- **Predictive accuracy**: Ridge and BayesianRidge achieve statistically indistinguishable RMSE under bootstrap resampling.
- **Uncertainty calibration**:
  - 90% predictive intervals are empirically well-calibrated across training sizes.
  - 95% predictive intervals exhibit systematic under-coverage for larger training sets.
- **Uncertainty usefulness**: Posterior predictive standard deviations show weak and inconsistent correlation with absolute prediction error.

These results suggest that, for this dataset and feature representation, Bayesian linear regression provides **reliable moderate-confidence uncertainty estimates** without improving point-prediction accuracy over Ridge regression.

---

## What This Repository Does *Not* Claim

To avoid misinterpretation, this work does **not** claim:
- Superiority of Bayesian regression in predictive accuracy
- Optimal uncertainty calibration at all confidence levels
- Suitability of BayesianRidge uncertainty for active learning or decision-making without further modeling
- Generalization beyond linear-Gaussian assumptions

---

## Reproducibility
- Random seeds are fixed where applicable.
- All results can be reproduced by restarting the kernel and running the notebook top-to-bottom.
- No external data dependencies beyond those loaded in the notebook.

---

## Dependencies
Key Python dependencies include:
- `numpy`
- `pandas`
- `scikit-learn`
- `scipy`
- `matplotlib`

Exact versions are not pinned but the analysis relies only on stable, widely used APIs.

---

## Intended Audience
This repository is intended for:
- Researchers evaluating uncertainty quantification in small-data regression
- Practitioners comparing Bayesian and frequentist linear models
- Readers interested in *empirical* rather than theoretical uncertainty validation

---

## License
This repository is provided for research and educational purposes.  
No warranty is implied.
