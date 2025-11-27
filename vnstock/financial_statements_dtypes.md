Below are the `data.info()` outputs for different financial statements and ratio dataframes in both Vietnamese and English from the VCI source:

### Báo cáo kết quả kinh doanh (Income Statement)

**Tiếng Việt**

```plaintext
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11 entries, 0 to 10
Data columns (total 60 columns):
 #   Column                                               Non-Null Count  Dtype
---  ------                                               --------------  -----
 0   CP                                                   11 non-null     object
 1   Năm                                                  11 non-null     int64
 2   Chứng khoán kinh doanh                               10 non-null     float64
 3   Chứng khoán kinh doanh                               10 non-null     float64
 4   Chứng khoán kinh doanh                               10 non-null     float64
 5   Chứng khoán đầu tư                                   10 non-null     float64
 6   Chứng khoán đầu tư                                   10 non-null     float64
 7   Cổ đông thiểu số                                     11 non-null     int64
 8   Cổ đông thiểu số                                     11 non-null     int64
 9   Lãi/Lỗ ròng trước thuế                               11 non-null     int64
 10  Cố tức đã nhận                                       10 non-null     float64
 11  Cố tức đã nhận                                       10 non-null     float64
 12  Tăng trưởng doanh thu (%)                            10 non-null     float64
 13  Doanh thu (Tỷ đồng)                                  11 non-null     int64
 14  Lợi nhuận sau thuế của Cổ đông công ty mẹ (Tỷ đồng)  11 non-null     int64
 15  Tăng trưởng lợi nhuận (%)                            10 non-null     float64
 16  Thu nhập tài chính                                   10 non-null     float64
 17  Thu nhập tài chính                                   10 non-null     float64
 18  Chi phí tiền lãi vay                                 10 non-null     float64
 19  Chi phí tiền lãi vay                                 10 non-null     float64
 20  Doanh thu thuần                                      10 non-null     float64
 21  Doanh thu thuần                                      11 non-null     int64
 22  Lãi gộp                                              10 non-null     float64
 23  Lãi gộp                                              11 non-null     int64
 24  Chi phí tài chính                                    10 non-null     float64
 25  Chi phí tài chính                                    10 non-null     float64
 26  Chi phí quản lý DN                                   11 non-null     int64
 27  Chi phí quản lý DN                                   10 non-null     float64
 28  Lãi/Lỗ từ hoạt động kinh doanh                       11 non-null     int64
 29  Lãi/Lỗ từ hoạt động kinh doanh                       10 non-null     float64
 30  Lãi lỗ trong công ty liên doanh, liên kết            11 non-null     int64
 31  Thu nhập/Chi phí khác                                11 non-null     int64
 32  Giá vốn hàng bán                                     11 non-null     int64
 33  Chi phí bán hàng                                     10 non-null     float64
 34  Chi phí bán hàng                                     10 non-null     float64
 35  Doanh thu bán hàng và cung cấp dịch vụ               11 non-null     int64
 36  Các khoản giảm trừ doanh thu                         11 non-null     int64
 37  Lãi/lỗ từ công ty liên doanh                         10 non-null     float64
 38  Thu nhập khác                                        11 non-null     int64
 39  Lợi nhuận khác                                       11 non-null     int64
 40  Thu nhập lãi và các khoản tương tự                   10 non-null     float64
 41  Chi phí lãi và các khoản tương tự                    10 non-null     float64
 42  Thu nhập lãi thuần                                   10 non-null     float64
 43  Thu nhập từ hoạt động dịch vụ                        10 non-null     float64
 44  Chi phí hoạt động dịch vụ                            10 non-null     float64
 45  Lãi thuần từ hoạt động dịch vụ                       10 non-null     float64
 46  Kinh doanh ngoại hối và vàng                         10 non-null     float64
 47  Hoạt động khác                                       10 non-null     float64
 48  Chi phí hoạt động khác                               10 non-null     float64
 49  Lãi/lỗ thuần từ hoạt động khác                       10 non-null     float64
 50  Tổng thu nhập hoạt động                              10 non-null     float64
 51  LN từ HĐKD trước CF dự phòng                         10 non-null     float64
 52  Chi phí dự phòng rủi ro tín dụng                     10 non-null     float64
 53  LN trước thuế                                        11 non-null     int64
 54  Thuế TNDN                                            10 non-null     float64
 55  Chi phí thuế TNDN hiện hành                          11 non-null     int64
 56  Chi phí thuế TNDN hoãn lại                           11 non-null     int64
 57  Lợi nhuận thuần                                      11 non-null     int64
 58  Cổ đông của Công ty mẹ                               11 non-null     int64
 59  Lãi cơ bản trên cổ phiếu                             11 non-null     int64
dtypes: float64(36), int64(23), object(1)
memory usage: 5.3+ KB
```

