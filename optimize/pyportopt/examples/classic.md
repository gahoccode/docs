# Classic Portfolio Optimization

```python
from pypfopt import EfficientFrontier, risk_models, expected_returns, DiscreteAllocation
from pypfopt.exceptions import OptimizationError
from pypfopt.expected_returns import mean_historical_return
from pypfopt.risk_models import (
    sample_cov,
)  # for covariance matrix, get more methods from risk_models
```

```python
def calculate_portfolio(prices_df, risk_free_rate=0.02, risk_aversion=1.0):
    log_returns = False
    returns = returns_from_prices(prices_df, log_returns=log_returns)

    mu = mean_historical_return(
        prices_df, log_returns=log_returns
    )  # Optional: add log_returns=True

    S = sample_cov(prices_df)
    ef_plot = EfficientFrontier(mu, S)

    ef_max_sharpe = EfficientFrontier(mu, S)
    ef_max_sharpe.max_sharpe(risk_free_rate=risk_free_rate)
    weights_max_sharpe = ef_max_sharpe.clean_weights()
    ret_tangent, std_tangent, sharpe = ef_max_sharpe.portfolio_performance(
        risk_free_rate=risk_free_rate
    )

    ef_min_vol = EfficientFrontier(mu, S)
    ef_min_vol.min_volatility()
    weights_min_vol = ef_min_vol.clean_weights()
    ret_min_vol, std_min_vol, sharpe_min_vol = ef_min_vol.portfolio_performance(
        risk_free_rate=risk_free_rate
    )

    ef_max_utility = EfficientFrontier(mu, S)
    ef_max_utility.max_quadratic_utility(risk_aversion=risk_aversion, market_neutral=False)
    weights_max_utility = ef_max_utility.clean_weights()
    ret_utility, std_utility, sharpe_utility = ef_max_utility.portfolio_performance(
        risk_free_rate=risk_free_rate
    )

    return (
        ret_tangent,
        std_tangent,
        sharpe,
        ret_min_vol,
        std_min_vol,
        sharpe_min_vol,
        ret_utility,
        std_utility,
        sharpe_utility,
        risk_aversion,
    )
```