# skfolio: Portfolio Optimization Framework

## Overview

**skfolio** is a Python library for portfolio optimization built on top of scikit-learn. It offers a unified interface and tools compatible with scikit-learn to build, fine-tune, and cross-validate portfolio models.

The framework addresses many shortcomings of traditional Mean-Variance Optimization (MVO) approach, including high sensitivity to input parameters, weight concentration, high turnover, and poor out-of-sample performance.

skfolio integrates numerous advanced portfolio optimization approaches (shrinkage, regularization, risk-parity, hierarchical clustering, etc.) with a machine-learning approach to perform model selection, validation, and parameter tuning while mitigating the risk of data leakage and overfitting.

> ⚠️ **Note:** The package is still under active development. The first stable version (1.0.0) is planned for release in early 2025. Until then, pinning versions is recommended if you are concerned about breaking changes.

## Installation

```bash
pip install skfolio
```

## Key Concepts

### Modern Portfolio Theory Evolution

Since Markowitz's development of modern portfolio theory (1952), mean-variance optimization (MVO) has been widely used but faces several limitations, including:

- High sensitivity to input parameters (expected returns and covariance)
- Weight concentration
- High turnover
- Poor out-of-sample performance

Research has shown that naive allocation strategies (1/N, inverse-vol, etc.) often outperform MVO out-of-sample (DeMiguel, 2007).

To address these shortcomings, skfolio integrates numerous approaches:
- Shrinkage estimators
- Additional constraints
- Regularization
- Uncertainty sets
- Higher moments
- Bayesian approaches
- Coherent risk measures
- Left-tail risk optimization
- Distributionally robust optimization
- Factor models
- Risk-parity
- Hierarchical clustering
- Ensemble methods
- Pre-selection techniques

## Core Features

### Portfolio Optimization Models

#### Naive Models
- **Equal-Weighted**: Simple 1/N allocation strategy
  - Parameters:
    - `portfolio_params` (dict): Parameters passed to Portfolio object

- **Inverse-Volatility**: Weight assets inversely proportional to their volatility
  - Parameters:
    - `risk_free_rate` (float): Risk-free rate used for returns calculation (default: 0)
    - `prior_estimator` (object): Estimator for prior model (default: EmpiricalPrior())
    - `portfolio_params` (dict): Parameters passed to Portfolio object

- **Random (Dirichlet)**: Random weight allocation for benchmarking
  - Parameters:
    - `alpha` (float/array): Dirichlet distribution parameter (default: 1.0)
    - `random_state` (int): Seed for random number generator
    - `portfolio_params` (dict): Parameters passed to Portfolio object

#### Convex Optimization Models
- **Mean-Risk**: Implements various risk measures and objective functions
  - Parameters:
    - `objective_function` (ObjectiveFunction): Optimization objective (default: MINIMIZE_RISK)
    - `risk_measure` (RiskMeasure): Risk measure to use (default: VARIANCE)
    - `alpha` (float): Confidence level for risk measures (default: 0.95)
    - `mu_target` (float): Target return constraint (default: None)
    - `risk_target` (float): Target risk constraint (default: None)
    - `risk_free_rate` (float): Risk-free rate (default: 0)
    - `min_weights` (float/dict): Minimum weight constraints (default: 0)
    - `max_weights` (float/dict): Maximum weight constraints (default: 1)
    - `budget` (tuple): Budget constraint bounds (default: (1, 1))
    - `groups` (list): Asset groups for group constraints
    - `linear_constraints` (list): Additional linear constraints
    - `l1_coef` (float): L1 regularization coefficient (default: 0)
    - `l2_coef` (float): L2 regularization coefficient (default: 0)
    - `transaction_costs` (float/dict): Transaction costs (default: 0)
    - `management_fees` (float/dict): Management fees (default: 0)
    - `mu_uncertainty_set_estimator` (object): Uncertainty set for expected returns
    - `covariance_uncertainty_set_estimator` (object): Uncertainty set for covariance
    - `prior_estimator` (object): Estimator for prior model (default: EmpiricalPrior())
    - `cardinality_constraints` (int): Maximum number of assets in portfolio
    - `threshold_constraints` (float): Min threshold for non-zero weights
    - `portfolio_params` (dict): Parameters passed to Portfolio object