**English**

```plaintext
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11 entries, 0 to 10
Data columns (total 58 columns):
 #   Column                                                   Non-Null Count  Dtype
---  ------                                                   --------------  -----
 0   ticker                                                   11 non-null     object
 1   yearReport                                               11 non-null     int64
 2   Minority Interest                                        11 non-null     int64
 3   Minority Interest                                        11 non-null     int64
 4   Net Profit/Loss before tax                               11 non-null     int64
 5   Dividends received                                       10 non-null     float64
 6   Dividends received                                       10 non-null     float64
 7   Provision for credit losses                              10 non-null     float64
 8   Provision for credit losses                              11 non-null     int64
 9   Revenue YoY (%)                                          10 non-null     float64
 10  Revenue (Bn. VND)                                        11 non-null     int64
 11  Attribute to parent company (Bn. VND)                    11 non-null     int64
 12  Attribute to parent company YoY (%)                      10 non-null     float64
 13  Financial Income                                         10 non-null     float64
 14  Financial Income                                         10 non-null     float64
 15  Interest Expenses                                        10 non-null     float64
 16  Interest Expenses                                        10 non-null     float64
 17  Net Sales                                                10 non-null     float64
 18  Net Sales                                                11 non-null     int64
 19  Gross Profit                                             10 non-null     float64
 20  Gross Profit                                             11 non-null     int64
 21  Financial Expenses                                       10 non-null     float64
 22  Financial Expenses                                       10 non-null     float64
 23  General & Admin Expenses                                 11 non-null     int64
 24  General & Admin Expenses                                 10 non-null     float64
 25  Operating Profit/Loss                                    11 non-null     int64
 26  Operating Profit/Loss                                    10 non-null     float64
 27  Net income from associated companies                     11 non-null     int64
 28  Other Income/Expenses                                    11 non-null     int64
 29  Cost of Sales                                            11 non-null     int64
 30  Selling Expenses                                         10 non-null     float64
 31  Selling Expenses                                         10 non-null     float64
 32  Sales                                                    11 non-null     int64
 33  Sales deductions                                         11 non-null     int64
 34  Gain/(loss) from joint ventures                          10 non-null     float64
 35  Other income                                             11 non-null     int64
 36  Net other income/expenses                                11 non-null     int64
 37  Interest and Similar Income                              10 non-null     float64
 38  Interest and Similar Expenses                            10 non-null     float64
 39  Net Interest Income                                      10 non-null     float64
 40  Fees and Comission Income                                10 non-null     float64
 41  Fees and Comission Expenses                              10 non-null     float64
 42  Net Fee and Commission Income                            10 non-null     float64
 43  Net gain (loss) from foreign currency and gold dealings  10 non-null     float64
 44  Net gain (loss) from trading of trading securities       10 non-null     float64
 45  Net gain (loss) from disposal of investment securities   10 non-null     float64
 46  Net Other income/(expenses)                              10 non-null     float64
 47  Other expenses                                           10 non-null     float64
 48  Net Other income/expenses                                10 non-null     float64
 49  Total operating revenue                                  10 non-null     float64
 50  Operating Profit before Provision                        10 non-null     float64
 51  Profit before tax                                        11 non-null     int64
 52  Tax For the Year                                         10 non-null     float64
 53  Business income tax - current                            11 non-null     int64
 54  Business income tax - deferred                           11 non-null     int64
 55  Net Profit For the Year                                  11 non-null     int64
 56  Attributable to parent company                           11 non-null     int64
 57  EPS_basis                                                11 non-null     int64
dtypes: float64(33), int64(24), object(1)
memory usage: 5.1+ KB
```

### Bảng cân đối kế toán (Balance Sheet)

**Tiếng Việt**

