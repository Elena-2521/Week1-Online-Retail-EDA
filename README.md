# 📊 Online Retail II — Exploratory Data Analysis (EDA)

**Internship:** ITSimplera — AI/ML Track
**Task:** Week 1 — Data Analysis & Business Understanding
**Author:** Alina Bukhari
**Registration No:** AIMLB01-1688

---

## 📌 Objective

A retail company wants to understand customer purchase behavior **before** investing in a recommendation system. This project explores real transaction data to identify sales patterns, data quality issues, and business insights — helping the company understand **who its customers are, which products sell the most, and which countries generate the most revenue.**

---

## 📂 Dataset

- **Name:** Online Retail II Dataset
- **Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Online+Retail+II)
- **Direct download (zip):** https://archive.ics.uci.edu/static/public/502/online+retail+ii.zip
- **Description:** Real transaction data from a UK-based online retailer, covering **December 2009 – December 2011**, including invoices, product descriptions, quantities, prices, and customer IDs.
- **Format:** One Excel file (`online_retail_II.xlsx`) with **two sheets**:
  - `Year 2009-2010`
  - `Year 2010-2011`

> ⚠️ **Note:** The dataset file is not included in this repository due to its size. Please download it from the link above and place it in the project's root folder (or upload it directly in Colab) before running the notebook.

---

## 🛠️ Tools & Libraries Used

| Tool | Purpose |
|---|---|
| Python (Google Colab) | Environment for writing and running the analysis |
| pandas | Data loading, cleaning, and aggregation |
| numpy | Numerical operations |
| matplotlib | Base plotting |
| seaborn | Statistical visualizations (heatmaps, boxplots) |

---

## 🔍 Steps Performed

### 1. Data Loading
- Loaded both Excel sheets (`Year 2009-2010` and `Year 2010-2011`) separately, then combined them into a single DataFrame using `pd.concat()`.
- **Sheet 1 shape:** 525,461 rows × 8 columns
- **Sheet 2 shape:** 541,910 rows × 8 columns
- **Combined shape:** **1,067,371 rows × 8 columns**

