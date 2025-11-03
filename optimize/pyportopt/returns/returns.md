Certainly! Here's the extracted page content including all methods, parameters, returns, return types, and any mathematical formulas provided:

---

# Expected Returns

Mean-variance optimization requires knowledge of the expected returns. In practice, these are difficult to know with certainty, so estimates are used, such as extrapolating historical data. Getting the correct inputs is crucial, and providing expected returns can sometimes do more harm than good. It's often suggested to focus on an appropriate risk model. The `expected_returns` module provides functions for estimating the expected returns of the assets, usually assuming annual returns output, and daily prices input (modifiable via `frequency` parameter).

Currently implemented methods:
- General return model function allowing the use of any return model.
- Mean historical return.
- Exponentially weighted mean historical return.
- CAPM (Capital Asset Pricing Model) estimate of returns.

Additionally, utility functions are provided to convert between returns and prices.

### Methods

1. **mean_historical_return**

   - **Parameters:**
     - **prices** (`pd.DataFrame`): Adjusted closing prices, with each row a date and each column a ticker/id.
     - **returns_data** (`bool`, defaults to `False`): If true, the first argument is returns instead of prices. These should not be log returns.
     - **compounding** (`bool`, defaults to `True`): Computes geometric mean returns if True, arithmetic otherwise.
     - **frequency** (`int`, optional): Number of periods in a year, defaults to 252 (trading days).
     - **log_returns** (`bool`, defaults to `False`): Whether to compute using log returns.
   
   - **Returns:** Annualised mean (daily) return for each asset.
   - **Return type:** `pd.Series`

2. **ema_historical_return**

   - **Parameters:**
     - **prices** (`pd.DataFrame`): Adjusted closing prices, with each row a date and each column a ticker/id.
     - **returns_data** (`bool`, defaults to `False`): If true, the first argument is returns instead of prices. These should not be log returns.
     - **compounding** (`bool`, defaults to `True`): Computes geometric mean returns if True, arithmetic otherwise.
     - **frequency** (`int`, optional): Number of periods in a year, defaults to 252.
     - **span** (`int`, optional): The time-span for the EMA, defaults to 500-day EMA.
     - **log_returns** (`bool`, defaults to `False`): Whether to compute using log returns.
   
   - **Returns:** Annualised exponentially-weighted mean (daily) return of each asset.
   - **Return type:** `pd.Series`

3. **capm_return**

   - **Formula:** Under CAPM, \( R_i = R_f + \beta_i (E(R_m) - R_f) \)
   - **Parameters:**
     - **prices** (`pd.DataFrame`): Adjusted closing prices, with each row a date and each column a ticker/id.
     - **market_prices** (`pd.DataFrame`, optional): Adjusted closing prices of the benchmark, defaults to None.
     - **returns_data** (`bool`, defaults to `False`): If true, the first arguments are returns instead of prices.
     - **risk_free_rate** (`float`, optional): Risk-free rate, defaults to 0.02.
     - **compounding** (`bool`, defaults to `True`): Computes geometric mean returns if True, arithmetic otherwise.
     - **frequency** (`int`, optional): Number of periods in a year, defaults to 252.
     - **log_returns** (`bool`, defaults to `False`): Whether to compute using log returns.
   
   - **Returns:** Annualised return estimate.
   - **Return type:** `pd.Series`

4. **returns_from_prices**

   - **Parameters:**
     - **prices** (`pd.DataFrame`): Adjusted closing prices, each row a date and each column a ticker/id.
     - **log_returns** (`bool`, defaults to `False`): Whether to compute using log returns.
   
   - **Returns:** (Daily) returns.
   - **Return type:** `pd.DataFrame`

5. **prices_from_returns**

   - **Parameters:**
     - **returns** (`pd.DataFrame`): (Daily) percentage returns of the assets.
     - **log_returns** (`bool`, defaults to `False`): Whether to compute using log returns.
   
   - **Returns:** (Daily) pseudo-prices.
   - **Return type:** `pd.DataFrame`

--- 

These methods and their parameters assist in calculating expected returns, each providing different approaches and nuances suitable for varying situations in financial analysis and portfolio optimization.