```plaintext
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11 entries, 0 to 10
Data columns (total 72 columns):
 #   Column                                                      Non-Null Count  Dtype
---  ------                                                      --------------  -----
 0   CP                                                          11 non-null     object
 1   Năm                                                         11 non-null     int64
 2   Hàng tồn kho ròng                                           11 non-null     int64
 3   Tài sản lưu động khác                                       11 non-null     int64
 4   Giá trị ròng tài sản đầu tư                                 11 non-null     int64
 5   Tài sản dài hạn khác                                        11 non-null     int64
 6   Các quỹ khác                                                11 non-null     int64
 7   Các quỹ khác                                                11 non-null     int64
 8   Vốn Ngân sách nhà nước và quỹ khác                          11 non-null     int64
 9   Vốn Ngân sách nhà nước và quỹ khác                          10 non-null     float64
 10  LỢI ÍCH CỦA CỔ ĐÔNG THIỂU SỐ                                10 non-null     float64
 11  Lợi thế thương mại                                          11 non-null     int64
 12  Tiền gửi tại ngân hàng nhà nước Việt Nam                    10 non-null     float64
 13  Tiền gửi tại các TCTD khác và cho vay các TCTD khác         10 non-null     float64
 14  Dự phòng giảm giá chứng khoán kinh doanh                    10 non-null     float64
 15  Các công cụ tài chính phái sinh và khoản nợ tài chính khác  10 non-null     float64
 16  Các công cụ tài chính phái sinh và khoản nợ tài chính khác  10 non-null     float64
 17  Cho vay khách hàng                                          10 non-null     float64
 18  Cho vay khách hàng                                          10 non-null     float64
 19  Dự phòng rủi ro cho vay khách hàng                          10 non-null     float64
 20  Chứng khoán đầu tư sẵn sàng để bán                          10 non-null     float64
 21  Chứng khoán đầu tư giữ đến ngày đáo hạn                     10 non-null     float64
 22  Dự phòng giảm giá chứng khoán đầu tư                        10 non-null     float64
 23  Đầu tư vào công ty con                                      11 non-null     int64
 24  Đầu tư vào công ty liên doanh                               11 non-null     int64
 25  Dự phòng giảm giá đầu tư dài hạn                            11 non-null     int64
 26  Tài sản cố định hữu hình                                    11 non-null     int64
 27  Tài sản cố định thuê tài chính                              11 non-null     int64
 28  Tài sản cố định vô hình                                     11 non-null     int64
 29  Tài sản Có khác                                             10 non-null     float64
 30  Các khoản nợ chính phủ và NHNN Việt Nam                     10 non-null     float64
 31  Tiền gửi và vay các Tổ chức tín dụng khác                   10 non-null     float64
 32  Tiền gửi của khách hàng                                     10 non-null     float64
 33  Vốn tài trợ, uỷ thác đầu tư của CP và các tổ chức TD khác   10 non-null     float64
 34  Phát hành giấy tờ có giá                                    10 non-null     float64
 35  Các khoản nợ khác                                           10 non-null     float64
 36  Vốn của tổ chức tín dụng                                    10 non-null     float64
 37  Quỹ của tổ chức tín dụng                                    10 non-null     float64
 38  Chênh lệch tỷ giá hối đoái                                  11 non-null     int64
 39  Chênh lệch đánh giá lại tài sản                             11 non-null     int64
 40  TÀI SẢN NGẮN HẠN (Tỷ đồng)                                  11 non-null     int64
 41  Tiền và tương đương tiền (Tỷ đồng)                          11 non-null     int64
 42  Giá trị thuần đầu tư ngắn hạn (Tỷ đồng)                     11 non-null     int64
 43  Các khoản phải thu ngắn hạn (Tỷ đồng)                       11 non-null     int64
 44  Trả trước cho người bán ngắn hạn (Tỷ đồng)                  11 non-null     int64
 45  Phải thu về cho vay ngắn hạn (Tỷ đồng)                      10 non-null     float64
 46  Hàng tồn kho, ròng (Tỷ đồng)                                11 non-null     int64
 47  Tài sản lưu động khác (Tỷ đồng)                             11 non-null     int64
 48  TÀI SẢN DÀI HẠN (Tỷ đồng)                                   11 non-null     int64
 49  TỔNG CỘNG NGUỒN VỐN (Tỷ đồng)                               11 non-null     int64
 50  Lãi chưa phân phối (Tỷ đồng)                                11 non-null     int64
 51  Quỹ đầu tư và phát triển (Tỷ đồng)                          11 non-null     int64
 52  Cổ phiếu phổ thông (Tỷ đồng)                                10 non-null     float64
 53  Vốn góp của chủ sở hữu (Tỷ đồng)                            11 non-null     int64
 54  Vốn và các quỹ (Tỷ đồng)                                    11 non-null     int64
 55  VỐN CHỦ SỞ HỮU (Tỷ đồng)                                    11 non-null     int64
 56  Trái phiếu chuyển đổi (Tỷ đồng)                             10 non-null     float64
 57  Vay và nợ thuê tài chính dài hạn (Tỷ đồng)                  11 non-null     int64
 58  Nợ dài hạn (Tỷ đồng)                                        11 non-null     int64
 59  Người mua trả tiền trước ngắn hạn (Tỷ đồng)                 11 non-null     int64
 60  Vay và nợ thuê tài chính ngắn hạn (Tỷ đồng)                 11 non-null     int64
 61  Nợ ngắn hạn (Tỷ đồng)                                       11 non-null     int64
 62  NỢ PHẢI TRẢ (Tỷ đồng)                                       11 non-null     int64
 63  TỔNG CỘNG TÀI SẢN (Tỷ đồng)                                 11 non-null     int64
 64  Lợi thế thương mại (Tỷ đồng)                                10 non-null     float64
 65  Trả trước dài hạn (Tỷ đồng)                                 11 non-null     int64
 66  Tài sản dài hạn khác (Tỷ đồng)                              11 non-null     int64
 67  Đầu tư dài hạn (Tỷ đồng)                                    11 non-null     int64
 68  Tài sản cố định (Tỷ đồng)                                   11 non-null     int64
 69  Phải thu dài hạn khác (Tỷ đồng)                             11 non-null     int64
 70  Phải thu về cho vay dài hạn (Tỷ đồng)                       10 non-null     float64
 71  Phải thu dài hạn (Tỷ đồng)                                  11 non-null     int64
dtypes: float64(27), int64(44), object(1)
memory usage: 6.3+ KB
```

