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

Use the following filter criteria to set the params parameter.
* CANSLIM: epsGrowth1Year, lastQuarterProfitGrowth, roe, avgTradingValue20Day, relativeStrength1Month
* Value: roe, pe, avgTradingValue20Day
* High Dividend: dividendYield, avgTradingValue20Day
* Breakout Buy: avgTradingValue20Day, forecastVolumeRatio, breakout: 'BULLISH'
* Price Increase + Volume Surge: avgTradingValue20Day, forecastVolumeRatio
* 52-Week High Breakout: avgTradingValue20Day, priceBreakOut52Week: 'BREAK_OUT'
* 52-Week Low Breakdown: avgTradingValue20Day, priceWashOut52Week: 'WASH_OUT'
* Short-term Uptrend: avgTradingValue20Day, uptrend: 'buy-signal'
* Short-term Outperformance: relativeStrength3Day
* Growth: epsGrowth1Year, roe, avgTradingValue20Day

**Sector Constraints**
* exchangeName: Stock exchange, e.g. "HOSE", "HNX", or "UPCOM". Use commas to separate multiple exchanges, e.g. "HOSE,HNX,UPCOM".
* hasFinancialReport: Has latest financial report. 1 means yes, 0 means no.
* industryName: Filter stocks by specific industry. Value format is Retail for retail industry. Other values can be:
    * Insurance
    * Real Estate
    * Technology
    * Oil & Gas
    * Financial Services
    * Utilities
    * Travel & Leisure
    * Industrial Goods & Services
    * Personal & Household Goods
    * Chemicals
    * Banks
    * Automobiles & Parts
    * Basic Resources
    * Food & Beverage
    * Media
    * Telecommunications
    * Construction & Materials
    * Health Care
