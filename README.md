# Quantitative Research Practice Projects

This repository contains three learning-focused quantitative research prototypes. The projects are designed to demonstrate practical research workflow: define a target, collect or simulate data, build features, avoid leakage, train models, and evaluate whether a signal is useful out of sample.

The notebooks use free or synthetic data where institutional feeds are unavailable. They are not production trading systems, but they are structured to reflect real quantitative research questions.

## Projects

1. **Earnings Prediction Engine**
   - Predicts whether companies beat, meet, or miss EPS expectations.
   - Uses `yfinance` earnings, price, and limited fundamental data.
   - Evaluates classification metrics, quintile hit rates, and IC-style ranking behavior.

2. **Forecast Combination Framework**
   - Builds a library of base equity signals and combines them with equal weights, inverse-IC-volatility weights, Bayesian-style IC weights, OLS, and ridge regression.
   - Uses strict walk-forward evaluation.
   - Demonstrates shrinkage, signal diagnostics, IC time series, and bias controls.

3. **Closing Auction Distribution Prototype**
   - Models the distribution of final uncross price moves during a closing auction.
   - Uses a synthetic auction message simulator because real auction orderbook data is proprietary.
   - Trains quantile regression models and evaluates prediction interval coverage.

4. **Credit Risk PD Model**
   - Builds a probability of default model using the public German Credit dataset.
   - Compares logistic regression and random forest models.
   - Evaluates ROC-AUC, Brier score, confusion matrix, and PD calibration buckets.

5. **Market Risk VaR and Expected Shortfall**
   - Estimates portfolio Value-at-Risk and Expected Shortfall with historical simulation and parametric methods.
   - Backtests VaR breaches against realized portfolio returns.
   - Demonstrates basic market risk concepts relevant to risk modelling.

## Project Structure

```text
notebooks/
  01_earnings_prediction_v1.ipynb
  02_forecast_combination_v1.ipynb
  03_closing_auction_distribution_v1.ipynb
  04_credit_risk_pd_model_v1.ipynb
  05_market_risk_var_expected_shortfall_v1.ipynb
data/
  raw/
  processed/
requirements.txt
```

## Setup

Create an environment and install dependencies:

```bash
pip install -r requirements.txt
```

Then open:

```text
notebooks/01_earnings_prediction_v1.ipynb
```

Run the notebook from top to bottom. The notebook will:

1. Download or simulate data.
2. Build a research dataset.
3. Engineer features without using future information.
4. Train baseline and machine learning models.
5. Evaluate results with research-style metrics.
6. Save generated datasets to `data/raw/` and `data/processed/`.

## Data Limitations

Free data has serious limitations:

- Historical analyst revision data is not available in the same quality as I/B/E/S.
- `yfinance` earnings history availability varies by ticker and can change over time.
- Fundamental statement history is limited and not as clean as Compustat.
- The universe does not fully handle survivorship bias.
- Options-implied volatility, short interest, and earnings premium features are excluded from V1.
- Real closing auction orderbook feeds are proprietary, so Project 3 uses synthetic auction data.
- The credit risk project uses a small public dataset and is not a regulatory PD model.
- The market risk project is a simplified educational VaR/ES prototype and is not a production risk engine.

Because of this, the right question is not "can this trade live capital?" The right question is "does this pipeline correctly test whether there is signal?"

## V2 Ideas

- Add WRDS I/B/E/S analyst revisions and estimate dispersion.
- Add Compustat quarterly fundamentals with point-in-time handling.
- Add CRSP returns and delisting-aware universe construction.
- Add abnormal return targets around earnings announcements.
- Add XGBoost or LightGBM after the baseline pipeline is stable.
- Add FRED macro variables and regime-conditioned forecast combination.
- Replace synthetic auction data with LOBSTER, TAQ, or exchange/vendor auction messages.