**English**

```plaintext
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11 entries, 0 to 10
Data columns (total 75 columns):
 #   Column                                                             Non-Null Count  Dtype
---  ------                                                             --------------  -----
 0   ticker                                                             11 non-null     object
 1   yearReport                                                         11 non-null     int64
 2   Net Inventories                                                    11 non-null     int64
 3   Other current assets                                               11 non-null     int64
 4   Investment in properties                                           11 non-null     int64
 5   Other non-current assets                                           11 non-null     int64
 6   Other Reserves                                                     11 non-null     int64
 7   Other Reserves                                                     11 non-null     int64
 8   Budget sources and other funds                                     11 non-null     int64
 9   Budget sources and other funds                                     10 non-null     float64
 10  MINORITY INTERESTS                                                 10 non-null     float64
 11  Goodwill                                                           11 non-null     int64
 12  Balances with the SBV                                              10 non-null     float64
 13  Placements with and loans to other credit institutions             10 non-null     float64
 14  Trading Securities, net                                            10 non-null     float64
 15  Trading Securities                                                 10 non-null     float64
 16  Provision for diminution in value of Trading Securities            10 non-null     float64
 17  Derivatives and other financial liabilities                        10 non-null     float64
 18  Derivatives and other financial liabilities                        10 non-null     float64
 19  Loans and advances to customers, net                               10 non-null     float64
 20  Loans and advances to customers                                    10 non-null     float64
 21  Less: Provision for losses on loans and advances to customers      10 non-null     float64
 22  Investment Securities                                              10 non-null     float64
 23  Available-for Sales Securities                                     10 non-null     float64
 24  Held-to-Maturity Securities                                        10 non-null     float64
 25  Less: Provision for diminution in value of investment securities   10 non-null     float64
 26  Investment in joint ventures                                       11 non-null     int64
 27  Investments in associate companies                                 11 non-null     int64
 28  Less: Provision for diminuation in value of long term investments  11 non-null     int64
 29  Tangible fixed assets                                              11 non-null     int64
 30  Leased assets                                                      11 non-null     int64
 31  Intagible fixed assets                                             11 non-null     int64
 32  Other Assets                                                       10 non-null     float64
 33  Due to Gov and borrowings from SBV                                 10 non-null     float64
 34  Deposits and borrowings from other credit institutions             10 non-null     float64
 35  Deposits from customers                                            10 non-null     float64
 36  Funds received from Gov, international and other institutions      10 non-null     float64
 37  Convertible bonds/CDs and other valuable papers issued             10 non-null     float64
 38  Other liabilities                                                  10 non-null     float64
 39  Capital                                                            10 non-null     float64
 40  Reserves                                                           10 non-null     float64
 41  Foreign Currency Difference reserve                                11 non-null     int64
 42  Difference upon Assets Revaluation                                 11 non-null     int64
 43  CURRENT ASSETS (Bn. VND)                                           11 non-null     int64
 44  Cash and cash equivalents (Bn. VND)                                11 non-null     int64
 45  Short-term investments (Bn. VND)                                   11 non-null     int64
 46  Accounts receivable (Bn. VND)                                      11 non-null     int64
 47  Prepayments to suppliers (Bn. VND)                                 11 non-null     int64
 48  Short-term loans receivables (Bn. VND)                             10 non-null     float64
 49  Inventories, Net (Bn. VND)                                         11 non-null     int64
 50  Other current assets (Bn. VND)                                     11 non-null     int64
 51  LONG-TERM ASSETS (Bn. VND)                                         11 non-null     int64
 52  TOTAL RESOURCES (Bn. VND)                                          11 non-null     int64
 53  Undistributed earnings (Bn. VND)                                   11 non-null     int64
 54  Investment and development funds (Bn. VND)                         11 non-null     int64
 55  Common shares (Bn. VND)                                            10 non-null     float64
 56  Paid-in capital (Bn. VND)                                          11 non-null     int64
 57  Capital and reserves (Bn. VND)                                     11 non-null     int64
 58  OWNER'S EQUITY(Bn.VND)                                             11 non-null     int64
 59  Convertible bonds (Bn. VND)                                        10 non-null     float64
 60  Long-term borrowings (Bn. VND)                                     11 non-null     int64
 61  Long-term liabilities (Bn. VND)                                    11 non-null     int64
 62  Advances from customers (Bn. VND)                                  11 non-null     int64
 63  Short-term borrowings (Bn. VND)                                    11 non-null     int64
 64  Current liabilities (Bn. VND)                                      11 non-null     int64
 65  LIABILITIES (Bn. VND)                                              11 non-null     int64
 66  TOTAL ASSETS (Bn. VND)                                             11 non-null     int64
 67  Good will (Bn. VND)                                                10 non-null     float64
 68  Long-term prepayments (Bn. VND)                                    11 non-null     int64
 69  Other long-term assets (Bn. VND)                                   11 non-null     int64
 70  Long-term investments (Bn. VND)                                    11 non-null     int64
 71  Fixed assets (Bn. VND)                                             11 non-null     int64
 72  Other long-term receivables (Bn. VND)                              11 non-null     int64
 73  Long-term loans receivables (Bn. VND)                              10 non-null     float64
 74  Long-term trade receivables (Bn. VND)                              11 non-null     int64
dtypes: float64(30), int64(44), object(1)
memory usage: 6.6+ KB
```

