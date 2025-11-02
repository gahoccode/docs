To fetch financial statements data using the Vnstock API, you can use the following methods. Each method retrieves specific types of financial data and returns them in structured data formats:

### 1. Báo cáo kết quả kinh doanh (Income Statement)
**Method**
```python
finance.income_statement(period='year', lang='en')
```

**Parameters**
- `period`: 'year' for annual reports, 'quarter' for quarterly reports.
- `lang`: 'vi' for Vietnamese, 'en' for English.

**Data Types and Structure**
- Returns a pandas DataFrame.
- Data includes columns like 'Chứng khoán kinh doanh', 'Lợi nhuận thuần', 'Lãi cơ bản trên cổ phiếu', etc.
- Data Frame includes columns of both `float64` and `int64` types.

### 2. Bảng cân đối kế toán (Balance Sheet)
**Method**
```python
finance.balance_sheet(period='year', lang='en')
```

**Parameters**
- `period`: 'year' for annual reports, 'quarter' for quarterly reports.
- `lang`: 'vi' for Vietnamese, 'en' for English.

**Data Types and Structure**
- Returns a pandas DataFrame.
- Data includes columns like 'Hàng tồn kho ròng', 'Tài sản cố định', 'Nợ ngắn hạn', etc.
- Data Frame includes columns of both `float64` and `int64` types.

### 3. Báo cáo lưu chuyển tiền tệ (Cash Flow Statement)
**Method**
```python
finance.cash_flow(period='year', lang='en')
```

**Parameters**
- `period`: 'year' for annual reports, 'quarter' for quarterly reports.
- `lang`: 'vi' for Vietnamese, 'en' for English.

**Data Types and Structure**
- Returns a pandas DataFrame.
- Data includes columns like 'Tiền và tương đương tiền', 'Lưu chuyển tiền từ hoạt động tài chính', etc.
- Data Frame includes columns of both `float64` and `int64` types.

### 4. Chỉ số tài chính (Financial Ratios)
**Method**
```python
ratios = finance.ratio(period='year', lang='en')
```

**Parameters**
- `period`: 'year' for annual reports, 'quarter' for quarterly reports.
- `lang`: 'vi' for Vietnamese, 'en' for English.

**Data Types and Structure**
- Returns a pandas DataFrame.
- Data includes columns like 'P/B', 'ROE', 'Chỉ số thanh toán hiện thời', etc.
- Data Frame includes columns of both `float64` and `int64` types.

Each of the above methods provides financial data as a structured pandas DataFrame, allowing for easy visualization and analysis in Python.

# Apply to MultiIndex DataFrame

Flatten the multiindex ratios dataframe by this method:
```python
from vnstock.core.utils.transform import flatten_hierarchical_index

flattened_df = flatten_hierarchical_index(
    ratios,  # multi-index df
    separator="_",  # separator for flattened columns
    handle_duplicates=True,  # handle duplicate column names
    drop_levels=0,  # or specify levels to drop
)
```