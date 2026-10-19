# Customer Churn Prediction & Retention Intelligence System

## 1. Project Overview

This project predicts customer churn using the IBM Telco Customer Churn dataset.
It combines exploratory data analysis, preprocessing, baseline model comparison,
CatBoost tuning, threshold analysis, SHAP explainability, and customer risk segmentation.

## 2. Business Problem

Customer churn can reduce recurring revenue. A predictive model can help prioritize
customers for retention outreach. Model predictions are risk estimates, not guarantees
that a customer will leave or that an intervention will prevent churn.

## 3. Dataset and Data Quality

- Original dataset: 7,043 rows and 21 columns.
- Target: Churn (Yes/No).
- Original churn rate: approximately 26.54%.
- Eleven blank TotalCharges values were found among customers with zero tenure.
- Those values were converted to numeric and filled with zero under a documented assumption.
- customerID was excluded from model features.
- No rows were dropped during cleaning.

## 4. Exploratory Data Analysis

Observed churn rates:

- Month-to-month contract: 42.71%.
- One-year contract: 11.27%.
- Two-year contract: 2.83%.
- Tenure 0-12 months: 47.44%.
- Tenure 49-72 months: 9.51%.
- Electronic check payment: 45.29%.

These are associations in this dataset and do not establish causal effects.

## 5. Modeling and Validation

Four baseline models were evaluated using a validation set:
Logistic Regression, Random Forest, Gradient Boosting, and CatBoost.

The selected tuned CatBoost configuration was chosen by validation ROC-AUC.

- Depth: 6
- Learning rate: 0.08
- L2 regularization: 5
- Best iteration: 75
- Validation ROC-AUC: 0.8518

The decision threshold was selected using validation data, with 0.30 chosen
as the F1-leading threshold among those tested.

## 6. Final Test Results

- Accuracy: 0.7569
- Balanced accuracy: 0.7436
- Precision: 0.5317
- Recall: 0.7153
- F1 score: 0.6100
- ROC-AUC: 0.8400
- Decision threshold: 0.30
- Test customers flagged: 378
- Percentage flagged: 35.76%

Confusion matrix (actual rows: no churn, churn; predicted columns: no churn, churn):

| | Predicted no churn | Predicted churn |
|---|---:|---:|
| Actual no churn | 599 | 177 |
| Actual churn | 80 | 201 |

The test set was reserved for final evaluation after model and threshold selection.
Test results were not used to choose the model or threshold.

## 7. Model Explainability

Global SHAP importance was calculated on a sample of 200 validation customers.

Top features by mean absolute SHAP value:

- Contract: 0.5464
- tenure: 0.4959
- InternetService: 0.4567
- OnlineSecurity: 0.2121
- PaymentMethod: 0.2023
- TechSupport: 0.1428
- MonthlyCharges: 0.1253
- PaperlessBilling: 0.1184
- TotalCharges: 0.0940
- StreamingTV: 0.0916

SHAP contributions explain the model's raw output and are not percentage-point
changes in probability or causal explanations.

## 8. Customer Risk Segmentation

Risk segments were created for a sample of 200 validation customers:

| risk_segment   |   customers |   mean_predicted_churn_probability |   actual_churn_rate |
|:---------------|------------:|-----------------------------------:|--------------------:|
| High           |          29 |                           0.723261 |           0.724138  |
| Low            |         127 |                           0.102857 |           0.0787402 |
| Medium         |          44 |                           0.438933 |           0.545455  |

- Low risk: predicted probability below 0.30.
- Medium risk: predicted probability from 0.30 through 0.60.
- High risk: predicted probability above 0.60.

These segment summaries are based on a sample, not the entire customer population.
Predicted probabilities have not been established as calibrated probabilities.

## 9. Limitations

- This is a public historical dataset, not live company data.
- Validation and test metrics may differ due to sampling variability.
- The 0.30 threshold was chosen using validation F1, not measured retention economics.
- False positives may incur outreach costs; false negatives may represent missed opportunities.
- Predictive associations do not prove causes of churn.
- No causal evidence establishes that a retention offer will prevent churn.
- The risk-segment summary uses a 200-customer validation sample.

## 10. Reproducibility and Saved Artifacts

The project stores data, models, metrics, figures, and customer explanations in Google Drive.

Key artifacts include:

- data/telco_churn_cleaned.csv
- artifacts/models/catboost_tuned_candidate.cbm
- artifacts/models/catboost_tuned_config.json
- results/metrics/final_test_metrics.json
- results/metrics/tuned_catboost_shap_importance.csv
- results/tuned_catboost_customer_risk_profiles.csv
- results/customer_explanations_business_friendly.csv
- results/final_test_predictions.csv

## 11. Conclusion

The tuned CatBoost model achieved a test ROC-AUC of 0.8400
and churn recall of 0.7153 at the selected threshold.
The project demonstrates a reproducible classification workflow, threshold trade-off
analysis, model explainability, and risk segmentation. Further business validation
would be required before deploying it for real retention decisions.
