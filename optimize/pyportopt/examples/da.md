
# Discrete Allocation
```python
from pypfopt.discrete_allocation import DiscreteAllocation, get_latest_prices
```

```python
def dollar_allocation(prices_df: pd.DataFrame, weights: Dict[str, float], total_portfolio_value: float) -> Tuple[Dict[str, float], float]:
    """
    Get the latest allocation from the prices_df and weights.

    Args:
        prices_df (pd.DataFrame): DataFrame containing prices of assets.
        weights (Dict[str, float]): Dictionary of asset weights.
        total_portfolio_value (float): Total value of the portfolio.

    Returns:
        allocation (Dict[str, float]): Dictionary of asset allocations.
        leftover (float): The leftover value in the portfolio.
    """
    latest_prices = get_latest_prices(prices_df)
    da = DiscreteAllocation(
        weights, latest_prices, total_portfolio_value=total_portfolio_value
    )
    allocation, leftover = da.greedy_portfolio()
    return allocation, leftover
```
