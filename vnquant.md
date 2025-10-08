Based on the README.md, I'll extract all the Python functions and their example use cases from the vnquant package, which is a tool for financial data analysis of the Vietnam stock market.

## 1. Data Loading Functions

### DataLoader

This is the main class for loading stock price data:

```python
# Import the DataLoader class
import vnquant.data as dt

# Initialize a DataLoader with basic parameters
loader = dt.DataLoader(
    symbols="VND",  # Single stock symbol as string
    start="2018-01-10",  # Start date in YYYY-MM-DD format
    end="2018-02-15",    # End date in YYYY-MM-DD format
    data_source="CAFE",  # Data source: 'CAFE' or 'VND'
    minimal=True,        # If True, returns minimal set of columns
    table_style="levels" # Table style: 'levels', 'prefix', or 'stack'
)


# Download the data
data = loader.download()
```

The `vnquant` package provides several table style parameters for fetching and formatting stock data. Here are the table style parameters and their respective methods for fetching:

### Table Style Parameters

1. **Levels**
   - **Description**: Returns a DataFrame with multi-level columns consisting of the stock symbols and basic stock indices such as `['high', 'low', 'open', 'close', 'adjust', 'volume', 'value']`.
   - **Method for Fetching**:
     ```python
     import vnquant.data as dt
     loader = dt.DataLoader('VND', '2018-02-02', '2018-04-02')
     data = loader.download()
     ```

2. **Prefix**
   - **Description**: Adds the stock symbol as a prefix to each column name.
   - **Method for Fetching**:
     ```python
     import vnquant.data as dt
     loader = dt.DataLoader(['VND', 'FPT'], '2018-02-02', '2018-04-02', table_style='prefix')
     data = loader.download()
     ```

3. **Stack**
   - **Description**: Returns the DataFrame with an additional column named `code` to indicate the stock symbol each record belongs to.
   - **Method for Fetching**:
    
     ```python
     import vnquant.data as dt
     loader = dt.DataLoader(['VND', 'FPT'], '2018-02-02', '2018-04-02', table_style='stack')
     data = loader.download()
     ```

The `vnquant` package provides different formats for output when using the `DataLoader` class to clone stock prices. Below are the sample outputs for each `table_style` parameter:

### 1. Multiple-level (`table_style='levels'`):
Attributes (Columns include multiple levels for arguments and symbols):

| Attributes | high | low | open | close | avg | volume |  
|---|---|---|---|---|---|---|  
| **Symbols** | VND | VND | VND | VND | VND | VND |  
| **Date** |   |   |   |   |   |   |  
| 2018-02-02 | 28.95 | 27.60 | 28.5 | 28.95 | 28.28 | 1700670.0 |  
| 2018-02-05 | 28.45 | 26.95 | 28.1 | 26.95 | 27.68 | 2150120.0 |  

### 2. Prefix (`table_style='prefix'`):
Each stock code is prefixed to each index to become a column name:

| VND_code | FPT_code | VND_high | FPT_high | VND_low | FPT_low | VND_open | FPT_open | VND_close | FPT_close | VND_adjust | FPT_adjust | VND_volume_match | FPT_volume_match | VND_value_match | FPT_value_match |  
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|  
| **Date** |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |  
| 2018-04-02 | VND | FPT | 29.80 | 61.7 | 29.10 | 61.0 | 29.10 | 61.5 | 29.55 | 61.5 | 6.52 | 21.98 | 2141980.0 | 2194820.0 | 6.320100e+10 | 1.347410e+11 |  

### 3. Stack (`table_style='stack'`):
A new column named `code` is added to demonstrate the stock symbols:

| code | high | low | open | close | adjust | volume_match | value_match |  
|---|---|---|---|---|---|---|---|  
| **Date** |   |   |   |   |   |   |   |  
| 2018-04-02 | FPT | 61.7 | 61.00 | 61.5 | 61.50 | 21.98 | 2194820.0 | 1.347410e+11 |  
| 2018-04-02 | VND | 29.8 | 29.10 | 29.1 | 29.55 | 6.52 | 2141980.0 | 6.320100e+10 |  
| 2018-03-30 | FPT | 61.3 | 59.40 | 59.6 | 60.70 | 21.69 | 2434830.0 | 1.474940e+11 |  

These examples illustrate the different ways you can structure and access stock data using the `vnquant` package depending on your analysis needs.


Example for loading multiple stocks:

```python
# Load multiple stocks at once
loader = dt.DataLoader(
    symbols=["VND", "VCB"], 
    start="2018-01-10", 
    end="2018-02-15", 
    minimal=True, 
    data_source="cafe"
)
data = loader.download()
```

Example for loading with full information:

