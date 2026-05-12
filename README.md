# Financial Analytics Toolkit

A collection of Python notebooks and reusable modules covering 
core financial analytics workflows like P&L analysis, variance 
engine, forecasting comparison, and Monte Carlo stress testing.

Built using real financial data from publicly listed O&G 
companies (Shell, ExxonMobil, Seplat Energy) as part of a 
deliberate transition into energy-finance data science.

---

## Business Problem

Finance teams at investment management firms and O&G commercial analytics divisions spend 2+ days every month producing manual P&L reports, variance commentary, and forward-looking stress tests. This toolkit automates those core workflows using Python — reducing reporting time and introducing quantitative forecasting into what is typically a qualitative process.

---

## Data Sources

All notebooks use real, publicly available financial data, no synthetic data.

| Source | What It Provides | Access |
|---|---|---|
| **yfinance** | Quarterly income statements, balance sheets, and cash flow for Shell (SHEL), ExxonMobil (XOM), TotalEnergies (TTE), Seplat (SEPL.L) | Free `pip install yfinance` |
| **Seplat Energy IR** | Nigerian E&P company annual reports — production volumes, revenue in USD/NGN, operating cost per barrel | seplatpetroleum.com/investors/financial-reports |
| **EIA Financial Performance Profiles** | Industry-level O&G financial data going back to 1977 — revenues, capex, production volumes | eia.gov/finance/performanceprofiles |
| **SEC EDGAR** | Detailed 10-K and 10-Q filings for US O&G majors — segment-level P&L, upstream vs downstream breakdown | efts.sec.gov/LATEST/search-index |

To pull the primary dataset used in these notebooks:

```python
import yfinance as yf

# Shell quarterly P&L (primary dataset)
shell = yf.Ticker("SHEL")
df = shell.quarterly_financials.T  # transpose for time-series format
df.index = pd.to_datetime(df.index)
df = df.sort_index()

# Seplat Energy (Nigerian context)
seplat = yf.Ticker("SEPL.L")
df_seplat = seplat.quarterly_financials.T
```

---

## What's Inside

| Notebook | Dataset Used | Key Output |
|---|---|---|
| `01_pl_analysis.ipynb` | Shell quarterly financials (yfinance) | Waterfall chart + auto-commentary |
| `02_variance_analysis.ipynb` | Shell annual vs quarterly actuals | Variance table + impact ranking |
| `03_forecasting.ipynb` | Shell + Seplat quarterly revenue series | ARIMA vs Prophet vs XGBoost comparison |
| `04_monte_carlo.ipynb` | EIA industry volatility parameters | P&L distribution + probability of loss |
| `src/analytics_toolkit.py` | — | Reusable Python module |

---

## Tech Stack

- **Python 3.11+**
- pandas · numpy · matplotlib · plotly · seaborn
- scikit-learn · scipy · prophet · statsmodels
- yfinance (live O&G financial data)

---

## How to Run

```bash
git clone https://github.com/LenoFred/financial-analytics-toolkit
cd financial-analytics-toolkit

python -m venv venv
source venv/bin/activate    # Mac/Linux
# venv\Scripts\activate     # Windows

pip install -r requirements.txt
jupyter notebook
```

Open any notebook in `/notebooks` and run all cells. 
Data is pulled live via yfinance — no manual download needed 
for the primary notebooks.

For the Seplat annual reports, download PDFs from 
seplatpetroleum.com/investors/financial-reports and place 
in `/data/seplat/`.

---

## Folder Structure
financial-analytics-toolkit/
├── notebooks/
│   ├── 01_pl_analysis.ipynb
│   ├── 02_variance_analysis.ipynb
│   ├── 03_forecasting.ipynb
│   └── 04_monte_carlo.ipynb
├── src/
│   ├── init.py
│   └── analytics_toolkit.py
├── data/
│   └── seplat/     (place downloaded PDFs here)
├── outputs/
│   └── (charts and exports)
├── requirements.txt
└── README.md

## Why O&G Financial Data

These notebooks specifically use Shell and Seplat financial data because the target application is commercial analytics for the energy sector, the workflows here mirror what Shell's Controller & Finance Operations data science team and Nigerian E&P company finance divisions do operationally.

---

## Author

**Allen Ikheovha Frederick**  
GenAI Engineer & Data Scientist | Financial Analytics · 
GenAI · Energy Finance  

[GitHub](https://github.com/LenoFred) · 
[LinkedIn](https://linkedin.com/in/allenfrederick1)