### Method `historical()`

The `historical()` function is used to retrieve historical market prices, specifically for stock price data in this context. It is located under a specific class for each asset type within the VietFin library.

#### Supported Intervals
- **`1m`**: one minute
- **`1h`**: one hour
- **`1d`**: one day
- **`1w`**: one week
- **`1mo`**: one month

(Note: Not all data sources support all intervals.)

#### Data Types
Historical market prices are usually provided in the form of OHLCV:
- **O**: Open
- **H**: High
- **L**: Low
- **C**: Close
- **V**: Volume

#### Required Parameters
- **`symbol`**: The stock ticker symbol for which historical data is requested.
- **`start_date`**: The beginning of the period for which data is retrieved.
- **`end_date`**: The end of the period for which data is retrieved.
- **`interval`**: The frequency of the data points (e.g., daily, weekly, etc.).

#### Default Values
- **`end_date`**: Defaults to the current date if not provided.
- **`start_date`**: Defaults to 60 days before the `end_date` if not provided.
- **`interval`**: Defaults to `1d` (one day) if not specified.

#### Sample Usage and Output
To retrieve historical prices of a stock ticker (e.g., "VNM"), you can follow this sample code:

```python
from vietfin import vf
import pandas as pd
vf.equity.price.historical(symbol="vnm")
```

**Expected output**:
- The function retrieves OHLCV data points for the specified ticker.
- If `end_date` and `start_date` are not provided, the function defaults to retrieving data from 60 days before the current date up to the current date.
- The output includes detailed information such as dates, open, high, low, close prices, and volume for each data point.

```plaintext
end_date not provided, set to 2024-02-27
start_date not provided, set to 2023-12-29
Retrieved 36 historical price data points for symbol VNM.
```

```plaintext
VfObject

results: [{'date': datetime.date(2023, 12, 29), 'open': 68700.0, 'high': 68700.0, ...
provider: tcbs
extra: {'command_run_at': '2024-02-27T01:10:17.464843+00:00', 'symbol': 'VNM', ...
raw_data: [{'ticker': 'VNM', 'data': [{'open': 67795.0, 'high': 67894.0, 'low': ...
```
**Display result in dataframe**
```python

vf.equity.price.historical(symbol="vnm").to_df().tail(5)
```
