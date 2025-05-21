# VnStock Financial Statement Analysis Guide

## Understanding VnStock Data Structures

The VnStock library provides access to Vietnamese financial market data through various classes and methods. When working with financial statements, it's important to understand their unique data structures.

## Key Financial Data Structures

VnStock returns financial data in three main dataframes, each structured differently:

1. **Ratio Dataframe**: Uses a **m
ulti-index column structure** with two levels:
   - First level: Category (e.g., 'Meta', 'Chỉ tiêu khả năng sinh lợi')
   - Second level: Specific metric (e.g., 'yearReport', 'ROE (%)')

2. **Balance Sheet**: Uses a flat column structure with descriptive names:
   - 'yearReport' for time periods

3. **Income Statement**: Also uses a flat column structure:
   - 'yearReport' for time periods

All three dataframes use 'yearReport' (or its multi-index equivalent) for time alignment.

## Working with Multi-Index Columns

The most challenging aspect of using VnStock's financial data is handling the multi-index columns in the ratio dataframe. Here's how to properly access this data:

1. **Access multi-index columns with tuples**: 
   - For year data: `df[('Meta', 'yearReport')]`
   - For ROE data: `df[('Chỉ tiêu khả năng sinh lợi', 'ROE (%)')]`

2. **Filter and set index with multi-index columns**:
   ```
   year_col = ('Meta', 'yearReport')
   df_filtered = df[df[year_col].isin(years)]
   df_by_year = df_filtered.set_index(year_col)
   ```

## Aligning Financial Data Across Statements

To analyze metrics across different statements, align all data by year:

1. Define year columns for each dataframe (accounting for multi-index in ratios)
2. Set the year column as the index in each dataframe
3. Perform calculations or comparisons using the aligned indexes

## Common Challenges and Solutions

 **Language Differences**: The library supports both English and Vietnamese. Be consistent with your `lang` parameter.

## Best Practices

2. **Handle Multi-Index Appropriately**: Check for multi-index columns and access them correctly using tuples.

3. **Use Consistent Alignment**: Always align data on 'yearReport' for time series analysis.

# Dataframe strucure
The yearReport column exists, but it's part of a multi-index tuple as ('Meta', 'yearReport')
Ratio.columns.to_list()


[('Meta', 'CP'),
 ('Meta', 'Năm'),
 ('Meta', 'Kỳ'),
 ('Chỉ tiêu cơ cấu nguồn vốn', '(Vay NH+DH)/VCSH'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'Nợ/VCSH'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'TSCĐ / Vốn CSH'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'Vốn CSH/Vốn điều lệ'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Vòng quay tài sản'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Vòng quay TSCĐ'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Số ngày thu tiền bình quân'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Số ngày tồn kho bình quân'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Số ngày thanh toán bình quân'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Chu kỳ tiền'),
 ('Chỉ tiêu hiệu quả hoạt động', 'Vòng quay hàng tồn kho'),
 ('Chỉ tiêu khả năng sinh lợi', 'Biên EBIT (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Biên lợi nhuận gộp (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Biên lợi nhuận ròng (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROE (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROIC (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROA (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'EBITDA (Tỷ đồng)'),
 ('Chỉ tiêu khả năng sinh lợi', 'EBIT (Tỷ đồng)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Tỷ suất cổ tức (%)'),
 ('Chỉ tiêu thanh khoản', 'Chỉ số thanh toán hiện thời'),
 ('Chỉ tiêu thanh khoản', 'Chỉ số thanh toán tiền mặt'),
 ('Chỉ tiêu thanh khoản', 'Chỉ số thanh toán nhanh'),
 ('Chỉ tiêu thanh khoản', 'Khả năng chi trả lãi vay'),
 ('Chỉ tiêu thanh khoản', 'Đòn bẩy tài chính'),
 ('Chỉ tiêu định giá', 'Vốn hóa (Tỷ đồng)'),
 ('Chỉ tiêu định giá', 'Số CP lưu hành (Triệu CP)'),
 ('Chỉ tiêu định giá', 'P/E'),
 ('Chỉ tiêu định giá', 'P/B'),
 ('Chỉ tiêu định giá', 'P/S'),
 ('Chỉ tiêu định giá', 'P/Cash Flow'),
 ('Chỉ tiêu định giá', 'EPS (VND)'),
 ('Chỉ tiêu định giá', 'BVPS (VND)'),
 ('Chỉ tiêu định giá', 'EV/EBITDA')]

 **English Version for the Ratio dataframe**
 [('Meta', 'ticker'),
 ('Meta', 'yearReport'),
 ('Meta', 'lengthReport'),
 ('Chỉ tiêu cơ cấu nguồn vốn', 'Fixed Asset-To-Equity'),
 ('Chỉ tiêu cơ cấu nguồn vốn', "Owners' Equity/Charter Capital"),
 ('Chỉ tiêu khả năng sinh lợi', 'Net Profit Margin (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROE (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'ROA (%)'),
 ('Chỉ tiêu khả năng sinh lợi', 'Dividend yield (%)'),
 ('Chỉ tiêu thanh khoản', 'Financial Leverage'),
 ('Chỉ tiêu định giá', 'Market Capital (Bn. VND)'),
 ('Chỉ tiêu định giá', 'Outstanding Share (Mil. Shares)'),
 ('Chỉ tiêu định giá', 'P/E'),
 ('Chỉ tiêu định giá', 'P/B'),
 ('Chỉ tiêu định giá', 'P/S'),
 ('Chỉ tiêu định giá', 'P/Cash Flow'),
 ('Chỉ tiêu định giá', 'EPS (VND)'),
 ('Chỉ tiêu định giá', 'BVPS (VND)')]

CashFlow.columns.to_list()
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

BalanceSheet.columns.to_list()
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

 