- **Risk Budgeting**: Allocate portfolio risk equally among assets
  - Parameters:
    - `risk_measure` (RiskMeasure): Risk measure to use (default: VARIANCE)
    - `budgets` (array): Custom budget weights (default: None for equal risk allocation)
    - `alpha` (float): Confidence level for risk measures (default: 0.95)
    - `min_weights` (float/dict): Minimum weight constraints (default: 0)
    - `max_weights` (float/dict): Maximum weight constraints (default: 1)
    - `budget` (tuple): Budget constraint bounds (default: (1, 1))
    - `prior_estimator` (object): Estimator for prior model (default: EmpiricalPrior())
    - `portfolio_params` (dict): Parameters passed to Portfolio object

- **Maximum Diversification**: Maximize diversification ratio
  - Parameters:
    - `min_weights` (float/dict): Minimum weight constraints (default: 0)
    - `max_weights` (float/dict): Maximum weight constraints (default: 1)
    - `budget` (tuple): Budget constraint bounds (default: (1, 1))
    - `groups` (list): Asset groups for group constraints
    - `linear_constraints` (list): Additional linear constraints
    - `prior_estimator` (object): Estimator for prior model (default: EmpiricalPrior())
    - `portfolio_params` (dict): Parameters passed to Portfolio object

- **Distributionally Robust CVaR**: Optimize considering worst-case CVaR
  - Parameters:
    - `objective_function` (ObjectiveFunction): Optimization objective (default: MINIMIZE_RISK)
    - `alpha` (float): Confidence level for CVaR (default: 0.95)
    - `radius` (float): Wasserstein radius (uncertainty level)
    - `norm` (int): Norm used in the Wasserstein distance (default: 2)
    - `risk_free_rate` (float): Risk-free rate (default: 0)
    - `min_weights` (float/dict): Minimum weight constraints (default: 0)
    - `max_weights` (float/dict): Maximum weight constraints (default: 1)
    - `budget` (tuple): Budget constraint bounds (default: (1, 1))
    - `prior_estimator` (object): Estimator for prior model (default: EmpiricalPrior())
    - `portfolio_params` (dict): Parameters passed to Portfolio object

#### Clustering-Based Models
- **Hierarchical Risk Parity**: Use hierarchical clustering to allocate investments
  - Parameters:
    - `risk_measure` (RiskMeasure): Risk measure to use (default: VARIANCE)
    - `alpha` (float): Confidence level for risk measures (default: 0.95)
    - `distance_estimator` (object): Estimator for distance matrix (default: PearsonDistance())
    - `hierarchical_clustering_estimator` (object): Estimator for hierarchical clustering
    - `order_method` (OrderMethod): Method for ordering clusters (default: HIERARCHICAL)
    - `min_weights` (float/dict): Minimum weight constraints (default: 0)
    - `max_weights` (float/dict): Maximum weight constraints (default: 1)
    - `budget` (tuple): Budget constraint bounds (default: (1, 1))
    - `prior_estimator` (object): Estimator for prior model (default: EmpiricalPrior())
    - `portfolio_params` (dict): Parameters passed to Portfolio object

- **Hierarchical Equal Risk Contribution**: Balance risk contribution across cluster hierarchy
  - Parameters:
    - `risk_measure` (RiskMeasure): Risk measure to use (default: VARIANCE)
    - `alpha` (float): Confidence level for risk measures (default: 0.95)
    - `distance_estimator` (object): Estimator for distance matrix (default: PearsonDistance())
    - `hierarchical_clustering_estimator` (object): Estimator for hierarchical clustering
    - `order_method` (OrderMethod): Method for ordering clusters (default: HIERARCHICAL)
    - `min_weights` (float/dict): Minimum weight constraints (default: 0)
    - `max_weights` (float/dict): Maximum weight constraints (default: 1)
    - `budget` (tuple): Budget constraint bounds (default: (1, 1))
    - `prior_estimator` (object): Estimator for prior model (default: EmpiricalPrior())
    - `portfolio_params` (dict): Parameters passed to Portfolio object

