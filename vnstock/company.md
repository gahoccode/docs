The document provides several methods to fetch various pieces of information about a company using a Python `Company` object, along with the data types and structures of the resulting data:

1. **Company Overview**
   - **Method**: `company.overview()`
   - **Data Structure**: DataFrame with columns `symbol`, `id`, `issue_share`, `history`, `company_profile`, `icb_name3`, `icb_name2`, `icb_name4`, `financial_ratio_issue_share`, `charter_capital`.
   - **Data Types**: Includes object, int64.

2. **Major Shareholders**
   - **Method**: `company.shareholders()`
   - **Data Structure**: DataFrame with columns `id`, `share_holder`, `quantity`, `share_own_percent`, `update_date`.
   - **Data Types**: Includes object, int64, float64.

3. **Officers**
   - **Method**: `company.officers(filter_by='working')`
   - **Data Structure**: DataFrame with columns `id`, `officer_name`, `officer_position`, `position_short_name`, `update_date`, `officer_own_percent`, `quantity`, `type`.
   - **Data Types**: Includes object, float64, int64.

4. **Subsidiaries**
   - **Method**: `company.subsidiaries()`
   - **Data Structure**: DataFrame with columns `id`, `sub_organ_code`, `ownership_percent`, `organ_name`, `type`.
   - **Data Types**: Includes object.

5. **Events**
   - **Method**: `company.events()`
   - **Data Structure**: DataFrame with columns `id`, `event_title`, `en__event_title`, `public_date`, `issue_date`, `source_url`, `event_list_code`, `ratio`, `value`, `record_date`, `exright_date`, `event_list_name`, `en__event_list_name`.
   - **Data Types**: Includes object, float64.

6. **News**
   - **Method**: `company.news()`
   - **Data Structure**: DataFrame with columns `id`, `news_title`, `news_sub_title`, `friendly_sub_title`, `news_image_url`, `news_source_link`, `created_at`, `public_date`, `updated_at`, `lang_code`, `news_id`, `news_short_content`, `news_full_content`, `close_price`, `ref_price`, `floor`, `ceiling`, `price_change_pct`.
   - **Data Types**: Includes object, int64, float64.

7. **Reports**
   - **Method**: `company.reports()`
   - **Data Structure**: DataFrame with columns `date`, `description`, `link`, `name`.
   - **Data Types**: Includes object.

8. **Financial Condition**
   - **Method**: `company.ratio_summary()`
   - **Data Structure**: DataFrame with columns like `symbol`, `year_report`, `length_report`, `update_date`, `revenue`, `revenue_growth`, `net_profit`, `net_profit_growth`, `ebit_margin`, `roe`, `roic`, `roa`, `pe`, `pb`, `eps`, `current_ratio`, `cash_ratio`, `quick_ratio`, `interest_coverage`, `ae`, `fae`, `net_profit_margin`, `gross_margin`, `ev`, `issue_share`, `ps`, `pcf`, `bvps`, `ev_per_ebitda`, `at`, `fat`, `acp`, `dso`, `dpo`, `eps_ttm`, `charter_capital`, `rtq4`, `charter_capital_ratio`, `rtq10`, `dividend`, `ebitda`, `ebit`, `le`, `de`, `ccc`, `rtq17`.
   - **Data Types**: Includes object, int64, float64.

9. **Trading Stats**
   - **Method**: `company.trading_stats()`
   - **Data Structure**: DataFrame with columns `symbol`, `exchange`, `ev`, `ceiling`, `floor`, `ref_price`, `open`, `match_price`, `close_price`, `price_change`, `price_change_pct`, `high`, `low`, `total_volume`, `high_price_1y`, `low_price_1y`, `pct_low_change_1y`, `pct_high_change_1y`, `foreign_volume`, `foreign_room`, `avg_match_volume_2w`, `foreign_holding_room`, `current_holding_ratio`, `max_holding_ratio`.
   - **Data Types**: Includes object, int64, float64.

These methods and structures provide comprehensive access to a company's data, including its shareholders, officers, subsidiaries, financials, and more, using the VNStock API.
