# 📊 Financial Portfolio Data Collection  
**(Magnificent 7 vs Market)**

**Notebook:** `01_data_collection.ipynb`  
**Author:** Wiseman Radebe  
**Date:** 2025-08-05  
**License:** MIT

---

## 🚀 Overview
This notebook collects, validates, and (optionally) exports historical price data for the **Magnificent 7** tech stocks and the **S&P 500 (SPY)**.  
The resulting dataset is the foundation for downstream **portfolio analysis**, **risk/return metrics**, and **visualizations**.

---

## 🗂️ Table of Contents
1. [Project Goals]
2. [Data Sources]
3. [Environment & Setup]
4. [Portfolio Configuration] 
5. [Data Collection]
6. [Data Quality Checks]
7. [Next Steps]
8. [Citations]

---

## 🎯 Project Goals
- **Collect** daily OHLCV price data for selected tickers.
- **Validate** integrity (missing values, date ranges, price sanity, volume).
- **Prepare** clean datasets for analysis in subsequent notebooks.
- **Analyse** dataset and perform **risk-return** analysis.
- **Visualize** price trends and correlations,

---

## 🔎 Data Sources
- **Yahoo Finance** via the Python package **`yfinance`**.

**Tracked Assets:**
- `AAPL`, `MSFT`, `GOOGL`, `AMZN`, `NVDA`, `TSLA`, `META`, `SPY`

---

## 🧰 Environment & Setup

### Install dependencies
```bash
pip install -r requirements.txt

``requirements.txt``
pandas
numpy
matplotlib
seaborn
yfinance
```

## ⚙️ Portfolio Configuration
Adjust these in the notebook to change your universe or date window:
```
TICKERS = ['AAPL', 'MSFT', 'GOOGL', 'AMZN', 'NVDA', 'TSLA', 'META', 'SPY']
START_DATE = '2021-01-01'
END_DATE   = '2025-01-01'
```
## 🧲 Data Collection
Robust download with basic error handling (inside the notebook):

```
def collect_stock_data(tickers, start_date, end_date):
    import yfinance as yf
    stock_data, failed = {}, []
    for t in tickers:
        try:
            df = yf.download(t, start=start_date, end=end_date, progress=False)
            if df.empty:
                failed.append(t)
            else:
                stock_data[t] = df
        except Exception:
            failed.append(t)
    return stock_data, failed

stock_data, failed_stocks = collect_stock_data(TICKERS, START_DATE, END_DATE)
```
✅ Data Quality Checks

The notebook evaluates:
- Observations count per ticker
- Missing values
- Date coverage (start/end)
- Average daily volume
- Close price range (min/max)

Example function:
```
def assess_data_quality(stock_data):
    report = {}
    for t, df in stock_data.items():
        report[t] = {
            "observations": len(df),
            "missing_values": int(df.isna().sum().sum()),
            "date_range": (df.index.min(), df.index.max()),
            "avg_volume": float(df["Volume"].mean()) if "Volume" in df else None,
            "price_range": (float(df["Close"].min()), float(df["Close"].max()))
        }
    return report

quality_report = assess_data_quality(stock_data)
```

## ⏭️ Next Steps

The following steps will be executed in subsequent notebooks to extend the analysis:


1. **Risk & Return Metrics**  
   - Compute **CAGR (Compound Annual Growth Rate)**, **annualized volatility**, **Sharpe Ratio**, and **maximum drawdown**.  
   - Benchmark performance of the **Magnificent 7 portfolio** against the **S&P 500 (SPY)**.

2. **Visualization**  
   - Plot price trends for each ticker and the aggregated portfolio.  
   - Create drawdown charts to visualize downside risk.  
   - Generate heatmaps to explore correlations between assets.

3. **Comparison & Insights**  
   - Compare risk-adjusted performance between Magnificent 7 and SPY.  
   - Highlight diversification benefits or concentration risks.  

---


## 📚 Citations
- yfinance Python package: Yahoo Finance market data.
