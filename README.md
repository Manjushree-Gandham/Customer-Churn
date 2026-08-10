# Customer Churn Prediction & Explainable Retention Intelligence

An internship-level machine learning project that predicts telecom customer churn and converts model predictions into customer risk levels and retention recommendations.

## Project Overview

Customer churn is a major business problem because losing existing customers can reduce recurring revenue and increase acquisition costs. This project builds a binary classification system to estimate churn probability and identify customers who may require proactive retention.

The project compares Decision Tree, tuned Random Forest, and tuned XGBoost models and evaluates them using multiple metrics rather than accuracy alone.

## Key Results

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Decision Tree | 73.46% | 50.00% | 47.33% | 48.63% | 0.6514 |
| Tuned Random Forest | 75.66% | 52.77% | **78.88%** | **63.24%** | 0.8447 |
| **Tuned XGBoost** | **80.41%** | **66.67%** | 52.41% | 58.68% | **0.8485** |

### Interpretation

- Tuned XGBoost achieved the highest test accuracy and ROC-AUC.
- Tuned Random Forest achieved the highest churn recall, identifying more customers who actually churned.
- The choice of model can therefore depend on the business objective: overall ranking/discrimination versus maximizing churner detection.

## Workflow

```text
Raw Customer Data
        ↓
Data Cleaning
        ↓
Exploratory Data Analysis
        ↓
Stratified Train/Test Split
        ↓
Categorical Encoding + Numerical Features
        ↓
5-Fold Stratified Cross-Validation
        ↓
Hyperparameter Tuning
        ↓
Decision Tree / Random Forest / XGBoost
        ↓
Accuracy + Precision + Recall + F1 + ROC-AUC
        ↓
ROC / Precision-Recall Analysis
        ↓
Feature Importance + SHAP Explainability
        ↓
Churn Probability
        ↓
Risk Level
        ↓
Retention Recommendations
```

## Dataset

The project uses the Telco Customer Churn dataset. The included CSV contains customer demographic, service, account, contract, billing, tenure, and charge information.

The target variable is `Churn`:
- `0` = No Churn
- `1` = Churn

## Data Preparation

The notebook:
- Removes `customerID` because it is an identifier.
- Converts `TotalCharges` to numeric.
- Handles missing/blank `TotalCharges` values.
- Converts `Churn` from Yes/No to 1/0.
- Uses a stratified train/test split.
- Uses `OneHotEncoder` for categorical variables.
- Keeps preprocessing inside the model pipeline to reduce leakage risk.

## Models

### Decision Tree
Used as an interpretable baseline model.

### Random Forest
An ensemble of decision trees with class balancing and randomized hyperparameter search.

### XGBoost
A gradient-boosted tree model tuned with randomized search and evaluated on the same held-out test set.

## Evaluation

The primary tuning metric is ROC-AUC because churn is an imbalanced classification problem. The final evaluation reports:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC
- Confusion Matrix
- ROC Curve
- Precision-Recall Curve

## Explainability

Tree-based feature importance and SHAP are used to understand which input features contribute to model predictions. This makes the project more useful for business decision support rather than treating the model as a black box.

## Customer Risk Segmentation

The prediction function converts churn probability into simple risk tiers:

- **Low Risk:** probability < 50%
- **Medium Risk:** probability 50%–75%
- **High Risk:** probability ≥ 75%

## Retention Recommendations

The project demonstrates rule-based actions based on customer attributes and predicted risk, including:
- Longer-term contract incentives
- Early-tenure loyalty offers
- Technical-support trials
- Automatic-payment incentives
- Personalized pricing review
- Priority retention outreach for high-risk customers

## Repository Structure

```text
customer-churn-prediction/
│
├── Customer_Churn_Internship.ipynb
├── WA_Fn-UseC_-Telco-Customer-Churn.csv
├── Customer_Churn_Internship_Presentation.pptx
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

## Installation

Create and activate a virtual environment, then install dependencies:

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install packages:

```bash
pip install -r requirements.txt
```

## Running the Notebook

Start Jupyter:

```bash
jupyter notebook
```

Open `Customer_Churn_Internship.ipynb` and run the cells from top to bottom.

Alternatively, open the notebook in VS Code and select the `.venv` Python kernel.

## Reproducibility

The project uses `RANDOM_STATE = 42` for reproducible train/test splitting and randomized hyperparameter search.

The notebook also saves the complete trained preprocessing + model pipeline as `customer_churn_complete_pipeline.pkl` when executed. Generated model artifacts are ignored by Git through `.gitignore`.

## Future Improvements

- Deploy a Streamlit dashboard
- Optimize classification thresholds according to business retention costs
- Add data-drift and model-performance monitoring
- Connect retention recommendations to campaign outcomes
- Add an API for real-time prediction

## Presentation

The repository includes the internship presentation:
`Customer_Churn_Internship_Presentation.pptx`

## Author

Internship project — Customer Churn Prediction & Explainable Retention Intelligence.
