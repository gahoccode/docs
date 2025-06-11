# Vnstock Library Methods for Financial Analysis

The vnstock library provides comprehensive access to financial data for Vietnamese companies. This document details the methods available for retrieving and analyzing company information, financial statements, and screening stocks.

## Setup and Initialization

There are two main approaches to initializing the classes and accessing their methods:

### Method 1: Using the Vnstock class (Recommended)



### Method 2: Direct import of specific classes

```python
from vnstock import Finance, Company, Screener

# Initialize the classes with a symbol
finance = Finance(symbol='VCI')
company = Company(symbol='VCI')
screener = Screener()

# Call methods directly
```

## Finance Class Methods

The Finance class provides several key methods to access different types of financial statements. Each method supports various parameters to customize the data retrieval.

### 1. `balance_sheet()` - Balance Sheet Statements

Retrieves a company's balance sheet, showing assets, liabilities, and shareholders' equity.

#### Parameters:

- `period` (str): Time period of data, options:
  - `'year'`: Annual data (default)
  - `'quarter'`: Quarterly data
  
- `lang` (str): Language for column names and labels, options:
  - `'vi'`: Vietnamese (default)
  - `'en'`: English
  
- `dropna` (bool): Whether to remove rows with NA values
  - `True`: Remove rows with NA values (default)
  - `False`: Keep all rows

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize with stock symbol and source
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get annual balance sheet in Vietnamese
annual_balance_sheet = stock.finance.balance_sheet(period='year', lang='vi', dropna=True)
print(annual_balance_sheet)

# Get quarterly balance sheet in English
quarterly_balance_sheet = stock.finance.balance_sheet(period='quarter', lang='en', dropna=True)
print(quarterly_balance_sheet)
```

**Method 2: Direct import of Finance class**
```python
from vnstock import Finance

# Initialize Finance class directly
finance = Finance(symbol='VCI')

# Get annual balance sheet in Vietnamese
annual_balance_sheet = finance.balance_sheet(period='year', lang='vi', dropna=True)
print(annual_balance_sheet)

# Get quarterly balance sheet in English
quarterly_balance_sheet = finance.balance_sheet(period='quarter', lang='en', dropna=True)
print(quarterly_balance_sheet)
```

### 2. `income_statement()` - Income Statements

Retrieves a company's income statement (profit and loss statement), showing revenues, costs, and expenses during a specific period.

#### Parameters:

- `period` (str): Time period of data, options:
  - `'year'`: Annual data (default)
  - `'quarter'`: Quarterly data
  
- `lang` (str): Language for column names and labels, options:
  - `'vi'`: Vietnamese (default)
  - `'en'`: English
  
- `dropna` (bool): Whether to remove rows with NA values
  - `True`: Remove rows with NA values (default)
  - `False`: Keep all rows

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize with stock symbol and source
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get annual income statement in Vietnamese
annual_income = stock.finance.income_statement(period='year', lang='vi', dropna=True)
print(annual_income)

# Get quarterly income statement in English
quarterly_income = stock.finance.income_statement(period='quarter', lang='en', dropna=True)
print(quarterly_income)
```

**Method 2: Direct import of Finance class**
```python
from vnstock import Finance

# Initialize Finance class directly
finance = Finance(symbol='VCI')

# Get annual income statement in Vietnamese
annual_income = finance.income_statement(period='year', lang='vi', dropna=True)
print(annual_income)

# Get quarterly income statement in English
quarterly_income = finance.income_statement(period='quarter', lang='en', dropna=True)
print(quarterly_income)
```

### 3. `cash_flow()` - Cash Flow Statements

Retrieves a company's cash flow statement, showing how changes in balance sheet accounts and income affect cash and cash equivalents.

#### Parameters:

- `period` (str): Time period of data, options:
  - `'year'`: Annual data (default)
  - `'quarter'`: Quarterly data
  
- `lang` (str): Language for column names and labels, options:
  - `'vi'`: Vietnamese (default)
  - `'en'`: English
  
- `dropna` (bool): Whether to remove rows with NA values
  - `True`: Remove rows with NA values (default)
  - `False`: Keep all rows

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize with stock symbol and source
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get annual cash flow statement in Vietnamese
annual_cash_flow = stock.finance.cash_flow(period='year', lang='vi', dropna=True)
print(annual_cash_flow)

# Get quarterly cash flow statement in English
quarterly_cash_flow = stock.finance.cash_flow(period='quarter', lang='en', dropna=False)
print(quarterly_cash_flow)
```

**Method 2: Direct import of Finance class**
```python
from vnstock import Finance

# Initialize Finance class directly
finance = Finance(symbol='VCI')

# Get annual cash flow statement in Vietnamese
annual_cash_flow = finance.cash_flow(period='year', lang='vi', dropna=True)
print(annual_cash_flow)

# Get quarterly cash flow statement in English
quarterly_cash_flow = finance.cash_flow(period='quarter', lang='en', dropna=False)
print(quarterly_cash_flow)
```

### 4. `ratio()` - Financial Ratios

Retrieves calculated financial ratios for a company, including profitability, liquidity, and solvency metrics.

#### Parameters:

- `period` (str): Time period of data, options:
  - `'year'`: Annual data (default)
  - `'quarter'`: Quarterly data
  
- `lang` (str): Language for column names and labels, options:
  - `'vi'`: Vietnamese (default)
  - `'en'`: English
  
- `dropna` (bool): Whether to remove rows with NA values
  - `True`: Remove rows with NA values (default)
  - `False`: Keep all rows

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize with stock symbol and source
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get annual financial ratios in Vietnamese
annual_ratios = stock.finance.ratio(period='year', lang='vi', dropna=True)
print(annual_ratios)

# Get quarterly financial ratios in English
quarterly_ratios = stock.finance.ratio(period='quarter', lang='en', dropna=True)
print(quarterly_ratios)
```

