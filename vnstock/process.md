```python
from vnstock import Vnstock
from vnstock.core.utils.transform import flatten_hierarchical_index

stock = Vnstock().stock(symbol="ACB", source="VCI")
ratios = stock.finance.ratio(period="year", lang="vi", dropna=True)
```

# Apply to MultiIndex DataFrame

```python
from vnstock.core.utils.transform import flatten_hierarchical_index
flattened_df = flatten_hierarchical_index(
    ratios,  # multi-index df
    separator="_",  # separator for flattened columns
    handle_duplicates=True,  # handle duplicate column names
    drop_levels=0,  # or specify levels to drop
)
```