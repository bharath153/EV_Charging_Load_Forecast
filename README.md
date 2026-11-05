# EV Fleet Charging Load Forecast — Gradient Boosting with Lag Features

> Forecasting synthetic fleet-depot charging demand from calendar and historical-load features

> [!NOTE]
> The repository name is retained for continuity, but the current implementation is **not a Temporal Fusion Transformer**. It uses a `GradientBoostingRegressor` with engineered lag and rolling-window features.

## Overview

This project demonstrates an EV charging-demand forecasting workflow for a synthetic fleet-depot load profile.

The pipeline:
- generates an hourly charging-demand series;
- builds calendar, lag, rolling-mean and rolling-standard-deviation features;
- trains a Gradient Boosting regressor;
- evaluates the holdout forecast;
- visualizes diurnal and weekly demand structure.

## Model

```text
GradientBoostingRegressor
n_estimators = 300
learning_rate = 0.05
max_depth = 5
subsample = 0.8
```

Representative inputs include:
- hour of day;
- day of week;
- recent load lags;
- 24-hour rolling statistics;
- same-hour previous-week demand.

## Data Scope

The charging-demand series is **synthetic**. The project demonstrates forecasting methodology and feature engineering; it is not a production grid-demand forecast and is not trained on utility or fleet-operator data.

## Outputs

The script exports:
- seven-day forecast vs. reference demand;
- hour × weekday load heatmap;
- prediction diagnostics and residuals;
- diurnal load profile;
- R², RMSE and MAPE in `metrics.json`.

## Run

```bash
git clone https://github.com/bharath153/EV_Charging_TFT.git
cd EV_Charging_TFT
pip install -r requirements.txt
python src/train_forecast.py
```

## Repository Structure

```text
EV_Charging_TFT/
├── src/
│   └── train_forecast.py
├── plots/
├── docs/
├── metrics.json
├── requirements.txt
└── README.md
```

## Engineering Interpretation

A production forecasting system would require measured charging sessions, exogenous variables, temporal backtesting, uncertainty calibration, seasonality checks and a deployment-oriented forecasting protocol.