**Method 2: Direct import of Finance class**
```python
from vnstock import Finance

# Initialize Finance class directly
finance = Finance(symbol='VCI')

# Get annual financial ratios in Vietnamese
annual_ratios = finance.ratio(period='year', lang='vi', dropna=True)
print(annual_ratios)

# Get quarterly financial ratios in English
quarterly_ratios = finance.ratio(period='quarter', lang='en', dropna=True)
print(quarterly_ratios)
```

## Complete Example

Here's a complete example demonstrating how to use all the Finance class methods to retrieve various financial statements for a company:

```python
from vnstock import Vnstock
import pandas as pd

# Initialize
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get financial statements
balance_sheet = stock.finance.balance_sheet(period='year', lang='en', dropna=True)
income_stmt = stock.finance.income_statement(period='year', lang='en', dropna=True)
cash_flow = stock.finance.cash_flow(period='year', lang='en', dropna=True)
ratios = stock.finance.ratio(period='year', lang='en', dropna=True)

# Display the first few rows of each
print("Balance Sheet:")
print(balance_sheet.head())

print("\nIncome Statement:")
print(income_stmt.head())

print("\nCash Flow Statement:")
print(cash_flow.head())

print("\nFinancial Ratios:")
print(ratios.head())

# Save to CSV files
balance_sheet.to_csv('balance_sheet.csv')
income_stmt.to_csv('income_statement.csv')
cash_flow.to_csv('cash_flow.csv')
ratios.to_csv('financial_ratios.csv')
```

## Practical Analysis Example

Here's an example of how to analyze financial data using the vnstock Finance class methods:

```python
from vnstock import Vnstock
import pandas as pd
import matplotlib.pyplot as plt

# Initialize with two different companies for comparison
company1 = Vnstock().stock(symbol='VCI', source='VCI')
company2 = Vnstock().stock(symbol='SSI', source='VCI')

# Get income statements for both companies
income1 = company1.finance.income_statement(period='year', lang='en', dropna=True)
income2 = company2.finance.income_statement(period='year', lang='en', dropna=True)

# Get relevant rows (may vary based on actual data structure)
revenue1 = income1.loc[income1.index.str.contains('Revenue', case=False)]
revenue2 = income2.loc[income2.index.str.contains('Revenue', case=False)]

# Create a plot
plt.figure(figsize=(12, 6))
plt.plot(revenue1.columns, revenue1.iloc[0], 'o-', label='VCI Revenue')
plt.plot(revenue2.columns, revenue2.iloc[0], 's-', label='SSI Revenue')
plt.title('Revenue Comparison: VCI vs SSI')
plt.xlabel('Year')
plt.ylabel('Revenue (VND)')
plt.legend()
plt.grid(True)
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig('revenue_comparison.png')
plt.show()
```

## Company Class Methods

The `Company` class provides methods to access company profile and information.

### 1. `profile()` - Company Profile Information

Retrieves detailed company profile information including business description, sector, industry, and key details.

#### Parameters:

- `lang` (str): Language for column names and labels, options:
  - `'vi'`: Vietnamese (default)
  - `'en'`: English

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize with stock symbol and source
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get company profile information
company_profile = stock.company.profile(lang='en')
print(company_profile)
```

**Method 2: Direct import of Company class**
```python
from vnstock import Company

# Initialize Company class directly
company = Company(symbol='VCI')

# Get company profile information
company_profile = company.profile(lang='en')
print(company_profile)
```

### 2. `officers()` - Company Officers/Management

Retrieves information about company officers and management team.

#### Parameters:

- `lang` (str): Language for column names and labels, options:
  - `'vi'`: Vietnamese (default)
  - `'en'`: English

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize with stock symbol and source
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get company officers information
management_team = stock.company.officers(lang='en')
print(management_team)
```

**Method 2: Direct import of Company class**
```python
from vnstock import Company

# Initialize Company class directly
company = Company(symbol='VCI')

# Get company officers information
management_team = company.officers(lang='en')
print(management_team)
```

### 3. `major_holders()` - Major Shareholders

Retrieves information about major shareholders of the company.

#### Parameters:

- `lang` (str): Language for column names and labels, options:
  - `'vi'`: Vietnamese (default)
  - `'en'`: English

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize with stock symbol and source
stock = Vnstock().stock(symbol='VCI', source='VCI')

# Get major shareholders information
major_shareholders = stock.company.major_holders(lang='en')
print(major_shareholders)
```

**Method 2: Direct import of Company class**
```python
from vnstock import Company

# Initialize Company class directly
company = Company(symbol='VCI')