- **Nested Clusters Optimization**: Optimize within and between hierarchical clusters
  - Parameters:
    - `inner_estimator` (object): Estimator for inner optimization (within clusters)
    - `outer_estimator` (object): Estimator for outer optimization (between clusters)
    - `distance_estimator` (object): Estimator for distance matrix (default: PearsonDistance())
    - `hierarchical_clustering_estimator` (object): Estimator for hierarchical clustering
    - `cv` (object): Cross-validation strategy (default: None)
    - `n_jobs` (int): Number of parallel jobs (default: None)
    - `verbose` (int): Verbosity level (default: 0)
    - `portfolio_params` (dict): Parameters passed to Portfolio object

#### Ensemble Methods
- **Stacking Optimization**: Combine multiple portfolio optimization strategies
  - Parameters:
    - `base_estimators` (list): List of portfolio optimization estimators
    - `final_estimator` (object): Estimator used to combine base estimators
    - `cv` (object): Cross-validation strategy (default: None)
    - `n_jobs` (int): Number of parallel jobs (default: None)
    - `verbose` (int): Verbosity level (default: 0)
    - `portfolio_params` (dict): Parameters passed to Portfolio object

### Estimators

#### Expected Returns Estimators
- **Empirical**: Estimate using historical data
  - Parameters:
    - `risk_free_rate` (float): Risk-free rate (default: 0)

- **Exponentially Weighted (EWMu)**: Weight recent observations more heavily
  - Parameters:
    - `alpha` (float): Smoothing factor between 0 and 1 (default: 0.5)
    - `risk_free_rate` (float): Risk-free rate (default: 0)
    - `adjust` (bool): Adjust for biased estimation (default: True)

- **Equilibrium**: Use market equilibrium assumptions
  - Parameters:
    - `risk_aversion` (float): Risk aversion parameter (default: 1.0)
    - `risk_free_rate` (float): Risk-free rate (default: 0)
    - `covariance_estimator` (object): Estimator for covariance (default: EmpiricalCovariance())

- **Shrinkage (ShrunkMu)**: Reduce estimation error through shrinkage
  - Parameters:
    - `shrinkage` (float): Shrinkage parameter between 0 and 1 (default: 0.5)
    - `prior_mu` (float/array): Prior estimate of mean returns (default: 0)
    - `risk_free_rate` (float): Risk-free rate (default: 0)

#### Covariance Estimators
- **Empirical**: Sample covariance matrix
  - Parameters:
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)

- **Gerber**: Robust covariance estimation
  - Parameters:
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)

- **Denoising (DenoiseCovariance)**: Remove noise from empirical correlations
  - Parameters:
    - `denoise_method` (str): Method for denoising ('trim' or 'shrink') (default: 'trim')
    - `alpha` (float): Parameter controlling denoising intensity (default: None)
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)

- **Detoning (DetoneCovariance)**: Remove common market factors
  - Parameters:
    - `n_components` (int): Number of eigenvectors to remove (default: 1)
    - `market_component` (bool): Remove market component (default: True)
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)

- **Exponentially Weighted (EWCovariance)**: Weight recent observations more heavily
  - Parameters:
    - `alpha` (float): Smoothing factor between 0 and 1 (default: 0.5)
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)
    - `adjust` (bool): Adjust for biased estimation (default: True)

- **Ledoit-Wolf (LedoitWolfCovariance)**: Shrinkage toward structured target
  - Parameters:
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)
    - `block_size` (int): Size of blocks for computation (default: 1000)

- **Oracle Approximating Shrinkage (OASCovariance)**: Data-driven shrinkage
  - Parameters:
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)

- **Shrunk Covariance (ShrunkCovariance)**: Shrinkage toward diagonal target
  - Parameters:
    - `shrinkage` (float): Shrinkage parameter between 0 and 1 (default: 0.1)
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)

