The excerpt is from the page on "Other Optimizers" from PyPortfolioOpt documentation. It describes alternative portfolio optimization methods beyond the efficient frontier methods, namely Hierarchical Risk Parity (HRP) and the Critical Line Algorithm (CLA). Below is the extract including methods, parameters, returns, return types, and any notable formulas or explanations.

---

## Other Optimizers

Efficient frontier methods involve the direct optimization of an objective subject to constraints. PyPortfolioOpt provides support for alternative schemes, like HRP and CLA, inheriting from `BaseOptimizer` or `BaseConvexOptimizer`.

### Hierarchical Risk Parity (HRP)

HRP is a portfolio optimization method developed by Marcos Lopez de Prado. The process involves:

1. Forming a distance matrix based on asset correlations.
2. Clustering assets into a tree via hierarchical clustering.
3. Forming the minimum variance portfolio within each tree branch.
4. Iteratively combining mini-portfolios at each node.

#### `HRPOpt` Class

- **Instance variables:**
  - Inputs:
    - `n_assets` - int
    - `tickers` - str list
    - `returns` - pd.DataFrame
  - Output:
    - `weights` - np.ndarray
    - `clusters` - linkage matrix

- **Public methods:**
  - `optimize(linkage_method='single')`: Computes HRP weights using SciPy hierarchical clustering.
    - **Parameters:** `linkage_method` (str) – which SciPy linkage method to use.
    - **Returns:** Weights for the HRP portfolio.
    - **Return type:** OrderedDict

  - `portfolio_performance(verbose=False, risk_free_rate=0.02, frequency=252)`: Calculates expected return, volatility, and Sharpe ratio for the optimized portfolio.
    - **Parameters:**
      - `verbose` (bool) – whether to print performance, defaults to False
      - `risk_free_rate` (float) – defaults to 0.02
      - `frequency` (int) – defaults to 252
    - **Returns:** Expected return, volatility, Sharpe ratio.
    - **Return type:** (float, float, float)

### The Critical Line Algorithm (CLA)

CLA is designed for portfolio optimization, efficiently deriving the entire efficient frontier, particularly when applying linear inequalities.

#### `CLA` Class

- **Instance variables:**
  - Inputs:
    - `n_assets` - int
    - `tickers` - str list
    - `mean` - np.ndarray
    - `cov_matrix` - np.ndarray
  - Outputs:
    - `weights` - np.ndarray

- **Public methods:**
  - `max_sharpe()`: Optimizes for the maximal Sharpe ratio.
    - **Returns:** Asset weights for the max-sharpe portfolio.
    - **Return type:** OrderedDict

  - `min_volatility()`: Optimizes for minimum volatility.
    - **Returns:** Asset weights for the volatility-minimizing portfolio.
    - **Return type:** OrderedDict

  - `portfolio_performance(verbose=False, risk_free_rate=0.02)`: Calculates expected return, volatility, and Sharpe ratio.
    - **Parameters:**
      - `verbose` (bool) – verbose output toggle
      - `risk_free_rate` (float) – defaults to 0.02
    - **Returns:** Expected return, volatility, Sharpe ratio.
    - **Return type:** (float, float, float)

### Implementing Your Own Optimizer

To create a custom optimizer, extend `BaseOptimizer` or `BaseConvexOptimizer` using utility methods like `clean_weights()`.

#### `BaseOptimizer` Class

- **Public methods:**
  - `set_weights(input_weights)`: Sets `self.weights` from a weights dictionary.
  - `clean_weights(cutoff=0.0001, rounding=5)`: Rounds weights and clips near-zero values.
    - **Returns:** Cleaned asset weights.
    - **Return type:** OrderedDict

#### `BaseConvexOptimizer` Class

- **Public methods:**
  - `add_constraint(new_constraint)`: Adds a DCP-compliant constraint.
  - `add_objective(new_objective, **kwargs)`: Adds a convex term into the objective function.

#### `portfolio_performance`

Utility function to evaluate return and risk for a given set of portfolio weights.

---

For the mathematical formulas or detailed explanations, users should refer to MARcos Lopez de Prado's works cited within the document.