# Get major shareholders information
major_shareholders = company.major_holders(lang='en')
print(major_shareholders)
```

## Stock Screener Functionality

The `Screener` class allows you to filter stocks based on various financial, technical, and market criteria.

### Using the Stock Screener

The main method of the Screener class is the `stock()` method, which allows filtering based on custom parameters.

#### Method: `stock(params, limit)`

- `params` (dict): Dictionary containing filtering parameters
- `limit` (int): Maximum number of results to return (default: 1700)

#### Example Usage:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock

# Initialize Vnstock
stock = Vnstock()

# Basic usage with exchange filter
df = stock.screener.stock(params={"exchangeName": "HOSE,HNX,UPCOM"}, limit=1700)
print(df.head())

# Advanced filtering with multiple parameters
params = {
    "exchangeName": "HOSE,HNX", 
    "marketCap": (100, 1000),  # Market cap between 100-1000 billion VND
    "dividendYield": (5, 10),  # Dividend yield between 5-10%
    "roe": (15, 50)            # ROE between 15-50%
}
filtered_stocks = stock.screener.stock(params=params, limit=500)
print(filtered_stocks)
```

**Method 2: Direct import of Screener class**
```python
from vnstock import Screener

# Initialize Screener class directly
screener = Screener()

# Basic usage with exchange filter
df = screener.stock(params={"exchangeName": "HOSE,HNX,UPCOM"}, limit=1700)
print(df.head())

# Advanced filtering with multiple parameters
params = {
    "exchangeName": "HOSE,HNX", 
    "marketCap": (100, 1000),  # Market cap between 100-1000 billion VND
    "dividendYield": (5, 10),  # Dividend yield between 5-10%
    "roe": (15, 50)            # ROE between 15-50%
}
filtered_stocks = screener.stock(params=params, limit=500)
print(filtered_stocks)
```

### Common Screening Parameters

The following parameters can be used in the `params` dictionary to filter stocks:

1. **Market Parameters**:
   - `exchangeName`: Stock exchange(s) - "HOSE", "HNX", "UPCOM" (use commas for multiple)
   - `marketCap`: Market capitalization range in billions VND - tuple (min, max)
   - `industry`: Industry name or code
   - `hasFinancialReport`: 1 for companies with recent financial reports, 0 otherwise

2. **Financial Metrics**:
   - `roe`: Return on Equity range - tuple (min, max)
   - `pe`: Price-to-Earnings ratio range - tuple (min, max)
   - `pb`: Price-to-Book ratio range - tuple (min, max)
   - `dividendYield`: Dividend yield percentage range - tuple (min, max)
   - `epsGrowth1Year`: EPS growth in the last year range - tuple (min, max)
   - `lastQuarterProfitGrowth`: Last quarter profit growth range - tuple (min, max)

3. **Technical Indicators**:
   - `avgTradingValue20Day`: 20-day average trading value range - tuple (min, max)
   - `relativeStrength1Month`: 1-month relative strength range - tuple (min, max)
   - `priceToSma20`: Price to 20-day Simple Moving Average ratio range - tuple (min, max)

4. **Ratings and Analysis**:
   - `stockRating`: Stock rating score (1-5, with 5 being best)
   - `businessModel`: Business model rating (1-5)
   - `businessOperation`: Business operation rating (1-5)
   - `financialHealth`: Financial health rating (1-5)

```python
from vnstock import Vnstock

# Initialize with a stock symbol and data source
stock = Vnstock().stock(symbol='VCI', source='VCI')
Data columns (total 84 columns):
 #   Column                         Non-Null Count  Dtype  
---  ------                         --------------  -----  
 0   ticker                         1613 non-null   object 
 1   exchange                       1613 non-null   object 
 2   industry                       1613 non-null   object 
 4   market_cap                     1268 non-null   float64
 5   roe                            1268 non-null   float64
 6   stock_rating                   855 non-null    float64
 7   business_operation             1553 non-null   float64
 8   business_model                 797 non-null    float64
 9   financial_health               1553 non-null   float64
 10  alpha                          1553 non-null   float64
 11  beta                           1553 non-null   float64
 12  uptrend                        26 non-null     object 
 13  active_buy_pct                 897 non-null    float64
 14  strong_buy_pct                 1132 non-null   float64
 15  high_vol_match                 950 non-null    float64
 16  forecast_vol_ratio             948 non-null    float64
 17  pe                             1235 non-null   float64
 18  pb                             1235 non-null   float64
 19  ev_ebitda                      1192 non-null   float64
 20  dividend_yield                 1268 non-null   float64
 21  price_vs_sma5                  301 non-null    object 
 22  price_vs_sma20                 960 non-null    object 
 23  revenue_growth_1y              1219 non-null   float64
 24  revenue_growth_5y              1171 non-null   float64
 25  eps_growth_1y                  1179 non-null   float64
 26  eps_growth_5y                  1050 non-null   float64
 27  gross_margin                   1118 non-null   float64
 28  net_margin                     986 non-null    float64
 29  doe                            1239 non-null   float64
 30  avg_trading_value_5d           1613 non-null   float64
 31  avg_trading_value_10d          1613 non-null   float64
 32  avg_trading_value_20d          1613 non-null   float64
 33  relative_strength_3d           910 non-null    float64
 34  rel_strength_1m                906 non-null    float64
 35  rel_strength_3m                901 non-null    float64
 36  rel_strength_1y                884 non-null    float64
 37  total_trading_value            963 non-null    float64
 38  foreign_transaction            357 non-null    object 
 39  price_near_realtime            960 non-null    float64
 40  rsi14                          960 non-null    float64
 41  foreign_vol_pct                1566 non-null   float64
 42  tc_rs                          910 non-null    float64
 43  tcbs_recommend                 98 non-null     object 
 44  tcbs_buy_sell_signal           960 non-null    object 
 45  foreign_buysell_20s            1564 non-null   float64
 46  num_increase_continuous_day    1143 non-null   float64
 47  num_decrease_continuous_day    1204 non-null   float64
 48  eps                            1112 non-null   float64
 49  macd_histogram                 960 non-null    object 
 50  vol_vs_sma5                    947 non-null    float64
 51  vol_vs_sma10                   956 non-null    float64
 52  vol_vs_sma20                   960 non-null    float64
 53  vol_vs_sma50                   960 non-null    float64
 54  price_vs_sma10                 215 non-null    object 
 55  price_vs_sma50                 960 non-null    object 
 56  price_break_out52_week         12 non-null     object 
 57  price_wash_out52_week          4 non-null      object 
 58  sar_vs_macd_hist               46 non-null     object 
 59  bolling_band_signal            143 non-null    object 
 60  dmi_signal                     17 non-null     object 
 61  rsi14_status                   960 non-null    object 
 62  price_growth_1w                959 non-null    float64
 63  price_growth_1m                960 non-null    float64
 64  breakout                       17 non-null     object 
 65  prev_1d_growth_pct             960 non-null    float64
 66  prev_1m_growth_pct             960 non-null    float64
 67  prev_1y_growth_pct             960 non-null    float64
 68  prev_5y_growth_pct             881 non-null    float64
 69  has_financial_report           1613 non-null   object 
 70  free_transfer_rate             1612 non-null   float64
 71  net_cash_per_market_cap        1117 non-null   float64
 72  net_cash_per_total_assets      1131 non-null   float64
 73  profit_last_4q                 1160 non-null   float64
 74  last_quarter_revenue_growth    1075 non-null   float64
 75  second_quarter_revenue_growth  1079 non-null   float64
 76  last_quarter_profit_growth     853 non-null    float64
 77  second_quarter_profit_growth   877 non-null    float64
 78  pct_1y_from_peak               960 non-null    float64
 79  pct_away_from_hist_peak        960 non-null    float64
 80  pct_1y_from_bottom             960 non-null    float64
 81  pct_off_hist_bottom            953 non-null    float64
 82  price_vs_sma100                960 non-null    object 
 83  heating_up                     10 non-null     object 
# Now access various components through stock objects
# For example: stock.finance, stock.company, stock.quote, etc.
```