- **Graphical Lasso CV (GraphicalLassoCV)**: Sparse precision matrix estimation
  - Parameters:
    - `alphas` (int/array): Range of alpha values to try (default: 4)
    - `n_refinements` (int): Number of times to refine alpha grid (default: 4)
    - `cv` (int/object): Cross-validation strategy (default: None)
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `tol` (float): Convergence tolerance (default: 1e-4)
    - `max_iter` (int): Maximum number of iterations (default: 100)
    - `verbose` (bool): Verbosity flag (default: False)

- **Implied Covariance**: Derived from option prices
  - Parameters:
    - `frequency` (int): Number of periods per year for annualization (default: 252)
    - `store_precision` (bool): Store precision matrix (default: True)
    - `assume_centered` (bool): Whether data is centered (default: False)
    - `market_data` (DataFrame): Market data including implied volatilities

#### Distance Estimators
- **Pearson Distance**: Based on Pearson correlation
  - Parameters:
    - `absolute` (bool): Use absolute values of correlations (default: False)
    - `covariance_estimator` (object): Estimator for covariance (default: EmpiricalCovariance())

- **Kendall Distance**: Based on Kendall rank correlation
  - Parameters:
    - `absolute` (bool): Use absolute values of correlations (default: False)

- **Spearman Distance**: Based on Spearman rank correlation
  - Parameters:
    - `absolute` (bool): Use absolute values of correlations (default: False)

- **Covariance Distance**: Distance metrics derived from covariance
  - Parameters:
    - `absolute` (bool): Use absolute values of correlations (default: False)
    - `covariance_estimator` (object): Estimator for covariance (default: EmpiricalCovariance())

- **Distance Correlation**: Measures dependence between random vectors
  - Parameters:
    - None specific to this estimator

- **Variation of Information**: Information-theoretic distance
  - Parameters:
    - `bins` (int): Number of bins for discretization (default: 'auto')
    - `method` (str): Method for entropy calculation (default: 'ml')

#### Distribution Estimators
- **Univariate**:
  - **Gaussian**: Normal distribution
    - Parameters:
      - `log_transform` (bool): Apply log transformation (default: False)
  
  - **Student's t**: t-distribution
    - Parameters:
      - `log_transform` (bool): Apply log transformation (default: False)
  
  - **Johnson Su**: Johnson SU distribution
    - Parameters:
      - `log_transform` (bool): Apply log transformation (default: False)
  
  - **Normal Inverse Gaussian**: NIG distribution
    - Parameters:
      - `log_transform` (bool): Apply log transformation (default: False)

- **Bivariate Copula**:
  - Parameters common to all copula types:
    - `copula_type` (CopulaType): Type of copula (GAUSSIAN, STUDENT, CLAYTON, etc.)
    - `rotation` (int): Degrees of rotation (0, 90, 180, 270)

- **Multivariate**:
  - **Vine Copula**: Flexible multivariate dependence modeling
    - Parameters:
      - `vine_type` (VineType): Type of vine structure (default: REGULAR)
      - `log_transform` (bool): Apply log transformation (default: False)
      - `central_assets` (list): Assets to use as central nodes (default: None)
      - `truncation_level` (int): Level of truncation (default: None)
      - `empirical_marginals` (bool): Use empirical marginals (default: False)
      - `n_jobs` (int): Number of parallel jobs (default: None)
      - `verbose` (int): Verbosity level (default: 0)

#### Prior Estimators
- **Empirical**: Based on historical data
  - Parameters:
    - `mu_estimator` (object): Expected returns estimator (default: EmpiricalMu())
    - `covariance_estimator` (object): Covariance estimator (default: EmpiricalCovariance())

- **Black & Litterman**: Incorporate investor views
  - Parameters:
    - `views` (list/dict): Investor views on expected returns
    - `confidences` (list/float): Confidence in views (default: 1.0)
    - `tau` (float): Weight on prior (default: 0.05)
    - `risk_aversion` (float): Risk aversion parameter (default: 1.0)
    - `market_prices` (array): Market capitalization weights (default: None)
    - `risk_free_rate` (float): Risk-free rate (default: 0)
    - `covariance_estimator` (object): Covariance estimator (default: EmpiricalCovariance())
    - `solve_equilibrium` (bool): Solve for equilibrium (default: True)

