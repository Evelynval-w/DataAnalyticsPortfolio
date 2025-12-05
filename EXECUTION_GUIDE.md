# Execution Guide: Credit Risk Assessment Model

This guide walks through the complete project execution from raw data to final results.

---

## Prerequisites

### Software Requirements
- Python 3.9 or higher
- Jupyter Notebook
- Git (for version control)
- Tableau Public or Power BI (optional, for dashboards)

### Hardware Recommendations
- RAM: 8GB minimum (16GB recommended for full dataset)
- Storage: 2GB free space

---

## Step 1: Environment Setup

### 1.1 Clone Repository
```bash
git clone https://github.com/yourusername/credit-risk-model.git
cd credit-risk-model
```

### 1.2 Create Virtual Environment
```bash
# Create environment
python -m venv venv

# Activate (Mac/Linux)
source venv/bin/activate

# Activate (Windows)
venv\Scripts\activate
```

### 1.3 Install Dependencies
```bash
pip install -r requirements.txt
```

---

## Step 2: Data Preparation

### 2.1 Download Data
1. Go to [Kaggle Lending Club Dataset](https://www.kaggle.com/datasets/wordsforthewise/lending-club)
2. Download the CSV file(s)
3. Place in `data/raw/` folder

### 2.2 Data Cleaning
Run the data cleaning notebook or script:
```bash
jupyter notebook notebooks/01_data_cleaning.ipynb
```

**Key Operations**:
- Load raw data
- Select relevant columns (30 of 145)
- Filter to completed loans
- Create target variable
- Stratified sampling (250k rows)
- Handle missing values
- Save to `data/processed/lending_club_cleaned.csv`

---

## Step 3: Exploratory Data Analysis

Run EDA notebook:
```bash
jupyter notebook notebooks/02_eda.ipynb
```

**Visualizations Created**:
- Target distribution (default vs. fully paid)
- Default rate by loan grade
- Correlation heatmap
- Feature distributions
- Geographic analysis

**Output**: Images saved to `images/` folder

---

## Step 4: Feature Engineering

Run feature engineering notebook:
```bash
jupyter notebook notebooks/03_feature_engineering.ipynb
```

**Features Created**:
| Feature | Description |
|---------|-------------|
| `loan_to_income` | Loan amount / Annual income |
| `monthly_debt_burden` | Monthly payment / Monthly income |
| `fico_avg` | Average of FICO range |
| `credit_history_years` | Years since first credit line |
| `grade_num` | Numeric encoding of grade (A=7 to G=1) |

---

## Step 5: Model Training

Run modeling notebook:
```bash
jupyter notebook notebooks/04_modeling.ipynb
```

### 5.1 Data Splitting
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)
```

### 5.2 Models Trained
1. **Logistic Regression** (baseline)
2. **Random Forest** (ensemble)
3. **XGBoost** (gradient boosting)

### 5.3 Hyperparameter Tuning
```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    'max_depth': [3, 5, 7],
    'n_estimators': [100, 200],
    'learning_rate': [0.01, 0.1]
}
```

### 5.4 Save Best Model
```python
import joblib
joblib.dump(best_model, 'models/xgboost_model.pkl')
```

---

## Step 6: Model Evaluation

### 6.1 Metrics Computed
- ROC-AUC Score
- Precision, Recall, F1-Score
- Confusion Matrix
- Classification Report

### 6.2 Visualizations
- ROC Curve comparison
- Precision-Recall Curve
- Feature Importance plot
- Confusion Matrix heatmap

---

## Step 7: Business Metrics

Run business metrics notebook:
```bash
jupyter notebook notebooks/05_business_metrics.ipynb
```

### 7.1 Expected Loss Calculation
```python
# Expected Loss = PD × LGD × EAD
avg_loan = df['loan_amnt'].mean()
lgd = 0.80  # 80% loss given default

df['expected_loss'] = df['default_prob'] * lgd * avg_loan
```

### 7.2 Risk Segmentation
```python
df['risk_tier'] = pd.cut(
    df['default_prob'],
    bins=[0, 0.1, 0.3, 0.5, 1.0],
    labels=['Low', 'Medium', 'High', 'Very High']
)
```

### 7.3 Portfolio Summary
Generate portfolio-level risk metrics and recommendations.

---

## Step 8: Database Integration

### 8.1 Create SQLite Database
```python
import sqlite3

conn = sqlite3.connect('data/processed/credit_risk.db')
df_predictions.to_sql('loan_predictions', conn, if_exists='replace')
```

### 8.2 Sample Queries
```sql
-- Default rate by risk tier
SELECT risk_tier, 
       COUNT(*) as loan_count,
       AVG(default_prob) as avg_pd,
       SUM(expected_loss) as total_el
FROM loan_predictions
GROUP BY risk_tier;
```

---

## Step 9: Dashboard Creation

### Option A: Tableau
1. Connect to `data/processed/risk_dashboard_data.csv`
2. Create visualizations:
   - Risk tier distribution
   - Expected loss by segment
   - Geographic risk map
   - Default rate trends

### Option B: Power BI
1. Import CSV data
2. Build dashboard with similar visualizations

---

## Step 10: Documentation & Git

### 10.1 Update README
Add final results and metrics to README.md

### 10.2 Git Workflow
```bash
# Stage changes
git add .

# Commit with message
git commit -m "Complete credit risk model with 0.XX AUC"

# Push to GitHub
git push origin main
```

---

## Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| Memory error loading data | Use `pd.read_csv(chunksize=50000)` or sample |
| XGBoost not installing | Try `pip install xgboost --no-cache-dir` |
| Jupyter not finding kernel | Run `python -m ipykernel install --user` |
| Date parsing errors | Check date format matches `%b-%y` |

### Getting Help
- Check pandas/sklearn documentation
- Stack Overflow for specific errors
- Open an issue on the GitHub repository

---

## Execution Checklist

- [ ] Environment setup complete
- [ ] Raw data downloaded and placed in `data/raw/`
- [ ] Data cleaning notebook executed
- [ ] EDA notebook executed with visualizations saved
- [ ] Feature engineering complete
- [ ] Models trained and evaluated
- [ ] Best model saved to `models/`
- [ ] Business metrics calculated
- [ ] SQLite database created
- [ ] Dashboard built (Tableau/Power BI)
- [ ] README updated with results
- [ ] Code pushed to GitHub

---

## File Outputs

After complete execution, you should have:

```
data/processed/
├── lending_club_cleaned.csv
├── risk_dashboard_data.csv
└── credit_risk.db

models/
└── xgboost_model.pkl

images/
├── target_distribution.png
├── correlation_heatmap.png
├── default_by_grade.png
├── roc_curve.png
└── feature_importance.png
```
