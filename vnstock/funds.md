Certainly! Below are the methods provided by Vnstock to retrieve information on funds, including sample outputs and clearly defined data types for each column.

### 1. Liệt kê quỹ (List Funds)
**Method:**
```python
fund.listing()
```
**Parameters:**
- `fund_type` (str, optional): Group classification of funds, default is an empty string to list all funds. Possible values:
  * `BALANCED`: Balanced funds
  * `BOND`: Bond funds
  * `STOCK`: Stock funds
  * `""`: Empty string (default) - All funds

**Sample Output:**
```shell
>>> fund.listing().head()
Total number of funds currently listed on Fmarket:  49
  short_name                                               name     fund_type                                    fund_owner_name  ...  nav_update_at fund_id_fmarket  fund_code   vsd_fee_id
0     SSISCA         QUỸ ĐẦU TƯ LỢI THẾ CẠNH TRANH BỀN VỮNG SSI  Quỹ cổ phiếu                       CÔNG TY TNHH QUẢN LÝ QUỸ SSI  ...     2024-07-09              11     SSISCA   SSISCAN001
1      VESAF  QUỸ ĐẦU TƯ CỔ PHIẾU TIẾP CẬN THỊ TRƯỜNG VINACA...  Quỹ cổ phiếu            CÔNG TY CỔ PHẦN QUẢN LÝ QUỸ VINACAPITAL  ...     2024-07-09              23      VESAF    VESAFN002
2       BVPF            QUỸ ĐẦU TƯ CỔ PHIẾU TRIỂN VỌNG BẢO VIỆT  Quỹ cổ phiếu                  CÔNG TY TNHH QUẢN LÝ QUỸ BẢO VIỆT  ...     2024-07-09              14       BVPF     BVPFN001
3       VEOF         QUỸ ĐẦU TƯ CỔ PHIẾU HƯNG THỊNH VINACAPITAL  Quỹ cổ phiếu            CÔNG TY CỔ PHẦN QUẢN LÝ QUỸ VINACAPITAL  ...     2024-07-09              20       VEOF     VEOFN003
4   VCBF-TBF                QUỸ ĐẦU TƯ CÂN BẰNG CHIẾN LƯỢC VCBF  Quỹ cân bằng  CÔNG TY LIÊN DOANH QUẢN LÝ QUỸ ĐẦU TƯ CHỨNG KH...  ...     2024-07-09              31    VCBFTBF  VCBFTBFN001
```
**Data Types:**
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

### 2. Tìm kiếm quỹ (Filter Fund)
**Method:**
```python
fund.filter('DC')
```
**Parameters:**
- `symbol` (str, required): Abbreviation of the fund to search. Enter a part of the name to list matching results.

**Sample Output:**
```shell
>>> fund.filter('DC')
   id shortName
0  40     VNDCF
1  67      DCIP
2  62    HDBOND
3  27      DCBF
4  25      DCDE
5  28      DCDS
6  29      DCAF
```
**Data Types:**
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 7 entries, 0 to 6
Data columns (total 2 columns):
 #   Column     Non-Null Count  Dtype 
---  ------     --------------  ----- 
 0   id         7 non-null      int64 
 1   shortName  7 non-null      object
dtypes: int64(1), object(1)
memory usage: 240.0+ bytes
```

### 3. Báo cáo tăng trưởng NAV (NAV Growth Report)
**Method:**
```python
fund.details.nav_report('SSISCA')
```
**Parameters:**
- `symbol` (str, required): Abbreviation of the fund to fetch. Enter a part of the name for matching results.

**Sample Output:**
```shell
>>> fund.details.nav_report('SSISCA')
Retrieving data for SSISCA
            date  nav_per_unit short_name
0     2017-01-04      14412.31     SSISCA
1     2017-01-11      14527.86     SSISCA
...
1539  2024-07-09      40055.88     SSISCA
```
**Data Types:**
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
memory usage: 36.2+ KB
```

### 4. Danh mục đầu tư lớn (Top Holdings)
**Method:**
```python
fund.details.top_holding('SSISCA')
```
**Parameters:**
- `symbol` (str, required): Abbreviation of the fund to fetch. Enter a part of the name for matching results.

**Sample Output:**
```shell
>>> fund.details.top_holding('SSISCA')

Retrieving data for SSISCA
  stock_code                industry  net_asset_percent type_asset   update_at  fundId short_name
0        FPT  Công nghệ và thông tin              17.10      STOCK  2024-07-05      11     SSISCA
1        MWG                  Bán lẻ               6.65      STOCK  2024-07-05      11     SSISCA
...
9        DHC        Sản xuất Phụ trợ               2.75      STOCK  2024-07-05      11     SSISCA
```
**Data Types:**
```shell
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
memory usage: 688.0+ bytes
```

### 5. Phân bổ theo ngành (Industry Allocation)
**Method:**
```python
fund.details.industry_holding('SSISCA')
```
**Parameters:**
- `symbol` (str, required): Abbreviation of the fund to fetch. Enter a part of the name for matching results.

**Sample Output:**
```shell
>>> fund.details.industry_holding('SSISCA')

Retrieving data for SSISCA
                      industry  net_asset_percent short_name
0                    Ngân hàng              20.46     SSISCA
...
14                 Chứng khoán               1.52     SSISCA
```
**Data Types:**
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
memory usage: 488.0+ bytes
```

### 6. Phân bổ theo tài sản (Asset Allocation)
**Method:**
```python
fund.details.asset_holding('SSISCA')
```
**Parameters:**
- `symbol` (str, required): Abbreviation of the fund to fetch. Enter a part of the name for matching results.

**Sample Output:**
```shell
>>> fund.details.asset_holding('SSISCA')
Retrieving data for SSISCA
   asset_percent                asset_type short_name
0          83.08                  Cổ phiếu     SSISCA
1          16.92  Tiền và tương đương tiền     SSISCA
```
**Data Types:**
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
memory usage: 176.0+ bytes
```
