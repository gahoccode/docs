The document provides several methods to fetch listing information using the `vnstock` library. Here are the extracted methods with their Python snippets, sample outputs, and data structure details:

1. **Liệt kê tất cả mã chứng khoán (List All Stock Symbols)**

   **Python Implementation:**
   ```python
   from vnstock import Listing
   listing = Listing(source='VCI')
   listing.all_symbols()
   ```

   **Sample Output:**
   ```shell
   >>> listing.all_symbols().head()

   ticker                                   organ_name
   0    A32                           Công ty Cổ phần 32
   1    AAA            Công ty Cổ phần Nhựa An Phát Xanh
   2    AAM              Công ty Cổ Phần Thủy Sản MeKong
   3    AAS      Công ty Cổ phần Chứng khoán SmartInvest
   4    AAT  Công ty Cổ phần Tập đoàn Tiên Sơn Thanh Hóa
   ```

   **Data Structure:**
   ```shell
   RangeIndex: 1598 entries, 0 to 1597
   Data columns (total 2 columns):
    #   Column      Non-Null Count  Dtype 
   ---  ------      --------------  ----- 
    0   ticker      1598 non-null   object
    1   organ_name  1598 non-null   object
   ```

2. **Liệt kê mã chứng khoán theo sàn (List Symbols by Exchange)**

   **Python Implementation:**
   ```python
   listing.symbols_by_exchange()
   ```

   **Sample Output:**
   ```shell
   >>> listing.symbols_by_exchange()

        symbol        id   type  ...     organ_name
   0       YTC   8425620  STOCK  ... (details omitted)
   ...
   2477    A32   8425330  STOCK  ... Công ty Cổ phần 32

   [2478 rows x 8 columns]
   ```

   **Data Structure:**
   ```shell
   RangeIndex: 2478 entries, 0 to 2477
   Data columns (total 8 columns):
    #   Column               Non-Null Count  Dtype 
   ---  ------               --------------  ----- 
    0   symbol               2478 non-null   object
    1   id                   2478 non-null   int64 
    2   type                 2478 non-null   object
    3   exchange             2478 non-null   object
    4   en_organ_name        2444 non-null   object
    5   en_organ_short_name  2444 non-null   object
    6   organ_short_name     2444 non-null   object
    7   organ_name           2444 non-null   object
   ```

3. **Liệt kê mã chứng khoán theo phân nhóm (List Symbols by Group)**

   **Python Implementation:**
   ```python
   listing.symbols_by_group('VN30')
   ```

   **Sample Output:**
   ```shell
  listing.symbols_by_group('VN30')
0     ACB
1     BCM
2     BID
3     BVH
4     CTG
5     FPT
6     GAS
7     GVR
8     HDB
9     HPG
10    MBB
11    MSN
12    MWG
13    PLX
14    POW
15    SAB
16    SHB
17    SSB
18    SSI
19    STB
20    TCB
21    TPB
22    VCB
23    VHM
24    VIB
25    VIC
26    VJC
27    VNM
28    VPB
29    VRE
Name: symbol, dtype: object
   ```

   **Data Structure:**
   ```shell
   <class 'pandas.core.series.Series'>
   RangeIndex: 30 entries, 0 to 29
   Series name: symbol
   Non-Null Count  Dtype 
   --------------  ----- 
   30 non-null     object
   dtypes: object(1)
   memory usage: 368.0+ bytes
   ```

4. **Liệt kê mã chứng khoán theo ngành icb (List Symbols by Industry ICB)**

   **Python Implementation:**
   ```python
   listing.symbols_by_industries()
   ```

   **Sample Output:**
   ```shell
   >>> listing.symbols_by_industries()
        symbol                                     organ_name                               icb_name3  ... icb_code4
   0       HIO               Công ty Cổ Phần Helio Energy               Sản xuất & Phân phối Điện  ... 7535
   ...
   1591    VRE              Công ty Cổ phần Vincom Retail                                   Bất động sản  ... 8633
   ```

   **Data Structure:**
   ```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1592 entries, 0 to 1591
Data columns (total 14 columns):
 #   Column         Non-Null Count  Dtype 
---  ------         --------------  ----- 
 0   symbol         1592 non-null   object
 1   organ_name     1592 non-null   object
 2   en_organ_name  1592 non-null   object
 3   icb_name3      1592 non-null   object
 4   en_icb_name3   1592 non-null   object
 5   icb_name2      1592 non-null   object
 6   en_icb_name2   1592 non-null   object
 7   icb_name4      1592 non-null   object
 8   en_icb_name4   1592 non-null   object
 9   com_type_code  1592 non-null   object
 10  icb_code1      1592 non-null   object
 11  icb_code2      1592 non-null   object
 12  icb_code3      1592 non-null   object
 13  icb_code4      1592 non-null   object
dtypes: object(14)
memory usage: 174.2+ KB
   ```

