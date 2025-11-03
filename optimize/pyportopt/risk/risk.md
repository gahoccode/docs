Here's the extracted page content from the provided context, including all relevant methods, parameters, returns, return types, and mathematical formulas:

---

### Risk Models

In addition to expected returns, mean-variance optimization requires a **risk model**. The covariance matrix is the most commonly-used risk model, describing asset volatilities and their co-dependence. Historical variance is generally more persistent than mean historical returns, which makes risk models crucial.

#### Covariance Matrix Estimation Methods

- **Sample Covariance Matrix**
  - **Parameters:**
    - `prices` (_pd.DataFrame_): Adjusted closing prices, with each row as a date and each column as a ticker/id.
    - `returns_data` (_bool_): Set this to `True` if passing returns instead of prices.
    - `frequency` (_int_): Number of periods in a year, defaults to 252.
    - `log_returns` (_bool_): Whether to compute using log returns.
  - **Returns:** Annualised sample covariance matrix.
  - **Return type:** `pd.DataFrame`
  - **Note:** It is unbiased but lacks robustness. Not recommended as the default choice.

- **Semicovariance Matrix**
  - **Parameters:**
    - `prices`, `returns_data`, `frequency`, `log_returns` (same as Sample Covariance).
    - `benchmark` (_float_): Benchmark return, defaults to daily risk-free rate.
  - **Returns:** Semicovariance matrix.
  - **Return type:** `pd.DataFrame`
  - **Formula:** Given Estrada's implementation:
    \[
    \frac{1}{n}\sum_{i = 1}^n \sum_{j = 1}^n \min \left( r_i, B \right) \min \left( r_j, B \right)
    \]

- **Exponentially Weighted Covariance Matrix**
  - **Parameters:**
    - `prices`, `returns_data`, `frequency`, `log_returns` (same as Sample Covariance).
    - `span` (_int_): Defaults to 180.
  - **Returns:** Annualised exponential covariance matrix.
  - **Return type:** `pd.DataFrame`

- **Shrinkage Methods (via `CovarianceShrinkage` class)**
  - **Parameters on Initialization:**
    - `prices`, `returns_data`, `frequency`, `log_returns` (same as Sample Covariance).
  - **Methods:**
    - `ledoit_wolf`: Calculate Ledoit-Wolf shrinkage estimate.
      - **Parameters:**
        - `shrinkage_target` (_str_): `constant_variance`, `single_factor`, or `constant_correlation`.
      - **Returns:** Shrunk sample covariance matrix.
      - **Return type:** `np.ndarray`

    - `oracle_approximating`: Calculate Oracle Approximating Shrinkage estimate.
      - **Returns:** Shrunk sample covariance matrix.
      - **Return type:** `np.ndarray`

- **Mathematical Formulation for Shrinkage:**
  - Formula: 
  \[
  \hat{\Sigma} = \delta F + (1-\delta) S
  \]
  - Where \( \delta \) is the shrinkage constant, \( F \) is the shrinkage target, and \( S \) is the sample covariance matrix.

- **Conversion Between Covariance and Correlation:**
  - `cov_to_corr`
    - **Parameters:**
      - `cov_matrix` (_pd.DataFrame_): Covariance matrix.
    - **Returns:** Correlation matrix.
    - **Return type:** `pd.DataFrame`

  - `corr_to_cov`
    - **Parameters:**
      - `corr_matrix` (_pd.DataFrame_): Correlation matrix.
      - `stdevs` (_array-like_): Vector of standard deviations.
    - **Returns:** Covariance matrix.
    - **Return type:** `pd.DataFrame`

#### Additional Utilities
- **Fix Non-Positive Semidefinite Matrices:**
  - `fix_nonpositive_semidefinite`
    - **Parameters:**
      - `matrix` (_pd.DataFrame_): Raw covariance matrix.
      - `fix_method` (_str_): "spectral" or "diag".
    - **Returns:** Positive semidefinite covariance matrix.
    - **Return type:** `pd.DataFrame`

#### References
- [1] Kritzman, Page & Turkington (2010)
- [2] Estrada (2006)
- [3] Ledoit & Wolf (2003)
- [4] Ledoit & Wolf (2001)
- [5] Chen et al. (2010)

---

This organized content summarizes the key elements related to risk models in the PyPortfolioOpt library.
