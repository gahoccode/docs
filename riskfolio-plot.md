# RiskFolio-Lib: Comprehensive Documentation

## Overview

RiskFolio-Lib is a Python library for portfolio optimization and quantitative strategic asset allocation. It provides a comprehensive set of tools for portfolio modeling, optimization, visualization, and reporting.

The library contains multiple modules:
- Portfolio: For portfolio optimization with different risk measures
- HCPortfolio: For hierarchical clustering portfolio optimization models
- ParamsEstimation: For estimating inputs of portfolio optimization models
- RiskFunctions: For calculating different risk measures
- PlotFunctions: For visualizing portfolio properties and risk measures
- Reports: For generating portfolio analysis reports
- AuxFunctions: For auxiliary functions

This documentation covers the plotting, reporting, and portfolio optimization capabilities of RiskFolio-Lib.

## Key Plotting Functions

### 1. `plot_series()`

Creates a chart with the compounded cumulative returns of portfolios.

**Parameters:**
- `returns`: Assets returns DataFrame
- `w`: Portfolio weights
- `cmap`: Colorscale for portfolio returns (default: 'tab20')
- `n_colors`: Number of distinct colors (default: 20)
- `height`: Height of the image in inches (default: 6)
- `width`: Width of the image in inches (default: 10)
- `ax`: Optional matplotlib axis to plot on

**Example Usage:**
```python
ax = rp.plot_series(returns=Y,
                    w=ws,
                    cmap='tab20',
                    height=6,
                    width=10,
                    ax=None)
```

**Visual Output:**
The function produces a line chart showing the compounded cumulative returns of the portfolio over time.

### 2. `plot_frontier()`

Creates a plot of the efficient frontier for a specified risk measure.

**Parameters:**
- `w_frontier`: Portfolio weights of points in the efficient frontier
- `returns`: Assets returns DataFrame
- `mu`: Vector of expected returns (optional)
- `cov`: Covariance matrix (optional)
- `rm`: Risk measure used (default: 'MV')
- `rf`: Risk-free rate (default: 0)
- `alpha`: Significance level for various risk measures (default: 0.05)
- `cmap`: Colorscale for risk-adjusted return (default: 'viridis')
- `w`: Additional portfolio to plot (optional)
- `label`: Name of portfolios for legend (default: 'Portfolio')
- `height/width`: Image dimensions in inches (default: 6/10)
- `t_factor`: Annualization factor (default: 252)

**Example Usage:**
```python
ax = rp.plot_frontier(w_frontier=ws,
                      mu=mu,
                      cov=cov,
                      returns=Y,
                      rm='MSV',
                      rf=0,
                      alpha=0.05,
                      cmap='viridis',
                      w=w1,
                      label='Max Risk Adjusted Return Portfolio',
                      marker='*',
                      s=16,
                      c='r',
                      height=6,
                      width=10,
                      t_factor=252,
                      ax=None)
```

**Visual Output:**
A scatter plot showing the efficient frontier with expected return on y-axis and risk measure on x-axis.

### 3. `plot_pie()`

Creates a pie chart representing portfolio weights.

**Parameters:**
- `w`: Portfolio weights
- `title`: Chart title (default: '')
- `others`: Percentage threshold for grouping small weights into 'Others' (default: 0.05)
- `nrow`: Number of legend rows (default: 25)
- `cmap`: Colorscale for asset weights (default: 'tab20')
- `n_colors`: Number of distinct colors (default: 20)
- `height/width`: Image dimensions in inches (default: 6/8)

**Example Usage:**
```python
ax = rp.plot_pie(w=w1,
                 title='Portfolio',
                 height=6,
                 width=10,
                 cmap="tab20",
                 ax=None)
```

**Visual Output:**
A pie chart showing the relative weights of assets in the portfolio.

### 4. `plot_bar()`

Creates a bar chart with portfolio weights.

**Parameters:**
- `w`: Portfolio weights
- `title`: Chart title (default: '')
- `kind`: Type of bar plot ('v' for vertical, 'h' for horizontal) (default: 'v')
- `others`: Threshold for grouping small weights (default: 0.05)
- `nrow`: Max number of bars (default: 25)
- `cpos/cneg/cothers`: Colors for positive/negative/others weights
- `height/width`: Image dimensions in inches (default: 6/10)

**Example Usage:**
```python
ax = rp.plot_bar(w1,
                 title='Portfolio',
                 kind="v",
                 others=0.05,
                 nrow=25,
                 height=6,
                 width=10,
                 ax=None)
```