### Báo cáo lưu chuyển tiền tệ (Cash Flow Statement)

**Tiếng Việt**

```plaintext
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11 entries, 0 to 10
Data columns (total 44 columns):
 #   Column                                                                  Non-Null Count  Dtype
---  ------                                                                  --------------  -----
 0   CP                                                                      11 non-null     object
 1   Năm                                                                     11 non-null     int64
 2   Tiền và tương đương tiền                                                11 non-null     int64
 3   Lãi/Lỗ chênh lệch tỷ giá chưa thực hiện                                 11 non-null     int64
 4   Lãi/Lỗ từ thanh lý tài sản cố định                                      10 non-null     float64
 5   Lãi/Lỗ từ thanh lý tài sản cố định                                      10 non-null     float64
 6   Lãi/Lỗ từ hoạt động đầu tư                                              11 non-null     int64
 7   Thu nhập lãi                                                            11 non-null     int64
 8   Thu lãi và cổ tức                                                       10 non-null     float64
 9   Tăng/Giảm các khoản phải thu                                            10 non-null     float64
 10  Tăng/Giảm các khoản phải thu                                            11 non-null     int64
 11  Tăng/Giảm hàng tồn kho                                                  11 non-null     int64
 12  Tăng/Giảm các khoản phải trả                                            11 non-null     int64
 13  Tăng/Giảm các khoản phải trả                                            10 non-null     float64
 14  Tăng/Giảm chi phí trả trước                                             11 non-null     int64
 15  Chi phí lãi vay đã trả                                                  11 non-null     int64
 16  Tiền thu nhập doanh nghiệp đã trả                                       11 non-null     int64
 17  Tiền thu khác từ các hoạt động kinh doanh                               11 non-null     int64
 18  Tiền chi khác từ các hoạt động kinh doanh                               11 non-null     int64
 19  Lưu chuyển tiền tệ ròng từ các hoạt động SXKD                           11 non-null     int64
 20  Tiền thu được từ thanh lý tài sản cố định                               11 non-null     int64
 21  Đầu tư vào các doanh nghiệp khác                                        11 non-null     int64
 22  Tiền thu từ việc bán các khoản đầu tư vào doanh nghiệp khác             11 non-null     int64
 23  Chi trả cho việc mua lại, trả cổ phiếu                                  11 non-null     int64
 24  Tiền thu được các khoản đi vay                                          11 non-null     int64
 25  Tiền trả các khoản đi vay                                               11 non-null     int64
 26  Tiền thanh toán vốn gốc đi thuê tài chính                               11 non-null     int64
 27  Cổ tức đã trả                                                           11 non-null     int64
 28  Lưu chuyển tiền thuần trong kỳ                                          11 non-null     int64
 29  Ảnh hưởng của chênh lệch tỷ giá                                         11 non-null     int64
 30  Tiền và tương đương tiền cuối kỳ                                        11 non-null     int64
 31  Khấu hao TSCĐ                                                           11 non-null     int64
 32  Dự phòng RR tín dụng                                                    11 non-null     int64
 33  (Lãi)/lỗ các hoạt động khác                                             10 non-null     float64
 34  Lưu chuyển tiền thuần từ HĐKD trước thay đổi VLĐ                        11 non-null     int64
 35  Lưu chuyển tiền thuần từ HĐKD trước thuế                                10 non-null     float64
 36  Chi từ các quỹ của TCTD                                                 10 non-null     float64
 37  Mua sắm TSCĐ                                                            11 non-null     int64
 38  Tiền thu cổ tức và lợi nhuận được chia                                  11 non-null     int64
 39  Lưu chuyển từ hoạt động đầu tư                                          11 non-null     int64
 40  Tăng vốn cổ phần từ góp vốn và/hoặc phát hành cổ phiếu                  11 non-null     int64
 41  Lưu chuyển tiền từ hoạt động tài chính                                  11 non-null     int64
 42  Tiền thu hồi cho vay, bán lại các công cụ nợ của đơn vị khác (Tỷ đồng)  11 non-null     int64
 43  Tiền chi cho vay, mua công cụ nợ của đơn vị khác (Tỷ đồng)              11 non-null     int64
dtypes: float64(8), int64(35), object(1)
memory usage: 3.9+ KB
```