```python
# Load with full information 
loader = dt.DataLoader(
    symbols=["VND"], 
    start="2018-01-10", 
    end="2018-02-15", 
    minimal=False  # Set to False to get all available columns
)
data = loader.download()
```

### FinanceLoader

This class is for loading financial reports (finance, business, cashflow, and basic index reports):

```python
# Import the FinanceLoader class
import vnquant.data as dt

# Initialize a FinanceLoader
loader = dt.FinanceLoader(
    symbol="VND",           # Only supports one symbol at a time
    start="2019-06-02",     # Start date
    end="2021-12-31"        # End date
)
```

Methods for retrieving different financial reports:

```python
# Get financial report
data_finan = loader.get_finan_report()

# Get business report
data_bus = loader.get_business_report()

# Get cashflow report
data_cash = loader.get_cashflow_report()

# Get basic index report (ROA, ROE, etc.)
data_basic = loader.get_basic_index()
```

## 2. Visualization Functions

### vnquant_candle_stick

This function visualizes stock price data with various technical indicators:

```python
# Import the plotting module
import vnquant.plot as pl

# Visualize a stock from a data source
pl.vnquant_candle_stick(
    data="VND",                # Symbol or DataFrame
    title="VND symbol from 2019-09-01 to 2019-11-01",
    xlab="Date", 
    ylab="Price",
    start_date="2019-09-01",   # Start date (required for symbol)
    end_date="2019-11-01",     # End date (required for symbol)
    data_source="CAFE",        # Data source when using symbol
    show_advanced=["volume", "macd", "rsi"],  # Technical indicators to show
    width=1600,                # Width of the chart
    height=800                 # Height of the chart
)
```

Example for visualizing from DataFrame:

```python
# Visualize from a DataFrame
import vnquant.plot as plt

plt.vnquant_candle_stick(
    data=data,               # DataFrame with OHLC or OHLCV structure
    title="Your data",
    ylab="Date", 
    xlab="Price",
    show_advanced=["volume", "macd", "rsi"]
)
```

## 3. Utility Functions

```python
# Check if a DataFrame is OHLC or OHLCV type
from vnquant import utils

# Check if DataFrame is OHLC type (has open, high, low, close columns)
is_ohlc = utils._isOHLC(data_vnd)

# Check if DataFrame is OHLCV type (has open, high, low, close, volume columns)
is_ohlcv = utils._isOHLCV(data_vnd)
```

## Complete Example Workflows

### Example 1: Loading and Visualizing a Single Stock

```python
import vnquant.data as dt
import vnquant.plot as pl

# Load stock data
loader = dt.DataLoader(
    symbols="VND", 
    start="2019-09-01", 
    end="2019-11-01", 
    data_source="CAFE"
)
data = loader.download()

# Visualize with candlestick chart
pl.vnquant_candle_stick(
    data=data,
    title="VND Stock Price Analysis",
    xlab="Date", 
    ylab="Price",
    show_advanced=["volume", "macd", "rsi"]
)
```

### Example 2: Comparing Multiple Stocks

```python
import vnquant.data as dt
import pandas as pd
import matplotlib.pyplot as plt

# Load multiple stocks
loader = dt.DataLoader(
    symbols=["VND", "VCB", "FPT"], 
    start="2020-01-01", 
    end="2021-01-01", 
    data_source="CAFE"
)
data = loader.download()

# Plotting the closing prices for comparison
plt.figure(figsize=(12, 6))
plt.plot(data['close']['VND'], label='VND')
plt.plot(data['close']['VCB'], label='VCB')
plt.plot(data['close']['FPT'], label='FPT')
plt.title('Comparison of Stock Prices')
plt.xlabel('Date')
plt.ylabel('Closing Price')
plt.legend()
plt.grid(True)
plt.show()
```

### Example 3: Financial Analysis

```python
import vnquant.data as dt

# Get financial data
finance_loader = dt.FinanceLoader(
    symbol="VND", 
    start="2019-01-01", 
    end="2021-12-31"
)

# Get different reports
financial_report = finance_loader.get_finan_report()
business_report = finance_loader.get_business_report()
cashflow_report = finance_loader.get_cashflow_report()
basic_indices = finance_loader.get_basic_index()

# Print basic financial ratios
print("ROE:", basic_indices.loc['ROE last 4 quarters'])
print("ROA:", basic_indices.loc['ROA last 4 quarters'])
print("Profit Growth:", basic_indices.loc['Profit After Tax Growth (YoY)'])
```


## Requirements
pandas>=0.19.2 
numpy>=1.20.2 
requests>=2.3.0 
wrapt>=1.10.0 
lxml>=4.3.0 
pypandoc>=1.4 
plotly>=4.2.1 
bs4>=0.0.1