### Example Use Case: CANSLIM Stock Screening

The CANSLIM investment strategy focuses on growth stocks. Here's how to implement it with vnstock:

**Method 1: Using the Vnstock class (Recommended)**
```python
from vnstock import Vnstock
import pandas as pd

# Initialize
stock = Vnstock()

# CANSLIM parameters
params = {
    "exchangeName": "HOSE,HNX,UPCOM",
    "epsGrowth1Year": (25, 999),            # Strong earnings growth
    "lastQuarterProfitGrowth": (20, 999),   # Recent quarterly growth
    "roe": (15, 999),                       # High return on equity
    "avgTradingValue20Day": (5000000, 999999999999),  # High trading volume
    "relativeStrength1Month": (10, 999)     # Strong relative strength
}

# Get CANSLIM stocks
canslim_stocks = stock.screener.stock(params=params, limit=100)

# Sort by EPS growth for best candidates
canslim_stocks = canslim_stocks.sort_values(by='epsGrowth1Year', ascending=False)

print("Top 10 CANSLIM Stock Candidates:")
print(canslim_stocks.head(10))

# Export to CSV
canslim_stocks.to_csv('canslim_stocks.csv')
```

**Method 2: Direct import of Screener class**
```python
from vnstock import Screener
import pandas as pd

# Initialize
screener = Screener()

# CANSLIM parameters
params = {
    "exchangeName": "HOSE,HNX,UPCOM",
    "epsGrowth1Year": (25, 999),            # Strong earnings growth
    "lastQuarterProfitGrowth": (20, 999),   # Recent quarterly growth
    "roe": (15, 999),                       # High return on equity
    "avgTradingValue20Day": (5000000, 999999999999),  # High trading volume
    "relativeStrength1Month": (10, 999)     # Strong relative strength
}

# Get CANSLIM stocks
canslim_stocks = screener.stock(params=params, limit=100)

# Sort by EPS growth for best candidates
canslim_stocks = canslim_stocks.sort_values(by='epsGrowth1Year', ascending=False)

print("Top 10 CANSLIM Stock Candidates:")
print(canslim_stocks.head(10))

# Export to CSV
canslim_stocks.to_csv('canslim_stocks.csv')
```

## Complete Example: Multi-Class Analysis

Here's a complete example demonstrating how to use all the classes together to perform a comprehensive analysis:

