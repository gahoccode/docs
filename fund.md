
### 1. List All Funds

**Python Implementation:**
```python
from vnstock import Fund

fund = Fund()
funds_list = fund.listing()
```

**Expected `data.info()` Output:**
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 49 entries, 0 to 48
Data columns (total 21 columns):
 #   Column                     Non-Null Count  Dtype  
---  ------                     --------------  -----  
 0   short_name                 49 non-null     object 
 1   name                       49 non-null     object 
 2   fund_type                  49 non-null     object 
 3   fund_owner_name            49 non-null     object 
 4   management_fee             49 non-null     float64
 5   inception_date             44 non-null     object 
 6   nav                        49 non-null     float64
 7   nav_change_previous        49 non-null     float64
 8   nav_change_last_year       45 non-null     float64
 9   nav_change_inception       49 non-null     float64
 10  nav_change_1m              46 non-null     float64
 11  nav_change_3m              46 non-null     float64
 12  nav_change_6m              43 non-null     float64
 13  nav_change_12m             42 non-null     float64
 14  nav_change_24m             34 non-null     float64
 15  nav_change_36m             28 non-null     float64
 16  nav_change_36m_annualized  28 non-null     float64
 17  nav_update_at              49 non-null     object 
 18  fund_id_fmarket            49 non-null     int64  
 19  fund_code                  49 non-null     object 
 20  vsd_fee_id                 49 non-null     object 
dtypes: float64(12), int64(1), object(8)
```

### 2. Search for Funds by Symbol

**Python Implementation:**
```python
from vnstock import Fund

fund = Fund()
funds_search = fund.filter('DC')
```

**Expected `data.info()` Output:**
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 7 entries, 0 to 6
Data columns (total 2 columns):
 #   Column     Non-Null Count  Dtype 
---  ------     --------------  ----- 
 0   id         7 non-null      int64 
 1   shortName  7 non-null      object
dtypes: int64(1), object(1)
```

### 3. Get NAV Growth Report

**Python Implementation:**
```python
from vnstock import Fund

fund = Fund()
nav_report = fund.details.nav_report('SSISCA')
```

**Expected `data.info()` Output:**
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1540 entries, 0 to 1539
Data columns (total 3 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   date          1540 non-null   object 
 1   nav_per_unit  1540 non-null   float64
 2   short_name    1540 non-null   object 
dtypes: float64(1), object(2)
```

### 4. Top Holdings

**Python Implementation:**
```python
from vnstock import Fund

fund = Fund()
top_holdings = fund.details.top_holding('SSISCA')
```

**Expected `data.info()` Output:**
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 10 entries, 0 to 9
Data columns (total 7 columns):
 #   Column             Non-Null Count  Dtype  
---  ------             --------------  -----  
 0   stock_code         10 non-null     object 
 1   industry           10 non-null     object 
 2   net_asset_percent  10 non-null     float64
 3   type_asset         10 non-null     object 
 4   update_at          10 non-null     object 
 5   fundId             10 non-null     int64  
 6   short_name         10 non-null     object 
dtypes: float64(1), int64(1), object(5)
```

### 5. Industry Allocation

**Python Implementation:**
```python
from vnstock import Fund

fund = Fund()
industry_allocation = fund.details.industry_holding('SSISCA')
```

**Expected `data.info()` Output:**
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 15 entries, 0 to 14
Data columns (total 3 columns):
 #   Column             Non-Null Count  Dtype  
---  ------             --------------  -----  
 0   industry           15 non-null     object 
 1   net_asset_percent  15 non-null     float64
 2   short_name         15 non-null     object 
dtypes: float64(1), object(2)
```

### 6. Asset Allocation

**Python Implementation:**
```python
from vnstock import Fund

fund = Fund()
asset_allocation = fund.details.asset_holding('SSISCA')
```

**Expected `data.info()` Output:**
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2 entries, 0 to 1
Data columns (total 3 columns):
 #   Column         Non-Null Count  Dtype  
---  ------         --------------  -----  
 0   asset_percent  2 non-null      float64
 1   asset_type     2 non-null      object 
 2   short_name     2 non-null      object 
dtypes: float64(1), object(2)
```

These methods allow you to get detailed information about the funds from the Vnstock API using Python.