**English**

```plaintext
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 11 entries, 0 to 10
Data columns (total 43 columns):
 #   Column                                                                   Non-Null Count  Dtype
---  ------                                                                   --------------  -----
 0   ticker                                                                   11 non-null     object
 1   yearReport                                                               11 non-null     int64
 2   Cash and cash equivalents                                                11 non-null     int64
 3   Unrealized foreign exchange gain/loss                                    11 non-null     int64
 4   Profit/Loss from disposal of fixed assets                                10 non-null     float64
 5   Profit/Loss from disposal of fixed assets                                10 non-null     float64
 6   Profit/Loss from investing activities                                    11 non-null     int64
 7   Interest Expense                                                         11 non-null     int64
 8   Interest income and dividends                                            10 non-null     float64
 9   Increase/Decrease in receivables                                         10 non-null     float64
 10  Increase/Decrease in receivables                                         11 non-null     int64
 11  Increase/Decrease in inventories                                         11 non-null     int64
 12  Increase/Decrease in payables                                            11 non-null     int64
 13  Increase/Decrease in payables                                            10 non-null     float64
 14  Increase/Decrease in prepaid expenses                                    11 non-null     int64
 15  Interest paid                                                            11 non-null     int64
 16  Business Income Tax paid                                                 11 non-null     int64
 17  Other receipts from operating activities                                 11 non-null     int64
 18  Other payments on operating activities                                   11 non-null     int64
 19  Net cash inflows/outflows from operating activities                      11 non-null     int64
 20  Proceeds from disposal of fixed assets                                   11 non-null     int64
 21  Investment in other entities                                             11 non-null     int64
 22  Proceeds from divestment in other entities                               11 non-null     int64
 23  Payments for share repurchases                                           11 non-null     int64
 24  Proceeds from borrowings                                                 11 non-null     int64
 25  Repayment of borrowings                                                  11 non-null     int64
 26  Finance lease principal payments                                         11 non-null     int64
 27  Dividends paid                                                           11 non-null     int64
 28  Net increase/decrease in cash and cash equivalents                       11 non-null     int64
 29  Foreign exchange differences Adjustment                                  11 non-null     int64
 30  Cash and Cash Equivalents at the end of period                           11 non-null     int64
 31  Depreciation and Amortisation                                            11 non-null     int64
 32  Profits from other activities                                            10 non-null     float64
 33  Operating profit before changes in working capital                       11 non-null     int64
 34  Net Cash Flows from Operating Activities before BIT                      10 non-null     float64
 35  Payment from reserves                                                    10 non-null     float64
 36  Purchase of fixed assets                                                 11 non-null     int64
 37  Gain on Dividend                                                         11 non-null     int64
 38  Net Cash Flows from Investing Activities                                 11 non-null     int64
 39  Increase in charter captial                                              11 non-null     int64
 40  Cash flows from financial activities                                     11 non-null     int64
 41  Collection of loans, proceeds from sales of debts instruments (Bn. VND)  11 non-null     int64
 42  Loans granted, purchases of debt instruments (Bn. VND)                   11 non-null     int64
dtypes: float64(8), int64(34), object(1)
memory usage: 3.8+ KB
```

