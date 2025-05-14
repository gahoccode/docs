"""
Functions extracted from the vnstock_ezchart demo notebook.
This collection includes visualization functions for financial data analysis.
"""

# Main initialization function
def ezchart_init():
    """
    Initialize the MPlot object for creating charts.
    
    Returns:
    -------
    MPlot object that provides various visualization methods
    """
    from vnstock_ezchart import *
    return MPlot()

# Data loading functions
def load_historical_data(symbol='GMD', start_date="2019-01-01", end_date='2024-03-22', resolution='1D'):
    """
    Load historical stock data using vnstock library.
    
    Parameters:
    ----------
    symbol : str
        Stock symbol/ticker (default: 'GMD')
    start_date : str
        Start date in 'YYYY-MM-DD' format (default: '2019-01-01')
    end_date : str
        End date in 'YYYY-MM-DD' format (default: '2024-03-22')
    resolution : str
        Time resolution for data, e.g. '1D' for daily (default: '1D')
    
    Returns:
    -------
    DataFrame with historical price data formatted for visualization
    """
    from vnstock import stock_historical_data
    import pandas as pd
    
    candle_df = stock_historical_data(
        symbol=symbol,
        start_date=start_date,
        end_date=end_date, 
        resolution=resolution, 
        type='stock', 
        beautify=True, 
        decor=False, 
        source='DNSE'
    )
    
    candle_df['time'] = pd.to_datetime(candle_df['time'])
    candle_df.set_index('time', inplace=True)
    
    return candle_df

def load_financial_report(symbol='SSI', report_type='IncomeStatement', frequency='Quarterly', periods=15):
    """
    Load financial report data using vnstock library.
    
    Parameters:
    ----------
    symbol : str
        Stock symbol/ticker (default: 'SSI')
    report_type : str
        Type of financial report, options include 'IncomeStatement', 'BalanceSheet', 'CashFlow' (default: 'IncomeStatement')
    frequency : str
        Report frequency, options include 'Quarterly', 'Yearly' (default: 'Quarterly')
    periods : int
        Number of periods to retrieve (default: 15)
    
    Returns:
    -------
    DataFrame with financial report data formatted for visualization
    """
    from vnstock import financial_report
    import pandas as pd
    
    income_df = financial_report(
        symbol=symbol, 
        report_type=report_type, 
        frequency=frequency, 
        periods=periods, 
        latest_year=None
    )
    
    income_df = income_df.T
    income_df.columns = income_df.iloc[0]
    income_df = income_df[1:]
    # convert all columns to numeric
    income_df = income_df.apply(pd.to_numeric, errors='coerce')
    
    return income_df

# Utility functions
def get_help(function_name):
    """
    Display help information for a specific chart function.
    
    Parameters:
    ----------
    function_name : str
        Name of the chart function to get help for
    
    Returns:
    -------
    Help text for the specified function
    """
    # In actual use: ezchart.help(function_name)
    pass

def list_color_palettes():
    """
    List all available color palettes.
    
    Returns:
    -------
    Dictionary keys of available color palettes
    """
    from vnstock_ezchart import Utils
    return Utils.brand_palettes.keys()

def create_color_map(palette_name='vnstock'):
    """
    Create a color map from a predefined palette.
    
    Parameters:
    ----------
    palette_name : str
        Name of the palette to create color map from (default: 'vnstock')
    
    Returns:
    -------
    Matplotlib colormap object
    """
    from vnstock_ezchart import Utils
    return Utils.create_cmap(palette_name)

def download_font(font_name='Roboto'):
    """
    Download a font for use in charts.
    
    Parameters:
    ----------
    font_name : str
        Name of the font to download (default: 'Roboto')
    """
    from vnstock_ezchart import Utils
    Utils.download_font(font_name)

def list_fonts():
    """
    List all available fonts.
    
    Returns:
    -------
    List of available fonts
    """
    from vnstock_ezchart import Utils
    return Utils.list_font()

# Chart functions
def bar_chart(data, title='', xlabel='', ylabel='', color_palette='vnstock', 
             data_labels=True, grid=False, figsize=(10, 6)):
    """
    Create a bar chart.
    
    Parameters:
    ----------
    data : pd.DataFrame or pd.Series
        Data to visualize
    title : str
        Chart title (default: '')
    xlabel : str
        X-axis label (default: '')
    ylabel : str
        Y-axis label (default: '')
    color_palette : str
        Name of color palette to use (default: 'vnstock')
    data_labels : bool
        Whether to show data labels (default: True)
    grid : bool
        Whether to show grid (default: False)
    figsize : tuple
        Figure size as (width, height) (default: (10, 6))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.bar(data, title=title, xlabel=xlabel, ...)
    pass

def histogram(data, title='', bins=10, color_palette='category', figsize=(8, 6)):
    """
    Create a histogram.
    
    Parameters:
    ----------
    data : pd.DataFrame or pd.Series
        Data to visualize
    title : str
        Chart title (default: '')
    bins : int
        Number of bins (default: 10)
    color_palette : str
        Name of color palette to use (default: 'category')
    figsize : tuple
        Figure size as (width, height) (default: (8, 6))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.hist(data, title=title, bins=bins, ...)
    pass

