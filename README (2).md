# Customer Churn Prediction & Retention Intelligence System

A machine learning project that predicts customer churn, explains model predictions with SHAP, and segments customers by estimated churn risk.

## Project Highlights

- Audited and cleaned the IBM Telco Customer Churn dataset.  
- Compared Logistic Regression, Random Forest, Gradient Boosting, and CatBoost.  
- Tuned CatBoost using validation ROC-AUC and early stopping.  
- Evaluated retention-targeting thresholds using precision, recall, and F1.  
- Explained model predictions using SHAP.  
- Created customer-level explanations and risk segments.  
- Preserved a separate test set for final evaluation.

## Final Test Results

| Metric | Result |
| :---- | ----: |
| ROC-AUC | 0.8400 |
| Accuracy | 0.7569 |
| Balanced accuracy | 0.7436 |
| Churn precision | 0.5317 |
| Churn recall | 0.7153 |
| Churn F1 | 0.6100 |

&nbsp;

The selected decision threshold was 0.30, chosen using validation data. At this threshold, 378 of 1,057 test customers were flagged as potentially at risk. These predictions are risk estimates, not guarantees of churn.

## Key Findings

Contract type, tenure, and internet service were the leading features by mean absolute SHAP value for the tuned CatBoost model.

In the dataset, churn was associated with month-to-month contracts, shorter tenure, and electronic-check payments. These relationships are predictive associations, not evidence of causation.

## Repository Structure

```
customer-churn-intelligence/
├── notebooks/
│   └── 01_data_understanding.ipynb
├── results/
│   ├── figures/
│   └── metrics/
├── artifacts/
│   └── models/
├── FINAL_PROJECT_REPORT.md
├── README.md
└── .gitignore
```

&nbsp;

## Dataset

This project uses the IBM Telco Customer Churn dataset from Kaggle:

[https\://www\.kaggle.com/datasets/blastchar/telco-customer-churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

Download the dataset from Kaggle and place the CSV in the `data/` directory to reproduce the workflow. Review the dataset's license and terms before redistributing the data.

## Limitations

- Results come from a public historical dataset, not live company data.  
- The decision threshold was not optimized using real retention costs.  
- Model explanations describe learned associations, not causal effects.  
- Performance on new customers may differ from the reported test results.

## Tools

Python, pandas, NumPy, scikit-learn, CatBoost, SHAP, Matplotlib, and Google Colab.