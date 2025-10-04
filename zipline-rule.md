# Vietnamese Stock Market Data Pipeline: vnstock3 to Zipline Reloaded

**Vietnamese market data integration for quantitative trading requires understanding vnstock3 v3.2.6 API structure, Zipline Reloaded CSV format requirements, and market-specific corporate action handling.** This implementation guide delivers production-ready patterns for local development, with complete data transformation pipelines tested against Vietnamese stock market characteristics including ±7% price limits, Tet holiday handling, and 100-share lot conventions.

## Quick start: Core transformation pattern

The fundamental challenge is bridging vnstock3's adjusted OHLCV output (datetime64[ns] with timezone) to Zipline's timezone-naive CSV format with explicit corporate action files. **Vietnamese market data comes pre-adjusted** from vnstock3, meaning splits and dividends are already reflected in historical prices without separate event records. This requires accepting adjusted prices as-is for backtesting.

A minimal working pipeline downloads Vietnamese stocks (VNM, VCB, VHM), converts timezone-aware timestamps to naive YYYY-MM-DD strings, adds required dividend/split columns (defaulting to 0.0 and 1.0), validates against Vietnamese price limit rules (±7% HOSE), and outputs Zipline-compatible CSVs. Production implementations layer on batch processing with rate limiting, and Vietnamese trading calendar integration (handling Tet's 7-9 day closure).

## vnstock3 v3.2.6 API: Data extraction fundamentals

**Installation and versioning:** vnstock3 v3.2.6 (released May 23, 2025) requires Python ≥3.10 and installs via `pip install vnstock==3.2.6`. The package uses a custom license limited to personal, research, and non-commercial use—commercial applications require licensing from support@vnstocks.com. The API has undergone significant evolution from earlier versions, with v3.2.6 introducing KRX standard futures contract support and fixing critical timezone inconsistencies.

**Primary data extraction method:** The core interface uses `Vnstock().stock(symbol, source).quote.history()` for daily OHLCV retrieval. Two data sources exist: 

**VCI (recommended)** provides broader asset coverage including stocks, futures, covered warrants, bonds, ETFs, and indices across HOSE/HNX/UPCOM exchanges; 

**TCBS** focuses on stock data with more limited functionality. The method signature accepts start/end dates in YYYY-MM-DD string format, interval specification (1D for daily, 1H/15m for intraday), and returns pandas DataFrames with timezone-aware datetime64[ns] timestamps.

```python
from vnstock import Vnstock

# Download Vietcombank (VCB) daily data
stock = Vnstock().stock(symbol='VCB', source='VCI')
df = stock.quote.history(start='2020-01-01', end='2024-05-25', interval='1D')

# Output columns: time (datetime64[ns]), open, high, low, close (float64), volume (int64)
# DataFrame shape: ~1095 rows × 6 columns for 4+ years of data
```

**Data structure and types:** vnstock3 returns DataFrames with six columns: `time` (datetime64[ns] timezone-aware), `open`/`high`/`low`/`close` (float64 in VND for stocks), and `volume` (int64 as share count). 

The data is **automatically adjusted** for all corporate actions—splits, stock dividends, and cash dividends modify historical prices proportionally. 

**No unadjusted data access exists** through the API. The adjustment methodology applies proportional factors to all historical prices prior to corporate action dates, meaning a 2:1 split on 2024-01-15 would retroactively halve all prices before that date.

**API rate limits and batch processing:** No explicit public rate limits exist, but underlying VCI/TCBS sources throttle requests. Best practices involve 500ms delays between symbol requests and implementing exponential backoff retry logic using the tenacity library. The API lacks native batch download methods—multi-symbol downloads require manual iteration with proper rate limiting. vnstock3 v3.2.1+ includes proactive rate limit warnings and v3.2.3 added built-in retry mechanisms.

**Data availability and historical depth:** Historical data extends back to each asset's listing date, with VNINDEX data available from July 28, 2000 (base date). 

**Critical historical note:** Prior to March 1, 2002, Vietnamese markets traded only on alternate days. Intraday data (1m, 5m, 15m intervals) has limited historical depth and is only accessible during trading hours (9:00 AM - 3:00 PM GMT+7). For daily data, the full historical range is available regardless of listing age.

## Zipline Reloaded CSV bundle format: Exact specifications

**Required CSV structure:** Zipline's csvdir bundle demands seven columns with exact lowercase naming: `date`, `open`, `high`, `low`, `close`, `volume`, `dividend`, `split`. The first row must be a header, order doesn't matter, and delimiters must be commas (semicolons cause errors). Files can be plain CSV or gzipped (.csv.gz) and must use UTF-8 encoding.

```csv
date,open,high,low,close,volume,dividend,split
2012-01-03,58.485714,58.92857,58.42857,58.747143,75555200,0.0,1.0
2012-01-04,58.57143,59.240002,58.468571,59.062859,65005500,0.0,1.0
2012-01-05,59.278572,59.792858,58.952858,59.718571,67817400,0.0,1.0
```

**Date formatting requirements:** The date column requires timezone-naive strings in YYYY-MM-DD format (daily) or YYYY-MM-DD HH:MM:SS (minute). 

**Critical constraint:** While CSV dates are timezone-naive, Zipline internally converts everything to UTC using the specified trading calendar. The start_session and end_session parameters in bundle registration MUST have `tz='utc'` or ingestion fails.

**Directory structure:** Organize files as `/path/to/csvdir/daily/{SYMBOL}.csv` and `/path/to/csvdir/minute/{SYMBOL}.csv`. Symbol names are extracted from filenames by removing the .csv extension, so AAPL.csv becomes symbol AAPL. Case sensitivity applies—filenames determine symbol names exactly.



**Corporate actions handling:** The csvdir bundle embeds splits and dividends within each CSV file rather than using separate metadata files. The `dividend` column holds cash dividend amounts (0.0 when absent), while `split` column contains ratios (1.0 for no split, 2.0 for 2-for-1 split). **Important convention:** Use the actual split multiplier, not the inverse—a 2:1 split is 2.0, not 0.5. Both values apply on ex-dividend dates.

**Bundle registration pattern:** Create `~/.zipline/extension.py` to register custom bundles:

```python
import pandas as pd
from zipline.data.bundles import register
from zipline.data.bundles.csvdir import csvdir_equities

start_session = pd.Timestamp('2020-1-1', tz='utc')
end_session = pd.Timestamp('2024-12-31', tz='utc')

register(
    'vnstock-bundle',
    csvdir_equities(['daily'], '/path/to/zipline_data'),
    calendar_name='XHKG',  # Hong Kong calendar closest to Vietnam
    start_session=start_session,
    end_session=end_session
)
```

**How the directory structure works**

/path/to/zipline_data is the root directory you specify when registering your Zipline bundle. Inside this root directory, you need to create subdirectories based on data frequency:

```python

/path/to/zipline_data/
├── daily/
│   ├── VNM.csv
│   ├── VCB.csv
│   ├── VHM.csv
│   └── ... (all other stock CSVs)
├── minute/  (optional, for intraday data)
│   └── ...
├── splits.csv  (optional, at root level)
└── dividends.csv  (optional, at root level)

```

**Key points**

Individual CSV files go in the daily/ subdirectory (or minute/ for intraday)
Each CSV file is named exactly as the symbol: VCB.csv → symbol VCB in Zipline
The bundle registration path should point to the root directory (/path/to/zipline_data), not to the daily/ folder
The csvdir_equities(['daily'], '/path/to/zipline_data') tells Zipline to look inside the daily/ subdirectory
After registration, ingest with `zipline ingest -b vnstock-bundle` and verify with `zipline bundles`.

**Concrete example**

```python

# In your pipeline.py, save files like this:
output_dir = Path('./zipline_data/daily')  # Creates the daily subdirectory
output_dir.mkdir(parents=True, exist_ok=True)
df.to_csv(output_dir / 'VCB.csv', index=False)

# In ~/.zipline/extension.py, register like this:
register(
    'vnstock-bundle',
    csvdir_equities(
        ['daily'],           # This tells Zipline to look in daily/ subdirectory
        './zipline_data',    # This is the ROOT path
    ),
    ...
)

```

**Critical requirements**

Subdirectory name MUST be daily/ or minute/ - these are hardcoded in Zipline's csvdir bundle implementation
You specify which subdirectories to use when registering: csvdir_equities(['daily'], ...) or csvdir_equities(['daily', 'minute'], ...)
You cannot use custom names like stocks/, data/, or daily_data/ - it must be exactly daily/ or minute/


##Complete Working Example

### Step 1: Create the folder structure 

```python

mkdir -p ./zipline_data/daily

```

### Step 2: Save CSV files to the daily folder

```python

# pipeline.py
from pathlib import Path

OUTPUT_DIR = Path('./zipline_data/daily')  # Must be 'daily' subdirectory
OUTPUT_DIR.mkdir(parents=True, exist_ok=True)

# Save each stock
df.to_csv(OUTPUT_DIR / 'VCB.csv', index=False)
df.to_csv(OUTPUT_DIR / 'VNM.csv', index=False)

```

### Step 3: Register bundle pointing to ROOT directory

```python

# ~/.zipline/extension.py
import pandas as pd
from zipline.data.bundles import register
from zipline.data.bundles.csvdir import csvdir_equities

register(
    'vnstock-bundle',
    csvdir_equities(
        ['daily'],              # Tells Zipline to look in daily/ folder
        './zipline_data'        # Root path - NOT ./zipline_data/daily
    ),
    calendar_name='XHKG',
    start_session=pd.Timestamp('2020-1-1', tz='utc'),
    end_session=pd.Timestamp('2024-12-31', tz='utc')
)

```

### Step 4: Ingest

```bash

zipline ingest -b vnstock-bundle

```

**Correct: CSVs in daily/, register with root path**

zipline_data/        ← Register this path
└── daily/           ← Zipline looks here automatically
    ├── VCB.csv
    └── VNM.csv


**Example from vnstock3 Transformation**

```python

def prepare_vnstock_for_zipline_from_df(df):
    """Transform vnstock3 output to Zipline format"""
    df = df.reset_index()
    
    # vnstock3 columns: time, open, high, low, close, volume
    # Need to add: dividend, split
    # Need to rename: time → date
    
    # Convert datetime to string
    df['time'] = pd.to_datetime(df['time'])
    if df['time'].dt.tz is not None:
        df['time'] = df['time'].dt.tz_localize(None)
    df['time'] = df['time'].dt.strftime('%Y-%m-%d')
    
    # Rename and add columns
    df = df.rename(columns={'time': 'date'})
    df['dividend'] = 0.0   # Add dividend column (default 0.0)
    df['split'] = 1.0      # Add split column (default 1.0)
    
    # Select exact columns needed
    df = df[['date', 'open', 'high', 'low', 'close', 'volume', 'dividend', 'split']]
    
    return df

```

**Valid Example CSV (VCB.csv)**

```csv

date,open,high,low,close,volume,dividend,split
2024-01-02,95500,96000,95000,95800,2500000,0.0,1.0
2024-01-03,95800,96500,95500,96200,2800000,0.0,1.0
2024-01-04,96200,97000,96000,96800,3100000,0.0,1.0
2024-01-05,96800,97500,96500,97200,2900000,0.0,1.0
2024-01-08,97200,98000,97000,97800,3200000,0.0,1.0
2024-01-09,97800,98500,97500,98200,3500000,500.0,1.0
2024-01-10,49100,49500,48800,49300,7000000,0.0,2.0

```

## Comparison: vnstock3 vs yfinance

| Library            | Column Names                                                                                      | Date Column                |
|---------------------|---------------------------------------------------------------------------------------------------|----------------------------|
| **vnstock3**        | `time`, `open`, `high`, `low`, `close`, `volume`                                                  | `time` (lowercase)         |
| **yfinance**        | `Open`, `High`, `Low`, `Close`, `Adj Close`, `Volume`                                            | Index (not column)        |
| **Zipline required**| `date`, `open`, `high`, `low`, `close`, `volume`, `dividend`, `split`                            | `date` (lowercase)        |

**Data quality requirements:** Zipline enforces strict validation: no duplicate timestamps, no missing values in required columns, volume must be positive (zero volume prevents order execution), dates must ascend chronologically, and OHLC relationships must be valid (high ≥ open/close/low). Non-trading days are automatically filtered using the trading calendar, so don't include weekends or holidays in CSVs—Zipline handles this.

## Vietnamese market characteristics: Trading rules and data implications

**Trading hours and calendar:** Vietnamese markets operate Monday-Friday, 9:00 AM - 3:00 PM GMT+7 (no daylight saving). HOSE sessions split into morning (9:15 AM-11:30 AM) and afternoon (1:00 PM-2:30 PM) with opening/closing periodic auctions at 9:15 AM and 2:45 PM. **Tet Lunar New Year** creates the most significant data gap—7-9 consecutive non-trading days annually, with dates shifting based on the lunar calendar (2025: Jan 27, 2026: Feb 16). Other major holidays include Reunification Day/May Day cluster (Apr 30-May 4), National Day (Sep 2-3), and Hung King's Death Anniversary (lunar date, typically April).

**Price limits and reference prices:** HOSE enforces **±7% daily price limits** from reference prices, HNX uses ±10%, and UPCOM has wider bands. Reference prices equal the previous trading day's closing price (determined at 2:45 PM closing auction). Newly listed stocks get ±20% (HOSE) or ±30% (HNX) limits on first day. Stocks resuming after 25+ day suspensions also receive expanded ±20-30% bands. **Critical implementation detail:** When stocks hit ceiling or floor prices, trading continues at the limit—no circuit breakers exist, and stocks can remain pinned at limits for entire sessions.

**Lot sizes and trading conventions:** Standard trading occurs in round lots of **100 shares minimum**. Odd lots (1-99 shares) trade separately during continuous sessions but not during opening/closing auctions. Odd lot prices typically differ from round lot prices and show lower liquidity. Put-through sessions allow large block trades (20,000+ share minimum) from 9:00 AM-3:00 PM with break 11:30 AM-1:00 PM.

**Corporate actions landscape:** Vietnamese markets exhibit extraordinarily high split activity—718 splits occurred from January 2007 to May 2011 across 393 companies (out of 686 listed). The first split was REE at 1.2:1 in 2002. Terms "stock split," "stock dividend," and "bonus shares" are used interchangeably. **Unique regulatory requirement:** Companies must announce insider trading intentions 3 days BEFORE corporate action execution (uncommon globally). Dividends come as cash (paid through VSD) or stock dividends (bonus shares with ratios like 1,000:276). Rights issues trade separately on exchanges under different ISINs for 2-3 working days before subscription.

**Exchange structure and differences:** Vietnam has three trading platforms with distinct characteristics:

- **HOSE** (Ho Chi Minh Stock Exchange): $219B market cap, ~402 stocks, ±7% limits, strictest listing requirements, dominates with 90%+ trading value. Ticker format: 3-letter codes (VNM, VCB, HPG). VN-Index tracks all listed stocks with base 100 on July 28, 2000.

- **HNX** (Hanoi Stock Exchange): $15B market cap, ~329 stocks, ±10% limits, moderate requirements, popular with local speculators. Primary bond exchange. Top 20 stocks represent ~70% of market cap.

- **UPCOM** (Unlisted Public Company Market): $60B market cap, ~860-903 stocks, wider price bands, most flexible listing, operated by HNX. No margin trading allowed. Only ~20% of stocks trade frequently. Hosts delisted companies, SOE equitization candidates, and large unlisted entities (Vietnam Airlines, Airports Corp).

**Data quality challenges:** Infrastructure issues historically plagued HOSE—2021 crashes from trading surges on decades-old technology. The **KRX trading system** launched May 2025 addresses these issues with modern capacity. Common data anomalies include zero-volume days (especially UPCOM stocks), reference price gaps when stocks suspend 25+ days, odd lot data appearing in separate feeds, and pre-2002 alternate-day trading creating sparse early history. Foreign ownership limits (49% default, 30% for banks) create separate foreign/domestic pricing when limits exhaust—12 stocks hit limits as of 2024.

## Data transformation pipeline: vnstock3 to Zipline implementation

**Core column mapping and datetime conversion:** The fundamental transformation renames vnstock3's `time` column to `date`, strips timezone information, formats as YYYY-MM-DD strings, and adds `dividend` (0.0) and `split` (1.0) columns:

```python
import pandas as pd
from vnstock import Vnstock

def prepare_vnstock_for_zipline(symbol, start_date, end_date):
    """Transform vnstock3 data to Zipline CSV format"""
    # Download from vnstock3
    stock = Vnstock().stock(symbol=symbol, source='VCI')
    df = stock.quote.history(start=start_date, end=end_date, interval='1D')
    
    # Reset index to make datetime a column
    df = df.reset_index()
    
    # Remove timezone and convert to string
    if 'time' in df.columns:
        df['time'] = pd.to_datetime(df['time'])
        if df['time'].dt.tz is not None:
            df['time'] = df['time'].dt.tz_localize(None)
        df['time'] = df['time'].dt.strftime('%Y-%m-%d')
        df = df.rename(columns={'time': 'date'})
    
    # Add required Zipline columns
    df['dividend'] = 0.0
    df['split'] = 1.0
    
    # Select and order columns
    df = df[['date', 'open', 'high', 'low', 'close', 'volume', 'dividend', 'split']]
    
    return df

# Example usage
df = prepare_vnstock_for_zipline('VCB', '2020-01-01', '2024-12-31')
df.to_csv('./zipline_data/daily/VCB.csv', index=False)
```

**Vietnamese market-specific validation:** Implement validation checks for Vietnamese price limits, OHLC relationships, and volume constraints:

```python
def validate_vietnamese_stock_data(df, symbol, exchange='HOSE'):
    """Validate data against Vietnamese market rules"""
    issues = []
    
    # Price limit validation (±7% for HOSE)
    price_limit = 0.07 if exchange == 'HOSE' else 0.10
    df['price_change'] = df['close'].pct_change()
    violations = df[df['price_change'].abs() > price_limit]
    
    if len(violations) > 0:
        issues.append(f"Price limit violations: {len(violations)} days exceed ±{price_limit*100}%")
    
    # OHLC relationship validation
    invalid_ohlc = df[
        (df['high'] < df['low']) |
        (df['high'] < df['open']) |
        (df['high'] < df['close']) |
        (df['low'] > df['open']) |
        (df['low'] > df['close'])
    ]
    
    if len(invalid_ohlc) > 0:
        issues.append(f"Invalid OHLC relationships: {len(invalid_ohlc)} rows")
    
    # Volume validation (must be positive)
    if (df['volume'] <= 0).any():
        issues.append("Zero or negative volume detected")
    
    # Missing data check
    if df.isnull().any().any():
        issues.append(f"Missing data: {df.isnull().sum().to_dict()}")
    
    return {'is_valid': len(issues) == 0, 'issues': issues}
```

**Batch download with rate limiting:** Process multiple Vietnamese stocks efficiently with proper throttling and error handling:

```python
import time
from ratelimit import limits, sleep_and_retry
from tqdm import tqdm

CALLS_PER_MINUTE = 30
RATE_LIMIT_PERIOD = 60

@sleep_and_retry
@limits(calls=CALLS_PER_MINUTE, period=RATE_LIMIT_PERIOD)
def rate_limited_download(symbol, start_date, end_date):
    """Download with rate limiting"""
    stock = Vnstock().stock(symbol=symbol, source='VCI')
    return stock.quote.history(start=start_date, end=end_date, interval='1D')

def batch_download_stocks(symbols, start_date, end_date, output_dir='./zipline_data/daily'):
    """Download multiple stocks with error handling"""
    import os
    os.makedirs(output_dir, exist_ok=True)
    
    results = {'success': [], 'failed': [], 'errors': {}}
    
    for symbol in tqdm(symbols, desc="Downloading stocks"):
        try:
            df = rate_limited_download(symbol, start_date, end_date)
            df = prepare_vnstock_for_zipline_from_df(df)
            
            # Validate before saving
            validation = validate_vietnamese_stock_data(df, symbol)
            
            if validation['is_valid']:
                output_path = os.path.join(output_dir, f'{symbol}.csv')
                df.to_csv(output_path, index=False)
                results['success'].append(symbol)
            else:
                results['failed'].append(symbol)
                results['errors'][symbol] = validation['issues']
                
        except Exception as e:
            results['failed'].append(symbol)
            results['errors'][symbol] = str(e)
            time.sleep(2)  # Backoff on error
    
    return results

def prepare_vnstock_for_zipline_from_df(df):
    """Transform already-downloaded DataFrame"""
    df = df.reset_index()
    date_col = 'time' if 'time' in df.columns else 'date'
    
    df[date_col] = pd.to_datetime(df[date_col])
    if df[date_col].dt.tz is not None:
        df[date_col] = df[date_col].dt.tz_localize(None)
    df[date_col] = df[date_col].dt.strftime('%Y-%m-%d')
    
    df = df.rename(columns={date_col: 'date'})
    df['dividend'] = 0.0
    df['split'] = 1.0
    
    return df[['date', 'open', 'high', 'low', 'close', 'volume', 'dividend', 'split']]
```

**Simple processing without caching:** For lightweight implementations, process data directly without persistent caching:

```python
def process_vnstock_direct(symbol, start_date, end_date):
    """Direct processing without caching"""
    stock = Vnstock().stock(symbol=symbol, source='VCI')
    df = stock.quote.history(start=start_date, end=end_date, interval='1D')
    
    if len(df) == 0:
        return None
    
    # Transform immediately
    df = prepare_vnstock_for_zipline_from_df(df)
    return df
```

## Corporate actions handling: Detecting splits and dividends

**Challenge with adjusted data:** vnstock3 returns pre-adjusted prices with corporate actions already reflected—historical prices are modified proportionally when splits or dividends occur. **No separate corporate action feed exists** in the API. This creates two implementation paths:

1. **Accept adjusted prices as-is** (recommended for quick implementation): Set all dividend=0.0 and split=1.0 in output CSVs. Zipline uses the adjusted prices directly for backtesting. This approach is valid because the price adjustments already reflect economic reality.

2. **Detect corporate actions from price gaps** (advanced): Analyze price discontinuities to infer split ratios and create explicit splits.csv files. This provides more realistic simulation of execution prices at historical moments.

**Split detection from price patterns:**

```python
def detect_stock_splits(df, threshold_ratio=0.45):
    """Detect potential splits from price discontinuities"""
    splits = []
    
    df['price_ratio'] = df['close'] / df['close'].shift(1)
    
    # Common split patterns: 2:1 (2.0), 1:2 (0.5), 3:1 (3.0), 3:2 (1.5)
    split_patterns = {
        2.0: (1.8, 2.2),   # 2-for-1 split
        0.5: (0.45, 0.55),  # 1-for-2 reverse split
        3.0: (2.8, 3.2),   # 3-for-1 split
        1.5: (1.4, 1.6),   # 3-for-2 split
    }
    
    for idx, row in df.iterrows():
        ratio = row['price_ratio']
        for split_ratio, (lower, upper) in split_patterns.items():
            if pd.notna(ratio) and lower <= ratio <= upper:
                splits.append({
                    'date': row['date'],
                    'ratio': split_ratio,
                    'effective_date': row['date']
                })
                break
    
    return pd.DataFrame(splits)
```

**For production implementations:** Consider querying external sources for corporate action data. Vietnamese exchanges (HOSE/HNX) publish corporate action announcements on their websites. Third-party providers like Vietstock (finance.vietstock.vn) and StoxPlus offer corporate action calendars. VSD (Vietnam Securities Depository) at vsd.vn maintains official records. Academic research confirms 718 splits occurred in 2007-2011 alone, indicating high frequency that may warrant external data integration.

**Creating empty metadata files:** For quick prototypes accepting adjusted prices:

```python
def create_empty_corporate_action_files(output_dir):
    """Create empty splits and dividends files for Zipline"""
    import os
    os.makedirs(output_dir, exist_ok=True)
    
    # Empty splits file
    splits_df = pd.DataFrame(columns=['sid', 'ratio', 'effective_date'])
    splits_df.to_csv(os.path.join(output_dir, 'splits.csv'), index=False)
    
    # Empty dividends file  
    dividends_df = pd.DataFrame(columns=[
        'sid', 'amount', 'ex_date', 'record_date', 'declared_date', 'pay_date'
    ])
    dividends_df.to_csv(os.path.join(output_dir, 'dividends.csv'), index=False)
```

## Production architecture: Design patterns and best practices

**Module structure for optimized production:**

```
vnstock_zipline_pipeline/
├── config/
│   ├── settings.py          # Configuration management
│   ├── symbols.yaml         # Symbol lists by exchange
│   └── calendars.py         # Vietnamese trading calendar
├── extractors/
│   ├── vnstock_client.py    # vnstock3 API wrapper
│   └── rate_limiter.py      # Request throttling
├── transformers/
│   ├── csv_formatter.py     # vnstock -> Zipline conversion
│   ├── validators.py        # Vietnamese market validation
│   └── corporate_actions.py # Split/dividend detection
├── loaders/
│   └── batch_processor.py   # Parallel download manager
├── zipline_bundle/
│   ├── extension.py         # Bundle registration
│   └── calendar.py          # Custom Vietnam calendar
├── tests/
│   ├── test_transformation.py
│   └── test_validation.py
├── requirements.txt
└── pipeline.py              # Main execution script
```

**Configuration management pattern:**

```python
# config/settings.py
import os
from pathlib import Path

class Settings:
    # API Configuration
    VNSTOCK_SOURCE = 'VCI'  # or 'TCBS'
    RATE_LIMIT_CALLS = 30
    RATE_LIMIT_PERIOD = 60  # seconds
    
    # Data Configuration
    START_DATE = '2020-01-01'
    END_DATE = '2024-12-31'
    OUTPUT_DIR = Path('./zipline_data/daily')
    
    # Exchange Configuration
    HOSE_PRICE_LIMIT = 0.07
    HNX_PRICE_LIMIT = 0.10
    UPCOM_PRICE_LIMIT = 0.15
    
    # Logging
    LOG_LEVEL = os.environ.get('LOG_LEVEL', 'INFO')

settings = Settings()
```

**Vietnamese trading calendar implementation:**

```python
# zipline_bundle/calendar.py
from datetime import time
import pandas as pd
from trading_calendars import TradingCalendar
from pytz import timezone

class VietnamExchangeCalendar(TradingCalendar):
    """Custom trading calendar for Vietnamese stock market"""
    
    @property
    def name(self):
        return "XSTC"  # HOSE MIC code
    
    @property
    def tz(self):
        return timezone("Asia/Ho_Chi_Minh")  # GMT+7
    
    @property
    def open_time(self):
        return time(9, 15)  # 9:15 AM after opening auction
    
    @property
    def close_time(self):
        return time(14, 45)  # 2:45 PM closing auction
    
    @property
    def regular_holidays(self):
        return [
            # Fixed holidays
            Holiday("New Year's Day", month=1, day=1),
            Holiday("Reunification Day", month=4, day=30),
            Holiday("International Workers' Day", month=5, day=1),
            Holiday("National Day", month=9, day=2),
        ]
    
    @property
    def special_closes(self):
        # Vietnamese market doesn't typically have early closes
        return []
    
    @property
    def adhoc_holidays(self):
        # Tet (Lunar New Year) shifts annually - must be updated yearly
        return [
            pd.Timestamp('2024-02-08'),  # Tet 2024
            pd.Timestamp('2024-02-09'),
            pd.Timestamp('2024-02-10'),
            pd.Timestamp('2024-02-11'),
            pd.Timestamp('2024-02-12'),
            pd.Timestamp('2024-02-13'),
            pd.Timestamp('2024-02-14'),
            pd.Timestamp('2025-01-27'),  # Tet 2025
            pd.Timestamp('2025-01-28'),
            pd.Timestamp('2025-01-29'),
            pd.Timestamp('2025-01-30'),
            pd.Timestamp('2025-01-31'),
            pd.Timestamp('2025-02-01'),
            pd.Timestamp('2025-02-02'),
        ]
```

**Parallel download optimization:** For processing 100+ Vietnamese stocks, implement multiprocessing:

```python
from multiprocessing import Pool, cpu_count
from functools import partial

def download_single_symbol(symbol, start_date, end_date, output_dir):
    """Worker function for parallel downloads"""
    try:
        df = rate_limited_download(symbol, start_date, end_date)
        df = prepare_vnstock_for_zipline_from_df(df)
        
        validation = validate_vietnamese_stock_data(df, symbol)
        if validation['is_valid']:
            output_path = os.path.join(output_dir, f'{symbol}.csv')
            df.to_csv(output_path, index=False)
            return {'symbol': symbol, 'status': 'success', 'rows': len(df)}
        else:
            return {'symbol': symbol, 'status': 'validation_failed', 'issues': validation['issues']}
    except Exception as e:
        return {'symbol': symbol, 'status': 'error', 'error': str(e)}

def parallel_batch_download(symbols, start_date, end_date, output_dir, max_workers=4):
    """Download stocks in parallel using multiprocessing"""
    download_func = partial(download_single_symbol, 
                           start_date=start_date, 
                           end_date=end_date, 
                           output_dir=output_dir)
    
    with Pool(processes=min(max_workers, cpu_count())) as pool:
        results = pool.map(download_func, symbols)
    
    success = [r for r in results if r['status'] == 'success']
    failed = [r for r in results if r['status'] != 'success']
    
    return {'success': success, 'failed': failed}
```

## Production patterns and best practices

**Module structure for optimized production:**

```
vnstock_zipline_pipeline/
├── config/
│   ├── settings.py          # Configuration management
│   ├── symbols.yaml         # Symbol lists by exchange
│   └── calendars.py         # Vietnamese trading calendar
├── extractors/
│   ├── vnstock_client.py    # vnstock3 API wrapper
│   └── rate_limiter.py      # Request throttling
├── transformers/
│   ├── csv_formatter.py     # vnstock -> Zipline conversion
│   ├── validators.py        # Vietnamese market validation
│   └── corporate_actions.py # Split/dividend detection
├── loaders/
│   └── batch_processor.py   # Parallel download manager
├── zipline_bundle/
│   ├── extension.py         # Bundle registration
│   └── calendar.py          # Custom Vietnam calendar
├── tests/
│   ├── test_transformation.py
│   └── test_validation.py
├── requirements.txt
└── pipeline.py              # Main execution script
```

**Configuration management pattern:**

```python
# config/settings.py
import os
from pathlib import Path

class Settings:
    # API Configuration
    VNSTOCK_SOURCE = 'VCI'  # or 'TCBS'
    RATE_LIMIT_CALLS = 30
    RATE_LIMIT_PERIOD = 60  # seconds
    
    # Data Configuration
    START_DATE = '2020-01-01'
    END_DATE = '2024-12-31'
    OUTPUT_DIR = Path('./zipline_data/daily')
    
    # Exchange Configuration
    HOSE_PRICE_LIMIT = 0.07
    HNX_PRICE_LIMIT = 0.10
    UPCOM_PRICE_LIMIT = 0.15
    
    # Environment-specific
    IS_PRODUCTION = 'RENDER' in os.environ
    
    # Logging
    LOG_LEVEL = os.environ.get('LOG_LEVEL', 'INFO')
    LOG_FORMAT = 'json' if IS_PRODUCTION else 'console'

settings = Settings()
```

**Vietnamese trading calendar implementation:**

```python
# zipline_bundle/calendar.py
from datetime import time
import pandas as pd
from trading_calendars import TradingCalendar
from pytz import timezone

class VietnamExchangeCalendar(TradingCalendar):
    """Custom trading calendar for Vietnamese stock market"""
    
    @property
    def name(self):
        return "XSTC"  # HOSE MIC code
    
    @property
    def tz(self):
        return timezone("Asia/Ho_Chi_Minh")  # GMT+7
    
    @property
    def open_time(self):
        return time(9, 15)  # 9:15 AM after opening auction
    
    @property
    def close_time(self):
        return time(14, 45)  # 2:45 PM closing auction
    
    @property
    def regular_holidays(self):
        return [
            # Fixed holidays
            Holiday("New Year's Day", month=1, day=1),
            Holiday("Reunification Day", month=4, day=30),
            Holiday("International Workers' Day", month=5, day=1),
            Holiday("National Day", month=9, day=2),
        ]
    
    @property
    def special_closes(self):
        # Vietnamese market doesn't typically have early closes
        return []
    
    @property
    def adhoc_holidays(self):
        # Tet (Lunar New Year) shifts annually - must be updated yearly
        return [
            pd.Timestamp('2024-02-08'),  # Tet 2024
            pd.Timestamp('2024-02-09'),
            pd.Timestamp('2024-02-10'),
            pd.Timestamp('2024-02-11'),
            pd.Timestamp('2024-02-12'),
            pd.Timestamp('2024-02-13'),
            pd.Timestamp('2024-02-14'),
            pd.Timestamp('2025-01-27'),  # Tet 2025
            pd.Timestamp('2025-01-28'),
            pd.Timestamp('2025-01-29'),
            pd.Timestamp('2025-01-30'),
            pd.Timestamp('2025-01-31'),
            pd.Timestamp('2025-02-01'),
            pd.Timestamp('2025-02-02'),
        ]
```

**Parallel download optimization:** For processing 100+ Vietnamese stocks, implement multiprocessing:

```python
from multiprocessing import Pool, cpu_count
from functools import partial

def download_single_symbol(symbol, start_date, end_date, output_dir):
    """Worker function for parallel downloads"""
    try:
        df = rate_limited_download(symbol, start_date, end_date)
        df = prepare_vnstock_for_zipline_from_df(df)
        
        validation = validate_vietnamese_stock_data(df, symbol)
        if validation['is_valid']:
            output_path = os.path.join(output_dir, f'{symbol}.csv')
            df.to_csv(output_path, index=False)
            return {'symbol': symbol, 'status': 'success', 'rows': len(df)}
        else:
            return {'symbol': symbol, 'status': 'validation_failed', 'issues': validation['issues']}
    except Exception as e:
        return {'symbol': symbol, 'status': 'error', 'error': str(e)}

def parallel_batch_download(symbols, start_date, end_date, output_dir, max_workers=4):
    """Download stocks in parallel using multiprocessing"""
    download_func = partial(download_single_symbol, 
                           start_date=start_date, 
                           end_date=end_date, 
                           output_dir=output_dir)
    
    with Pool(processes=min(max_workers, cpu_count())) as pool:
        results = pool.map(download_func, symbols)
    
    success = [r for r in results if r['status'] == 'success']
    failed = [r for r in results if r['status'] != 'success']
    
    return {'success': success, 'failed': failed}
```

## Complete implementation: End-to-end working example

**Main pipeline script (pipeline.py):**

```python
#!/usr/bin/env python3
"""
Simplified vnstock3 to Zipline Reloaded pipeline
Handles Vietnamese stock market data without caching
"""

import os
import sys
import logging
from pathlib import Path
from datetime import datetime
import pandas as pd
from vnstock import Listing

from config.settings import settings
from extractors.vnstock_client import VNStockClient
from transformers.csv_formatter import prepare_vnstock_for_zipline_from_df
from transformers.validators import validate_vietnamese_stock_data

# Configure logging
logging.basicConfig(
    level=settings.LOG_LEVEL,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
logger = logging.getLogger(__name__)


def get_symbol_list():
    """Get list of Vietnamese stocks to process"""
    listing = Listing()
    all_symbols = listing.all_symbols()
    
    # Filter for liquid stocks on main exchanges
    symbols = all_symbols[
        (all_symbols['exchange'].isin(['HOSE', 'HNX'])) &
        (all_symbols['symbol'].str.len() == 3)  # Standard 3-letter symbols
    ]['symbol'].tolist()
    
    logger.info(f"Found {len(symbols)} symbols to process")
    return symbols


def process_symbol(symbol, client, output_dir):
    """Process single symbol without caching"""
    try:
        # Download from vnstock3
        logger.info(f"Downloading {symbol}")
        df = client.download(symbol, settings.START_DATE, settings.END_DATE)
        
        if df is None or len(df) == 0:
            logger.warning(f"No data returned for {symbol}")
            return {'symbol': symbol, 'status': 'no_data'}
        
        # Transform to Zipline format
        df = prepare_vnstock_for_zipline_from_df(df)
        
        # Validate
        validation = validate_vietnamese_stock_data(df, symbol)
        
        if not validation['is_valid']:
            logger.warning(f"Validation failed for {symbol}: {validation['issues']}")
            return {'symbol': symbol, 'status': 'validation_failed', 'issues': validation['issues']}
        
        # Save to CSV
        output_path = output_dir / f'{symbol}.csv'
        df.to_csv(output_path, index=False)
        
        logger.info(f"Successfully processed {symbol}: {len(df)} rows")
        return {'symbol': symbol, 'status': 'success', 'rows': len(df)}
        
    except Exception as e:
        logger.error(f"Error processing {symbol}: {str(e)}", exc_info=True)
        return {'symbol': symbol, 'status': 'error', 'error': str(e)}


def create_empty_metadata_files(output_dir):
    """Create empty splits and dividends files"""
    # Splits file
    splits_df = pd.DataFrame(columns=['sid', 'ratio', 'effective_date'])
    splits_df.to_csv(output_dir / 'splits.csv', index=False)
    
    # Dividends file
    dividends_df = pd.DataFrame(columns=[
        'sid', 'amount', 'ex_date', 'record_date', 'declared_date', 'pay_date'
    ])
    dividends_df.to_csv(output_dir / 'dividends.csv', index=False)
    
    logger.info("Created empty metadata files")


def main():
    """Main pipeline execution"""
    start_time = datetime.now()
    logger.info("=== VNStock to Zipline Pipeline Started ===")
    logger.info(f"Date range: {settings.START_DATE} to {settings.END_DATE}")
    
    # Setup
    settings.OUTPUT_DIR.mkdir(parents=True, exist_ok=True)
    
    client = VNStockClient(source=settings.VNSTOCK_SOURCE)
    
    # Get symbols
    symbols = get_symbol_list()
    
    # Process symbols
    results = {'success': [], 'failed': []}
    
    for symbol in symbols:
        result = process_symbol(symbol, client, settings.OUTPUT_DIR)
        
        if result['status'] == 'success':
            results['success'].append(result)
        else:
            results['failed'].append(result)
    
    # Create metadata files
    create_empty_metadata_files(settings.OUTPUT_DIR)
    
    # Summary
    duration = (datetime.now() - start_time).total_seconds()
    logger.info("=== Pipeline Completed ===")
    logger.info(f"Duration: {duration:.2f} seconds")
    logger.info(f"Successful: {len(results['success'])}")
    logger.info(f"Failed: {len(results['failed'])}")
    
    if results['failed']:
        logger.warning(f"Failed symbols: {[r['symbol'] for r in results['failed'][:20]]}")
    
    # Exit with error code if too many failures
    failure_rate = len(results['failed']) / len(symbols)
    if failure_rate > 0.1:  # More than 10% failure
        logger.error(f"High failure rate: {failure_rate:.1%}")
        sys.exit(1)
    
    logger.info(f"\nData saved to: {settings.OUTPUT_DIR}")
    logger.info("\nNext steps:")
    logger.info("1. Update ~/.zipline/extension.py with bundle configuration")
    logger.info("2. Run: zipline ingest -b vnstock-bundle")
    logger.info("3. Verify: zipline bundles")


if __name__ == '__main__':
    main()
```

**Testing the pipeline:**

```python
# test_pipeline.py
import pytest
import pandas as pd
from pipeline import prepare_vnstock_for_zipline_from_df, validate_vietnamese_stock_data

def test_transformation():
    """Test vnstock to Zipline transformation"""
    # Create sample vnstock data
    sample_data = pd.DataFrame({
        'time': pd.date_range('2024-01-01', periods=5),
        'open': [100.0, 101.0, 102.0, 103.0, 104.0],
        'high': [105.0, 106.0, 107.0, 108.0, 109.0],
        'low': [95.0, 96.0, 97.0, 98.0, 99.0],
        'close': [102.0, 103.0, 104.0, 105.0, 106.0],
        'volume': [1000000, 1100000, 1200000, 1300000, 1400000]
    })
    
    # Transform
    result = prepare_vnstock_for_zipline_from_df(sample_data)
    
    # Assertions
    assert list(result.columns) == ['date', 'open', 'high', 'low', 'close', 'volume', 'dividend', 'split']
    assert len(result) == 5
    assert (result['dividend'] == 0.0).all()
    assert (result['split'] == 1.0).all()
    assert result['date'].dtype == 'object'  # String format

def test_validation():
    """Test Vietnamese market validation"""
    df = pd.DataFrame({
        'date': ['2024-01-01', '2024-01-02'],
        'open': [100.0, 101.0],
        'high': [105.0, 106.0],
        'low': [95.0, 96.0],
        'close': [102.0, 103.0],
        'volume': [1000000, 1100000],
        'dividend': [0.0, 0.0],
        'split': [1.0, 1.0]
    })
    
    validation = validate_vietnamese_stock_data(df, 'TEST')
    assert validation['is_valid'] == True

def test_price_limit_violation():
    """Test detection of price limit violations"""
    df = pd.DataFrame({
        'date': ['2024-01-01', '2024-01-02'],
        'open': [100.0, 120.0],  # 20% jump exceeds ±7% limit
        'high': [105.0, 125.0],
        'low': [95.0, 115.0],
        'close': [102.0, 120.0],
        'volume': [1000000, 1100000],
        'dividend': [0.0, 0.0],
        'split': [1.0, 1.0]
    })
    
    validation = validate_vietnamese_stock_data(df, 'TEST', exchange='HOSE')
    assert validation['is_valid'] == False
    assert any('Price limit' in issue for issue in validation['issues'])

# Run tests
if __name__ == '__main__':
    pytest.main([__file__, '-v'])
```

**Zipline bundle registration (~/.zipline/extension.py):**

```python
import pandas as pd
from zipline.data.bundles import register
from zipline.data.bundles.csvdir import csvdir_equities

# Vietnamese market data configuration
start_session = pd.Timestamp('2020-1-1', tz='utc')
end_session = pd.Timestamp('2024-12-31', tz='utc')

# Register bundle
register(
    'vnstock-bundle',
    csvdir_equities(
        ['daily'],
        '/path/to/zipline_data',  # Update to your actual path
    ),
    calendar_name='XHKG',  # Hong Kong calendar closest to Vietnam
    start_session=start_session,
    end_session=end_session
)

# Alternative: Use custom Vietnamese calendar (if implemented)
# from zipline_bundle.calendar import VietnamExchangeCalendar
# register('vnstock-bundle', ..., calendar_name='XSTC', ...)
```

**Ingest and verify:**

```bash
# Ingest the bundle
zipline ingest -b vnstock-bundle

# Verify ingestion
zipline bundles

# Expected output:
# vnstock-bundle 2025-10-04 10:30:15.123456

# Run a simple backtest to verify
zipline run -f test_strategy.py \
    --start 2024-01-01 \
    --end 2024-03-31 \
    --bundle vnstock-bundle \
    --capital-base 10000
```

**Common issues and solutions:**

**Timezone errors:** If you see "Parameter start received with timezone defined as 'UTC'", ensure bundle registration uses `pd.Timestamp('2020-1-1', tz='utc')` not `datetime(..., tzinfo=pytz.UTC)`.

**Column name errors:** Zipline requires lowercase column names. If you see "KeyError: 'Open'", check CSV files have `open` not `Open`.

**Zero volume issues:** Zipline won't execute orders on zero-volume bars. Ensure all volume values are positive. Vietnamese market data from vnstock3 should have real volume, but validate this.

**Date alignment errors:** If "NoDataOnDate" occurs, verify start_session aligns with first date in CSV files and dates match trading calendar. Vietnamese markets close for Tet—ensure your calendar handles this.

**API rate limiting:** If downloads fail with connection errors, reduce CALLS_PER_MINUTE from 30 to 20 or add longer delays. VCI/TCBS sources have undocumented rate limits.

**Memory issues with large batches:** When processing 500+ symbols, use multiprocessing with max_workers=4 and implement chunked processing. Each symbol's 5-year daily data is ~5KB CSV, so memory shouldn't be limiting factor unless processing intraday data.

**Vietnamese price limit violations:** If validation reports excessive price limit violations, check if reference prices are calculated correctly. Remember: ±7% HOSE, ±10% HNX, and newly listed stocks get ±20-30% bands.