- **Factor Model**: Based on factor exposures
  - Parameters:
    - `factor_prior_estimator` (object): Prior estimator for factors (default: EmpiricalPrior())
    - `common_factor_estimator` (bool): Estimate common factor (default: False)
    - `fit_intercept` (bool): Include intercept in model (default: True)
    - `noise` (float): Noise level for returns (default: 1e-10)
    - `robust` (bool): Use robust regression (default: False)

- **Synthetic Data**: Generate stressed scenarios
  - Parameters:
    - `distribution_estimator` (object): Estimator for distributions
    - `n_samples` (int): Number of samples to generate (default: None)
    - `sample_args` (dict): Arguments for sample method (default: None)
    - `fix_seed` (int): Random seed for reproducibility (default: None)

#### Uncertainty Set Estimators
- **On Expected Returns**:
  - **Empirical**: Based on historical data
    - Parameters:
      - `radius` (float): Radius of uncertainty set
  
  - **Circular Bootstrap (BootstrapMuUncertaintySet)**: Bootstrap-based uncertainty
    - Parameters:
      - `radius` (float): Radius of uncertainty set
      - `n_samples` (int): Number of bootstrap samples (default: 1000)
      - `block_size` (int): Size of blocks for circular bootstrap (default: 21)
      - `alpha` (float): Confidence level (default: 0.95)

- **On Covariance**:
  - **Empirical**: Based on historical data
    - Parameters:
      - `radius` (float): Radius of uncertainty set
  
  - **Circular Bootstrap (BootstrapCovarianceUncertaintySet)**: Bootstrap-based uncertainty
    - Parameters:
      - `radius` (float): Radius of uncertainty set
      - `n_samples` (int): Number of bootstrap samples (default: 1000)
      - `block_size` (int): Size of blocks for circular bootstrap (default: 21)
      - `alpha` (float): Confidence level (default: 0.95)

### Pre-Selection Transformers
- **Non-Dominated Selection**: Select efficient assets
  - Parameters:
    - `objective_functions` (list): List of objective functions to consider (default: [MAXIMIZE_MEAN, MINIMIZE_VARIANCE])
    - `n` (int): Number of assets to select (default: None for all non-dominated)

- **Select K Extremes**: Choose best or worst performers
  - Parameters:
    - `k` (int): Number of assets to select
    - `measure` (Measure): Measure to rank assets (default: MEAN)
    - `highest` (bool): Select highest (True) or lowest (False) values (default: True)

- **Drop Highly Correlated Assets**: Remove redundant assets
  - Parameters:
    - `threshold` (float): Correlation threshold above which to drop assets (default: 0.7)
    - `method` (str): Method for selecting which asset to drop ('min_mean', 'max_mean', 'min_variance', 'max_variance') (default: 'min_mean')
    - `absolute` (bool): Use absolute correlation values (default: True)

- **Select Non-Expiring Assets**: Filter out delisted assets
  - Parameters:
    - `min_length` (float): Minimum fraction of data points required (default: 1.0)

- **Select Complete Assets**: Handle missing data
  - Parameters:
    - `drop_inf` (bool): Drop assets with infinity values (default: True)
    - `threshold` (float): Maximum fraction of missing values allowed (default: 0)

### Cross-Validation and Model Selection
- Compatible with all `sklearn` methods (KFold, etc.)

- **Walk Forward**: Time series validation
  - Parameters:
    - `train_size` (int): Number of training samples
    - `test_size` (int): Number of test samples
    - `step` (int): Step between consecutive windows (default: 1)
    - `start_train_pct` (float): Percentage of data for first train set (default: None)
    - `start_test_pct` (float): Percentage of data for first test set (default: None)
    - `end_train_pct` (float): Percentage of data for last train set (default: None)
    - `end_test_pct` (float): Percentage of data for last test set (default: None)

- **Combinatorial Purged Cross-Validation**: Avoid data leakage
  - Parameters:
    - `n_folds` (int): Total number of folds
    - `n_test_folds` (int): Number of folds used for testing
    - `embargo` (float): Fraction of data to embargo between train and test sets (default: 0)
    - `purge` (bool): Whether to purge overlapping returns (default: True)

