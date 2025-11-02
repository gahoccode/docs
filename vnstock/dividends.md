# Dividends
## Method 1: Using Vnstock class

**Dividend data is available from TCBS source regardles of what method is used.**

```python
from vnstock import Vnstock
import warnings
warnings.filterwarnings("ignore")
company = Vnstock().stock(symbol=symbol, source='TCBS').company
```

**Parameters**
- `symbol`: Stock symbol.
- `source`: Data source.

**Returns**
- Returns a pandas DataFrame.

```python
RangeIndex: 15 entries, 0 to 14
Data columns (total 4 columns):
 #   Column                    Non-Null Count  Dtype  
---  ------                    --------------  -----  
 0   exercise_date             15 non-null     object 
 1   cash_year                 15 non-null     int64  
 2   cash_dividend_percentage  15 non-null     float64
 3   issue_method              15 non-null     object 
dtypes: float64(1), int64(1), object(2)
```

## Method 2: Direct Company class instantiation (TCBS source only)

### Create company object with stock symbol
### TCBS source provides access to dividend data
```python
from vnstock import Company

company = Company(symbol='ACB', source='TCBS')
```

### Get dividend history
```python
dividends_df = company.dividends()
print(dividends_df.head())
```

## Method 3: Using Company class
### Alternative TCBS approach (explicit import)
```python
from vnstock.explorer.tcbs import Company
```

### Initialize for a specific stock
```python
company = Company('ACB')
```

### Retrieve dividend data
```python
dividends_df = company.dividends()
```