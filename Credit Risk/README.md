# Credit Risk Modeling Portfolio

End-to-end credit default prediction — Give Me Some Credit (Kaggle, 150,000 applicants).

## Setup — 3 steps

1. Place all files in one folder (e.g. `My Portfolio\`) — notebooks, CSVs, everything together
2. Open Jupyter from inside that folder
3. Run notebooks in order: **01 → 02 → 03 → 04 → 05 → 06**

## Your folder should look like this

```
My Portfolio\
├── cs-training.csv          ← raw data (already included)
├── cs-testing.csv           ← raw data (already included)
├── 01_eda.ipynb
├── 02_features.ipynb
├── 03_modelling.ipynb
├── 04_explainability.ipynb
├── 05_scorecard.ipynb
├── 06_monitoring.ipynb
├── requirements.txt
└── README.md
```

After running all notebooks, these folders are created automatically:
```
data\      ← parquet files created by notebooks
models\    ← trained model files
reports\   ← all plots and CSV outputs
```

## Install dependencies

```bash
pip install -r requirements.txt
```

## Notebooks

| # | Notebook | Creates |
|---|---|---|
| 01 | EDA & Cleaning | data/cs_clean.parquet |
| 02 | Feature Engineering | data/cs_features.parquet |
| 03 | Modelling | models/lr_final.pkl, models/xgb_final.json |
| 04 | Explainability | reports/shap_*.png |
| 05 | Scorecard | reports/scorecard_*.png, reports/lorenz_curve.png |
| 06 | Monitoring | reports/monitoring_dashboard.png, reports/monitoring_report.md |

## Results

| Model | AUC | Gini | KS |
|---|---|---|---|
| Logistic Regression | ~0.82 | ~0.64 | ~0.39 |
| Random Forest | ~0.85 | ~0.70 | ~0.43 |
| XGBoost | ~0.87 | ~0.74 | ~0.47 |

## Dataset
Give Me Some Credit — https://www.kaggle.com/c/GiveMeSomeCredit  
150,000 applicants · 6.68% default rate · 13.4:1 class imbalance
