# Credit Risk Modeling Pipeline

A full end-to-end credit risk modeling project built on the **Give Me Some Credit** dataset (Kaggle, 150,000 loan applicants). The project replicates the modeling workflow used by retail banks and consumer lending institutions — from raw data through to a production-ready credit scorecard and model monitoring framework.

---

## Project Overview

The goal was to predict the probability that a borrower experiences serious financial distress (90+ days past due) within two years. The dataset presents real-world challenges: severe class imbalance (6.68% default rate), missing income data (19.8%), and delinquency coding artifacts — all of which were handled systematically.

The pipeline spans six notebooks:

| Notebook | What was done |
|---|---|
| `01_eda.ipynb` | Exploratory analysis, MCAR test for missingness, class imbalance quantification, outlier detection, and data cleaning |
| `02_features.ipynb` | Weight of Evidence (WoE) encoding, Information Value (IV) feature selection, and 10 domain-driven engineered features |
| `03_modelling.ipynb` | Trained and compared Logistic Regression, Random Forest, and XGBoost using 5-fold stratified cross-validation with SMOTE oversampling |
| `04_explainability.ipynb` | SHAP TreeExplainer for global and local model explanations, beeswarm plots, waterfall charts, and adverse action notice generation |
| `05_scorecard.ipynb` | Converted the logistic regression into a PDO-scaled credit scorecard, Lorenz curve, Gini coefficient, and cutoff analysis |
| `06_monitoring.ipynb` | Population Stability Index (PSI) for score drift detection, Gini decay tracking across simulated time windows, and a Champion-Challenger framework |

---

## Key Results

| Model | AUC-ROC | Gini | KS Statistic |
|---|---|---|---|
| Logistic Regression | 0.82 | 0.64 | 0.39 |
| Random Forest | 0.85 | 0.70 | 0.43 |
| **XGBoost** | **0.87** | **0.74** | **0.47** |

---

## Technical Highlights

**Feature engineering** — beyond the raw features, 10 domain-specific variables were constructed including a weighted delinquency severity score, debt-to-income ratio, log-transformed income, and a utilization × delinquency interaction term. Features were ranked by Information Value (IV) and only those above the 0.02 threshold were retained.

**Imbalance handling** — the 13.4:1 class imbalance was addressed using SMOTE oversampling within the cross-validation loop (applied only to training folds), combined with `class_weight='balanced'` in the logistic regression.

**WoE encoding** — Weight of Evidence encoding was applied to all selected features, which linearises the log-odds relationship for logistic regression and is standard practice in retail credit scoring.

**PDO scorecard** — the logistic regression was converted to an integer credit score using the Points to Double the Odds (PDO) method (PDO=20, base score=600, base odds=50:1), matching the format used by FICO and major bank scorecards in production.

**SHAP explainability** — SHAP TreeExplainer was used to produce both global explanations (feature importance, beeswarm) and individual applicant explanations (waterfall charts). The top three SHAP drivers for any declined applicant can be extracted as adverse action reasons, satisfying SR 11-7 and GDPR right-to-explanation requirements.

**Model monitoring** — Population Stability Index was computed across six simulated monthly windows to detect score distribution drift. A Champion-Challenger test compared the full model against a simpler challenger candidate, following standard model governance practice.

---

## Dataset

**Give Me Some Credit** — Kaggle (2011 competition)  
150,000 applicants · 10 features · 6.68% default rate · 13.4:1 class imbalance  
https://www.kaggle.com/c/GiveMeSomeCredit

---

## Tech Stack

`Python` · `pandas` · `scikit-learn` · `XGBoost` · `SHAP` · `imbalanced-learn` · `matplotlib` · `seaborn` · `joblib` · `pyarrow`

---

## How to Run

```bash
pip install -r requirements.txt
```

Open Jupyter from the project folder and run notebooks `01` through `06` in order. Each notebook reads from and writes to the local `data/`, `models/`, and `reports/` subfolders.