### Risk Measures
skfolio implements various risk measures, accessible through the `RiskMeasure` enum:

- **Variance**: Standard deviation squared
  ```python
  risk_measure=RiskMeasure.VARIANCE
  ```

- **Semi-Variance**: Downside deviation squared
  ```python
  risk_measure=RiskMeasure.SEMI_VARIANCE
  ```

- **Mean Absolute Deviation**: Average absolute deviation from mean
  ```python
  risk_measure=RiskMeasure.MAD
  ```

- **First Lower Partial Moment**: Expected shortfall below mean
  ```python
  risk_measure=RiskMeasure.FLPM
  ```

- **CVaR** (Conditional Value at Risk): Expected shortfall beyond VaR
  ```python
  risk_measure=RiskMeasure.CVAR
  alpha=0.95  # Confidence level
  ```

- **EVaR** (Entropic Value at Risk): Upper bound of CVaR
  ```python
  risk_measure=RiskMeasure.EVAR
  alpha=0.95  # Confidence level
  ```

- **Worst Realization**: Worst observed return
  ```python
  risk_measure=RiskMeasure.WORST_REALIZATION
  ```

- **CDaR** (Conditional Drawdown at Risk): Expected drawdown beyond DaR
  ```python
  risk_measure=RiskMeasure.CDAR
  alpha=0.95  # Confidence level
  ```

- **Maximum Drawdown**: Maximum peak-to-trough decline
  ```python
  risk_measure=RiskMeasure.MAX_DRAWDOWN
  ```

- **Average Drawdown**: Mean of all drawdowns
  ```python
  risk_measure=RiskMeasure.AVERAGE_DRAWDOWN
  ```

- **EDaR** (Entropic Drawdown at Risk): Upper bound of CDaR
  ```python
  risk_measure=RiskMeasure.EDAR
  alpha=0.95  # Confidence level
  ```

- **Ulcer Index**: Root mean square of drawdowns
  ```python
  risk_measure=RiskMeasure.ULCER_INDEX
  ```

- **Gini Mean Difference**: Average of absolute differences between returns
  ```python
  risk_measure=RiskMeasure.GINI_MEAN_DIFFERENCE
  ```

- **Value at Risk**: Quantile of return distribution
  ```python
  risk_measure=RiskMeasure.VAR
  alpha=0.95  # Confidence level
  ```

- **Drawdown at Risk**: Quantile of drawdown distribution
  ```python
  risk_measure=RiskMeasure.DAR
  alpha=0.95  # Confidence level
  ```

- **Entropic Risk Measure**: Exponential risk measure
  ```python
  

## Practical Examples

### Basic Usage

```python
# Import necessary modules
from sklearn.model_selection import train_test_split
from skfolio import RiskMeasure
from skfolio.datasets import load_sp500_dataset
from skfolio.optimization import MeanRisk
from skfolio.preprocessing import prices_to_returns

# Load dataset and convert prices to returns
prices = load_sp500_dataset()
X = prices_to_returns(prices)
X_train, X_test = train_test_split(X, test_size=0.33, shuffle=False)

# Create and fit a minimum variance model
model = MeanRisk()
model.fit(X_train)

# Predict portfolio performance on test set
portfolio = model.predict(X_test)

# View results
print(portfolio.annualized_sharpe_ratio)
print(portfolio.summary())
```

### Maximum Sharpe Ratio Optimization

```python
from skfolio.optimization import MeanRisk, ObjectiveFunction

# Create a Maximum Sharpe Ratio model
model = MeanRisk(
    risk_measure=RiskMeasure.STANDARD_DEVIATION,
    objective_function=ObjectiveFunction.MAXIMIZE_RATIO,
    portfolio_params=dict(name="Max Sharpe"),
)

# Fit the model on training data
model.fit(X_train)

# Get the optimal weights
print(model.weights_)

# Predict on test data
portfolio = model.predict(X_test)

