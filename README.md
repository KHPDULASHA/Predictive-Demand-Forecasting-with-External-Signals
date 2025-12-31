# 📈 Retail Demand Forecasting Engine

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Library](https://img.shields.io/badge/Library-XGBoost-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)

## 📌 Executive Summary
This project implements an end-to-end Machine Learning pipeline to forecast daily product demand for a retail chain. By analyzing 5 years of historical sales data across 10 stores and 50 items, the model predicts future inventory needs to minimize **stockouts** (lost revenue) and **overstocking** (holding costs).

Using **XGBoost** and advanced **Time-Series Feature Engineering**, the model achieves a significant improvement over baseline naive forecasting methods, providing actionable insights for inventory optimization.

---

## 💼 Business Problem
Retail logistics struggle with demand volatility. Traditional methods (moving averages) fail to capture complex patterns like:
* **Seasonality:** Yearly trends (e.g., Summer peaks).
* **Weekly Cycles:** Weekend vs. Weekday purchasing behavior.
* **External Events:** Impact of holidays (Christmas, Black Friday).

**The Goal:** Build a data-driven "Crystal Ball" to predict sales 3 months in advance with high precision.

---

## 🛠️ Technical Approach

### 1. Data Processing & EDA
* **Dataset:** [Store Item Demand Forecasting Challenge](https://www.kaggle.com/c/demand-forecasting-kernels-only/data)
* **Cleaning:** Handled non-stationary data types and date conversions.
* **Analysis:** Visualized seasonal decomposition to confirm yearly and weekly patterns.

### 2. Feature Engineering (The "Secret Sauce")
To transform raw dates into machine-readable signals, I engineered the following features:
* **Lag Features:** `lag_1` (yesterday), `lag_7` (last week), `lag_365` (last year) to capture autocorrelation.
* **Rolling Statistics:** `rolling_mean_7` to capture short-term trend stability.
* **Time Context:** Extracted `day_of_week`, `month`, `quarter`, and `is_weekend`.
* **External Signals:** Integrated US Holiday data using the `holidays` library to flag high-impact event days.

### 3. Model Development
* **Algorithm:** XGBoost Regressor (Gradient Boosting).
* **Validation:** Time-based split (Train: 2013-2016, Test: 2017).
* **Baseline:** Compared against a Naive Forecast (predicting tomorrow = yesterday).

---

## 📊 Results & Evaluation

The model was evaluated using **MAE (Mean Absolute Error)** and **SMAPE** to measure business impact.

| Metric | Baseline (Naive) | XGBoost Model | Improvement |
| :--- | :--- | :--- | :--- |
| **MAE** | 15.20 | **13.05** | ✅ ~14% |
| **RMSE** | 19.50 | **16.80** | ✅ |

> *Interpretation: On average, the model's prediction is within ~13 units of the actual sales count, significantly reducing the risk of inventory mismanagement compared to simple averaging.*

### Feature Importance
The analysis confirmed that **Lag 1** and **Lag 7** are the strongest predictors of future demand, validating the importance of recent sales history.


---

## 🚀 Installation & Usage

### Prerequisites
* Python 3.8+
* Jupyter Notebook

### Setup
1.  **Clone the repository**
    ```bash
    git clone https://github.com/KHPDULASHA/Predictive-Demand-Forecasting-with-External-Signals.git
    cd demand-forecasting
    ```

2.  **Install dependencies**
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn xgboost holidays
    ```

3.  **Run the Notebook**
    Open `DFPR.ipynb` in Jupyter or VS Code to reproduce the analysis.

---

## 🔮 Future Improvements
* **Hyperparameter Tuning:** Implement GridSearch for optimizing XGBoost parameters.
* **Deep Learning:** Experiment with LSTM (Long Short-Term Memory) networks for longer-horizon forecasting.
* **Deployment:** Containerize the model using Docker and serve via a Flask API.

---

## 👤 Author
**Pramudi Dulasha**
* https://www.linkedin.com/in/pramudi-dulasha-53b942294/


_Data Source provided by Kaggle. This project is for educational and portfolio purposes._