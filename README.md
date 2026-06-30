# Uncertainty-Aware Portfolio Optimization using Machine Learning

## Overview

This project develops a machine learning pipeline for predicting short-term stock movements and demonstrates how prediction uncertainty can be incorporated into portfolio construction. Using historical NIFTY-50 data, Gradient Boosting models are trained to estimate the probability of positive future returns. Multiple bootstrapped models are then used to quantify predictive uncertainty through ensemble disagreement, which serves as a measure of confidence in the model's forecasts.

The notebook also compares a simple long-short strategy with an equal-weight benchmark.

---

## Features

- Feature engineering using historical price and volume data
- Time-aware expanding-window cross-validation
- Gradient Boosting Classifier for stock movement prediction
- Hyperparameter tuning
- Feature selection using Permutation Importance
- Uncertainty estimation using bootstrap ensembles
- Long-short portfolio construction
- Performance comparison with an equal-weight benchmark

---

## Dataset

The project uses historical **NIFTY-50** stock data containing:

- Date
- Symbol
- Closing Price
- Trading Volume

The target variable indicates whether the **21-day forward return** is positive.

---

## Methodology

### Feature Engineering

The following features are generated:

- 5-day return
- 21-day return
- 63-day return
- 21-day rolling volatility
- 63-day rolling volatility
- Price relative to 52-week high
- Price relative to 52-week low
- Volume Z-score

The prediction target is a binary label indicating whether the stock's forward 21-day return is positive.

### Model Training

A **Gradient Boosting Classifier** is trained using an expanding-window validation strategy to avoid look-ahead bias. Hyperparameters including the number of estimators, learning rate, and tree depth are tuned using validation ROC-AUC.

### Feature Selection

Permutation Importance is used to identify the most informative predictors. The model is also retrained using the top-ranked features for comparison.

### Uncertainty Estimation

Prediction uncertainty is estimated by training multiple bootstrapped Gradient Boosting models.

For each prediction:

- Mean probability represents the predicted confidence.
- Standard deviation across ensemble predictions represents predictive uncertainty.

### Portfolio Construction

Stocks are ranked according to predicted probabilities.

- Top decile → Long positions
- Bottom decile → Short positions

Portfolio returns are compared against an equal-weight benchmark using cumulative return curves.

---

## Results

The notebook reports:

- Cross-validation ROC-AUC
- Test ROC-AUC
- Feature importance rankings
- Comparison between full and reduced feature sets
- Ensemble uncertainty analysis
- Long-short portfolio performance
- Benchmark comparison

---

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Scikit-learn

---

## Repository Structure

```text
.
├── Assn3.ipynb
├── NIFTY50_all.csv
├── README.md
└── requirements.txt
```

---

## Future Improvements

- Regression-based return prediction
- Probabilistic calibration
- Transaction cost modelling
- Risk-adjusted portfolio optimization
- Dynamic position sizing based on uncertainty
- Walk-forward backtesting

---

## Author

**Arunima**  
Department of Mathematics and Scientific Computing  
Indian Institute of Technology Kanpur