**Visual Output:**
A bar chart showing the weights of assets in the portfolio.

### 5. `plot_frontier_area()`

Creates a chart showing the asset composition across the efficient frontier.

**Parameters:**
- `w_frontier`: Weights of portfolios in the efficient frontier
- `nrow`: Number of legend rows (default: 25)
- `cmap`: Colorscale for asset weights (default: 'tab20')
- `n_colors`: Number of distinct colors (default: 20)
- `height/width`: Image dimensions in inches (default: 6/10)

**Example Usage:**
```python
ax = rp.plot_frontier_area(w_frontier=ws,
                           cmap="tab20",
                           height=6,
                           width=10,
                           ax=None)
```

**Visual Output:**
An area chart showing how the portfolio composition changes across the efficient frontier.

### 6. `plot_risk_con()`

Creates a chart with the risk contribution per asset of the portfolio.

**Parameters:**
- `w`: Portfolio weights
- `returns`: Assets returns DataFrame
- `cov`: Covariance matrix (optional)
- `rm`: Risk measure used (default: 'MV')
- `rf`: Risk-free rate (default: 0)
- `alpha`: Significance level for risk measures (default: 0.05)
- `percentage`: If risk contribution is expressed as percentage (default: False)
- `erc_line`: If equal risk contribution line is plotted (default: True)
- `color`: Color for asset risk contributions (default: 'tab:blue')
- `erc_linecolor`: Color for equal risk contribution line (default: 'r')
- `height/width`: Image dimensions in inches (default: 6/10)
- `t_factor`: Annualization factor (default: 252)

**Example Usage:**
```python
ax = rp.plot_risk_con(w=w2,
                      cov=cov,
                      returns=Y,
                      rm='MSV',
                      rf=0,
                      alpha=0.05,
                      color="tab:blue",
                      height=6,
                      width=10,
                      t_factor=252,
                      ax=None)
```

**Visual Output:**
A bar chart showing the risk contribution of each asset in the portfolio.

### 7. `plot_factor_risk_con()`

Creates a chart with the risk contribution per risk factor of the portfolio.

**Parameters:**
- `w`: Portfolio weights
- `returns`: Assets returns DataFrame
- `factors`: Risk factors returns DataFrame
- `cov`: Covariance matrix (optional)
- `B`: Loadings matrix (optional)
- `rm`: Risk measure used (default: 'MV')
- `feature_selection`: Method for loadings estimation (default: 'stepwise')
- `percentage`: If risk contribution is expressed as percentage (default: False)
- `erc_line`: If equal risk contribution line is plotted (default: True)
- `color`: Color for factor risk contributions (default: 'tab:orange')
- `height/width`: Image dimensions (default: 6/10)
- `t_factor`: Annualization factor (default: 252)

**Example Usage:**
```python
ax = rp.plot_factor_risk_con(w=w3,
                             cov=cov,
                             returns=Y,
                             factors=X,
                             B=None,
                             const=True,
                             rm='MSV',
                             rf=0,
                             feature_selection="stepwise",
                             stepwise="Forward",
                             criterion="pvalue",
                             threshold=0.05,
                             height=6,
                             width=10,
                             t_factor=252,
                             ax=None)
```

**Visual Output:**
A bar chart showing the risk contribution of each risk factor in the portfolio.

### 8. `plot_hist()`

Creates a histogram of portfolio returns with risk measures.

**Parameters:**
- `returns`: Assets returns DataFrame
- `w`: Portfolio weights
- `alpha`: Significance level for risk measures (default: 0.05)
- `bins`: Number of histogram bins (default: 50)
- `height/width`: Image dimensions in inches (default: 6/10)

**Example Usage:**
```python
ax = rp.plot_hist(returns=Y,
                  w=w1,
                  alpha=0.05,
                  bins=50,
                  height=6,
                  width=10,
                  ax=None)
```

**Visual Output:**
A histogram showing the distribution of portfolio returns with indicators for risk measures.

### 9. `plot_range()`

Creates a histogram of portfolio returns with range risk measures.

**Parameters:**
- `returns`: Assets returns DataFrame
- `w`: Portfolio weights
- `alpha`: Significance level for losses (default: 0.05)
- `beta`: Significance level for gains (default: None)
- `bins`: Number of histogram bins (default: 50)
- `height/width`: Image dimensions in inches (default: 6/10)