# Evaluate performance
print(f"Annualized Sharpe Ratio: {portfolio.annualized_sharpe_ratio}")
```

### Risk Parity Portfolio

```python
from skfolio.optimization import RiskBudgeting

# Create a risk parity model using variance as risk measure
model = RiskBudgeting(
    risk_measure=RiskMeasure.VARIANCE,
    portfolio_params=dict(name="Risk Parity - Variance"),
)

# Fit the model
model.fit(X_train)

# Get optimal weights
print(model.weights_)

# Analyze risk contribution
portfolio = model.predict(X_train)
portfolio.plot_contribution(measure=RiskMeasure.ANNUALIZED_VARIANCE)
```

### Advanced Optimization with Constraints

```python
from skfolio.optimization import MeanRisk, ObjectiveFunction

# Create model with constraints
model = MeanRisk(
    objective_function=ObjectiveFunction.MAXIMIZE_RATIO,
    risk_measure=RiskMeasure.CVAR,
    min_weights={"AAPL": 0.10, "JPM": 0.05},  # Minimum position in specific assets
    max_weights=0.8,  # Maximum position in any asset
    transaction_costs={"AAPL": 0.0001, "RRC": 0.0002},  # Asset-specific transaction costs
    groups=[
        ["Equity"] * 3 + ["Fund"] * 5 + ["Bond"] * 12,
        ["US"] * 2 + ["Europe"] * 8 + ["Japan"] * 10,
    ],
    linear_constraints=[
        "Equity <= 0.5 * Bond",
        "US >= 0.1",
        "Europe >= 0.5 * Fund",
        "Japan <= 1",
    ],
)

# Fit the model
model.fit(X_train)
```

### Hierarchical Risk Parity with CVaR

```python
from skfolio.optimization import HierarchicalRiskParity

# Create a Hierarchical Risk Parity model using CVaR as risk measure
model = HierarchicalRiskParity(
    risk_measure=RiskMeasure.CVAR, 
    portfolio_params=dict(name="HRP-CVaR")
)

# Fit the model
model.fit(X_train)

# Analyze clusters with dendrogram
model.hierarchical_clustering_estimator_.plot_dendrogram(heatmap=True)

# Predict performance
portfolio = model.predict(X_test)
print(portfolio.summary())
```

### Factor Model Integration

```python
from skfolio.datasets import load_factors_dataset
from skfolio.prior import FactorModel

# Load asset and factor data
factor_prices = load_factors_dataset()
X, y = prices_to_returns(prices, factor_prices)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, shuffle=False)

# Create model with factor model as prior estimator
model = MeanRisk(prior_estimator=FactorModel())
model.fit(X_train, y_train)

# Predict using the factor model
portfolio = model.predict(X_test)
print(portfolio.calmar_ratio)
```

### Black-Litterman Model

```python
from skfolio.prior import BlackLitterman

# Define investor views
views = ["AAPL - BBY == 0.03 ", "CVX - KO == 0.04", "MSFT == 0.06 "]

# Create Black-Litterman model
model = MeanRisk(
    objective_function=ObjectiveFunction.MAXIMIZE_RATIO,
    prior_estimator=BlackLitterman(views=views),
)

# Fit and evaluate
model.fit(X_train)
portfolio = model.predict(X_test)
```

### Cross-Validation

```python
from sklearn.model_selection import KFold
from skfolio import cross_val_predict

# Create model
model = MeanRisk()

# Perform cross-validation
mmp = cross_val_predict(model, X_test, cv=KFold(n_splits=5))

# Analyze cross-validated performance
mmp.plot_cumulative_returns()
print(mmp.summary())
```

### Synthetic Data and Stress Testing

```python
from skfolio.distribution import VineCopula
from skfolio.prior import SyntheticData

# Create distribution estimator
vine = VineCopula(log_transform=True, n_jobs=-1)

# Use for synthetic data generation
prior = SyntheticData(distribution_estimator=vine, n_samples=2000)

# Create model using synthetic data
model = MeanRisk(risk_measure=RiskMeasure.CVAR, prior_estimator=prior)
model.fit(X)

