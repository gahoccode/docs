# FinQuant: Financial Portfolio Management, Analysis, and Optimization

FinQuant is a Python library designed for financial portfolio management, analysis, and optimization. This documentation details its core functionalities, use cases, and provides explanations of key functions.

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Core Features](#core-features)
4. [Portfolio Management](#portfolio-management)
   - [Building a Portfolio](#building-a-portfolio)
   - [Portfolio Properties](#portfolio-properties)
   - [Portfolio Operations](#portfolio-operations)
5. [Assets](#assets)
   - [Asset Class](#asset-class)
   - [Stock Class](#stock-class)
   - [Market Class](#market-class)
6. [Returns Calculation](#returns-calculation)
   - [Daily Returns](#daily-returns)
   - [Cumulative Returns](#cumulative-returns)
   - [Historical Mean Returns](#historical-mean-returns)
7. [Quantitative Analysis](#quantitative-analysis)
   - [Risk Metrics](#risk-metrics)
   - [Performance Ratios](#performance-ratios)
   - [Portfolio Statistics](#portfolio-statistics)
8. [Moving Averages](#moving-averages)
   - [Simple Moving Average](#simple-moving-average)
   - [Exponential Moving Average](#exponential-moving-average)
   - [Bollinger Bands](#bollinger-bands)
9. [Portfolio Optimization](#portfolio-optimization)
   - [Efficient Frontier](#efficient-frontier)
   - [Monte Carlo Optimization](#monte-carlo-optimization)
10. [Visualization](#visualization)
11. [Use Cases and Examples](#use-cases-and-examples)

## Introduction

FinQuant is a comprehensive Python library for financial portfolio management, analysis, and optimization. It provides tools for portfolio construction, performance analysis, risk assessment, and optimization using modern portfolio theory concepts.

The library is designed to be easily extendable and user-friendly, making it suitable for hobby investors, students, financial analysts, and anyone interested in quantitative finance.

## Installation

FinQuant can be installed through various methods:

### Dependencies
- `python>=3.10.0`
- `numpy>=1.15`
- `scipy>=1.2.0`
- `pandas>=2.0`
- `matplotlib>=3.0`
- `quandl>=3.4.5`
- `yfinance>=0.1.43`

### From PyPI
```bash
pip install FinQuant
```

### From GitHub
```bash
git clone https://github.com/fmilthaler/FinQuant.git
cd FinQuant
python setup.py install
```

## Core Features

FinQuant provides the following core features:

1. **Portfolio Management**: Create, analyze, and manage financial portfolios
2. **Risk Analysis**: Calculate various risk metrics (volatility, downside risk, VaR)
3. **Performance Evaluation**: Compute performance ratios (Sharpe, Sortino, Treynor)
4. **Returns Analysis**: Calculate different types of returns (daily, cumulative, log)
5. **Technical Analysis**: Compute moving averages and Bollinger Bands
6. **Portfolio Optimization**: Optimize portfolios using Efficient Frontier or Monte Carlo methods
7. **Data Retrieval**: Get financial data from Quandl or Yahoo Finance
8. **Visualization**: Plot portfolio characteristics, efficient frontiers, and more

## Portfolio Management

The core of FinQuant is the `Portfolio` class, which provides a comprehensive framework for portfolio management.

### Building a Portfolio

The easiest way to create a portfolio is through the `build_portfolio()` function:

```python
from finquant.portfolio import build_portfolio

# Method 1: From stock symbols (data pulled from Yahoo Finance or Quandl)
names = ['AAPL', 'MSFT', 'AMZN', 'GOOG']
pf = build_portfolio(names=names, data_api="yfinance")

# Method 2: From existing data
import pandas as pd
df_data = pd.read_csv('stock_data.csv', index_col='Date', parse_dates=True)
pf = build_portfolio(data=df_data)
```

**Function Parameters:**
- `pf_allocation`: (Optional) DataFrame with columns 'Name' and 'Allocation' for stock weights
- `names`: (Optional) List of stock symbols to retrieve from data API
- `start_date`, `end_date`: (Optional) Date range for data retrieval
- `data`: (Optional) DataFrame of stock prices (columns are stock names)
- `data_api`: (Optional) Data source ('quandl' or 'yfinance', default: 'quandl')
- `market_index`: (Optional) Market index for beta and Treynor ratio calculations

### Portfolio Properties

Once a portfolio is created, you can examine its properties:

```python
# Display portfolio properties
pf.properties()
```

This displays:
- Expected annual return
- Portfolio volatility
- Sharpe ratio
- Skewness
- Kurtosis
- Stock allocations
- Other metrics (if market index provided): Beta, R-squared, Treynor ratio

### Portfolio Operations

The `Portfolio` class provides numerous methods for portfolio analysis:

**Returns Calculation:**
```python
# Calculate different types of returns
daily_returns = pf.comp_daily_returns()
log_returns = pf.comp_daily_log_returns()
cumulative_returns = pf.comp_cumulative_returns()
```

**Risk Metrics:**
```python
# Calculate risk metrics
volatility = pf.comp_volatility()
downside_risk = pf.comp_downside_risk()
var = pf.comp_var()  # Value at Risk
```

**Performance Ratios:**
```python
# Calculate performance ratios
sharpe = pf.comp_sharpe()
sortino = pf.comp_sortino()
treynor = pf.comp_treynor()  # Requires market index
```

**Portfolio Components:**
```python
# Get a specific stock from the portfolio
apple_stock = pf.get_stock("AAPL")

# Compute the covariance matrix
cov_matrix = pf.comp_cov()

# Get current weights
weights = pf.comp_weights()
```

## Assets

FinQuant provides classes for individual assets that make up a portfolio.

### Asset Class

The `Asset` class is the parent class for all financial assets:

```python
from finquant.asset import Asset

# Create a generic asset (rarely used directly)
asset = Asset(data=price_series, name="MyAsset", asset_type="Stock")
```

**Methods:**
- `comp_daily_returns()`: Calculate daily returns
- `comp_expected_return(freq=252)`: Calculate expected annualized return
- `comp_volatility(freq=252)`: Calculate annualized volatility
- `properties()`: Display asset properties

### Stock Class

The `Stock` class represents individual stocks or funds in a portfolio:

```python
from finquant.stock import Stock

# Stocks are usually created through build_portfolio()
# But can be created manually:
stock = Stock(investmentinfo=info_df, data=price_series)
```

**Additional Methods:**
- `comp_beta(market_daily_returns)`: Calculate beta versus a market index
- `comp_rsquared(market_daily_returns)`: Calculate R-squared versus market returns

### Market Class

The `Market` class represents a market index:

```python
from finquant.market import Market

# Create a market index
market = Market(data=index_price_series)
```

This is primarily used for calculating portfolio beta and Treynor ratio.

## Returns Calculation

FinQuant provides several functions for calculating different types of returns.

### Daily Returns

```python
from finquant.returns import daily_returns

# Calculate daily percentage returns
returns_df = daily_returns(price_df)
```

Formula: R = (price_t - price_t-1) / price_t-1

### Cumulative Returns

```python
from finquant.returns import cumulative_returns

# Calculate cumulative returns
cum_returns_df = cumulative_returns(price_df, dividend=0)
```

Formula: R = (price_t - price_t0 + dividend) / price_t0

### Historical Mean Returns

```python
from finquant.returns import historical_mean_return

# Calculate annualized mean returns based on historical data
mean_returns = historical_mean_return(data, freq=252)
```

### Other Return Functions

- `daily_log_returns(data)`: Calculate daily logarithmic returns
- `weighted_mean_daily_returns(data, weights)`: Calculate weighted mean daily returns

## Quantitative Analysis

FinQuant provides extensive functions for quantitative analysis of portfolios.

### Risk Metrics

**Volatility:**
```python
from finquant.quants import weighted_std

# Calculate portfolio volatility
volatility = weighted_std(cov_matrix, weights)
```

**Downside Risk:**
```python
from finquant.quants import downside_risk

# Calculate downside risk
dr = downside_risk(data, weights, risk_free_rate=0.005)
```

**Value at Risk (VaR):**
```python
from finquant.quants import value_at_risk

# Calculate Value at Risk
var = value_at_risk(investment, mu, sigma, conf_level=0.95)
```

### Performance Ratios

**Sharpe Ratio:**
```python
from finquant.quants import sharpe_ratio

# Calculate Sharpe ratio
sharpe = sharpe_ratio(exp_return, volatility, risk_free_rate=0.005)
```

**Sortino Ratio:**
```python
from finquant.quants import sortino_ratio

# Calculate Sortino ratio
sortino = sortino_ratio(exp_return, downs_risk, risk_free_rate=0.005)
```

**Treynor Ratio:**
```python
from finquant.quants import treynor_ratio

# Calculate Treynor ratio
treynor = treynor_ratio(exp_return, beta, risk_free_rate=0.005)
```

### Portfolio Statistics

```python
from finquant.quants import annualised_portfolio_quantities

# Calculate key portfolio metrics at once
exp_return, volatility, sharpe = annualised_portfolio_quantities(
    weights, means, cov_matrix, risk_free_rate=0.005, freq=252
)
```

## Moving Averages

FinQuant provides functions for calculating and visualizing moving averages.

### Simple Moving Average

```python
from finquant.moving_average import sma

# Calculate Simple Moving Average
sma_values = sma(data, span=100)
```

### Exponential Moving Average

```python
from finquant.moving_average import ema

# Calculate Exponential Moving Average
ema_values = ema(data, span=100)
```

### Bollinger Bands

```python
from finquant.moving_average import plot_bollinger_band

# Plot Bollinger Bands
plot_bollinger_band(data, sma, span=100)
```

### Computing Multiple Moving Averages

```python
from finquant.moving_average import compute_ma, ema

# Compute a band of moving averages and identify buy/sell signals
spans = [10, 50, 100, 150, 200]
ma = compute_ma(data, ema, spans, plot=True)
```

## Portfolio Optimization

FinQuant provides two main approaches to portfolio optimization:

### Efficient Frontier

The Efficient Frontier represents the optimal portfolios that offer the highest expected return for a defined level of risk.

```python
# Calculate and plot the efficient frontier
pf.ef_plot_efrontier()

# Find minimum volatility portfolio
min_vol_weights = pf.ef_minimum_volatility(verbose=True)

# Find maximum Sharpe ratio portfolio
max_sharpe_weights = pf.ef_maximum_sharpe_ratio(verbose=True)

# Find minimum volatility for a target return
target_return = 0.2
efficient_return_weights = pf.ef_efficient_return(target_return, verbose=True)

# Find maximum Sharpe ratio for a target volatility
target_volatility = 0.15
efficient_volatility_weights = pf.ef_efficient_volatility(target_volatility, verbose=True)

# Plot optimal portfolios
pf.ef.plot_optimal_portfolios()
```

**EfficientFrontier Class Parameters:**
- `mean_returns`: Series of individual expected returns for all stocks
- `cov_matrix`: Covariance matrix of returns
- `risk_free_rate`: Risk-free rate (default: 0.005)
- `freq`: Number of trading days in a year (default: 252)
- `method`: Optimization method (default: 'SLSQP')

### Monte Carlo Optimization

Monte Carlo optimization generates thousands of random portfolios and identifies the optimal ones:

```python
# Run Monte Carlo optimization
opt_weights, opt_results = pf.mc_optimisation(num_trials=5000)

# Plot Monte Carlo optimization results
pf.mc_plot_results()

# Display properties of optimized portfolios
pf.mc_properties()
```

**Monte Carlo Process:**
1. Generate thousands of random weight allocations
2. Calculate expected return, volatility, and Sharpe ratio for each
3. Identify portfolios with minimum volatility and maximum Sharpe ratio
4. Return optimal weights and visualization

## Visualization

FinQuant offers various visualization functions:

```python
# Plot portfolio stocks (return vs volatility)
pf.plot_stocks()

# Plot efficient frontier
pf.ef_plot_efrontier()

# Plot optimal portfolios on efficient frontier
pf.ef.plot_optimal_portfolios()

# Plot Monte Carlo optimization results
pf.mc_plot_results()

# Overlay Monte Carlo results and efficient frontier
# (Call the above functions in sequence)
```

## Use Cases and Examples

### Use Case 1: Portfolio Analysis
```python
from finquant.portfolio import build_portfolio

# Create a portfolio with 4 tech stocks
names = ['AAPL', 'MSFT', 'AMZN', 'GOOG']
pf = build_portfolio(names=names, data_api="yfinance")

# Analyze portfolio characteristics
pf.properties()

# Visualize stocks in the portfolio
pf.plot_stocks()

# Calculate and display the covariance matrix
cov_matrix = pf.comp_cov()
print(cov_matrix)
```

### Use Case 2: Risk Assessment
```python
# Calculate and analyze different risk metrics
volatility = pf.comp_volatility()
downside_risk = pf.comp_downside_risk()
var = pf.comp_var()

print(f"Portfolio Volatility: {volatility:.4f}")
print(f"Downside Risk: {downside_risk:.4f}")
print(f"Value at Risk (95%): {var:.4f}")

# Analyze returns
daily_returns = pf.comp_daily_returns()
cumulative_returns = pf.comp_cumulative_returns()
```

### Use Case 3: Portfolio Optimization
```python
# Find the minimum volatility portfolio
min_vol_weights = pf.ef_minimum_volatility(verbose=True)

# Find the maximum Sharpe ratio portfolio
max_sharpe_weights = pf.ef_maximum_sharpe_ratio(verbose=True)

# Visualize the efficient frontier
pf.ef_plot_efrontier()
pf.ef.plot_optimal_portfolios()

# Alternatively, use Monte Carlo optimization
opt_weights, opt_results = pf.mc_optimisation(num_trials=5000)
pf.mc_plot_results()
```

### Use Case 4: Technical Analysis with Moving Averages
```python
from finquant.moving_average import compute_ma, ema, plot_bollinger_band

# Extract data for a single stock
apple_data = pf.get_stock('AAPL').data.copy(deep=True)

# Calculate and plot moving average band with buy/sell signals
spans = [20, 50, 100, 200]
ma = compute_ma(apple_data, ema, spans, plot=True)

# Plot Bollinger Bands
plot_bollinger_band(apple_data, ema, span=20)
```

### Use Case 5: Creating a Custom Portfolio with Specified Weights
```python
import pandas as pd
from finquant.portfolio import build_portfolio

# Define stock names and allocations
stocks = ['AAPL', 'MSFT', 'AMZN', 'GOOG']
allocations = [0.3, 0.3, 0.2, 0.2]  # 30% AAPL, 30% MSFT, 20% AMZN, 20% GOOG

# Create allocation DataFrame
pf_allocation = pd.DataFrame({
    'Name': stocks,
    'Allocation': allocations
})

# Build portfolio with custom allocations
pf = build_portfolio(names=stocks, pf_allocation=pf_allocation, data_api="yfinance")

# Analyze the custom portfolio
pf.properties()
```

---

FinQuant provides a comprehensive toolkit for financial portfolio management, making advanced portfolio theory and optimization accessible to Python users. From basic portfolio analysis to advanced optimization techniques, FinQuant offers tools suitable for various levels of financial knowledge and investment strategies.