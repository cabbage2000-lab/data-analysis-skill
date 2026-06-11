# Time-Series Analysis & Forecasting

Load when the data has a time dimension and the user needs trend analysis or forecasting.

## Method Tiers (choose in this order; do not bring in heavier methods)

| Tier | Method | When |
|------|------|------|
| Default | Exponential smoothing (Holt-Winters), ARIMA / SARIMA (statsmodels) | The vast majority of business series; interpretable, stable on small data |
| Optional | Prophet | Pronounced holiday/multi-seasonal effects and prophet is already installed |
| Never | LSTM and other deep learning | Heavy dependencies; no better than classical methods on small data (explicitly excluded by requirements) |

## Pre-Forecast Checks (fail → degrade to trend description)

1. **Number of points**: monthly series < 24 points, weekly < 52 → **no model forecasting**; describe trend and seasonality only, and say why (sample too small to estimate seasonal terms stably)
2. **Gaps & frequency**: is the time index evenly spaced, any missing months? Fill gaps or resample first, and record it in the Data Processing Notes
3. **Structural breaks**: level shifts visible to the eye (product revamp, pandemic) → annotate them in the report; consider modeling only the post-break data
4. **Stationarity**: run an ADF test before ARIMA; difference as needed

## Standard Flow

1. Resample to the analysis granularity (day/week/month) → 2. STL decomposition (trend/seasonal/residual; the decomposition plot goes into the report) → 3. Fit the chosen model → 4. Residual diagnostics (Ljung-Box) → 5. Forecast + **confidence intervals**

Forecasts must carry intervals: "next 3 months forecast X (95% interval [L, U])". A point forecast alone is not acceptable. Forecast horizon must not exceed 1/4 of the history length; beyond that, state the extrapolation risk.

## Exponential Smoothing Example (statsmodels)

```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing
# Monthly data, yearly seasonality; fall back to trend-only when the sample covers < 2 full seasonal cycles
model = ExponentialSmoothing(series, trend="add", seasonal="add", seasonal_periods=12).fit()
forecast = model.forecast(3)
```

## Dependency Degradation

statsmodels missing and pip install fails: skip ARIMA/exponential smoothing; describe the trend with moving averages + YoY/MoM tables instead, and state in the report "why no model forecast was made".
