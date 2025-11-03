The page covers the `plotting` module in PyPortfolioOpt, which assists in creating visualizations for portfolio optimization tasks. It outlines multiple plotting functions, parameters, and usage examples. Below is a detailed outline:

### Plotting Efficient Frontier

The `plotting` module allows visualization of the efficient frontier using various parameters like risk, utility, and return.

**Example:**
```python
ef = EfficientFrontier(mu, S, weight_bounds=(None, None))
ef.add_constraint(lambda w: w[0] >= 0.2)
ef.add_constraint(lambda w: w[2] == 0.15)
ef.add_constraint(lambda w: w[3] + w[4] <= 0.10)

fig, ax = plt.subplots()
plotting.plot_efficient_frontier(ef, ax=ax, show_assets=True)
plt.show()
```

For more parameters:
```python
risk_range = np.linspace(0.10, 0.40, 100)
plotting.plot_efficient_frontier(ef, ef_param="risk", ef_param_range=risk_range,
                                 show_assets=True, showfig=True)
```

**Complex Example:**
```python
fig, ax = plt.subplots()
ef_max_sharpe = ef.deepcopy()
plotting.plot_efficient_frontier(ef, ax=ax, show_assets=False)

ef_max_sharpe.max_sharpe()
ret_tangent, std_tangent, _ = ef_max_sharpe.portfolio_performance()
ax.scatter(std_tangent, ret_tangent, marker="*", s=100, c="r", label="Max Sharpe")

n_samples = 10000
w = np.random.dirichlet(np.ones(ef.n_assets), n_samples)
rets = w.dot(ef.expected_returns)
stds = np.sqrt(np.diag(w @ ef.cov_matrix @ w.T))
sharpes = rets / stds
ax.scatter(stds, rets, marker=".", c=sharpes, cmap="viridis_r")

ax.set_title("Efficient Frontier with random portfolios")
ax.legend()
plt.tight_layout()
plt.savefig("ef_scatter.png", dpi=200)
plt.show()
```

### Plotting Functions

#### `plot_covariance`

Generates a plot of the covariance or correlation matrix.

**Parameters:**
- **`cov_matrix`**: (DataFrame or ndarray) - Covariance matrix.
- **`plot_correlation`**: (bool, optional) - Plot correlation matrix instead, defaults to False.
- **`show_tickers`**: (bool, optional) - Use tickers as labels, defaults to True.

**Returns:** matplotlib axis

#### `plot_dendrogram`

Plots clusters as a dendrogram.

**Parameters:**
- **`hrp`**: The HRPpt object already optimized.
- **`show_tickers`**: (bool, optional) - Ticker labels, defaults to True.
- **`filename`**: (str, optional) - Save plot as a file, defaults to None.
- **`showfig`**: (bool, optional) - Show the figure, defaults to False.

**Returns:** matplotlib axis

#### `plot_efficient_frontier`

Plots the efficient frontier using a CLA or EfficientFrontier object.

**Parameters:**
- **`opt`**: (EfficientFrontier or CLA) - Instantiated optimizer before optimization.
- **`ef_param`**: (str) - Parameter for range (utility, risk, return), defaults to "return".
- **`ef_param_range`**: (array or list) - Parameter value range using `np.arange` or `np.linspace`.
- **`points`**: (int, optional) - Number of plotted points, defaults to 100.
- **`show_assets`**: (bool, optional) - Include asset risks/returns, defaults to True.
- **`show_tickers`**: (bool, optional) - Annotate each asset with ticker, defaults to False.
- **`filename`**: (str, optional) - Save to file, defaults to None.
- **`showfig`**: (bool, optional) - Show figure, defaults to False.

**Returns:** matplotlib axis

#### `plot_weights`

Plots the portfolio weights as a horizontal bar chart.

**Parameters:**
- **`weights`**: ({ticker: weight} dict) - Weights from PyPortfolioOpt optimizer.
- **`ax`**: (matplotlib.axes) - Axis to plot to, optional.

**Returns:** matplotlib axis

### Additional Information

- To save a plot, use `filename="somefile.png"` as a keyword argument. This is processed by the `_plot_io()` helper method, which also manages plot display settings like DPI and whether to show the figure.
- Mathematical functions like `np.linspace` can help in defining ranges for multi-point plotting.

The documentation provides visual examples and links to associated figures in the guide.
