
# Highest NAV Fund

```python
def highest_nav_fund(fund):
    """
    Find and display the fund with the highest NAV from the fund listing.
    
    Parameters
    ----------
    fund : object
        Fund object with listing() and details.nav_report() methods
        
    Returns
    -------
    tuple
        (highest_nav_fund_data, fund_details, summary_text) - Series with fund data, 
        NAV report, and formatted summary string
    """
    # Get fund listing and sort by NAV
    fund_list = fund.listing()
    highest_nav = fund_list.sort_values(by="nav", ascending=False).iloc[0]
    
    # Build summary text
    summary_lines = []
    summary_lines.append(
        f"Fund with highest NAV: {highest_nav['short_name']} "
        f"({highest_nav['fund_code']})"
    )
    summary_lines.append(f"NAV: {highest_nav['nav']:,.2f}")
    summary_lines.append(f"Fund type: {highest_nav['fund_type']}")
    summary_lines.append(f"Fund owner: {highest_nav['fund_owner_name']}")
    summary_lines.append(f"Inception date: {highest_nav['inception_date']}")
    summary_lines.append(
        f"NAV change since inception: {highest_nav['nav_change_inception']:.2f}%"
    )
    
    # Handle potential missing 3-year annualized data
    if pd.notna(highest_nav["nav_change_36m_annualized"]):
        summary_lines.append(
            f"NAV change (3 years annualized): "
            f"{highest_nav['nav_change_36m_annualized']:.2f}%"
        )
    else:
        summary_lines.append("NAV change (3 years annualized): N/A")
    
    # Create summary text and print
    summary_text = "\n".join(summary_lines)
    print(summary_text)
    
    # Get detailed NAV report
    fund_code = highest_nav["short_name"]
    fund_details = fund.details.nav_report(fund_code)
    
    return highest_nav, fund_details, summary_text
```