### Chỉ số tài chính (Financial Ratios)

# Apply to MultiIndex DataFrame

```python
flattened_df = flatten_hierarchical_index(
    ratios,  # multi-index df
    separator="_",  # separator for flattened columns
    handle_duplicates=True,  # handle duplicate column names
    drop_levels=0,  # or specify levels to drop
)
```

**Tiếng Việt**

```plaintext
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 13 entries, 0 to 12
Data columns (total 37 columns):

# Column Non-Null Count Dtype

---

0 (Meta, CP) 13 non-null object
1 (Meta, Năm) 13 non-null int64
 2 (Meta, Kỳ) 13 non-null int64
 3 (Chỉ tiêu cơ cấu nguồn vốn, (Vay NH+DH)/VCSH) 13 non-null float64
4 (Chỉ tiêu cơ cấu nguồn vốn, Nợ/VCSH) 13 non-null float64
5 (Chỉ tiêu cơ cấu nguồn vốn, TSCĐ / Vốn CSH) 13 non-null float64
6 (Chỉ tiêu cơ cấu nguồn vốn, Vốn CSH/Vốn điều lệ) 13 non-null float64
7 (Chỉ tiêu hiệu quả hoạt động, Vòng quay tài sản) 13 non-null float64
8 (Chỉ tiêu hiệu quả hoạt động, Vòng quay TSCĐ) 13 non-null float64
9 (Chỉ tiêu hiệu quả hoạt động, Số ngày thu tiền bình quân) 13 non-null float64
10 (Chỉ tiêu hiệu quả hoạt động, Số ngày tồn kho bình quân) 13 non-null float64
11 (Chỉ tiêu hiệu quả hoạt động, Số ngày thanh toán bình quân) 13 non-null float64
12 (Chỉ tiêu hiệu quả hoạt động, Chu kỳ tiền) 13 non-null float64
13 (Chỉ tiêu hiệu quả hoạt động, Vòng quay hàng tồn kho) 13 non-null float64
14 (Chỉ tiêu khả năng sinh lợi, Biên EBIT (%)) 13 non-null float64
15 (Chỉ tiêu khả năng sinh lợi, Biên lợi nhuận gộp (%)) 13 non-null float64
16 (Chỉ tiêu khả năng sinh lợi, Biên lợi nhuận ròng (%)) 13 non-null float64
17 (Chỉ tiêu khả năng sinh lợi, ROE (%)) 13 non-null float64
18 (Chỉ tiêu khả năng sinh lợi, ROIC (%)) 13 non-null float64
19 (Chỉ tiêu khả năng sinh lợi, ROA (%)) 13 non-null float64
20 (Chỉ tiêu khả năng sinh lợi, EBITDA (Tỷ đồng)) 13 non-null int64
 21 (Chỉ tiêu khả năng sinh lợi, EBIT (Tỷ đồng)) 13 non-null float64
22 (Chỉ tiêu khả năng sinh lợi, Tỷ suất cổ tức (%)) 13 non-null float64
23 (Chỉ tiêu thanh khoản, Chỉ số thanh toán hiện thời) 13 non-null float64
24 (Chỉ tiêu thanh khoản, Chỉ số thanh toán tiền mặt) 13 non-null float64
25 (Chỉ tiêu thanh khoản, Chỉ số thanh toán nhanh) 13 non-null float64
26 (Chỉ tiêu thanh khoản, Khả năng chi trả lãi vay) 13 non-null float64
27 (Chỉ tiêu thanh khoản, Đòn bẩy tài chính) 13 non-null float64
28 (Chỉ tiêu định giá, P/B) 13 non-null float64
29 (Chỉ tiêu định giá, Vốn hóa (Tỷ đồng)) 13 non-null int64
 30 (Chỉ tiêu định giá, Số CP lưu hành (Triệu CP)) 13 non-null int64
 31 (Chỉ tiêu định giá, P/E) 13 non-null float64
32 (Chỉ tiêu định giá, P/S) 13 non-null float64
33 (Chỉ tiêu định giá, P/Cash Flow) 13 non-null float64
34 (Chỉ tiêu định giá, EPS (VND)) 13 non-null float64
35 (Chỉ tiêu định giá, BVPS (VND)) 13 non-null float64
36 (Chỉ tiêu định giá, EV/EBITDA) 13 non-null float64
dtypes: float64(31), int64(5), object(1)
memory usage: 3.9+ KB
None
```

