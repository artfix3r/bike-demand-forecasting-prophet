# 🚲 Bike Demand Forecasting with Facebook Prophet

A complete time series forecasting pipeline for predicting daily bike-sharing 
demand using Facebook Prophet, enriched with weather features, holiday effects, 
lag-based feature engineering, cross-validation, and hyperparameter tuning.

---

## 📌 Project Overview

This project forecasts daily bike rental counts using the **Capital Bikeshare 
dataset (2011–2012)**. The goal is to build a robust, interpretable forecasting 
model by combining Prophet's built-in seasonality components with external 
regressors capturing weather patterns and temporal dependencies.

---

## 📂 Dataset

- **Source:** Capital Bikeshare System (Washington D.C.)
- **Period:** January 2011 – December 2012
- **Granularity:** Daily
- **Target Variable:** Total bike rentals per day (`y`)

---

## ⚙️ Pipeline Steps

1. **Data Preprocessing**
   - Date parsing and formatting for Prophet (`ds`, `y`)
   - Encoding weather situation into binary features (`weathersit2`, `weathersit3`)

2. **Holiday Engineering**
   - Custom holiday calendar including:
     - Christmas (window: -5 to +3)
     - New Year's Eve (window: -3 to +3)
     - Easter (window: -3 to +3)
     - General US public holidays (window: -2 to +2)

3. **Feature Engineering**
   - Lag features: `temp`, `atemp` at 1, 3, 5, and 7-day lags
   - Captures autocorrelation and short-term seasonal patterns

4. **Model Building**
   - Facebook Prophet with:
     - Yearly and weekly seasonality enabled
     - Custom regressors: `workingday`, `temp`, `atemp`, `hum`, 
       `windspeed`, `weathersit2`, `weathersit3`, lag features

5. **Cross-Validation**
   - Initial training window: 521 days
   - Horizon: 30 days
   - Period: 15 days
   - Metric: **RMSE**

6. **Hyperparameter Tuning**
   - Grid search over:
     - `changepoint_prior_scale`: [0.05, 0.5]
     - `seasonality_prior_scale`: [10, 20]
     - `holidays_prior_scale`: [10, 20]
     - `seasonality_mode`: [additive, multiplicative]
   - Best configuration: `changepoint_prior_scale=0.05`, 
     `seasonality_mode=additive`, `seasonality_prior_scale=20`, 
     `holidays_prior_scale=20` → **RMSE ≈ 981.74**

---

## 📊 Results

| Config | Seasonality Mode | RMSE |
|--------|-----------------|------|
| Best   | Additive        | ~981 |
| Worst  | Multiplicative  | ~2432 |

Additive seasonality significantly outperformed multiplicative mode for 
this dataset.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python | Core language |
| Facebook Prophet | Time series forecasting |
| Pandas | Data manipulation |
| Scikit-learn | Parameter grid generation |
| Google Colab | Development environment |

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/your-username/bike-demand-forecasting-prophet.git
cd bike-demand-forecasting-prophet

# Install dependencies
pip install prophet pandas scikit-learn

# Run the notebook
jupyter notebook bike_demand_prophet_forecasting.ipynb
```

---

## 📁 Repository Structure
bike-demand-forecasting-prophet/
│
├── bike_demand_prophet_forecasting.ipynb # Main notebook
├── data/
│ └── day.csv # Capital Bikeshare dataset
├── README.md
└── requirements.txt


---

## 👤 Author

**Yusif İmamverdiyev**  

[GitHub](https://github.com/artfix3r) · [LinkedIn](https://www.linkedin.com/in/yusif-imamverdiyev/?locale=en)

---

## 📄 License

This project is licensed under the MIT License.
