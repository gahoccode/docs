The page on Mean-Variance Optimization in PyPortfolioOpt provides a detailed description of how the library facilitates efficient frontier optimization using convex optimization techniques. Here's an extraction of the main content, including details on classes, methods, parameters, returns, and mathematical formulas:

### Introduction
Mathematical optimization, particularly convex optimization, is pivotal in finance and helps solve portfolio optimization problems. PyPortfolioOpt uses `cvxpy` to perform these optimizations easily.

### EfficientFrontier Class
The `EfficientFrontier` class is central for generating optimal portfolios based on various objective functions and parameters.

#### Constructor: `__init__`
- **Parameters:**
  - `expected_returns` (pd.Series, list, np.ndarray): Expected returns for each asset.
  - `cov_matrix` (pd.DataFrame or np.array): Covariance of returns for each asset.
  - `weight_bounds` (tuple or tuple list, optional): Bounds for weights, default is (0, 1).
  - `solver` (str): Solver name.
  - `verbose` (bool, optional): Flag for printing debugging info.
  - `solver_options` (dict, optional): Solver parameters.
- **Raises:**
  - `TypeError` if `expected_returns` is not a series, list or array.
  - `TypeError` if `cov_matrix` is not a dataframe or array.

#### Methods
- **`min_volatility()`**
  - Minimize portfolio volatility.
  - **Returns:** Asset weights (OrderedDict)

- **`max_sharpe(risk_free_rate=0.02)`**
  - Maximize the Sharpe Ratio.
  - **Parameters:**
    - `risk_free_rate` (float, optional): Risk-free rate, default 0.02.
  - **Returns:** Asset weights (OrderedDict)

- **`max_quadratic_utility(risk_aversion=1, market_neutral=False)`**
  - Maximize quadratic utility: \(\max_w w^T \mu - \frac \delta 2 w^T \Sigma w\).
  - **Parameters:**
    - `risk_aversion` (positive float): Risk aversion parameter, default 1.
    - `market_neutral` (bool, optional): Market neutrality flag, default False.
  - **Returns:** Asset weights (OrderedDict)

- **`efficient_risk(target_volatility, market_neutral=False)`**
  - Maximize return for a given target risk.
  - **Parameters:**
    - `target_volatility` (float): Desired maximum volatility.
  - **Returns:** Asset weights (OrderedDict)

- **`efficient_return(target_return, market_neutral=False)`**
  - Calculate the Markowitz portfolio: Minimize volatility for a given target return.
  - **Parameters:**
    - `target_return` (float): Desired return.
  - **Returns:** Asset weights (OrderedDict)

- **`portfolio_performance(verbose=False, risk_free_rate=0.02)`**
  - Calculate expected return, volatility, and Sharpe ratio.
  - **Parameters:**
    - `verbose` (bool, optional): Print performance flag.
    - `risk_free_rate` (float, optional): Risk-free rate, default 0.02.
  - **Returns:** (Expected return, volatility, Sharpe ratio) (tuple of float)

### Objective Functions
Objective functions are required for optimization, each accepting `weights` and either `expected_returns` or `cov_matrix`. 

Mathematical formulations:
- L2 Regularisation: \(\gamma ||w||^2\)
- Portfolio return: Negative mean return
- Portfolio variance: Total variance calculation
- Quadratic utility: \(\mu - \frac 1 2 \delta w^T \Sigma w\)
- Sharpe ratio: Negative Sharpe ratio

### Convex Optimization Problem Form
Minimize: 
\[
\begin{align*} 
\underset{\mathbf{x}}{\text{minimise}} & \quad f(\mathbf{x}) \\
\text{subject to} & \quad g_i(\mathbf{x}) \leq 0, \quad i = 1, \ldots, m \\
& \quad A\mathbf{x} = b 
\end{align*}
\]
where \(\mathbf{x} \in \mathbb{R}^n\), and \(f(\mathbf{x}), g_i(\mathbf{x})\) are convex functions.

### Tips and Caveats
- L2 Regularisation: Used to produce more non-negligible weights in the portfolio.
- Solver selection: PyPortfolioOpt uses `cvxpy`'s default solver settings, but you can specify a solver.

This concise extraction covers the core functionalities and mathematical underpinnings of PyPortfolioOpt's Mean-Variance Optimization as found in the documentation.
