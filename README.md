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
1. [Project Goals](#-project-goals)  
2. [Data Sources](#-data-sources)  
3. [Environment & Setup](#-environment--setup)  
4. [Portfolio Configuration](#-portfolio-configuration)  
5. [Data Collection](#-data-collection)  
6. [Data Quality Checks](#-data-quality-checks)  
7. [(Optional) Data Export](#-optional-data-export)  
8. [Sample Output](#-sample-output)  
9. [Next Steps](#-next-steps)  
10. [Citations](#-citations)

---

## 🎯 Project Goals
- **Collect** daily OHLCV price data for selected tickers.
- **Validate** integrity (missing values, date ranges, price sanity, volume).
- **Prepare** clean datasets for analysis in subsequent notebooks.

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

##⚙️ Portfolio Configuration
Adjust these in the notebook to change your universe or date window:

TICKERS = ['AAPL', 'MSFT', 'GOOGL', 'AMZN', 'NVDA', 'TSLA', 'META', 'SPY']
START_DATE = '2021-01-01'
END_DATE   = '2025-01-01'
