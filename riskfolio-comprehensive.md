# Riskfolio-Lib: A Comprehensive Guide to Portfolio Optimization in Python

Riskfolio-Lib is a powerful Python library for portfolio optimization and quantitative strategic asset allocation. It helps students, academics, and practitioners build investment portfolios based on advanced mathematical models with minimal effort. This guide will walk you through the installation, basic concepts, and main functionalities of Riskfolio-Lib.

## Table of Contents
1. [Installation](#installation)
2. [Basic Concepts](#basic-concepts)
3. [Portfolio Optimization Models](#portfolio-optimization-models)
4. [Step-by-Step Examples](#step-by-step-examples)
   - [Mean-Variance Optimization](#mean-variance-optimization)
   - [Risk Parity Portfolio](#risk-parity-portfolio)
   - [Custom Constraints](#custom-constraints)
5. [Plotting and Visualization](#plotting-and-visualization)
6. [Reporting](#reporting)
7. [Additional Resources](#additional-resources)

## Installation

You can install Riskfolio-Lib using pip:

```bash
pip install riskfolio-lib
```

Some advanced features may require additional dependencies, such as CVXPY solvers like MOSEK or CVXOPT. For optimal performance with large portfolios, consider installing these additional solvers.

## Basic Concepts

Riskfolio-Lib works with a `Portfolio` object that manages all aspects of the portfolio optimization process. Here's the basic workflow:

1. **Data Preparation**: Prepare your asset returns data as a pandas DataFrame
2. **Portfolio Object**: Create a Portfolio object with your data
3. **Parameters Estimation**: Calculate statistical parameters (returns, covariance, etc.)
4. **Optimization**: Run the optimization algorithm with desired parameters
5. **Analysis**: Analyze and visualize the results

## Portfolio Optimization Models

Riskfolio-Lib supports multiple portfolio optimization models:

1. **Mean-Risk Optimization**: 
   - Maximum Return Portfolio
   - Minimum Risk Portfolio
   - Maximum Risk-Adjusted Return Ratio Portfolio
   - Maximum Utility Portfolio

2. **Risk Parity Portfolio Optimization**

3. **Hierarchical Risk Parity (HRP)**

4. **Hierarchical Equal Risk Contribution (HERC)**

5. **Nested Clustered Optimization (NCO)**

The library supports 24 different risk measures including:
- Standard Deviation
- Mean Absolute Deviation
- Conditional Value at Risk (CVaR)
- Entropic Value at Risk (EVaR)
- Worst Realization (Minimax)
- Maximum Drawdown
- Many others

## Step-by-Step Examples

### Mean-Variance Optimization

Here's a basic example of how to run a mean-variance optimization:

```python
import numpy as np
import pandas as pd
import yfinance as yf
import riskfolio as rp
import matplotlib.pyplot as plt

# Download data
assets = ['AAPL', 'MSFT', 'AMZN', 'GOOG', 'META']
start_date = '2018-01-01'
end_date = '2023-01-01'

data = yf.download(assets, start=start_date, end=end_date)
data = data.loc[:, ('Adj Close', slice(None))]
data.columns = assets
returns = data.pct_change().dropna()

# Create the Portfolio object
port = rp.Portfolio(returns=returns)

# Calculate asset statistics
port.assets_stats(method_mu='hist', 
                  method_cov='hist')

# Optimize portfolio
model = 'Classic'  # Markowitz portfolio

# Select an objective function and a risk measure
objective = 'Sharpe'  # Maximize Sharpe ratio
rm = 'MV'  # Risk measure: Variance or standard deviation

# Constraints
constraints = {
    'Budget': 1,        # Fully invested
    'Weights_Sum': 1,   # Sum of weights = 1
    'Weights': [0, 1]   # Long-only (weights between 0 and 1)
}

# Optimize
w = port.optimization(model=model, 
                      obj=objective,
                      rm=rm,
                      rf=0.02,  # Risk-free rate
                      l=0,      # Risk aversion coefficient (not used with Sharpe)
                      hist=True)

print(w)

# Plot portfolio weights
ax = rp.plot_pie(w=w, title='Optimized Portfolio Weights', others=0.05, nrow=25, cmap="tab20")
plt.show()
```

### Risk Parity Portfolio

Here's how to create a risk parity portfolio:

```python
import numpy as np
import pandas as pd
import yfinance as yf
import riskfolio as rp
import matplotlib.pyplot as plt

# Download data
assets = ['AAPL', 'MSFT', 'AMZN', 'GOOG', 'META', 'JNJ', 'JPM', 'V', 'PG', 'XOM']
start_date = '2018-01-01'
end_date = '2023-01-01'

data = yf.download(assets, start=start_date, end=end_date)
data = data.loc[:, ('Adj Close', slice(None))]
data.columns = assets
returns = data.pct_change().dropna()

# Create the Portfolio object
port = rp.Portfolio(returns=returns)

# Calculate asset statistics
port.assets_stats(method_mu='hist', 
                  method_cov='hist')

# Optimize portfolio for Risk Parity
model = 'RP'  # Risk Parity
rm = 'MV'    # Risk measure: Variance or standard deviation

# Constraints
constraints = {
    'Budget': 1,
    'Weights_Sum': 1,
    'Weights': [0, 1]
}

# Optimize
w_rp = port.optimization(model=model,
                         rm=rm,
                         rf=0.02,
                         b=None,  # When None, the risk contribution is equal for all assets
                         hist=True)

print(w_rp)

# Plot portfolio weights
ax = rp.plot_pie(w=w_rp, title='Risk Parity Portfolio Weights', others=0.05, nrow=25, cmap="tab20")
plt.show()

# Plot risk contribution
ax = rp.plot_risk_con(w_rp, port.cov, rm=rm, rf=0.0, alpha=0.05, 
                      title='Risk Contribution', others=0.05, nrow=25, cmap="tab20")
plt.show()
```

### Custom Constraints

You can add custom constraints to your optimization:

```python
import numpy as np
import pandas as pd
import yfinance as yf
import riskfolio as rp
import matplotlib.pyplot as plt

# Download data
assets = ['AAPL', 'MSFT', 'AMZN', 'GOOG', 'META', 'JNJ', 'JPM', 'V', 'PG', 'XOM']
start_date = '2018-01-01'
end_date = '2023-01-01'

data = yf.download(assets, start=start_date, end=end_date)
data = data.loc[:, ('Adj Close', slice(None))]
data.columns = assets
returns = data.pct_change().dropna()

# Create the Portfolio object
port = rp.Portfolio(returns=returns)

# Calculate asset statistics
port.assets_stats(method_mu='hist', 
                  method_cov='hist')

# Define asset classes/sectors
asset_classes = {
    'Technology': ['AAPL', 'MSFT', 'GOOG'],
    'Retail': ['AMZN'],
    'Social Media': ['META'],
    'Healthcare': ['JNJ'],
    'Financial': ['JPM', 'V'],
    'Consumer': ['PG'],
    'Energy': ['XOM']
}

# Create constraints using constraints module
A, B = rp.assets_constraints(asset_classes, returns.columns)

# Add sector constraints (e.g., Technology <= 40%, Financial >= 15%)
A_sector = np.array([[1, 0, 0, 0, 0],  # Technology <= 40%
                     [0, 0, 0, 1, 0]])  # Financial >= 15%
B_sector = np.array([0.4, 0.15])

# Add custom constraints to the Ainequality matrix
if port.ainequality is None:
    port.ainequality = A
    port.binequality = B
else:
    port.ainequality = np.vstack([port.ainequality, A])
    port.binequality = np.append(port.binequality, B)

# Add sector constraints
port.ainequality = np.vstack([port.ainequality, A_sector @ A])
port.binequality = np.append(port.binequality, B_sector)

# Optimize portfolio
model = 'Classic'
objective = 'Sharpe'
rm = 'MV'

constraints = {
    'Budget': 1,
    'Weights_Sum': 1,
    'Weights': [0, 1]
}

w_constrained = port.optimization(model=model, 
                                  obj=objective,
                                  rm=rm,
                                  rf=0.02,
                                  l=0,
                                  hist=True)

print(w_constrained)

# Plot portfolio weights
ax = rp.plot_pie(w=w_constrained, title='Constrained Portfolio Weights', others=0.05, nrow=25, cmap="tab20")
plt.show()
```

## Plotting and Visualization

Riskfolio-Lib provides several visualization functions:

```python
import numpy as np
import pandas as pd
import yfinance as yf
import riskfolio as rp
import matplotlib.pyplot as plt

# Download data and prepare the Portfolio object as shown earlier
# ...

# Plot efficient frontier
points = 50  # Number of portfolios in efficient frontier
frontier = port.efficient_frontier(model='Classic', rm=rm, points=points, rf=0.02)

# Calculate returns and risks of frontier
returns_frontier = frontier.iloc[:, 0].values
risks_frontier = frontier.iloc[:, 1].values

# Calculate risk-return of individual assets
ret = port.mu.values
risk = np.sqrt(np.diag(port.cov.values))

# Plot frontier
ax = rp.plot_frontier(w_frontier=frontier, 
                      mu=port.mu, 
                      cov=port.cov, 
                      returns=returns_frontier, 
                      risks=risks_frontier, 
                      rf=0.02, 
                      alpha=0.05, 
                      cmap='viridis', 
                      w=w,  # Highlight optimized portfolio
                      label='Portfolio',
                      marker='*',
                      s=16,
                      c='r',
                      height=6,
                      width=10,
                      ax=None)

plt.show()

# Risk contribution plot
ax = rp.plot_risk_con(w=w, 
                      cov=port.cov, 
                      rm=rm, 
                      rf=0.02, 
                      alpha=0.05, 
                      title='Risk Contribution', 
                      others=0.05, 
                      nrow=25, 
                      cmap="tab20")
plt.show()

# Correlation matrix plot
ax = rp.plot_correlation(returns, 
                         graph=True, 
                         labels=True, 
                         encoding=None, 
                         dendrogram=True, 
                         cmap="viridis", 
                         linecolor="white", 
                         ax=None)
plt.show()
```

## Reporting

Riskfolio-Lib provides functions to create reports in Jupyter Notebook and Excel:

```python
import numpy as np
import pandas as pd
import yfinance as yf
import riskfolio as rp

# Download data and prepare the Portfolio object as shown earlier
# ...

# Create portfolio
w = port.optimization(model='Classic', 
                      obj='Sharpe', 
                      rm='MV', 
                      rf=0.02, 
                      l=0,
                      hist=True)

# Create Jupyter Notebook report
jupyter_report = rp.jupyter_report(returns, 
                                   w, 
                                   rf=0.02, 
                                   alpha=0.05, 
                                   model='Classic', 
                                   rm='MV', 
                                   hist=True, 
                                   objective='Sharpe', 
                                   risk_cont=True,
                                   benchmark=None)

# View the report
jupyter_report

# Create Excel report
excel_report = rp.excel_report(returns, 
                               w, 
                               rf=0.02, 
                               alpha=0.05, 
                               model='Classic', 
                               rm='MV', 
                               hist=True, 
                               objective='Sharpe', 
                               risk_cont=True,
                               benchmark=None,
                               file_name='portfolio_report.xlsx')
```

## Additional Resources

- [Riskfolio-Lib Documentation](https://riskfolio-lib.readthedocs.io/)
- [Riskfolio-Lib GitHub Repository](https://github.com/dcajasn/Riskfolio-Lib)
- [Portfolio Optimization Course](https://riskfolio-lib.readthedocs.io/en/latest/course.html)

This guide provides a solid foundation for getting started with Riskfolio-Lib. As you become more familiar with the library, you can explore its more advanced features such as:

- Black-Litterman model integration
- Factor models
- Advanced risk measures like Entropic Value at Risk
- Hierarchical clustering portfolio optimization
- Worst-case optimization

Riskfolio-Lib is a powerful tool that brings sophisticated portfolio optimization techniques within reach of Python users, allowing both beginners and advanced practitioners to build and test a wide range of investment strategies.