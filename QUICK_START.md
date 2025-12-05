# Quick Start Guide

Get the Credit Risk Model running in 5 minutes.

---

## 1. Setup (2 min)

```bash
# Clone and enter project
git clone https://github.com/yourusername/credit-risk-model.git
cd credit-risk-model

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

---

## 2. Get Data (1 min)

Download from [Kaggle](https://www.kaggle.com/datasets/wordsforthewise/lending-club) and place in:
```
data/raw/accepted_2007_to_2018Q4.csv
```

---

## 3. Run Notebooks (2 min)

```bash
jupyter notebook notebooks/
```

Execute in order:
1. `01_data_cleaning.ipynb` → Creates cleaned dataset
2. `02_eda.ipynb` → Generates visualizations
3. `03_feature_engineering.ipynb` → Creates features
4. `04_modeling.ipynb` → Trains models
5. `05_business_metrics.ipynb` → Calculates risk metrics

---

## 4. View Results

- **Model**: `models/xgboost_model.pkl`
- **Visualizations**: `images/` folder
- **Dashboard Data**: `data/processed/risk_dashboard_data.csv`

---

## Key Commands

| Task | Command |
|------|---------|
| Start Jupyter | `jupyter notebook` |
| Run all notebooks | Use "Run All" in each notebook |
| Save model | Automatic in notebook |
| Export for Tableau | CSV in `data/processed/` |

---

## Need Help?

See [EXECUTION_GUIDE.md](EXECUTION_GUIDE.md) for detailed instructions.
