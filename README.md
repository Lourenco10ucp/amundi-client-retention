# Amundi Client Retention — Predictive Analytics Project

## Business Context
Amundi is Europe's largest asset manager, with over €2.3 trillion in assets under management across 100 million retail clients in 35 countries. Each week, the retail engagement team receives approximately 7,700 prospective client leads but can contact no more than 1,200, incurring a €5 cost per contact regardless of outcome.

The goal of this project is to build a data-driven pipeline that identifies which clients to contact each week in order to **maximise expected profit**.

## Approach
A three-stage machine learning pipeline was developed in Python:

1. **Classification** — predicts whether a client will invest (binary)
2. **Regression** — predicts how much a client will invest (conditional on investing)
3. **Expected Profit Ranking** — combines both outputs into a single score:

$$\text{Expected Profit} = P(\text{invest}) \times (0.045 \times \text{Predicted Amount}) - €5$$

Clients are ranked by this score and the top candidates up to the 1,200-contact cap are selected. Clients with negative expected profit are excluded even if the budget is not exhausted.

## Models
| Stage | Model | Metric | Score |
|-------|-------|--------|-------|
| Classification | Random Forest (calibrated) | ROC AUC | 0.777 |
| Regression | HistGradientBoosting | R² | 0.972 |
| Regression | HistGradientBoosting | RMSE | 127.92 |

The final classifier-regressor pair was selected based on **joint holdout profit**, not individual metrics.

## Results
| Metric | Value |
|--------|-------|
| Holdout realised profit | €4,734 |
| Clients selected (Period 5) | 824 of 6,711 |
| Contact budget used | 69% of 1,200 cap |

The model identified that contacting beyond 824 clients would generate negative expected profit — meaning the 1,200-contact cap was not binding.

## Repository Structure
- `FinalCode_Group6.ipynb` — full Python pipeline (preprocessing, modelling, evaluation)
- `Report_Group6.pdf` — final business report with methodology and recommendations

## Tools & Libraries
Python, scikit-learn, XGBoost, pandas, matplotlib, seaborn

## Authors
Group 6 — Católica Lisbon School of Business & Economics, MSc Business Analytics (2026)
