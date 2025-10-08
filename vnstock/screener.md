To screen stocks using the Vnstock API, you can use the `Screener` class in Python. Below are the methods and sample outputs for screening stocks, along with data information:

### Method to Screen Stocks

#### Python Code
```python
from vnstock import Screener
screener_df = Screener().stock(params={"exchangeName": "HOSE,HNX,UPCOM"}, limit=1700)
```

#### Parameters
- `params`: Filtering parameters, by default, it selects all 3 exchanges, so you don't need to input anything extra.
- `limit`: The maximum number of results returned.

### Sample Output

#### Command
```shell
>>> screener_df.head()
```

#### Sample Data
```
  ticker exchange                 industry  market_cap  roe  ...  pct_away_from_hist_peak  pct_1y_from_bottom  pct_off_hist_bottom        price_vs_sma100  heating_up
0    A32    UPCOM  Hàng cá nhân & Gia dụng         NaN  NaN  ...                      NaN                 NaN                  NaN                   None        None
1    AAA      HSX                 Hóa chất      3249.0  6.8  ...                    -62.7                 5.2                266.5  Giá nằm dưới SMA(100)        None
2    AAM      HSX     Thực phẩm và đồ uống        73.0 -3.2  ...                    -58.4                16.7                 38.0  Giá nằm trên SMA(100)        None
3    AAS    UPCOM        Dịch vụ tài chính      1998.0  3.0  ...                    -56.7                61.1                174.8  Giá nằm trên SMA(100)        None
4    AAT      HSX  Hàng cá nhân & Gia dụng       232.0 -0.9  ...                    -82.5                 7.6                  2.2  Giá nằm dưới SMA(100)        None

[5 rows x 83 columns]
```

### Data Information

#### Shell Command to View Data Information
```shell
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
```

This information provides details on the available columns, their data types, and non-null counts in the stock screener dataset.
