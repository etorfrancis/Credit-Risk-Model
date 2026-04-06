# Model Monitoring Report

## Model Details
- Champion: XGBoost (n_estimators=500, max_depth=5, lr=0.05)
- Dataset: Give Me Some Credit — 150,000 observations
- Training default rate: 6.68%

## Baseline Performance
- AUC:  0.9075
- Gini: 0.8150

## Monitoring Results
| Month | PSI | Status | Gini | Default Rate |
|---|---|---|---|---|
| M+1 | 0.0010 | No shift | 0.8094 | 6.46% |
| M+2 | 0.0009 | No shift | 0.8117 | 6.89% |
| M+3 | 0.0007 | No shift | 0.8176 | 6.58% |
| M+4 | 0.0079 | No shift | 0.7895 | 6.45% |
| M+5 | 0.0411 | No shift | 0.7803 | 6.74% |
| M+6 | 0.1405 | Moderate | 0.8051 | 7.12% |

## Champion-Challenger
- Champion Gini: 0.8150
- Challenger Gini: 0.7400
- Outcome: Champion retained

## Recommended Actions
- Monthly PSI monitoring
- Model review if PSI > 0.25
- Retrain if Gini drops > 5 points
- Quarterly champion-challenger
