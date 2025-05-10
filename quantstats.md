# QuantStats: Portfolio Analytics for Quants

QuantStats is a powerful Python library designed for portfolio profiling and analytics. It provides quants and portfolio managers with comprehensive tools to analyze performance through detailed metrics, visualizations, and automated reports.

## Overview

QuantStats offers a streamlined workflow for portfolio analysis through three main modules:

1. **Stats Module**: Calculate performance metrics like Sharpe ratio, win rate, volatility, and more
2. **Plots Module**: Visualize performance with drawdowns, rolling statistics, and return distributions
3. **Reports Module**: Generate comprehensive tearsheets and HTML reports for sharing

## Installation

### Using pip
```bash
pip install quantstats --upgrade --no-cache-dir
```

### Using conda
```bash
conda install -c ranaroussi quantstats
```

## Requirements

- Python 3.6+
- pandas ≥ 0.24.0
- numpy ≥ 1.15.0
- scipy ≥ 1.2.0
- matplotlib ≥ 3.0.0
- seaborn ≥ 0.9.0
- tabulate ≥ 0.8.0
- yfinance ≥ 0.1.38
- plotly ≥ 3.4.1 (optional, for using `plots.to_plotly()`)

## Quick Start Guide

### Basic Usage

```python
import quantstats as qs

# Extend pandas functionality with metrics
qs.extend_pandas()

# Download returns data for a stock
stock = qs.utils.download_returns('META')

# Calculate Sharpe ratio
sharpe = qs.stats.sharpe(stock)
print(f"Sharpe Ratio: {sharpe}")

# Or using the extended pandas functionality
sharpe = stock.sharpe()
print(f"Sharpe Ratio: {sharpe}")
```

### Visualization

```python
# Create a performance snapshot
qs.plots.snapshot(stock, title='META Performance', show=True)

# Using extended pandas functionality
stock.plot_snapshot(title='META Performance', show=True)
```

### Creating Reports

QuantStats offers several report types:

```python
# Basic metrics report
qs.reports.metrics(stock, mode='basic')

# Full metrics report
qs.reports.metrics(stock, mode='full')

# Basic plots report
qs.reports.plots(stock, mode='basic')

# Full plots report
qs.reports.plots(stock, mode='full')

# Combined basic metrics and plots
qs.reports.basic(stock)

# Combined full metrics and plots
qs.reports.full(stock)

# Generate complete HTML tearsheet with benchmark comparison
qs.reports.html(stock, "SPY", output="my_report.html")
```

## Detailed Module Reference

### Stats Module

The `quantstats.stats` module provides extensive performance metrics:

#### Return Metrics
* `avg_return()`: Calculate average return
* `cagr()`: Compound Annual Growth Rate
* `comp()`: Compounded returns
* `expected_return()`: Expected return based on historical data
* `geometric_mean()`: Geometric mean of returns
* `ghpr()`: Geometric Holding Period Return
* `monthly_returns()`: Returns organized by month

#### Risk Metrics
* `conditional_value_at_risk()` / `cvar()`: Expected Shortfall
* `value_at_risk()` / `var()`: Value at Risk
* `drawdown_details()`: Detailed drawdown analysis
* `max_drawdown()`: Maximum drawdown
* `to_drawdown_series()`: Convert returns to drawdown series
* `volatility()`: Return volatility
* `ulcer_index()`: Ulcer Index for downside risk

#### Ratio Metrics
* `sharpe()`: Sharpe ratio
* `sortino()`: Sortino ratio
* `adjusted_sortino()`: Adjusted Sortino ratio
* `calmar()`: Calmar ratio
* `information_ratio()`: Information ratio
* `gain_to_pain_ratio()`: Gain to pain ratio
* `risk_return_ratio()`: Risk-return ratio
* `win_loss_ratio()`: Win/loss ratio
* `win_rate()`: Win rate percentage
* `payoff_ratio()`: Average win / average loss
* `profit_factor()`: Gross profit / gross loss
* `common_sense_ratio()`: Performance measure incorporating multiple factors

#### Advanced Analysis
* `greeks()`: Calculate option greeks
* `rolling_greeks()`: Rolling option greeks
* `implied_volatility()`: Estimated implied volatility
* `kurtosis()`: Distribution kurtosis
* `outliers()`: Identify outlier returns
* `r_squared()` / `r2()`: R-squared correlation
* `remove_outliers()`: Remove outliers from return series
* `skew()`: Return distribution skew
* `kelly_criterion()`: Kelly criterion for optimal position sizing

