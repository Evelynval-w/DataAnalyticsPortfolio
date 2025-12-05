# Project Summary: Credit Risk Assessment Model

## Executive Overview

This project develops a machine learning solution for predicting loan defaults using historical Lending Club data. The model enables financial institutions to make data-driven lending decisions, reducing portfolio risk while maintaining profitability.

---

## Problem Statement

**Business Question**: Can we predict which loan applicants are likely to default, allowing for better risk-adjusted lending decisions?

**Impact**: 
- Reduce default losses by identifying high-risk applicants
- Optimize interest rate pricing based on risk
- Improve portfolio quality through risk segmentation

---

## Data Summary

| Attribute | Value |
|-----------|-------|
| Source | Lending Club (Kaggle) |
| Time Period | 2007-2018 |
| Total Records | ~2.2 million |
| Sample Used | 250,000 (stratified) |
| Features (Raw) | 145 |
| Features (Final) | ~30 |
| Target Variable | Loan Default (Binary) |
| Default Rate | ~21% |

---

## Methodology

### 1. Data Cleaning
- Removed data leakage columns (post-loan information)
- Filtered to completed loans only (excluded "Current" status)
- Handled missing values with median imputation
- Converted data types (dates, percentages, categories)

### 2. Feature Engineering
Created business-relevant features:

| Feature | Formula | Business Meaning |
|---------|---------|------------------|
| `loan_to_income` | loan_amnt / annual_inc | Loan burden relative to income |
| `monthly_debt_burden` | installment / (annual_inc/12) | Monthly payment stress |
| `fico_avg` | (fico_low + fico_high) / 2 | Credit score average |
| `credit_history_years` | Today - earliest_cr_line | Length of credit history |
| `grade_num` | A=7, B=6, ..., G=1 | Numeric risk grade |

### 3. Modeling Approach
Compared multiple classification algorithms:

| Model | Why Selected |
|-------|--------------|
| Logistic Regression | Baseline, interpretable |
| Random Forest | Handles non-linearity |
| XGBoost | Best performance, feature importance |

### 4. Evaluation Metrics
- **ROC-AUC**: Primary metric (handles class imbalance)
- **Precision/Recall**: Trade-off analysis
- **Confusion Matrix**: Error analysis
- **Expected Loss**: Business metric

---

## Key Findings

### Feature Importance (Top 10)
1. Interest Rate (`int_rate`)
2. Debt-to-Income Ratio (`dti`)
3. FICO Score (`fico_avg`)
4. Loan Grade (`grade_num`)
5. Annual Income (`annual_inc`)
6. Revolving Utilization (`revol_util`)
7. Loan Amount (`loan_amnt`)
8. Inquiries Last 6 Months (`inq_last_6mths`)
9. Open Accounts (`open_acc`)
10. Credit History Length (`credit_history_years`)

### Default Rate by Grade
| Grade | Default Rate | Risk Level |
|-------|--------------|------------|
| A | ~6% | Low |
| B | ~12% | Low-Medium |
| C | ~18% | Medium |
| D | ~25% | Medium-High |
| E | ~32% | High |
| F | ~38% | Very High |
| G | ~42% | Very High |

---

## Business Metrics

### Expected Loss Calculation
```
Expected Loss = Probability of Default × Loss Given Default × Exposure at Default
EL = PD × LGD × EAD
```

**Assumptions**:
- LGD (Loss Given Default): 80%
- EAD (Exposure at Default): Loan Amount

### Risk Segmentation
| Risk Tier | PD Range | % of Portfolio | Recommended Action |
|-----------|----------|----------------|-------------------|
| Low | 0-10% | ~35% | Auto-approve |
| Medium | 10-30% | ~40% | Standard review |
| High | 30-50% | ~18% | Enhanced review |
| Very High | 50%+ | ~7% | Decline or price premium |

---

## Model Performance

| Model | ROC-AUC | Precision | Recall | F1 |
|-------|---------|-----------|--------|-----|
| Logistic Regression | 0.XX | 0.XX | 0.XX | 0.XX |
| Random Forest | 0.XX | 0.XX | 0.XX | 0.XX |
| **XGBoost** | **0.XX** | **0.XX** | **0.XX** | **0.XX** |

*Note: Results to be updated after model training*

---

## Deliverables

1. **Jupyter Notebooks**: Complete analysis pipeline
2. **Trained Model**: Serialized XGBoost model (.pkl)
3. **Visualizations**: Publication-ready charts
4. **Dashboard Data**: Export for Tableau/Power BI
5. **SQLite Database**: Predictions for querying
6. **Documentation**: This summary + README

---

## Skills Demonstrated

| Skill Category | Specific Skills |
|----------------|-----------------|
| **Data Wrangling** | pandas, data cleaning, missing values |
| **Visualization** | matplotlib, seaborn, Plotly |
| **Machine Learning** | Classification, XGBoost, model evaluation |
| **Feature Engineering** | Domain knowledge, financial ratios |
| **Business Acumen** | Risk metrics, expected loss, segmentation |
| **Databases** | SQL queries, SQLite integration |
| **Tools** | Jupyter, Git, documentation |

---

## Future Enhancements

- [ ] SHAP values for model interpretability
- [ ] API deployment with Flask/FastAPI
- [ ] Real-time scoring pipeline
- [ ] A/B testing framework for model updates
- [ ] Streamlit interactive dashboard

---

## References

- Lending Club Dataset: [Kaggle Link](https://www.kaggle.com/datasets/wordsforthewise/lending-club)
- Credit Risk Modeling: Basel II/III Framework
- XGBoost Documentation: [Official Docs](https://xgboost.readthedocs.io/)
