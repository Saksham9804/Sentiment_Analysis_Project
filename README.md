# Twitter Engagement Ratio Trading Strategy

A quantitative trading strategy that leverages Twitter engagement metrics to identify stocks with unusual bot activity and constructs a monthly rebalancing portfolio based on engagement ratio analysis.

## Project Overview

This project analyzes Twitter metrics (posts, comments, likes, impressions) for major US stocks to identify potential bot activity through engagement ratio analysis. The strategy constructs a monthly rebalancing portfolio of the top 5 stocks with the highest engagement ratios and backtests performance from November 2021 to January 2023.

## Strategy Hypothesis

The core hypothesis is that **higher engagement ratios (comments/likes) indicate potential bot activity**. In organic Twitter engagement, the ratio of comments to likes typically remains relatively low. When this ratio spikes significantly, it may indicate coordinated bot activity or unusual market attention.

## Dataset

**File**: `twitter_sentiment_data.csv`

**Columns**:
- `date`: Trading date
- `symbol`: Stock ticker symbol
- `twitterPosts`: Number of Twitter posts mentioning the stock
- `twitterComments`: Total comments on posts
- `twitterLikes`: Total likes on posts
- `twitterImpressions`: Total impressions
- `twitterSentiment`: Sentiment score (0-1 scale)

**Coverage**:
- Time Period: November 18, 2021 - January 4, 2023
- Stocks: 67+ major US equities including AAPL, TSLA, AMD, NVDA
- Total Records: 26,487 daily observations

## Methodology

**1. Data Preprocessing**
```python
# Calculate engagement ratio
df['engagement_ratio'] = df['twitterComments'] / df['twitterLikes']

# Filter for meaningful engagement
df = df[(df['twitterLikes'] > 500) & (df['twitterComments'] > 200)]
```

**2. Portfolio Construction**
- Monthly aggregation of engagement ratios
- Cross-sectional ranking of stocks by engagement ratio each month
- Select top 5 stocks with highest engagement ratios
- Monthly rebalancing at month-end
- Equal-weighted portfolio (20% per stock)

**3. Backtesting**
- Download historical price data using `yfinance`
- Calculate daily returns and compute portfolio returns
- Analyze cumulative performance

## Getting Started

**Prerequisites**
```bash
pip install pandas numpy matplotlib seaborn yfinance
```

**Usage**
```python
import pandas as pd
import numpy as np
import yfinance as yf

# Load data
df = pd.read_csv('twitter_sentiment_data.csv')

# See Analysis.ipynb for full implementation
```

## Files in Repository

- `Analysis.ipynb`: Complete analysis notebook with strategy implementation
- `twitter_sentiment_data.csv`: Historical Twitter engagement data
- `README.md`: This file

## Key Insights

1. Engagement ratio (comments/likes) can indicate unusual market attention
2. The strategy identifies stocks with potential coordinated social media activity
3. Monthly rebalancing balances transaction costs with signal freshness
4. Equal weighting reduces concentration risk across selected stocks

## Limitations

- Data period limited to Nov 2021 - Jan 2023
- Backtest doesn't include transaction costs, slippage, or market impact
- Social media metrics can be noisy and unreliable
- Engagement ratio is a proxy, not definitive bot identification
- Strategy developed during a specific market period

## Disclaimer

**This project is for educational and research purposes only.**

This is not financial advice. Past performance does not guarantee future results. Trading involves risk of loss. Always do your own research and consult with financial professionals before making investment decisions.

---

Built with Python, Pandas, NumPy, Matplotlib, Seaborn, yfinance
