# Fundamental Stock Analysis Tool

This project is a Python-based tool for analysing stocks using financial data from Yahoo Finance. It calculates a custom score based on various financial metrics, inspired by the Piotroski F-Score but with some modifications to better suit modern financial analysis needs.

## Features

- Fetches financial data (balance sheet, income statement, cash flow statement) for given stock tickers using `yfinance`
- Option to save financial statements as CSV files
- Calculates a custom score based on:
  - Profitability
  - Leverage and Liquidity
  - Operating Efficiency
- Retrieves the P/E ratio for each stock
- Provides a summary DataFrame with scores and P/E ratios for easy comparison

## Modified Scoring Criteria

This tool uses a modified version of the Piotroski F-Score, with the following key changes:

1. Net Income Growth: Instead of just checking for positive Return on Assets (RoA) in the current year, the tool compares the current year's net income to the previous year's.
2. Debt Ratio: Rather than checking if long-term debt has decreased, the tool assigns a point if the debt ratio is below 0.4.
3. Current Ratio: The tool checks if the current ratio is greater than 1, instead of looking at year-over-year changes.
4. P/E Ratio: While not part of the scoring system, the P/E ratio is calculated and included in the output for additional context.

## Installation

```bash
pip install yahoo_fin yfinance pandas
```

## Usage

1. Import the necessary libraries and define your stock tickers:

```python
import yfinance as yf
import pandas as pd

TICKERS = ['TSLA']  # Add more tickers as needed
```

2. Fetch financial statements:

```python
def get_financial_statements(ticker, save_to_csv=False):
    # ... (function implementation)
    
    if save_to_csv:
        balance_sheet.to_csv(f"{ticker}_balance_sheet.csv")
        income_statement.to_csv(f"{ticker}_income_statement.csv")
        cashflow_statement.to_csv(f"{ticker}_cashflow_statement.csv")
    
    return balance_sheet, income_statement, cashflow_statement, years

# Usage example:
balance_sheet, income_statement, cashflow_statement, years = get_financial_statements('TSLA', save_to_csv=True)
```

Note: By default, `save_to_csv` is set to `False`. If set to `True`, the function will save the financial statements as CSV files in the current working directory.

3. Run the analysis:

```python
result_summary = analyse_stocks(TICKERS)
print(result_summary)
```

## Output

The tool generates a DataFrame with the following columns:

- Ticker
- PE Ratio
- Profitability Score (0-5)
- Leverage Score (0-2)
- Operating Efficiency Score (0-2)
- Total Score (sum of all scores)

## Disclaimer

This tool is for educational and research purposes only. Always conduct your own due diligence before making investment decisions.

## Contributing

Feel free to fork this project and submit pull requests with improvements or additional features.

## License

[MIT License](https://opensource.org/licenses/MIT)