**Example Usage:**
```python
ax = rp.plot_range(returns=Y,
                   w=w1,
                   alpha=0.05,
                   a_sim=100,
                   beta=None,
                   b_sim=None,
                   bins=50,
                   height=6,
                   width=10,
                   ax=None)
```

**Visual Output:**
A histogram showing the distribution of portfolio returns with range risk measures indicators.

### 10. `plot_drawdown()`

Creates a chart with the evolution of portfolio prices and drawdown.

**Parameters:**
- `returns`: Assets returns DataFrame
- `w`: Portfolio weights
- `alpha`: Significance level for drawdown measures (default: 0.05)
- `height/width`: Image dimensions in inches (default: 8/10)
- `height_ratios`: Relative heights of the rows (default: [2, 3])

**Example Usage:**
```python
ax = rp.plot_drawdown(returns=Y,
                      w=w1,
                      alpha=0.05,
                      height=8,
                      width=10,
                      ax=None)
```

**Visual Output:**
A multi-panel chart showing portfolio values and drawdowns over time.

### 11. `plot_table()`

Creates a table with information about risk measures and risk-adjusted return ratios.

**Parameters:**
- `returns`: Assets returns DataFrame
- `w`: Portfolio weights
- `MAR`: Minimum acceptable return (default: 0)
- `alpha`: Significance level for risk measures (default: 0.05)
- `height/width`: Image dimensions in inches (default: 9/12)
- `t_factor`: Annualization factor (default: 252)
- `ini_days`: Days of compounding for first return (default: 1)
- `days_per_year`: Days per year assumption (default: 252)

**Example Usage:**
```python
ax = rp.plot_table(returns=Y,
                   w=w1,
                   MAR=0,
                   alpha=0.05,
                   height=9,
                   width=12,
                   t_factor=252,
                   ax=None)
```

**Visual Output:**
A table showing various risk and performance metrics for the portfolio.

## Risk Measures Available

When using the plotting functions, especially `plot_frontier()`, the following risk measures can be specified using the `rm` parameter:

### Dispersion Risk Measures:
- `'MV'`: Standard Deviation
- `'KT'`: Square Root Kurtosis
- `'MAD'`: Mean Absolute Deviation
- `'GMD'`: Gini Mean Difference
- `'CVRG'`: CVaR range of returns
- `'TGRG'`: Tail Gini range of returns
- `'EVRG'`: EVaR range of returns
- `'RVRG'`: RLVaR range of returns
- `'RG'`: Range of returns

### Downside Risk Measures:
- `'MSV'`: Semi Standard Deviation
- `'SKT'`: Square Root Semi Kurtosis
- `'FLPM'`: First Lower Partial Moment (Omega Ratio)
- `'SLPM'`: Second Lower Partial Moment (Sortino Ratio)
- `'CVaR'`: Conditional Value at Risk
- `'TG'`: Tail Gini
- `'EVaR'`: Entropic Value at Risk
- `'RLVaR'`: Relativistic Value at Risk
- `'WR'`: Worst Realization (Minimax)

### Drawdown Risk Measures:
- `'MDD'`: Maximum Drawdown of uncompounded returns (Calmar Ratio)
- `'ADD'`: Average Drawdown of uncompounded cumulative returns
- `'DaR'`: Drawdown at Risk of uncompounded cumulative returns
- `'CDaR'`: Conditional Drawdown at Risk of uncompounded cumulative returns
- `'EDaR'`: Entropic Drawdown at Risk of uncompounded cumulative returns
- `'RLDaR'`: Relativistic Drawdown at Risk of uncompounded cumulative returns
- `'UCI'`: Ulcer Index of uncompounded cumulative returns

## Usage Notes

1. Most plotting functions return the matplotlib axis object, allowing for further customization.
2. The `cmap` parameter allows for customizing the color palette of the plots.
3. Functions like `plot_frontier()` can visualize multiple portfolios on the same chart.
4. Risk measures can be specified through the `rm` parameter in applicable functions.
5. The `t_factor` parameter (typically set to 252 for daily returns) is used to annualize returns and risks.

## Integration with Portfolio Optimization

The plotting functions in RiskFolio-Lib are designed to work seamlessly with the outputs from portfolio optimization. A typical workflow involves:

1. Creating a Portfolio object and estimating inputs
2. Running optimization to get portfolio weights
3. Using plotting functions to visualize the portfolio properties