```python
0   CP                                                          13 non-null     object
1   Năm                                                         13 non-null     int64
2   Kỳ                                                          13 non-null     int64
3   (Vay NH+DH)/VCSH                                            13 non-null     float64
4   Nợ/VCSH                                                     13 non-null     float64
5   TSCĐ / Vốn CSH                                              13 non-null     float64
6   Vốn CSH/Vốn điều lệ                                         13 non-null     float64
7   Vòng quay tài sản                                           13 non-null     float64
8   Vòng quay TSCĐ                                              13 non-null     float64
9   Số ngày thu tiền bình quân                                  13 non-null     float64
10  Số ngày tồn kho bình quân                                   13 non-null     float64
11  Số ngày thanh toán bình quân                                13 non-null     float64
12  Chu kỳ tiền                                                 13 non-null     float64
13  Vòng quay hàng tồn kho                                      13 non-null     float64
14  Biên EBIT (%)                                               13 non-null     float64
15  Biên lợi nhuận gộp (%)                                      13 non-null     float64
16  Biên lợi nhuận ròng (%)                                     13 non-null     float64
17  ROE (%)                                                     13 non-null     float64
18  ROIC (%)                                                    13 non-null     float64
19  ROA (%)                                                     13 non-null     float64
20  EBITDA (Tỷ đồng)                                            13 non-null     int64
21  EBIT (Tỷ đồng)                                              13 non-null     float64
22  Tỷ suất cổ tức (%)                                          13 non-null     float64
23  Chỉ số thanh toán hiện thời                                 13 non-null     float64
24  Chỉ số thanh toán tiền mặt                                  13 non-null     float64
25  Chỉ số thanh toán nhanh                                     13 non-null     float64
26  Khả năng chi trả lãi vay                                    13 non-null     float64
27  Đòn bẩy tài chính                                           13 non-null     float64
28  P/B                                                         13 non-null     float64
29  Vốn hóa (Tỷ đồng)                                           13 non-null     int64
30  Số CP lưu hành (Triệu CP)                                   13 non-null     int64
31  P/E                                                         13 non-null     float64
32  P/S                                                         13 non-null     float64
33  P/Cash Flow                                                 13 non-null     float64
34  EPS (VND)                                                   13 non-null     float64
35  BVPS (VND)                                                  13 non-null     float64
36  EV/EBITDA                                                   13 non-null     float64
```

**_English_**

```python
0   ticker                                                    13 non-null     object
1   yearReport                                                13 non-null     int64
2   lengthReport                                              13 non-null     int64
3   (ST+LT borrowings)/Equity                                 13 non-null     float64
4   Debt/Equity                                               13 non-null     float64
5   Fixed Asset-To-Equity                                     13 non-null     float64
6   Owners' Equity/Charter Capital                            13 non-null     float64
7   Asset Turnover                                            13 non-null     float64
8   Fixed Asset Turnover                                      13 non-null     float64
9   Days Sales Outstanding                                    13 non-null     float64
10  Days Inventory Outstanding                                13 non-null     float64
11  Days Payable Outstanding                                  13 non-null     float64
12  Cash Cycle                                                13 non-null     float64
13  Inventory Turnover                                        13 non-null     float64
14  EBIT Margin (%)                                           13 non-null     float64
15  Gross Profit Margin (%)                                   13 non-null     float64
16  Net Profit Margin (%)                                     13 non-null     float64
17  ROE (%)                                                   13 non-null     float64
18  ROIC (%)                                                  13 non-null     float64
19  ROA (%)                                                   13 non-null     float64
20  EBITDA (Bn. VND)                                          13 non-null     int64
21  EBIT (Bn. VND)                                            13 non-null     float64
22  Dividend yield (%)                                        13 non-null     float64
23  Current Ratio                                             13 non-null     float64
24  Cash Ratio                                                13 non-null     float64
25  Quick Ratio                                               13 non-null     float64
26  Interest Coverage                                         13 non-null     float64
27  Financial Leverage                                        13 non-null     float64
28  P/B                                                       13 non-null     float64
29  Market Capital (Bn. VND)                                  13 non-null     int64
30  Outstanding Share (Mil. Shares)                           13 non-null     int64
31  P/E                                                       13 non-null     float64
32  P/S                                                       13 non-null     float64
33  P/Cash Flow                                               13 non-null     float64
34  EPS (VND)                                                 13 non-null     float64
35  BVPS (VND)                                                13 non-null     float64
36  EV/EBITDA                                                 13 non-null     float64
```