```python
from vnstock import Vnstock
import pandas as pd
import matplotlib.pyplot as plt

# Initialize with two different companies for comparison
stock1 = Vnstock().stock(symbol='VCB', source='VCI')
stock2 = Vnstock().stock(symbol='TCB', source='VCI')

# 1. Get company profile information
profile1 = stock1.company.profile(lang='en')
profile2 = stock2.company.profile(lang='en')
print("Company Profiles:")
print(f"VCB: {profile1['organShortName'].values[0]}")
print(f"TCB: {profile2['organShortName'].values[0]}")

# 2. Get financial data
income1 = stock1.finance.income_statement(period='year', lang='en', dropna=True)
income2 = stock2.finance.income_statement(period='year', lang='en', dropna=True)

ratios1 = stock1.finance.ratio(period='year', lang='en', dropna=True)
ratios2 = stock2.finance.ratio(period='year', lang='en', dropna=True)

# 3. Perform screening for similar companies in the banking sector
screener = Vnstock().screener
bank_params = {
    "exchangeName": "HOSE,HNX,UPCOM",
    "industryName": "Banking",
    "marketCap": (50000, 999999999),  # Large banks only
    "roe": (10, 999)                  # Good profitability
}
banks = screener.stock(params=bank_params, limit=10)

# 4. Compare ROE of the banks
plt.figure(figsize=(12, 6))
plt.bar(banks['ticker'], banks['roe'])
plt.title('ROE Comparison of Vietnamese Banks')
plt.xlabel('Bank Ticker')
plt.ylabel('Return on Equity (%)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig('bank_roe_comparison.png')

# 5. Create final analysis report
print("\nBank Analysis Results:")
print(f"Total banks analyzed: {len(banks)}")
print(f"Highest ROE Bank: {banks.loc[banks['roe'].idxmax(), 'ticker']} with ROE of {banks['roe'].max():.2f}%")
print(f"Average Banking Sector ROE: {banks['roe'].mean():.2f}%")
print(f"VCB ROE: {banks.loc[banks['ticker'] == 'VCB', 'roe'].values[0]:.2f}%")
print(f"TCB ROE: {banks.loc[banks['ticker'] == 'TCB', 'roe'].values[0]:.2f}%")

# Export results
banks.to_csv('vietnamese_banks_analysis.csv')
```
# Example Use Cases for vnstock Library

Here are practical example use cases demonstrating how to use the vnstock library for Vietnamese stock market analysis:

## 1. Setting Up and Basic Usage

```python
from vnstock import Vnstock
# Initialize with a default stock symbol and data source
stock = Vnstock().stock(symbol='ACB', source='VCI')
```

## 2. Market Overview Analysis

**Get list of all VN30 stocks for market analysis:**
```python
vn30_stocks = stock.listing.symbols_by_group('VN30')
print(f"There are {len(vn30_stocks)} stocks in the VN30 index")
```

**Create a market dashboard for top banking stocks:**
```python
banking_board = stock.trading.price_board(['VCB','ACB','TCB','BID','MBB'])
# Format as a dashboard with key metrics
banking_board_display = banking_board[['listing.symbol', 'match.match_price', 
                                       'match.price_change_ratio', 'match.total_volume']]
```

## 3. Technical Analysis

**Get historical data for moving average analysis:**
```python
import pandas as pd
import matplotlib.pyplot as plt

# Get 1-year historical data for VNIndex
vnindex_hist = stock.quote.history(symbol='VNINDEX', start='2024-01-01', end='2025-03-19', interval='1D')

# Calculate moving averages
vnindex_hist['MA20'] = vnindex_hist['close'].rolling(window=20).mean()
vnindex_hist['MA50'] = vnindex_hist['close'].rolling(window=50).mean()
vnindex_hist['MA200'] = vnindex_hist['close'].rolling(window=200).mean()

# Plot the chart
plt.figure(figsize=(12, 6))
plt.plot(vnindex_hist['time'], vnindex_hist['close'], label='VNINDEX')
plt.plot(vnindex_hist['time'], vnindex_hist['MA20'], label='MA20')
plt.plot(vnindex_hist['time'], vnindex_hist['MA50'], label='MA50')
plt.plot(vnindex_hist['time'], vnindex_hist['MA200'], label='MA200')
plt.title('VNINDEX with Moving Averages')
plt.legend()
plt.grid(True)
```

**Analyze intraday trading pattern:**
```python
# Get intraday data to analyze trading volume by time of day
intraday = stock.quote.intraday(symbol='ACB', page_size=10000)

# Group data by hour to see time-based trading patterns
intraday['hour'] = pd.to_datetime(intraday['time']).dt.hour
hourly_volume = intraday.groupby('hour')['volume'].sum()
```

## 4. Fundamental Analysis

**Evaluate company financial health:**
```python
# Get balance sheet and income statement data
balance_sheet = stock.finance.balance_sheet(period='year', lang='en')
income_stmt = stock.finance.income_statement(period='year', lang='en')

# Calculate basic financial metrics year-over-year
recent_years = balance_sheet['yearReport'].unique()[-5:]  # Last 5 years
filtered_bs = balance_sheet[balance_sheet['yearReport'].isin(recent_years)]
filtered_is = income_stmt[income_stmt['yearReport'].isin(recent_years)]

# Calculate debt-to-equity trend
filtered_bs['debt_to_equity'] = (filtered_bs['TOTAL ASSETS (Bn. VND)'] - filtered_bs['OWNER\'S EQUITY(Bn.VND)']) / filtered_bs['OWNER\'S EQUITY(Bn.VND)']

# Plot financial metrics trend
plt.figure(figsize=(12, 8))
plt.subplot(2, 1, 1)
plt.plot(filtered_is['yearReport'], filtered_is['Revenue (Bn. VND)'], marker='o', label='Revenue')
plt.plot(filtered_is['yearReport'], filtered_is['Attribute to parent company (Bn. VND)'], marker='o', label='Net Profit')
plt.title('Revenue and Profit Trend')
plt.legend()

plt.subplot(2, 1, 2)
plt.plot(filtered_bs['yearReport'], filtered_bs['debt_to_equity'], marker='o')
plt.title('Debt-to-Equity Ratio')
```

## 5. Competitor Analysis

