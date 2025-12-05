# Credit Risk Assessment Model

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3+-orange.svg)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow.svg)

A machine learning model to predict loan default probability using Lending Club data (2007-2018). This project demonstrates end-to-end credit risk modeling with business metrics calculation and interactive dashboards.

## 🎯 Project Objectives

- Predict loan default probability using classification algorithms
- Engineer financial features (debt-to-income, credit utilization, etc.)
- Calculate business metrics: Expected Loss, Risk-Adjusted Returns
- Build interactive risk segmentation dashboard
- Deploy model with interpretable results

## 📊 Dataset

- **Source**: [Lending Club Loan Data](https://www.kaggle.com/datasets/wordsforthewise/lending-club)
- **Period**: 2007-2018
- **Sample Size**: 250,000 loans (stratified sample)
- **Target**: Loan default (binary classification)
- **Default Rate**: ~21%

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| **Data Processing** | pandas, NumPy |
| **Visualization** | matplotlib, seaborn, Plotly |
| **Machine Learning** | scikit-learn, XGBoost |
| **Database** | SQLite, PostgreSQL |
| **Dashboard** | Tableau / Power BI |
| **Environment** | Jupyter Notebook, Git |

## 📁 Project Structure

```
credit-risk-model/
├── data/
│   ├── raw/                    # Original Lending Club data
│   └── processed/              # Cleaned and featured data
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_modeling.ipynb
│   └── 05_business_metrics.ipynb
├── models/
│   └── xgboost_model.pkl       # Trained model
├── images/
│   ├── correlation_heatmap.png
│   ├── default_by_grade.png
│   └── roc_curve.png
├── README.md
├── requirements.txt
├── PROJECT_SUMMARY.md
└── EXECUTION_GUIDE.md
```

## 🚀 Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/credit-risk-model.git
cd credit-risk-model
```

### 2. Create virtual environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run notebooks in order
```bash
jupyter notebook notebooks/
```

## 📈 Key Results

| Metric | Value |
|--------|-------|
| ROC-AUC Score | 0.XX |
| Precision | 0.XX |
| Recall | 0.XX |
| Expected Loss Reduction | XX% |

## 🔍 Feature Importance

Top predictors of loan default:
1. **Interest Rate** - Higher rates correlate with higher default
2. **Debt-to-Income Ratio** - Financial stress indicator
3. **FICO Score** - Credit worthiness measure
4. **Loan Grade** - Lending Club's risk assessment
5. **Credit Utilization** - Revolving credit usage

## 💼 Business Impact

- **Risk Segmentation**: Categorized loans into Low/Medium/High/Very High risk tiers
- **Expected Loss Calculation**: Portfolio-level risk quantification
- **Recommendations**: Data-driven lending threshold suggestions

## 📊 Visualizations

### Default Rate by Loan Grade
![Default by Grade](images/default_by_grade.png)

### ROC Curve Comparison
![ROC Curve](images/roc_curve.png)

## 🔮 Future Improvements

- [ ] Implement SHAP values for model interpretability
- [ ] Add real-time prediction API with Flask/FastAPI
- [ ] Integrate with PostgreSQL for production database
- [ ] Create Streamlit dashboard for interactive exploration

## 👤 Author

**Makuochukwu**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your LinkedIn](https://linkedin.com/in/yourprofile)

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

*This project is part of my Data Science Portfolio demonstrating skills in machine learning, financial analysis, and business intelligence.*