* marketCap: Market capitalization in billion VND
* priceNearRealtime: Current stock price in VND
* foreignVolumePercent: Foreign volume as percentage of total volume
* alpha: Stock return over market return
* beta: Stock volatility relative to market
* freeTransferRate: Percentage of freely transferable shares
**Growth**
* revenueGrowth1Year: Revenue growth rate in past year
* revenueGrowth5Year: Average revenue growth rate over past 5 years
* epsGrowth1Year: Earnings per share growth rate in past year
* epsGrowth5Year: Average earnings per share growth rate over past 5 years
* lastQuarterRevenueGrowth: Revenue growth rate in latest quarter
* secondQuarterRevenueGrowth: Revenue growth rate in second latest quarter
* lastQuarterProfitGrowth: Profit growth rate in latest quarter
* secondQuarterProfitGrowth: Profit growth rate in second latest quarter
**Financial Ratio**
* grossMargin: Gross profit margin
* netMargin: Net profit margin
* roe: Return on equity
* doe: Dividend on equity
* dividendYield: Dividend yield
* eps: Earnings per share in VND
* pe: Price to earnings ratio
* pb: Price to book ratio
* evEbitda: Enterprise value to EBITDA ratio
* netCashPerMarketCap: Net cash to market cap ratio
* netCashPerTotalAssets: Net cash to total assets ratio
* profitForTheLast4Quarters: Total profit in last 4 quarters in billion VND
**Price and Volume Volatility**
* suddenlyHighVolumeMatching: Signal indicating sudden surge in matched volume. 0 means no, 1 means yes
* totalTradingValue: Total trading value today in billion VND
* avgTradingValue5Day: Average trading value over 5 days in billion VND
* avgTradingValue10Day: Average trading value over 10 days in billion VND
* avgTradingValue20Day: Average trading value over 20 days in billion VND
* priceGrowth1Week: Price growth rate over past week
* priceGrowth1Month: Price growth rate over past month
* percent1YearFromPeak: Percentage change from 1-year high
* percentAwayFromHistoricalPeak: Percentage change from all-time high
* percent1YearFromBottom: Percentage change from 1-year low
* percentOffHistoricalBottom: Percentage change from all-time low
* priceVsSMA5: Price vs 5-day SMA relationship. Values can be ABOVE, BELOW, CROSS_ABOVE, or CROSS_BELOW
* priceVsSma10: Price vs 10-day SMA relationship. Values can be ABOVE, BELOW, CROSS_ABOVE, or CROSS_BELOW
* priceVsSMA20: Price vs 20-day SMA relationship. Values can be ABOVE, BELOW, CROSS_ABOVE, or CROSS_BELOW
* priceVsSma50: Price vs 50-day SMA relationship. Values can be ABOVE, BELOW, CROSS_ABOVE, or CROSS_BELOW
* priceVsSMA100: Price vs 100-day SMA relationship. Values can be ABOVE, BELOW, CROSS_ABOVE, or CROSS_BELOW
* forecastVolumeRatio: Ratio of forecast volume to actual volume today
* volumeVsVSma5: Current volume vs 5-day volume SMA ratio
* volumeVsVSma10: Current volume vs 10-day volume SMA ratio
* volumeVsVSma20: Current volume vs 20-day volume SMA ratio
* volumeVsVSma50: Current volume vs 50-day volume SMA ratio
**Market Behavior**
* strongBuyPercentage: Percentage of strong buy signals based on technical analysis
* activeBuyPercentage: Percentage of active buy signals based on technical analysis
* foreignTransaction: Foreign trading type today. Values can be buyMoreThanSell, sellMoreThanBuy, or noTransaction
* foreignBuySell20Session: Net foreign buy/sell value in last 20 sessions in billion VND
* numIncreaseContinuousDay: Number of consecutive up days
* numDecreaseContinuousDay: Number of consecutive down days
**Technical Signals**
* rsi14: 14-day Relative Strength Index
* rsi14Status: RSI status. Values can be intoOverBought, intoOverSold, outOfOverBought, or outOfOverSold
* tcbsBuySellSignal: TCBS buy/sell signal. Values can be BUY or SELL
* priceBreakOut52Week: 52-week price breakout signal. Values can be BREAK_OUT or NO_BREAK_OUT
* priceWashOut52Week: 52-week price washout signal. Values can be WASH_OUT or NO_WASH_OUT
* macdHistogram: MACD histogram signal. Values can be macdHistGT0Increase, macdHistGT0Decrease, macdHistLT0Increase, or macdHistLT0Decrease
* relativeStrength3Day: 3-day relative strength vs market
* relativeStrength1Month: 1-month relative strength vs market
* relativeStrength3Month: 3-month relative strength vs market
* relativeStrength1Year: 1-year relative strength vs market
* tcRS: TCBS relative strength vs market
* sarVsMacdHist: SAR vs MACD histogram signal. Values can be BUY or SELL
**Trading Signal**
* bollingBandSignal: Bollinger Band signal. Values can be BUY or SELL
* dmiSignal: Directional Movement Index signal. Values can be BUY or SELL
* uptrend: Uptrend signal. Values can be buy-signal or sell-signal
* breakout: Breakout signal. Values can be BULLISH or BEARISH
**TCBS Rating**
* tcbsRecommend: TCBS recommendation. Values can be BUY or SELL
* stockRating: TCBS stock rating score. Scale 1-5, with 5 being best
* businessModel: TCBS business model rating. Scale 1-5, with 5 being best
* financialHealth: TCBS financial health rating. Scale 1-5, with 5 being best