```python
# Compare financial ratios across banking sector
banks = ['VCB', 'ACB', 'TCB', 'BID', 'MBB']
bank_ratios = {}

for bank in banks:
    bank_stock = Vnstock().stock(symbol=bank, source='VCI')
    ratios = bank_stock.finance.ratio(period='year', lang='en').iloc[0]  # Most recent year
    bank_ratios[bank] = {
        'ROE': ratios['ROE (%)'],
        'ROA': ratios['ROA (%)'],
        'P/E': ratios['P/E'],
        'P/B': ratios['P/B']
    }

bank_comparison = pd.DataFrame(bank_ratios).T
print("Banking Sector Comparison:")
print(bank_comparison)
```

## 6. Investment Screening

```python
# Screen for high-ROE stocks with low P/B ratio
screener = stock.screener.stock(params={"exchangeName": "HOSE"}, limit=100)
filtered_stocks = screener[(screener['roe'] > 15) & 
                          (screener['price_vs_sma100'] == 'Giá nằm trên SMA(100)') &
                          (screener['last_quarter_profit_growth'] > 0)]

# Sort by market cap to find the largest companies meeting criteria
investment_candidates = filtered_stocks.sort_values('market_cap', ascending=False).head(10)
print("Top 10 Investment Candidates:")
print(investment_candidates[['ticker', 'market_cap', 'roe', 'last_quarter_profit_growth']])
```

## 7. Ownership Analysis

```python
# Analyze foreign ownership in a company
company_info = stock.company
ownership = company_info.shareholders()

# Calculate total percent owned by foreigners
foreign_owners = ownership[ownership['share_holder'].str.contains('Limited|Ltd|LLC|Fund|Corp', case=False, na=False)]
foreign_ownership_pct = foreign_owners['share_own_percent'].sum()

print(f"Foreign ownership percentage: {foreign_ownership_pct:.2%}")
```

## 8. Event Impact Analysis

```python
# Analyze stock performance around dividend events
events = stock.company.events()
dividend_events = events[events['event_list_name'] == 'Trả cổ tức bằng tiền mặt']

for index, event in dividend_events.iterrows():
    # Get stock prices around the ex-dividend date
    exright_date = event['exright_date']
    start_date = pd.to_datetime(exright_date) - pd.Timedelta(days=30)
    end_date = pd.to_datetime(exright_date) + pd.Timedelta(days=30)
    
    # Convert dates to the required string format 'YYYY-MM-DD'
    start_str = start_date.strftime('%Y-%m-%d')
    end_str = end_date.strftime('%Y-%m-%d')
    
    # Get price history around the event
    event_prices = stock.quote.history(start=start_str, end=end_str, interval='1D')
    
    # Additional analysis on price behavior before/after ex-dividend date
    # ...
```

## 9. Seasonal Performance Analysis

```python
# Analyze quarterly performance patterns over multiple years
quarterly_data = stock.finance.income_statement(period='quarter', lang='en')

# Group by quarter to analyze seasonal patterns
quarterly_data['quarter'] = quarterly_data['lengthReport']
quarterly_perf = quarterly_data.groupby(['yearReport', 'quarter'])['Revenue YoY (%)'].mean().unstack()

# Plot seasonal performance by quarter
quarterly_perf.mean().plot(kind='bar', figsize=(10, 6), title='Average Quarterly Performance')
```

## 10. News Sentiment Analysis

