The methods to fetch historical prices in the provided context, along with their corresponding data types (dtypes) and dataframe structures, are summarized as follows:

### Vietnam Stock:

#### Historical Prices:
- **Method**:
  ```python
  from vnstock import Quote
  quote = Quote(symbol='VCI', source='VCI')
  quote.history(start='2020-01-01', end='2024-05-25')
  ```
- **Dtypes**:
  ```shell
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 1095 entries, 0 to 1094
  Data columns (total 6 columns):
   #   Column   Non-Null Count  Dtype
  ---  ------   --------------  -----
   0   time     1095 non-null   datetime64[ns]
   1   open     1095 non-null   float64
   2   high     1095 non-null   float64
   3   low      1095 non-null   float64
   4   close    1095 non-null   float64
   5   volume   1095 non-null   int64
  memory usage: 51.5 KB
  ```

### Forex (FX):

- **Method**:
  ```python
  fx.quote.history(start='2024-02-28', end='2024-05-25')
  ```
- **Dtypes**:
  ```shell
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 63 entries, 0 to 62
  Data columns (total 5 columns):
   #   Column   Non-Null Count  Dtype
  ---  ------   --------------  -----
   0   time     63 non-null     datetime64[ns]
   1   open     63 non-null     float64
   2   high     63 non-null     float64
   3   low      63 non-null     float64
   4   close    63 non-null     float64
  memory usage: 2.6 KB
  ```

### Crypto:

- **Method**:
  ```python
  crypto.quote.history(start='2023-01-01', end='2024-12-31')
  ```
- **Dtypes**:
  ```shell
  <class 'pandas.core.frame.DataFrame'>
  Index: 17 entries, 151 to 167
  Data columns (total 6 columns):
   #   Column     Non-Null Count  Dtype
  ---  ------     --------------  -----
   0   time       17 non-null     datetime64[ns]
   1   open       17 non-null     float64
   2   high       17 non-null     float64
   3   low        17 non-null     float64
   4   close      17 non-null     float64
   5   volume     17 non-null     int64
  memory usage: 952.0 bytes
  ```

### International Indices:

- **Method**:
  ```python
  index.quote.history(start='2023-01-01', end='2024-12-31')
  ```
- **Dtypes**:
  ```shell
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 351 entries, 0 to 350
  Data columns (total 6 columns):
   #   Column   Non-Null Count  Dtype
  ---  ------   --------------  -----
   0   time     351 non-null    datetime64[ns]
   1   open     351 non-null    float64
   2   high     351 non-null    float64
   3   low      351 non-null    float64
   4   close    351 non-null    float64
   5   volume   351 non-null    int64
  memory usage: 16.6 KB
  ```

These methods enable retrieval of historical prices, formatted in a DataFrame structure with columns specified by datatypes for time, open, high, low, close, and volume.
