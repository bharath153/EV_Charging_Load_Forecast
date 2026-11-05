# Technical Notes — EV Charging Load Forecasting

## Purpose

This repository demonstrates time-series feature engineering and supervised forecasting for synthetic EV fleet-depot charging demand.

## Data

An hourly synthetic demand series is generated with calendar and load-pattern structure.

## Features

The supervised model uses engineered predictors such as:
- hour of day;
- day of week;
- recent demand lags;
- 24-hour rolling mean and standard deviation;
- same-hour previous-week demand.

## Model

The implementation uses scikit-learn's `GradientBoostingRegressor`.

It is **not a Temporal Fusion Transformer**.

## Evaluation

A chronological holdout split is used for forecast evaluation. Saved metrics include R², RMSE and MAPE.

## Limitations

The dataset is synthetic and omits many factors relevant to real charging demand, including fleet schedules, tariff response, weather, charger availability and holidays. A production study would require time-aware backtesting on measured data and calibrated forecast uncertainty.
