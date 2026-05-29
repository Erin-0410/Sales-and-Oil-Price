# Sales Forecasting with Oil Price and Store Data

## Project Overview

This project explores short-term retail sales forecasting using historical sales, store information, promotions, transactions, holidays, and oil price data.

The main goal is to predict future sales by building a clean machine learning workflow. Instead of only focusing on one final model, this project compares several modeling approaches and shows how feature engineering can help traditional machine learning models work better for time-series forecasting.


## Motivation

Accurate sales forecasting can help businesses make better decisions about:

- inventory planning
- staffing
- promotion strategy
- store-level operations
- demand planning

Retail sales are affected by many different factors, including time patterns, holidays, customer traffic, promotions, and external economic signals. This project combines multiple data sources to study those relationships.

## Dataset

The project uses the Corporación Favorita grocery sales dataset.

Main files used:

| File | Description |
| --- | --- |
| `train.csv` | Historical sales by date, store, and product family |
| `test.csv` | Future dates for prediction |
| `stores.csv` | Store metadata such as city, state, type, and cluster |
| `transactions.csv` | Daily transaction count by store |
| `oil.csv` | Daily oil price |
| `holidays_events.csv` | Holiday and event information |


## Project Workflow

1. Load and inspect the data
2. Clean missing oil price values with interpolation
3. Merge sales, store, transaction, oil, and holiday data
4. Explore sales patterns with visualizations
5. Create time-series features
6. Compare multiple models
7. Evaluate predictions using the last 30 days as validation
8. Interpret feature importance
9. Summarize key findings and limitations

## Feature Engineering

Since regular machine learning models do not automatically understand time order, I added time-based and lag-based features.

### Time Features

- year
- month
- day
- day of week
- weekend indicator

### Lag Features

- sales 1 day ago
- sales 7 days ago
- sales 14 days ago
- sales 28 days ago

### Rolling Features

- 7-day rolling mean
- 14-day rolling mean
- 28-day rolling mean

These features help the model learn recent demand, weekly patterns, and short-term sales momentum.

## Models Compared

The notebook compares:

- Naive baseline using previous-day sales
- Linear Regression
- Ridge Regression
- Random Forest
- LightGBM if installed, otherwise Gradient Boosting

The purpose of comparing multiple models is to show the modeling process rather than pretending one model was chosen immediately.

## Evaluation Metrics

The models are evaluated using:

- **MAE**: average size of prediction error
- **RMSE**: penalizes larger errors more heavily
- **R²**: explains how much variation the model captures

The validation set uses the final 30 days of available historical data.

## Key Insights

- Lag features were highly useful because recent sales history gives the model memory.
- Transactions were strongly related to sales and acted as a store traffic signal.
- Time features helped capture weekly and seasonal patterns.
- Oil price was less directly related to daily store sales but still useful as an external feature.
- Tree-based models generally handled nonlinear relationships better than simple linear models.

## Limitations

This project has several limitations:

- The final notebook focuses on Store 16 to keep runtime manageable.
- Transactions may not always be available for true future forecasting.
- Promotion information is simplified.
- Random Forest and boosting models do not naturally model time order without manual lag features.
- External data such as weather, local events, and regional economic indicators were not included.


## Final Summary

This project explored retail sales forecasting using machine learning models and feature engineering on the Corporación Favorita dataset. The results showed that lag features and ensemble models were especially effective at capturing time based sales patterns and improving prediction accuracy compared to simpler forecasting approaches.
