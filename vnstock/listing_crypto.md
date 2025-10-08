To fetch listing information on FX, Crypto, and world index using the Vnstock API, you can use the following Python snippets and corresponding methods. These snippets highlight how to extract international stock symbols and include details on data structures, shapes, sizes, and data types as shown by `data.info()`.

### Tìm mã chứng khoán quốc tế
To search for international stock symbols (`symbol_id`), you can use the following method:

#### Python Code:
```python
from vnstock.explorer.msn.listing import Listing
Listing().search_symbol_id('USD')
```

#### Sample Data Output:
```shell
>>> from vnstock.explorer.msn.listing import Listing
>>> Listing().search_symbol_id('USD')

                symbol symbol_id exchange_name  exchange_code_mic  ...                                           eng_name description                                         local_name locale
0                  USD    a2521h     NYSE ARCA               ARCX  ...                     ProShares Ultra Semiconductors                                 ProShares Ultra Semiconductors  en-us
1                  USD    aaa5bh     Australia               XASX  ...                           BetaShares US Dollar ETF                                       BetaShares US Dollar ETF  en-au
2             SPRPUS8P    buam8m                  INDX_DEFAULT-SP  ...  S&P Risk Parity Index (USD-Only Constituents) ...              S&P Risk Parity Index (USD-Only Constituents) ...  en-us
3  SPCRR2B10BCPKUSD.TR    bp2ic7                    INDX_24HRS-SP  ...                  S&P Pak USD2 Bil and USD10 Bil GR                              S&P Pak USD2 Bil and USD10 Bil GR  en-us
4              RGAHU_T    bxyrec                INDX_DEFAULT-FTSE  ...  FTSE EPRA Nareit Developed ex Australia hedged...              FTSE EPRA Nareit Developed ex Australia hedged...  en-gb
5     SPCRR2B10BCCOUSD    bkn7u2                    INDX_24HRS-SP  ...                     S&P Col USD2 Bil and USD10 Bil                                 S&P Col USD2 Bil and USD10 Bil  en-us
6             FGCICUHN    bxwl5r                INDX_DEFAULT-FTSE  ...  FTSE Global Core Infrastructure 50/50 100% Hed...              FTSE Global Core Infrastructure 50/50 100% Hed...  en-gb
7             GPPS008U    blhayc                  INDX_24HRS-FTSE  ...  FTSE Japan 100% Hedged to USD Net Tax (US RIC)...              FTSE Japan 100% Hedged to USD Net Tax (US RIC)...  en-gb
8        SPCRU2BRLAUSD    c4yww7                  INDX_DEFAULT-SP  ...         S&P Latin America Under USD2 Billion (USD)                     S&P Latin America Under USD2 Billion (USD)  en-us
9              RLHAU_T    bxyvh7                INDX_DEFAULT-FTSE  ...  FTSE EPRA Nareit Australia hedged in USD Net R...              FTSE EPRA Nareit Australia hedged in USD Net R...  en-gb

[10 rows x 10 columns]
```

#### Data Structure Information:
```shell
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 10 entries, 0 to 9
Data columns (total 10 columns):
 #   Column             Non-Null Count  Dtype 
---  ------             --------------  ----- 
 0   symbol             10 non-null     object
 1   symbol_id          10 non-null     object
 2   exchange_name      10 non-null     object
 3   exchange_code_mic  10 non-null     object
 4   short_name         10 non-null     object
 5   friendly_name      10 non-null     object
 6   eng_name           10 non-null     object
 7   description        10 non-null     object
 8   local_name         10 non-null     object
 9   locale             10 non-null     object
dtypes: object(10)
memory usage: 928.0+ bytes
```

The `search_symbol_id` method allows you to identify international stock symbols, making use of the varied columns in the result to understand the context, exchange details, and localization of each symbol. The sample data and its structure can guide your exploration of FX, Crypto, and world index listings.