```python
# Basic news sentiment analysis
import re
from textblob import TextBlob  # You'll need to install this package

# Get recent news
recent_news = stock.company.news().head(20)

# Simple sentiment analysis function
def analyze_sentiment(text):
    if isinstance(text, str):
        # Clean text
        text = re.sub(r'<[^>]+>', '', text)  # Remove HTML tags
        return TextBlob(text).sentiment.polarity  # Return polarity (-1 to 1)
    return 0

# Apply sentiment analysis to news titles
recent_news['sentiment'] = recent_news['news_title'].apply(analyze_sentiment)

# Classify sentiment
recent_news['sentiment_category'] = recent_news['sentiment'].apply(
    lambda x: 'Positive' if x > 0.05 else ('Negative' if x < -0.05 else 'Neutral'))

# Count by sentiment
sentiment_count = recent_news['sentiment_category'].value_counts()
print("News Sentiment Analysis:")
print(sentiment_count)
```
Ratio.columns.to_list()
[('Meta', 'CP'),
 ('Meta', 'Năm'),
 ('Meta', 'Kỳ'),
 ('Chỉ tiêu cơ cấu nguồn vốn', '(Vay NH+DH)/VCSH'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'Nợ/VCSH'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'TSCĐ / Vốn CSH'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'Vốn CSH/Vốn điều lệ'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Vòng quay tài sản'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Vòng quay TSCĐ'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Số ngày thu tiền bình quân'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Số ngày tồn kho bình quân'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Số ngày thanh toán bình quân'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Chu kỳ tiền'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Vòng quay hàng tồn kho'),
 ('Chỉ tiêu khả năng sinh lợi', 'Biên EBIT (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Biên lợi nhuận gộp (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Biên lợi nhuận ròng (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROE (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROIC (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROA (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'EBITDA (Tỷ đồng)'),
 ('Chỉ tiêu khả năng sinh lợi', 'EBIT (Tỷ đồng)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Tỷ suất cổ tức (%)'),
 ('Chỉ tiêu thanh khoản', 'Chỉ số thanh toán hiện thời'),
 ('Chỉ tiêu thanh khoản', 'Chỉ số thanh toán tiền mặt'),
 ('Chỉ tiêu thanh khoản', 'Chỉ số thanh toán nhanh'),
 ('Chỉ tiêu thanh khoản', 'Khả năng chi trả lãi vay'),
 ('Chỉ tiêu thanh khoản', 'Đòn bẩy tài chính'),
 ('Chỉ tiêu định giá', 'Vốn hóa (Tỷ đồng)'),
 ('Chỉ tiêu định giá', 'Số CP lưu hành (Triệu CP)'),
 ('Chỉ tiêu định giá', 'P/E'),
 ('Chỉ tiêu định giá', 'P/B'),
 ('Chỉ tiêu định giá', 'P/S'),
 ('Chỉ tiêu định giá', 'P/Cash Flow'),
 ('Chỉ tiêu định giá', 'EPS (VND)'),
 ('Chỉ tiêu định giá', 'BVPS (VND)'),
 ('Chỉ tiêu định giá', 'EV/EBITDA')]

CashFlow.columns.to_list()
 ['ticker',
 'yearReport',
 'Net Profit/Loss before tax',
 'Depreciation and Amortisation',
 'Provision for credit losses',
 'Unrealized foreign exchange gain/loss',
 'Profit/Loss from investing activities',
 'Interest Expense',
 'Operating profit before changes in working capital',
 'Increase/Decrease in receivables',
 'Increase/Decrease in inventories',
 'Increase/Decrease in payables',
 'Increase/Decrease in prepaid expenses',
 'Interest paid',
 'Business Income Tax paid',
 'Other receipts from operating activities',
 'Other payments on operating activities',
 'Net cash inflows/outflows from operating activities',
 'Purchase of fixed assets',
 'Proceeds from disposal of fixed assets',
 'Loans granted, purchases of debt instruments (Bn. VND)',
 'Collection of loans, proceeds from sales of debts instruments (Bn. VND)',
 'Investment in other entities',
 'Proceeds from divestment in other entities',
 'Gain on Dividend',
 'Net Cash Flows from Investing Activities',
 'Increase in charter captial',
 'Payments for share repurchases',
 'Proceeds from borrowings',
 'Repayment of borrowings',
 'Dividends paid',
 'Cash flows from financial activities',
 'Net increase/decrease in cash and cash equivalents',
 'Cash and cash equivalents',
 'Foreign exchange differences Adjustment',
 'Cash and Cash Equivalents at the end of period']

BalanceSheet.columns.to_list()
 ['ticker',
 'yearReport',
 'CURRENT ASSETS (Bn. VND)',
 'Cash and cash equivalents (Bn. VND)',
 'Short-term investments (Bn. VND)',
 'Accounts receivable (Bn. VND)',
 'Net Inventories',
 'Other current assets',
 'LONG-TERM ASSETS (Bn. VND)',
 'Long-term loans receivables (Bn. VND)',
 'Fixed assets (Bn. VND)',
 'Investment in properties',
 'Long-term investments (Bn. VND)',
 'Other non-current assets',
 'TOTAL ASSETS (Bn. VND)',
 'LIABILITIES (Bn. VND)',
 'Current liabilities (Bn. VND)',
 'Long-term liabilities (Bn. VND)',
 "OWNER'S EQUITY(Bn.VND)",
 'Capital and reserves (Bn. VND)',
 'Other Reserves',
 'Undistributed earnings (Bn. VND)',
 'MINORITY INTERESTS',
 'TOTAL RESOURCES (Bn. VND)',
 'Prepayments to suppliers (Bn. VND)',
 'Short-term loans receivables (Bn. VND)',
 'Inventories, Net (Bn. VND)',
 'Other current assets (Bn. VND)',
 'Investment and development funds (Bn. VND)',
 'Common shares (Bn. VND)',
 'Paid-in capital (Bn. VND)',
 'Long-term borrowings (Bn. VND)',
 'Advances from customers (Bn. VND)',
 'Short-term borrowings (Bn. VND)',
 'Good will (Bn. VND)',
 'Long-term prepayments (Bn. VND)',
 'Other long-term assets (Bn. VND)',
 'Other long-term receivables (Bn. VND)',
 'Long-term trade receivables (Bn. VND)',
 'Quick Ratio']

 overview.columns.to_list()

 ['symbol',
 'exchange',
 'industry',
 'company_type',
 'no_shareholders',
 'foreign_percent',
 'outstanding_share',
 'issue_share',
 'established_year',
 'no_employees',
 'stock_rating',
 'delta_in_week',
 'delta_in_month',
 'delta_in_year',
 'short_name',
 'website',
 'industry_id',
 'industry_id_v2']

 """
Functions extracted from the VnStock notebook.
This collection includes all the main functions used in the notebook for stock data analysis.
"""

# Main wrapper functions

def stock(symbol='ACB', source='TCBS'):
    """
    Initialize a stock object for data retrieval operations.
    
    Parameters:
    ----------
    symbol : str
        Stock symbol/ticker (default: 'ACB')
    source : str
        Data source, options include 'TCBS', 'VCI', 'MSN', 'HOSE' (default: 'TCBS')
    
    Returns:
    -------
    Stock object with methods for accessing different types of data
    """
    from vnstock import Vnstock
    return Vnstock().stock(symbol=symbol, source=source)


# Quote functions

def history(symbol=None, start='2024-01-01', end='2024-06-21', interval='1D'):
    """
    Get historical price data for a stock.
    
    Parameters:
    ----------
    symbol : str
        Stock symbol/ticker (optional if object already initialized with symbol)
    start : str
        Start date in 'YYYY-MM-DD' format (default: '2024-01-01')
    end : str
        End date in 'YYYY-MM-DD' format (default: '2024-06-21')
    interval : str
        Time interval for data, e.g. '1D' for daily (default: '1D')
    
    Returns:
    -------
    DataFrame with historical price data (time, open, high, low, close, volume)
    """
    # In actual use, this would be called from a stock object instance:
    # stock.quote.history(symbol=symbol, start=start, end=end, interval=interval)
    pass


def intraday(symbol=None, page_size=1000, show_log=False):
    """
    Get intraday trading data (matched orders) for a stock.
    
    Parameters:
    ----------
    symbol : str
        Stock symbol/ticker (optional if object already initialized with symbol)
    page_size : int
        Number of records to return (default: 1000)
    show_log : bool
        Whether to display log information (default: False)
    
    Returns:
    -------
    DataFrame with intraday trading data (time, price, volume, match_type)
    """
    # In actual use: stock.quote.intraday(symbol=symbol, page_size=page_size, show_log=show_log)
    pass


# Trading functions

def price_board(symbols):
    """
    Get price board data for a list of stock symbols.
    
    Parameters:
    ----------
    symbols : list
        List of stock symbols to retrieve data for, e.g. ['ACB', 'FPT', 'VNM']
    
    Returns:
    -------
    DataFrame with price board data including current price, volume, and various metrics
    """
    # In actual use: stock.trading.price_board(symbols)
    pass


# Company information functions

def overview():
    """
    Get overview information for a company.
    
    Returns:
    -------
    DataFrame with company overview data including exchange, industry, outstanding shares, etc.
    """
    # In actual use: stock.company.overview()
    pass


def profile():
    """
    Get company profile information.
    
    Returns:
    -------
    DataFrame with detailed company profile, history, and business information
    """
    # In actual use: stock.company.profile()
    pass


def shareholders():
    """
    Get information about company shareholders.
    
    Returns:
    -------
    DataFrame with shareholder information including ownership percentages
    """
    # In actual use: stock.company.shareholders()
    pass


def insider_deals():
    """
    Get information about insider trading activities.
    
    Returns:
    -------
    DataFrame with insider deal information including dates, methods, actions, etc.
    """
    # In actual use: stock.company.insider_deals()
    pass


def subsidiaries():
    """
    Get information about company subsidiaries or affiliated companies.
    
    Returns:
    -------
    DataFrame with subsidiary information including ownership percentages
    """
    # In actual use: stock.company.subsidiaries()
    pass


def officers():
    """
    Get information about company officers/management.
    
    Returns:
    -------
    DataFrame with officer information including positions and ownership percentages
    """
    # In actual use: stock.company.officers()
    pass


def events():
    """
    Get information about company events like earnings announcements, dividends, etc.
    
    Returns:
    -------
    DataFrame with event information including dates, descriptions, etc.
    """
    # In actual use: stock.company.events()
    pass


def news():
    """
    Get company news and announcements.
    
    Returns:
    -------
    DataFrame with news information including titles, sources, and publication dates
    """
    # In actual use: stock.company.news()
    pass


def dividends():
    """
    Get dividend history for a company.
    
    Returns:
    -------
    DataFrame with dividend information including dates, percentages, and payment methods
    """
    # In actual use: stock.company.dividends()
    pass

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 15 entries, 0 to 14
Data columns (total 4 columns):
 #   Column                    Non-Null Count  Dtype  
---  ------                    --------------  -----  
 0   exercise_date             15 non-null     object 
 1   cash_year                 15 non-null     int64  
 2   cash_dividend_percentage  15 non-null     float64
 3   issue_method              15 non-null     object 
dtypes: float64(1), int64(1), object(2)
memory usage: 608.0+ bytes


# Financial report functions

def balance_sheet(period='year'):
    """
    Get balance sheet data for a company.
    
    Parameters:
    ----------
    period : str
        Time period, either 'year' or 'quarter' (default: 'year')
    
    Returns:
    -------
    DataFrame with balance sheet data including assets, liabilities, equity, etc.
    """
    # In actual use: stock.finance.balance_sheet(period=period)
    pass


def income_statement(period='year'):
    """
    Get income statement data for a company.
    
    Parameters:
    ----------
    period : str
        Time period, either 'year' or 'quarter' (default: 'year')
    
    Returns:
    -------
    DataFrame with income statement data including revenue, expenses, profits, etc.
    """
    # In actual use: stock.finance.income_statement(period=period)
    pass


def cash_flow(period='year'):
    """
    Get cash flow statement data for a company.
    
    Parameters:
    ----------
    period : str
        Time period, either 'year' or 'quarter' (default: 'year')
    
    Returns:
    -------
    DataFrame with cash flow data including operating, investing, and financing activities
    """
    # In actual use: stock.finance.cash_flow(period=period)
    pass


def ratio(period='year', dropna=True):
    """
    Get financial ratios for a company.
    
    Parameters:
    ----------
    period : str
        Time period, either 'year' or 'quarter' (default: 'year')
    dropna : bool
        Whether to drop rows with NA values (default: True)
    
    Returns:
    -------
    DataFrame with financial ratios like P/E, P/B, ROE, ROA, etc.
    """
    # In actual use: stock.finance.ratio(period=period, dropna=dropna)
    pass