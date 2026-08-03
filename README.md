# Time Series Analysis: Forecasting Toulouse Temperatures

> ** Note:** This README provides an English overview of the project. The comprehensive academic report (`TimeSeries.pdf`) is written in **French**.

## Academic Context
This research project was conducted during our **M1 in Applied Mathematics (4th year)** at INSA Toulouse, as part of the "Reading Seminar" course.
*   **Authors:** Amélie Monzie, Léo Parnotte, & Jules Voegtlé
*   **Supervisor:** Prof. Cathy Maugis-Rabusseau

---

## Project Overview
This study focuses on modeling and forecasting the monthly average temperatures in Toulouse (France) from 1947 to 2020, using data from the National Centers for Environmental Information. The dataset exhibits a clear upward trend and strong annual seasonality.

The core objective is to compare the predictive performances and limitations of two distinct time series forecasting methodologies:
1.  **Additive Decomposition** followed by ARMA modeling of the residuals.
2.  **Stationarization via Differentiation** followed by SARIMA modeling[cite: 2].

---

## Methodologies & Mathematical Modeling

### 1. Additive Decomposition & ARMA
We first modeled the time series $Y_t$ using an additive approach:

$$Y_t = m_t + s_t + X_t$$

*   **Trend ($m_t$):** Estimated using a moving average $M_{2q}$ (with period $2q=12$).
*   **Seasonality ($s_t$):** Estimated by averaging the trend-corrected monthly data.
*   **Residual Noise ($X_t$):** After verifying stationarity (Dickey-Fuller & KPSS tests) and rejecting the white noise hypothesis (Ljung-Box test), we identified the best-fitting ARMA model minimizing AIC/BIC criteria, resulting in an **ARMA(3,2)** model.
*   **Forecasting:** The future trend was extrapolated using constant, B-splines, and penalized polynomial methods to simulate different climate growth scenarios.

### 2. Differentiation & SARIMA
To directly address non-stationarity, we applied a seasonal differentiation (period $r=12$) to eliminate the annual seasonality and linear trend:

$$\nabla_{12}Y_t = (1 - B^{12})Y_t$$

Based on the Box-Jenkins methodology (ACF/pACF analysis) and information criteria evaluation, we selected and validated the **$SARIMA(2,0,1)(0,1,1)_{12}$** model.

---

## Key Findings & Forecasts (up to 2035)

Both methods performed exceptionally well for short-term validation (successfully predicting the year 2020 within the 95% confidence interval). However, long-term forecasting revealed distinct behaviors:
*   **SARIMA:** Provided a highly conservative and stable forecast, essentially replicating historical dynamics without projecting extreme future trend growth.
*   **Additive Model (Splines & Penalized Polynomials):** Proved highly valuable for exploring different physical climate change scenarios. The B-spline extrapolation highlighted a "maximum growth" scenario (approx. $+1.5^\circ C$ in 15 years), while the penalized polynomial offered a moderate, realistic growth scenario ($+0.5^\circ C$).
