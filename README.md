# Forecasting Rainfall with Random Forests and Proportional Lag Subsetting  
**PSTAT 274+231 Final Project — UC Santa Barbara**  
Adarsh Nagar | Brooks Piper

---

## Overview

This project explores a graduate-level, data-driven investigation into modern time series forecasting. Leveraging a hybrid methodology that incorporates the **Random Forest** algorithm and proportional lag-based feature engineering, we rigorously benchmark performance against traditional econometric models such as **Box-Jenkins ARIMA** and **Auto-ARIMA**.

Our empirical results, drawn from 7 years of rainfall data (2017–2024) from the **BGC Jena Weather Station**, reveal that **Random Forest models trained on only 5–10% of available lags significantly outperform classic statistical models**, challenging the dominant paradigms in stochastic modeling.

---

## Motivation

Despite the dominance of ARIMA/SARIMA frameworks in time series forecasting, these models are **parametrically brittle**, often suffering under real-world violations such as heteroskedasticity, non-stationarity, and seasonal complexity.

Inspired by Tyralis & Papacharalampous (2017), we rigorously test the hypothesis that **smaller subsets of lagged inputs** can yield superior generalization performance when embedded in **non-parametric tree-based learners**, particularly Random Forests.

---

## Data & Preprocessing

- **Source**: [BGC Jena Weather Dataset (Kaggle)](https://www.kaggle.com/datasets/matthewjansen/bgc-jena-weather-station-dataset-20172024)
- **Sampling**: Hourly → Monthly mean aggregation (to mitigate noise and reduce overfitting risk)
- **Target Variable**: `Rainfall (mm)`
- **Total Points**: 86 monthly observations from 2017 to 2024

---

## Methodology

### 1. **Random Forest with Lag Proportionality**
- Engineered lagged features from time series
- Trained models with varying lag proportions: 5%, 10%, ..., 50%
- Feature selection via **permutation importance**
- Final RF model fit only on features with non-zero importance

### 2. **Box-Jenkins (Manual ARIMA/SARIMA)**
- ACF & PACF used to select ARIMA and SARIMAX model orders
- Compared models using AIC and Ljung-Box residual diagnostics

### 3. **Auto ARIMA**
- Automatically tuned via stepwise AIC optimization
- Benchmarked for convenience and model performance

---

## Results

| Method                  | Mean Squared Error (Test) |
|------------------------|---------------------------|
| **Random Forest (5%)** | **0.000034**              |
| Random Forest (10%)    | 0.000035                  |
| Auto ARIMA             | 0.000037                  |
| Box-Jenkins SARIMA     | 0.000042                  |
| Random Forest (25%)    | 0.000047                  |

### Insight
The **5% lag Random Forest** outperformed all competitors. Surprisingly, **smaller proportions of input data** led to better results, supporting the hypothesis that **model parsimony can outperform complexity when paired with intelligent subsetting**.

---

## Academic Rigor

This project synthesizes methods from:
- **Machine Learning**: Ensemble modeling, variable importance, and out-of-bag validation
- **Classical Statistics**: Time series diagnostics (ACF/PACF), ARIMA modeling, heteroskedasticity testing
- **Stochastic Processes**: Forecasting over temporal domains with recursive structures

We treated model comparison as a controlled experiment, ensuring identical forecast windows, fair resampling strategies, and interpretable metric comparisons (e.g., MSE under fixed scales).

---

## References

1. Tyralis, H., & Papacharalampous, G. (2017). *Variable Selection in Time Series Forecasting Using Random Forests*. Algorithms, 10(4), 114.  
2. Engle, R. F. (1982). *Autoregressive Conditional Heteroskedasticity*. Econometrica, 50(4), 987–1007.  
3. Jansen, M. (2024). *BGC Jena Weather Dataset (2017–2024)*. Kaggle.  

> *"Progress, in science and in life, requires not just the ability to model the world — but to reimagine it."* — A.N.

---