### Plots Module

The `quantstats.plots` module offers visualization tools:

#### Return Visualizations
* `returns()`: Plot returns over time
* `log_returns()`: Plot logarithmic returns
* `daily_returns()`: Daily returns distribution
* `histogram()`: Return distribution histogram
* `distribution()`: Probability distribution with overlaid normal curve
* `monthly_heatmap()`: Calendar heatmap of monthly returns
* `yearly_returns()`: Annual returns comparison

#### Risk Visualizations
* `drawdown()`: Drawdown periods visualization
* `drawdowns_periods()`: Historical drawdown periods
* `rolling_volatility()`: Rolling volatility
* `rolling_sharpe()`: Rolling Sharpe ratio
* `rolling_sortino()`: Rolling Sortino ratio
* `rolling_beta()`: Rolling beta to benchmark

#### Summary Visualizations
* `snapshot()`: Performance summary dashboard with key metrics
* `earnings()`: Earnings metrics visualization

### Reports Module

The `quantstats.reports` module generates comprehensive reports:

* `metrics(mode='basic|full')`: Display basic or full metrics tables
* `plots(mode='basic|full')`: Display basic or full visualization set
* `basic()`: Combined basic metrics and plots
* `full()`: Combined full metrics and plots
* `html()`: Generate complete HTML tearsheet

## Extended Pandas Functionality

Using `qs.extend_pandas()` adds QuantStats methods directly to pandas Series objects:

```python
import quantstats as qs
qs.extend_pandas()

# Download stock data
stock = qs.utils.download_returns('META')

# Use methods directly on the Series
stock.sharpe()
stock.sortino()
stock.volatility()
stock.max_drawdown()

# Create visualizations
stock.plot_snapshot()
stock.plot_drawdown()
stock.plot_monthly_heatmap()
```

## Utils Module

The `quantstats.utils` module provides helpful utilities:

* `download_returns()`: Download price data and convert to returns
* `to_returns()`: Convert prices to returns
* `to_prices()`: Convert returns to prices
* `df_to_sheet()`: Convert DataFrame to Excel sheet
* `make_index()`: Create date range index

## Practical Examples

### Portfolio Comparison

```python
import quantstats as qs
import pandas as pd

# Download returns data
spy = qs.utils.download_returns('SPY')
qqq = qs.utils.download_returns('QQQ')

# Compare performance
qs.reports.html(qqq, spy, output='tech_vs_market.html', 
                title='Tech vs. Broader Market')
```

### Custom Portfolio Analysis

```python
import quantstats as qs
import pandas as pd
import numpy as np

# Create portfolio with random weights
tickers = ['AAPL', 'MSFT', 'AMZN', 'GOOGL']
weights = np.array([0.3, 0.3, 0.2, 0.2])

# Download returns
returns = pd.DataFrame()
for ticker in tickers:
    returns[ticker] = qs.utils.download_returns(ticker)

# Calculate portfolio returns
portfolio = returns.dot(weights)

# Generate report with S&P 500 benchmark
qs.reports.html(portfolio, 'SPY', output='portfolio_analysis.html',
                title='My Tech Portfolio')
```

### Analyzing Strategy Returns

```python
import quantstats as qs
import pandas as pd

# Load strategy returns from CSV
strategy_returns = pd.read_csv('strategy_returns.csv', 
                               index_col=0, parse_dates=True)['returns']

# Generate comprehensive report
qs.reports.full(strategy_returns, benchmark='SPY',
                title='Algorithmic Trading Strategy Performance')
```

## Known Issues

- Monthly returns heatmap cannot be suppressed when using `savefig` parameter

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch
3. Implement your changes
4. Submit a pull request

Good places to start are issues labeled with "help wanted" on the GitHub repository.

## License

QuantStats is distributed under the Apache Software License. See the LICENSE.txt file for details.

## Resources

- GitHub Repository: [https://github.com/ranaroussi/quantstats](https://github.com/ranaroussi/quantstats)
- Issues/Bug Reports: [https://github.com/ranaroussi/quantstats/issues](https://github.com/ranaroussi/quantstats/issues)

---

This documentation provides a comprehensive overview of QuantStats, its capabilities, and how to use it effectively for portfolio analytics and performance measurement. The library offers powerful tools for quants and portfolio managers to gain deeper insights into their investment strategies.