# Perform stress test for specific asset
vine = VineCopula(log_transform=True, central_assets=["BAC"], n_jobs=-1)
vine.fit(X)
X_stressed = vine.sample(n_samples=10_000, conditioning={"BAC": -0.2})
ptf_stressed = model.predict(X_stressed)
```

## Hyperparameter Tuning

```python
from sklearn.model_selection import GridSearchCV, RandomizedSearchCV
from scipy.stats import loguniform
from skfolio.model_selection import WalkForward

# Grid search for optimal parameters
grid_search = GridSearchCV(
    estimator=MeanRisk(),
    cv=KFold(n_splits=5, shuffle=False),
    param_grid={
        "risk_measure": [
            RiskMeasure.VARIANCE,
            RiskMeasure.CVAR,
            RiskMeasure.CDAR,
        ],
        "l2_coef": [0.01, 0.05, 0.1],
    },
)
grid_search.fit(X_train)
best_model = grid_search.best_estimator_

# Random search with time series validation
randomized_search = RandomizedSearchCV(
    estimator=MeanRisk(),
    cv=WalkForward(train_size=252, test_size=60),
    param_distributions={
        "l2_coef": loguniform(1e-3, 1e-1),
    },
)
randomized_search.fit(X_train)
```

## Pipeline Integration

```python
from sklearn import set_config
from sklearn.pipeline import Pipeline
from skfolio.pre_selection import SelectKExtremes

# Configure pandas output
set_config(transform_output="pandas")

# Create pipeline with pre-selection and optimization
model = Pipeline(
    [
        ("pre_selection", SelectKExtremes(k=10, highest=True)),
        ("optimization", MeanRisk()),
    ]
)

# Fit pipeline
model.fit(X_train)

# Predict
portfolio = model.predict(X_test)
```

## Key Classes and Methods

### Portfolio Class

The `Portfolio` class is an array-container that holds portfolio returns and provides various analysis methods:

```python
# Create and analyze portfolio
portfolio = model.predict(X_test)

# Plot portfolio properties
portfolio.plot_cumulative_returns()
portfolio.plot_composition()
portfolio.plot_contribution(measure=RiskMeasure.VARIANCE)

# Get portfolio statistics
print(portfolio.annualized_sharpe_ratio)
print(portfolio.annualized_mean)
print(portfolio.annualized_standard_deviation)
print(portfolio.max_drawdown)

# Full summary
print(portfolio.summary())
```

### Population Class

The `Population` class manages multiple portfolios for comparative analysis:

```python
from skfolio import Population

# Create population from multiple portfolios
population = Population([portfolio1, portfolio2, portfolio3])

# Comparative analysis
population.plot_cumulative_returns()
population.plot_composition()

# Summary statistics
print(population.summary())
```

## Best Practices

1. **Data Preparation**:
   - Use `prices_to_returns()` to convert price data to returns
   - Use `train_test_split()` without shuffling to avoid data leakage

2. **Model Selection**:
   - Start with simple models (Equal-Weighted, Inverse-Volatility) as benchmarks
   - Progress to more sophisticated models as needed
   - Use cross-validation to evaluate out-of-sample performance

3. **Hyperparameter Tuning**:
   - Use appropriate CV strategies for time series data
   - Consider WalkForward or CombinatorialPurgedCV to prevent data leakage

4. **Risk Management**:
   - Compare different risk measures (Variance, CVaR, CDaR)
   - Evaluate tail risk especially during market stress periods
   - Use synthetic data for stress testing

5. **Constraints**:
   - Implement realistic constraints (min/max weights, transaction costs)
   - Consider sector/region diversification constraints
   - Use regularization to control turnover

## Conclusion

skfolio provides a comprehensive framework for portfolio optimization that integrates seamlessly with scikit-learn's machine learning tools. By offering numerous optimization approaches, risk measures, and validation techniques, it enables sophisticated portfolio construction and testing with a focus on out-of-sample performance.

The library's sklearn-compatible API allows users to leverage the entire sklearn ecosystem for model selection, hyperparameter tuning, and pipeline creation, making it a powerful tool for quantitative finance practitioners and researchers.