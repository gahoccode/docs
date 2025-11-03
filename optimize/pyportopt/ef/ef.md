Certainly! Here is the extracted information about the "General Efficient Frontier" including methods, parameters, returns, return types, and any relevant mathematical formulas.

# General Efficient Frontier

The method of mean-variance optimization can be applied whenever you have expected returns and a covariance matrix. However, you may opt for different risk models not dependent on covariance matrices or objectives unrelated to portfolio return. PyPortfolioOpt offers several alternatives and supports custom optimization problems.

## Efficient Semivariance

### Method
- **Functionality**: Optimizes portfolios along the mean-semivariance frontier, penalizing only downside volatility.
- **Formulation**: 
   - Maximize portfolio return for a target semivariance \(s^*\).
   
   \[
   \begin{aligned}
   & \underset{w}{\text{maximize}} & & w^T \mu \\
   & \text{subject to} \\
   &&& n^T n \leq s^* \\
   &&& B w - p + n = 0 \\
   &&& w^T \mathbf{1} = 1 \\
   &&& n \geq 0 \\
   &&& p \geq 0.
   \end{aligned}
   \]

### Class
- **`pypfopt.efficient_frontier.EfficientSemivariance`**

**Parameters:**
- `expected_returns` : np.ndarray
- `returns` : pd.DataFrame
- `frequency` : Default is 252
- `benchmark` : Default is 0
- `weight_bounds` : Default is (0, 1)
- `solver`, `verbose`, `solver_options`: Optional

**Public Methods**:
- `min_semivariance()`
- `max_quadratic_utility(risk_aversion=1, market_neutral=False)`
- `efficient_risk(target_semideviation, market_neutral=False)`
- `efficient_return(target_return, market_neutral=False)`

### Parameters:
- **`efficient_return(target_return, market_neutral=False)`**
  - **target_return** : float - Required.
  - **market_neutral** : bool - Optional.
  
  **Returns**: 
  - Asset weights (OrderedDict)

- **`efficient_risk(target_semideviation, market_neutral=False)`**
  - **target_semideviation** : float - Required.
  - **market_neutral** : bool - Optional.
  
  **Returns**: 
  - Asset weights (OrderedDict)

## Efficient CVaR

### Method
- **Functionality**: Optimizes portfolios along the mean-CVaR frontier.
- **Formulation**:
  - Minimize the CVaR for a given target return.
  - \[
    F_\beta (w, \alpha) = \alpha + \frac{1}{1-\beta} \frac 1 T \sum [-w^T r - \alpha]^+
    \]
  
### Class
- **`pypfopt.efficient_frontier.EfficientCVaR`**

**Parameters:**
- `expected_returns`, `returns`
- `beta`: Default is 0.95
- `weight_bounds`, `solver`, `verbose`, `solver_options`: Optional

**Public Methods**:
- `min_cvar()`
- `efficient_risk(target_cvar, market_neutral=False)`
- `efficient_return(target_return, market_neutral=False)`

### Parameters:
- **`efficient_return(target_return, market_neutral=False)`**
  - **target_return** : float - Required.
  - **market_neutral** : bool - Optional.
  
  **Returns**: 
  - Asset weights (OrderedDict)

- **`efficient_risk(target_cvar, market_neutral=False)`**
  - **target_cvar** : float - Required.
  - **market_neutral** : bool - Optional.
  
  **Returns**: 
  - Asset weights (OrderedDict)

## EfficientCDaR

### Method
- **Functionality**: Optimizes portfolios along the mean-CDaR frontier, using CDaR measure.
- **Formulation**:
  - It uses a linear problem similar to CVaR formulation.

### Class
- **`pypfopt.efficient_frontier.EfficientCDaR`**

**Parameters:**
- `expected_returns`, `returns`
- `beta`: Default is 0.95
- `weight_bounds`, `solver`, `verbose`, `solver_options`: Optional

**Public Methods**:
- `min_cdar()`
- `efficient_risk(target_cdar, market_neutral=False)`
- `efficient_return(target_return, market_neutral=False)`

### Parameters:
- **`efficient_return(target_return, market_neutral=False)`**
  - **target_return** : float - Required.
  - **market_neutral** : bool - Optional.
  
  **Returns**: 
  - Asset weights (OrderedDict)

- **`efficient_risk(target_cdar, market_neutral=False)`**
  - **target_cdar** : float - Required.
  - **market_neutral** : bool - Optional.
  
  **Returns**: 
  - Asset weights (OrderedDict)

## Custom Optimization Problems

### Method
- **Functionality**: Allows custom optimization problems, such as minimizing tracking error.

### Class
- **`pypfopt.base_optimizer.BaseConvexOptimizer`**

**Public Methods**:
- `convex_objective(custom_objective, weights_sum_to_one=True, **kwargs)`
- `nonconvex_objective(custom_objective, objective_args=None, weights_sum_to_one=True, constraints=None, solver='SLSQP', initial_guess=None)`

**Parameters:**
- `custom_objective`
- `weights_sum_to_one` : Default is True
- `objective_args`, `constraints`, `solver`, `initial_guess`: Optional

**Returns**: 
- Asset weights (OrderedDict)

These methods and classes provide extensive options for custom financial optimizations in various risk-adjusted frameworks.