def pie_chart(data, labels, title='', color_palette='stock', figsize=(8, 8)):
    """
    Create a pie chart.
    
    Parameters:
    ----------
    data : pd.Series
        Values for pie slices
    labels : pd.Series
        Labels for pie slices
    title : str
        Chart title (default: '')
    color_palette : str
        Name of color palette to use (default: 'stock')
    figsize : tuple
        Figure size as (width, height) (default: (8, 8))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.pie(data=data, labels=labels, title=title, ...)
    pass

def time_series(data, title='', xlabel='', ylabel='', color_palette='stock', figsize=(10, 6)):
    """
    Create a time series plot.
    
    Parameters:
    ----------
    data : pd.Series with datetime index
        Time series data to visualize
    title : str
        Chart title (default: '')
    xlabel : str
        X-axis label (default: '')
    ylabel : str
        Y-axis label (default: '')
    color_palette : str
        Name of color palette to use (default: 'stock')
    figsize : tuple
        Figure size as (width, height) (default: (10, 6))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.timeseries(data, title=title, xlabel=xlabel, ...)
    pass

def heatmap(data, annot=True, cmap=None, fmt=".2f", figsize=(10, 8)):
    """
    Create a heatmap.
    
    Parameters:
    ----------
    data : pd.DataFrame
        Matrix data to visualize
    annot : bool
        Whether to annotate cells with values (default: True)
    cmap : matplotlib colormap
        Colormap to use (default: None)
    fmt : str
        Format string for annotations (default: ".2f")
    figsize : tuple
        Figure size as (width, height) (default: (10, 8))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.heatmap(data, annot=annot, cmap=cmap, ...)
    pass

def scatter_plot(data, x, y, title='', figsize=(10, 6)):
    """
    Create a scatter plot.
    
    Parameters:
    ----------
    data : pd.DataFrame
        Data containing x and y columns
    x : str
        Column name for x-axis
    y : str
        Column name for y-axis
    title : str
        Chart title (default: '')
    figsize : tuple
        Figure size as (width, height) (default: (10, 6))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.scatter(data=data, x=x, y=y, title=title, ...)
    pass

def treemap(values, labels, title='', color_palette='category', figsize=(10, 6)):
    """
    Create a treemap.
    
    Parameters:
    ----------
    values : list
        List of values determining rectangle sizes
    labels : list
        List of labels for rectangles
    title : str
        Chart title (default: '')
    color_palette : str
        Name of color palette to use (default: 'category')
    figsize : tuple
        Figure size as (width, height) (default: (10, 6))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.treemap(values=values, labels=labels, title=title, ...)
    pass

def boxplot(data, title='', ylabel='', figsize=(10, 8)):
    """
    Create a boxplot.
    
    Parameters:
    ----------
    data : pd.Series or pd.DataFrame
        Data to visualize
    title : str
        Chart title (default: '')
    ylabel : str
        Y-axis label (default: '')
    figsize : tuple
        Figure size as (width, height) (default: (10, 8))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.boxplot(data, title=title, ylabel=ylabel, ...)
    pass

def pairplot(data):
    """
    Create a pairplot showing relationships between variables.
    
    Parameters:
    ----------
    data : pd.DataFrame
        Data containing multiple columns to compare
    
    Returns:
    -------
    Seaborn PairGrid object
    """
    # In actual use: ezchart.pairplot(data)
    pass

def wordcloud(text, title='', color_palette='vnstock', fontname='DejaVu Sans', figsize=(10, 6)):
    """
    Create a word cloud visualization.
    
    Parameters:
    ----------
    text : str
        Text to visualize as word cloud
    title : str
        Chart title (default: '')
    color_palette : str
        Name of color palette to use (default: 'vnstock')
    fontname : str
        Font to use (default: 'DejaVu Sans')
    figsize : tuple
        Figure size as (width, height) (default: (10, 6))
    """
    # In actual use: ezchart.wordcloud(text, title=title, color_palette=color_palette, ...)
    pass

def table_chart(data, figsize=(6, 10), header=True, edges="horizontal", show=True):
    """
    Create a table visualization.
    
    Parameters:
    ----------
    data : pd.DataFrame
        Table data to visualize
    figsize : tuple
        Figure size as (width, height) (default: (6, 10))
    header : bool
        Whether to show header row (default: True)
    edges : str
        Type of edges to display, options: "horizontal", "vertical", "both", "none" (default: "horizontal")
    show : bool
        Whether to display the table (default: True)
    """
    # In actual use: ezchart.table(data, figsize=figsize, header=header, ...)
    pass

def combo_chart(bar_data, line_data, left_ylabel='', right_ylabel='', title='', 
               color_palette='vnstock', figsize=(10, 6)):
    """
    Create a combination chart with bars and line.
    
    Parameters:
    ----------
    bar_data : pd.Series
        Data for bar chart
    line_data : pd.Series
        Data for line chart
    left_ylabel : str
        Y-axis label for bar chart (default: '')
    right_ylabel : str
        Y-axis label for line chart (default: '')
    title : str
        Chart title (default: '')
    color_palette : str
        Name of color palette to use (default: 'vnstock')
    figsize : tuple
        Figure size as (width, height) (default: (10, 6))
    
    Returns:
    -------
    Figure and Axes objects
    """
    # In actual use: ezchart.combo_chart(bar_data, line_data, left_ylabel=left_ylabel, ...)
    pass