### 2. Basic Information
- Displayed dataset shape, column names, and data types using `.shape`, `.columns`, `.dtypes`, `.info()`, and `.describe()`.
- Columns: `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, `Country`.

### 3. Missing Values
Identified missing data without removing any rows:

| Column | Missing Count | Missing % |
|---|---|---|
| Customer ID | 243,007 | 22.77% |
| Description | 4,382 | 0.41% |

📷 *[images/MissingValues_plot.png]*

### 4. Duplicate Rows
- **34,335 fully duplicate rows found** — approximately **3.22%** of the dataset.
- Rows were inspected but **not removed**, per task instructions (observation-only stage).

### 5. Feature Engineering
- Created a new `Revenue` column: `Revenue = Quantity × Price`.

### 6. Top 10 Best-Selling Products — By Quantity

| Product | Quantity Sold |
|---|---|
| WORLD WAR 2 GLIDERS ASSTD DESIGNS | 108,545 |
| WHITE HANGING HEART T-LIGHT HOLDER | 93,050 |
| ASSORTED COLOUR BIRD ORNAMENT | 81,306 |
| JUMBO BAG RED RETROSPOT | 78,090 |
| BROCADE RING PURSE | 70,700 |
| PACK OF 60 PINK PAISLEY CAKE CASES | 56,575 |
| 60 TEATIME FAIRY CAKE CASES | 54,366 |
| SMALL POPCORN HOLDER | 49,616 |
| PACK OF 72 RETROSPOT CAKE CASES | 49,344 |
| PACK OF 72 RETRO SPOT CAKE CASES | 46,106 |

📷 *[images/Top10ByQuantity.png]*

### 7. Top 10 Best-Selling Products — By Revenue

| Product | Revenue (£) |
|---|---|
| REGENCY CAKESTAND 3 TIER | 327,813.65 |
| DOTCOM POSTAGE | 322,647.47 |
| WHITE HANGING HEART T-LIGHT HOLDER | 257,533.90 |
| JUMBO BAG RED RETROSPOT | 148,800.64 |
| PARTY BUNTING | 147,948.50 |
| ASSORTED COLOUR BIRD ORNAMENT | 131,413.85 |
| PAPER CHAIN KIT 50'S CHRISTMAS | 121,662.14 |
| POSTAGE | 112,341.00 |
| CHILLI LIGHTS | 84,854.16 |
| ROTATING SILVER ANGELS T-LIGHT HLDR | 73,814.72 |

📷 *[images/Top10ByRevenue.png]*

### 8. Sales Performance by Country

| Country | Revenue (£) |
|---|---|
| United Kingdom | 16,382,580 |
| EIRE (Ireland) | 615,519.6 |
| Netherlands | 548,524.9 |
| Germany | 417,988.6 |
| France | 328,191.8 |
| Australia | 167,129.1 |
| Switzerland | 99,728.76 |
| Spain | 91,859.48 |
| Sweden | 87,809.42 |
| Denmark | 65,741.09 |

📷 *[images/BestCountriesByRev.png]*

### 9. Revenue Over Time — Monthly Trend
- Converted `InvoiceDate` to a proper datetime format and grouped revenue by month.
- Plotted a line chart showing revenue trends from Dec 2009 to Dec 2011, with visible seasonal peaks.

📷 *[images/MonthlyRevenueTrend.png]*

### 10. Correlation Heatmap

| | Quantity | Price | Revenue |
|---|---|---|---|
| **Quantity** | 1.00 | -0.001 | 0.76 |
| **Price** | -0.001 | 1.00 | 0.06 |
| **Revenue** | 0.76 | 0.06 | 1.00 |

📷 *[images/CorrHeatmap.png]*

### 11. Outlier Detection (Box Plots + IQR Method)
Visualized outliers using box plots and quantified them using the IQR (Interquartile Range) method:

| Column | Outliers Detected |
|---|---|
| Quantity | 116,489 |
| Price | 68,105 |
| Revenue | 90,922 |

📷 *[images/Boxplot_Outliers.png]*

> No outliers were removed — this stage is observation-only, as instructed.

---

## 💡 Business Insights

1. **UK dominates revenue** — the United Kingdom generates the vast majority of total revenue (~£16.4M), far ahead of secondary markets like Ireland and the Netherlands, showing heavy reliance on the domestic market.

2. **A small set of products drive most sales** — the top 10 products by quantity differ from the top 10 by revenue (e.g., "World War 2 Gliders" sells the most units but doesn't appear in the top revenue list), showing some high-volume items are low-cost while a few pricier items generate outsized revenue.

3. **Sales are seasonal** — the monthly revenue trend shows clear peaks, likely tied to the holiday shopping season (Nov–Dec), suggesting inventory and staffing should scale up ahead of this period.

4. **Missing Customer IDs are a data quality risk** — 22.77% of transactions have no Customer ID, meaning nearly a quarter of the data can't be linked to a specific buyer, which will limit any future customer-based recommendation system.

5. **Returns/cancellations exist in the data** — invoices starting with "C" and negative Quantity/Revenue values represent cancelled orders; these should not be treated as genuine purchase signals in a recommendation model, and indicate a need for return-policy analysis in the next phase.

6. **Outliers are present across all numeric fields** — over 100,000 outlier values in Quantity alone suggest a mix of bulk/wholesale orders and possible data entry issues that should be investigated before any modeling stage.

---

## ✅ Task Compliance Checklist

- [x] Loaded dataset and displayed shape, columns, data types
- [x] Identified and reported all missing values and duplicate rows
- [x] Analyzed top 10 best-selling products by quantity and revenue
- [x] Analyzed sales performance by country
- [x] Plotted revenue over time (monthly trend)
- [x] Created a correlation heatmap
- [x] Detected and visualized outliers using box plots
- [x] Documented at least 5 business insights
- [x] No data was removed — observation-only analysis
- [x] All plots include titles, axis labels, and legends
- [x] Notebook runs from top to bottom without errors

---

## 📁 Repository Structure

```
online-retail-eda-week1/
│
├── ITSimplera_Task1.ipynb     # Main analysis notebook
├── README.md                   # This documentation file
└── images/                     # Screenshots of charts (referenced above)
```

---

## 🚀 How to Run

1. Download the dataset from the [UCI link](https://archive.ics.uci.edu/ml/datasets/Online+Retail+II).
2. Open `ITSimplera_Task1.ipynb` in Google Colab.
3. Upload the dataset file when prompted (or mount Google Drive).
4. Run all cells from top to bottom (**Runtime → Run all**).

---

## 🔮 Next Steps

This EDA lays the groundwork for a future recommendation system. Before modeling, the following should be addressed:
- Handle or exclude rows with missing Customer IDs
- Decide how to treat cancelled/returned orders
- Account for seasonality in any time-aware model
- Investigate flagged outlier transactions