For example:
```python
# Create Portfolio object
port = rp.Portfolio(returns=Y)

# Estimate inputs
port.assets_stats(method_mu='hist', method_cov='hist')

# Optimize portfolio
w = port.optimization(model='Classic', rm='MSV', obj='Sharpe', rf=0.0, l=0, hist=True)

# Plot results
ax = rp.plot_pie(w=w, title='Optimized Portfolio', height=6, width=10)
```

This integration makes it easy to analyze and visualize the results of different portfolio optimization strategies.

## Report Generation Functions

The `Reports` module in RiskFolio-Lib provides functions to create comprehensive portfolio analysis reports that combine multiple visualizations and metrics. These reports are especially useful for sharing portfolio analysis results with stakeholders or for documenting optimization outcomes.

### 1. `jupyter_report()`

Creates a comprehensive matplotlib report with multiple charts and tables for analyzing portfolio risk and performance characteristics.

**Parameters:**
- `returns`: Assets returns DataFrame
- `w`: Portfolio weights
- `rm`: Risk measure used (default: 'MV')
- `rf`: Risk-free rate (default: 0)
- `alpha`: Significance level for risk measures (default: 0.05)
- `solver`: Solver for EVaR and related measures (default: 'CLARABEL')
- `percentage`: If risk contribution is expressed as percentage (default: False)
- `erc_line`: If equal risk contribution line is plotted (default: True)
- `height`: Average height of charts in inches (default: 6)
- `width`: Width of the image in inches (default: 14)
- `t_factor`: Annualization factor (default: 252)
- `ini_days`: Days of compounding for first return (default: 1)
- `days_per_year`: Days per year assumption (default: 252)
- `bins`: Number of histogram bins (default: 50)

**Example Usage:**
```python
ax = rp.jupyter_report(returns,
                       w,
                       rm='MV',
                       rf=0,
                       alpha=0.05,
                       height=6,
                       width=14,
                       others=0.05,
                       nrow=25)
```

**Output:**
The function produces a multi-panel report containing:
1. Portfolio weights visualization
2. Risk contribution analysis
3. Historical cumulative returns
4. Drawdown analysis
5. Return distribution with risk metrics
6. Performance and risk statistics table

### 2. `excel_report()`

Creates an Excel report (with formulas) that provides detailed information for analyzing portfolio risk and profitability.

**Parameters:**
- `returns`: Assets returns DataFrame
- `w`: Portfolio weights
- `rf`: Risk-free rate (default: 0)
- `alpha`: Significance level for risk measures (default: 0.05)
- `solver`: Solver for EVaR and EDaR (default: 'CLARABEL')
- `t_factor`: Annualization factor (default: 252)
- `ini_days`: Days of compounding for first return (default: 1)
- `days_per_year`: Days per year assumption (default: 252)
- `name`: Name or path where the Excel report will be saved (default: 'report')

**Example Usage:**
```python
rp.excel_report(returns,
                w,
                rf=0,
                alpha=0.05,
                t_factor=252,
                ini_days=1,
                days_per_year=252,
                name="portfolio_report")
```

**Output:**
The function generates an Excel file with multiple sheets containing:
1. Portfolio weights
2. Return and risk metrics
3. Performance ratios
4. Historical performance data
5. Formulas that allow for interactive analysis

## Integration with Portfolio Optimization and Plotting

The report generation functions are designed to work seamlessly with the outputs from portfolio optimization and plotting functions. A complete workflow might involve:

1. Creating a Portfolio object and estimating inputs
2. Running optimization to get portfolio weights
3. Creating individual visualizations with plotting functions
4. Generating comprehensive reports for analysis and presentation

For example:
```python
# Create Portfolio object and optimize
port = rp.Portfolio(returns=Y)
port.assets_stats(method_mu='hist', method_cov='hist')
w = port.optimization(model='Classic', rm='MV', obj='Sharpe', rf=0.0, l=0, hist=True)

# Generate individual plots if needed
ax1 = rp.plot_pie(w=w, title='Portfolio Weights')
ax2 = rp.plot_risk_con(w=w, cov=port.cov, returns=Y, rm='MV')

# Generate comprehensive reports
ax_report = rp.jupyter_report(returns=Y, w=w, rm='MV', rf=0)
rp.excel_report(returns=Y, w=w, name="portfolio_report")
```

These report generation functions provide a convenient way to combine multiple visualizations and metrics into a single comprehensive view of portfolio properties and performance.