For a comprehensive list of all available screening parameters and conditions, refer to the official documentation: [Screening Parameters Reference](https://docs.vnstock.site/functions/screener/#ieu-kien-loc)

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
# Example Use Cases for vnstock Library

Here are practical example use cases demonstrating how to use the vnstock library for Vietnamese stock market analysis:

## 1. Setting Up and Basic Usage

```python
from vnstock import Vnstock
# Initialize with a default stock symbol and data source
stock = Vnstock().stock(symbol='ACB', source='VCI')
```

## 2. Listing Stocks

**Get list of all VN30 stocks for market analysis:**
```python
vn30_stocks = stock.listing.symbols_by_group('VN30')
print(f"There are {len(vn30_stocks)} stocks in the VN30 index")
```


## 3. Index Data

**Get historical data for moving average analysis:**
```python
import pandas as pd

# Get 1-year historical data for VNIndex
vnindex_hist = stock.quote.history(symbol='VNINDEX', start='2024-01-01', end='2025-03-19', interval='1D')


vnindex_hist.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 500 entries, 0 to 499
Data columns (total 6 columns):
 #   Column  Non-Null Count  Dtype         
---  ------  --------------  -----         
 0   time    500 non-null    datetime64[ns]
 1   open    500 non-null    float64       
 2   high    500 non-null    float64       
 3   low     500 non-null    float64       
 4   close   500 non-null    float64       
 5   volume  500 non-null    int64         
```

## 7. Ownership Analysis
# Analyze foreign ownership in a company

```python   
company_info = stock.company
ownership = company_info.shareholders()
```

```python 
ownership.info()
```
```python
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 88 entries, 0 to 87
Data columns (total 5 columns):
 #   Column             Non-Null Count  Dtype  
---  ------             --------------  -----  
 0   id                 88 non-null     object 
 1   share_holder       88 non-null     object 
 2   quantity           88 non-null     int64  
 3   share_own_percent  88 non-null     float64
 4   update_date        88 non-null     object 
```

# Calculate total percent owned by foreigners
foreign_owners = ownership[ownership['share_holder'].str.contains('Limited|Ltd|LLC|Fund|Corp', case=False, na=False)]
foreign_ownership_pct = foreign_owners['share_own_percent'].sum()

```python
print(f"Foreign ownership percentage: {foreign_ownership_pct:.2%}")
```

## 8. Event Impact Analysis

```python
# Analyze stock performance around dividend events
events = stock.company.events()

events.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 37 entries, 0 to 36
Data columns (total 13 columns):
 #   Column               Non-Null Count  Dtype  
---  ------               --------------  -----  
 0   id                   37 non-null     object 
 1   event_title          37 non-null     object 
 2   en__event_title      37 non-null     object 
 3   public_date          37 non-null     object 
 4   issue_date           37 non-null     object 
 5   source_url           37 non-null     object 
 6   event_list_code      37 non-null     object 
 7   ratio                22 non-null     float64
 8   value                22 non-null     float64
 9   record_date          37 non-null     object 
 10  exright_date         37 non-null     object 
 11  event_list_name      37 non-null     object 
 12  en__event_list_name  37 non-null     object




```

## 10. News Analysis

```python
# Basic news sentiment analysis
import re
from textblob import TextBlob  # You'll need to install this package

# Get recent news
recent_news = stock.company.news()
recent_news.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 10 entries, 0 to 9
Data columns (total 18 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   id                  10 non-null     object 
 1   news_title          10 non-null     object 
 2   news_sub_title      10 non-null     object 
 3   friendly_sub_title  10 non-null     object 
 4   news_image_url      10 non-null     object 
 5   news_source_link    10 non-null     object 
 6   created_at          0 non-null      object 
 7   public_date         10 non-null     int64  
 8   updated_at          0 non-null      object 
 9   lang_code           10 non-null     object 
 10  news_id             10 non-null     object 
 11  news_short_content  10 non-null     object 
 12  news_full_content   10 non-null     object 
 13  close_price         10 non-null     int64  
 14  ref_price           10 non-null     int64  
 15  floor               10 non-null     int64  
 16  ceiling             10 non-null     int64  
 17  price_change_pct    10 non-null     float64


# Data structure for financial statements dataframes 

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

income_stmt.info()
 #   Column                                 Non-Null Count  Dtype  
---  ------                                 --------------  -----  
 0   ticker                                 12 non-null     object 
 1   yearReport                             12 non-null     int64  
 2   Revenue YoY (%)                        12 non-null     float64
 3   Revenue (Bn. VND)                      12 non-null     int64  
 4   Attribute to parent company (Bn. VND)  12 non-null     int64  
 5   Attribute to parent company YoY (%)    12 non-null     float64
 6   Financial Income                       12 non-null     int64  
 7   Interest Expenses                      12 non-null     int64  
 8   Sales                                  12 non-null     int64  
 9   Sales deductions                       12 non-null     int64  
 10  Net Sales                              12 non-null     int64  
 11  Cost of Sales                          12 non-null     int64  
 12  Gross Profit                           12 non-null     int64  
 13  Financial Expenses                     12 non-null     int64  
 14  Gain/(loss) from joint ventures        12 non-null     int64  
 15  Selling Expenses                       12 non-null     int64  
 16  General & Admin Expenses               12 non-null     int64  
 17  Operating Profit/Loss                  12 non-null     int64  
 18  Other income                           12 non-null     int64  
 19  Net income from associated companies   12 non-null     int64  
 20  Other Income/Expenses                  12 non-null     int64  
 21  Net other income/expenses              12 non-null     int64  
 22  Profit before tax                      12 non-null     int64  
 23  Business income tax - current          12 non-null     int64  
 24  Business income tax - deferred         12 non-null     int64  
 25  Net Profit For the Year                12 non-null     int64  
 26  Minority Interest                      12 non-null     int64  
 27  Attributable to parent company         12 non-null     int64  

ratio.columns.to_list()

[('Meta', 'ticker'),
 ('Meta', 'yearReport'),
 ('Meta', 'lengthReport'),
 ('Chỉ tiêu cơ cấu nguồn vốn', '(ST+LT borrowings)/Equity'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'Debt/Equity'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'Fixed Asset-To-Equity'),
 ('Chỉ tiêu cơ cấu nguồn vốn', "Owners' Equity/Charter Capital"),
 ('Chỉ tiêu hiệu quả hoạt động', 'Asset Turnover'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Fixed Asset Turnover'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Days Sales Outstanding'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Days Inventory Outstanding'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Days Payable Outstanding'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Cash Cycle'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Inventory Turnover'),
 ('Chỉ tiêu khả năng sinh lợi', 'EBIT Margin (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Gross Profit Margin (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Net Profit Margin (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROE (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROIC (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROA (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'EBITDA (Bn. VND)'),
 ('Chỉ tiêu khả năng sinh lợi', 'EBIT (Bn. VND)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Dividend yield (%)'),
 ('Chỉ tiêu thanh khoản', 'Current Ratio'),
 ('Chỉ tiêu thanh khoản', 'Cash Ratio'),
 ('Chỉ tiêu thanh khoản', 'Quick Ratio'),
 ('Chỉ tiêu thanh khoản', 'Interest Coverage'),
 ('Chỉ tiêu thanh khoản', 'Financial Leverage'),
 ('Chỉ tiêu định giá', 'Market Capital (Bn. VND)'),
 ('Chỉ tiêu định giá', 'Outstanding Share (Mil. Shares)'),
 ('Chỉ tiêu định giá', 'P/E'),
 ('Chỉ tiêu định giá', 'P/B'),
 ('Chỉ tiêu định giá', 'P/S'),
 ('Chỉ tiêu định giá', 'P/Cash Flow'),
 ('Chỉ tiêu định giá', 'EPS (VND)'),
 ('Chỉ tiêu định giá', 'BVPS (VND)'),
 ('Chỉ tiêu định giá', 'EV/EBITDA')]

# Apply to MultiIndex DataFrame
``` 
flattened_df = flatten_hierarchical_index(
    ratios,  # multi-index df
    separator="_",  # separator for flattened columns
    handle_duplicates=True,  # handle duplicate column names
    drop_levels=0,  # or specify levels to drop
)
```

cash_flow.columns.to_list()
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

balance_sheet.columns.to_list()
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
fund_list = fund.listing()

fund_list.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 57 entries, 0 to 56
Data columns (total 21 columns):
 #   Column                     Non-Null Count  Dtype  
---  ------                     --------------  -----  
 0   short_name                 57 non-null     object 
 1   name                       57 non-null     object 
 2   fund_type                  57 non-null     object 
 3   fund_owner_name            57 non-null     object 
 4   management_fee             57 non-null     float64
 5   inception_date             48 non-null     object 
 6   nav                        57 non-null     float64
 7   nav_change_previous        57 non-null     float64
 8   nav_change_last_year       54 non-null     float64
 9   nav_change_inception       57 non-null     float64
 10  nav_change_1m              57 non-null     float64
 11  nav_change_3m              56 non-null     float64
 12  nav_change_6m              54 non-null     float64
 13  nav_change_12m             51 non-null     float64
 14  nav_change_24m             44 non-null     float64
 15  nav_change_36m             35 non-null     float64
 16  nav_change_36m_annualized  35 non-null     float64
 17  nav_update_at              57 non-null     object 
 18  fund_id_fmarket            57 non-null     int64  
 19  fund_code                  57 non-null     object 
 20  vsd_fee_id                 57 non-null     object 
dtypes: float64(12), int64(1), object(8)

# Fund Data Functions

The vnstock library provides access to fund data from fmarket.vn, allowing investors to easily retrieve and analyze investment fund information.

## Initialization

To access fund data, you can use the `Fund` class directly or through the Vnstock class:

```python
# Method 1: Direct import of Fund class
from vnstock import Fund
fund = Fund()

# Method 2: Using the Vnstock class
from vnstock import Vnstock
fund = Vnstock().fund()
```

## Fund Listing

Retrieves a list of all available funds or filtered by fund type.

### Parameters:

- `fund_type` (str, optional): Type of fund to filter by. Options include:
  - `'BALANCED'`: Balanced funds
  - `'BOND'`: Bond funds
  - `'STOCK'`: Stock funds
  - `''`: Empty string (default) - All funds

### Example Usage:

```python
# Get all funds
all_funds = fund.listing()

# Get only stock funds
stock_funds = fund.listing(fund_type='STOCK')
```

### Sample Output:

```
Total number of funds currently listed on Fmarket: 49
  short_name                  fund_name fund_type  inception_date  \
0     VESAF  Quỹ đầu tư cổ phiếu Việt Nam     STOCK     2017-04-10   
1     VNDAF  Quỹ đầu tư cổ phiếu Tăng trưởng VINACAPITAL     STOCK     2018-04-12   

   nav_at_inception  current_nav  nav_change_1w  nav_change_1m  \
0          10000.0      19359.0          -0.35          -1.22   
1          10000.0      17750.0          -0.45          -1.28   
```

## Fund Details

### Asset Holdings

Retrieves the asset allocation breakdown for a specific fund.

#### Parameters:

- `symbol` (str, required): Fund symbol/ticker

#### Example Usage:

```python
# Get asset holdings for a specific fund
asset_holdings = fund.details.asset_holding('SSISCA')
```

#### Sample Output:

```
Retrieving data for SSISCA
   asset_percent                asset_type short_name
0          83.08                  Cổ phiếu     SSISCA
1          16.92  Tiền và tương đương tiền     SSISCA
```

### Industry Allocation

Retrieves the industry allocation breakdown for a specific fund.

#### Parameters:

- `symbol` (str, required): Fund symbol/ticker

#### Example Usage:

```python
# Get industry allocation for a specific fund
industry_allocation = fund.details.industry_holding('SSISCA')
```

#### Sample Output:

```
              industry  net_asset_percent short_name
0                Ngân hàng           19.25     SSISCA
1                Bất động sản          13.83     SSISCA
2                  Bán lẻ           10.63     SSISCA
```

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
