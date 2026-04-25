# Earnings Prediction Engine V1

This project is a learning-focused quantitative research prototype. It builds a simple machine learning pipeline that predicts whether a company will beat, meet, or miss consensus EPS expectations around earnings announcements.

The project intentionally uses free data through `yfinance`, so it is not a production-grade substitute for WRDS, I/B/E/S, Compustat, or CRSP. The goal is to practice the research workflow: define a target, collect imperfect data, engineer pre-announcement features, train with time-aware splits, and evaluate whether the signal is structurally useful.

## Project Structure

```text
notebooks/
  01_earnings_prediction_v1.ipynb
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

1. Download earnings and price data with `yfinance`.
2. Build a company-quarter dataset.
3. Create beat, meet, and miss labels from EPS surprise.
4. Engineer historical earnings and technical features.
5. Train baseline and machine learning classifiers using time-based splits.
6. Evaluate classification metrics and quant-style quintile hit rates.
7. Save the processed dataset to `data/processed/earnings_features_v1.csv`.

## Data Limitations

Free data has serious limitations:

- Historical analyst revision data is not available in the same quality as I/B/E/S.
- `yfinance` earnings history availability varies by ticker and can change over time.
- Fundamental statement history is limited and not as clean as Compustat.
- The universe does not fully handle survivorship bias.
- Options-implied volatility, short interest, and earnings premium features are excluded from V1.

Because of this, the right question for V1 is not "can this trade live capital?" The right question is "does this pipeline correctly test whether there is signal?"

## V2 Ideas

- Add WRDS I/B/E/S analyst revisions and estimate dispersion.
- Add Compustat quarterly fundamentals with point-in-time handling.
- Add CRSP returns and delisting-aware universe construction.
- Add abnormal return targets around earnings announcements.
- Add XGBoost or LightGBM after the baseline pipeline is stable.
