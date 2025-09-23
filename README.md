# Analysis-of-Financial-Time-Series

Python implementations from *Analysis of Financial Time Series* by Ruey S. Tsay, with modifications and additional analyses.

## Overview

This repository provides Python implementations of concepts and examples from Tsay’s book, with enhancements including AR model selection, characteristic roots computation, and cycle length estimation. The code is fully executable using online datasets and does not require local downloads.

Key features:

* **Time Series Visualization**

  * Line plots and scatter plots for exploratory analysis
  * Clear visualization of trends and patterns

* **ACF and PACF Analysis**

  * Autocorrelation and partial autocorrelation function plots
  * Useful for identifying appropriate AR and MA orders

* **AR and ARIMA Modeling**

  * Automatic AR lag selection via AIC
  * Model fitting using `AutoReg` and `ARIMA`
  * Estimation of AR coefficients and standard errors

* **Characteristic Roots and Stochastic Cycles**

  * Computation of characteristic roots of AR models
  * Modulus and frequency analysis
  * Average cycle length estimation in quarters

* **Forecasting**

  * One-step-ahead and multi-step forecasts
  * Forecast evaluation metrics

## Datasets

All datasets are linked directly in the code using URLs; no local downloads are required. Examples include:

* U.S. real GNP growth rates (1947–1991)
* Bitcoin daily prices
* Stock price indices

## Python Packages Used

* `pandas` — data handling
* `numpy` — numerical computations
* `matplotlib` — plotting and visualization
* `statsmodels` — time series modeling (`AutoReg`, `ARIMA`, ACF/PACF, Ljung-Box test)

Install dependencies via pip if needed:

```bash
pip install pandas numpy matplotlib statsmodels
```

## Example Usage

```python
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.ar_model import ar_select_order, AutoReg

# Load dataset
url = "https://faculty.chicagobooth.edu/-/media/faculty/ruey-s-tsay/teaching/fts3/dgnp82.txt"
gnp = pd.read_csv(url, header=None, names=["GNP"])

# Plot the series
plt.plot(gnp["GNP"])
plt.show()

# Select best AR lags
mod = ar_select_order(gnp["GNP"], maxlag=12, ic='aic', old_names=False)
selected_lags = mod.ar_lags

# Fit AR model
res = AutoReg(gnp["GNP"], lags=selected_lags, old_names=False).fit()
print(res.summary())
```

## Notes

* All code has been tested with Python 3.12 and the latest versions of the packages.
* The repository combines examples from Tsay’s book with practical modifications and extensions for modern Python workflows.

## Citation

If you use this repository in research or projects, please cite:

> Tsay, R. S. (2010). *Analysis of Financial Time Series*. 3rd Edition. Wiley.

