<div align="center">

# 🛍️ Customer Data Analysis for Business Insights

<img src="https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/Pandas-2.x-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
<img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
<img src="https://img.shields.io/badge/Matplotlib-Seaborn-11557C?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/Status-Completed-2ea44f?style=for-the-badge"/>

<br/>

> **Analyze. Segment. Act.**
> A complete RFM-based customer segmentation pipeline for a mid-sized Indian retail company — turning raw transaction data into actionable marketing insights.

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Business Problem](#-business-problem)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Workflow](#-workflow)
- [RFM Analysis](#-rfm-analysis)
- [Customer Segments](#-customer-segments)
- [Visualizations](#-visualizations)
- [Key Findings](#-key-findings)
- [How to Run](#-how-to-run)
- [Dependencies](#-dependencies)
- [Author](#-author)

---

## 🔍 Overview

This project performs end-to-end customer data analysis using **Python and Pandas** on a synthetic retail dataset of:

| Metric | Value |
|---|---|
| 👥 Unique Customers | 1,000 |
| 🧾 Total Transactions | 23,050 |
| 🏙️ Cities Covered | Indian metro & tier-2 cities |
| 📅 Reference Date | 2025-07-30 |

---

## 💼 Business Problem

A mid-sized Indian retail company needs to:

- 🎯 **Improve targeted marketing** by understanding customer behavior
- 💎 **Retain high-value customers** before they churn
- 📊 **Segment customers** based on purchase patterns
- 📣 **Generate actionable insights** for the marketing team

---

## 📂 Dataset

Two CSV files are provided:

<details>
<summary><b>📋 Customer_Master_Data2.csv</b> — click to expand</summary>

| Column | Type | Description |
|---|---|---|
| `CustomerID` | object | Unique customer identifier |
| `Name` | object | Customer's full name |
| `Email` | object | Customer's email address |
| `Gender` | object | Male / Female / Not Disclosed |
| `Age` | int | Age between 18 and 75 |
| `City` | object | Indian metro or tier-2 city |
| `MaritalStatus` | object | Single / Married / Divorced / Widowed |
| `NumChildren` | int | Number of children in household |
| `JoinDate` | datetime | Date of first registration |

</details>

<details>
<summary><b>🧾 Customer_Transactions2.csv</b> — click to expand</summary>

| Column | Type | Description |
|---|---|---|
| `CustomerID` | object | Links to customer master data |
| `TransactionDate` | datetime | Date of transaction (`%m/%d/%y` format) |
| `TransactionAmount` | float | Amount spent in ₹ |

</details>

---

## 🗂️ Project Structure

```
📦 customer-data-analysis/
 ┣ 📓 miniproject_complete.ipynb   ← Main analysis notebook
 ┣ 📊 Customer_Master_Data2.csv    ← Customer demographic data
 ┣ 📊 Customer_Transactions2.csv   ← Transaction history
 ┗ 📄 README.md                    ← You are here
```

---

## 🔄 Workflow

```
Load Data → Clean & Validate → Merge Datasets → RFM Calculation
    → Score R/F/M → Combine Scores → Assign Segments → Visualize
```

| Step | Task | Status |
|---|---|---|
| 1 | Load both CSVs into DataFrames | ✅ |
| 2 | Clean data, fix dtypes, check nulls | ✅ |
| 3 | Merge master + transaction data | ✅ |
| 4 | Compute Recency, Frequency, Monetary | ✅ |
| 5 | Score RFM on 1–5 scale using quantiles | ✅ |
| 6 | Create combined RFM segment string | ✅ |
| 7 | Assign business segment labels | ✅ |
| 8 | Visualize insights | ✅ |

---

## 📐 RFM Analysis

RFM is a proven customer segmentation framework:

| Metric | Formula | Meaning |
|---|---|---|
| **Recency (R)** | Days since last purchase | How recently did they buy? |
| **Frequency (F)** | Total number of transactions | How often do they buy? |
| **Monetary (M)** | Sum of all transaction amounts | How much do they spend? |

Each metric is scored **1 to 5** using `pd.qcut()`:

```
R Score → 1 = Stale buyer    5 = Very recent buyer
F Score → 1 = Rare buyer     5 = Very frequent buyer
M Score → 1 = Low spender    5 = High spender
```

Scores are combined into a 3-digit code → `"555"` = Champion, `"111"` = Lost

---

## 🏷️ Customer Segments

| Segment | Rule Logic | Count | Strategy |
|---|---|---|---|
| 🏆 **Champions** | R 4–5, F 4–5, M 4–5 | 131 | Early access, premium offers |
| 💙 **Loyal Customers** | F 4–5, R 2–5 | 206 | Reward points, upsell |
| 🌱 **Potential Loyalist** | R 4–5, F 2–3 | 167 | Welcome packs, onboarding |
| ⚠️ **At Risk** | R 1–2, F 3–5 | 146 | Reactivation campaigns |
| 💰 **Big Spenders** | M 4–5, F 2–3, R 3–4 | 17 | Nurture for loyalty |
| ❌ **Lost** | R 1, F 1–2, M 1–2 | 73 | Exit surveys / cut losses |
| 🔘 **Others** | Mixed scores | 260 | General campaigns |

---

## 📊 Visualizations

The notebook generates **4 key charts**:

| # | Chart | Insight |
|---|---|---|
| 1 | 📊 Bar Chart | Customer count per segment |
| 2 | 💹 Bar Chart | Revenue contribution per segment (with % labels) |
| 3 | 🔵 Scatter Plot | Recency vs Monetary colored by segment |
| 4 | 📈 Pareto Chart | Top 20% customers → ~80% of revenue |

---

## 🔑 Key Findings

```
📅 Recency Range    →   1 to 524 days
🔁 Frequency Range  →   6 to 38 transactions per customer
💸 Monetary Range   →   ₹5,052 to ₹44,785 per customer
🏆 Top Segment      →   Loyal Customers (206 customers)
⚠️  At Risk Count   →   146 customers need reactivation
📉 Lost Customers   →   73 customers — lowest ROI group
```

> 💡 **Pareto Insight:** The top 20% of customers by spend contribute approximately **80% of total revenue** — confirming the classic Pareto principle in retail.

---

## ▶️ How to Run

**1. Clone the repository**
```bash
git clone https://github.com/your-username/customer-data-analysis.git
cd customer-data-analysis
```

**2. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn
```

**3. Launch the notebook**
```bash
jupyter notebook miniproject_complete.ipynb
```

**4. Update file paths** in cells 1 & 4 to point to your local CSV files, then run:
```
Kernel → Restart & Run All
```

> ⚠️ **Note on date parsing:** `TransactionDate` is in `M/D/YY` format. Use `format='%m/%d/%y'` with `pd.to_datetime()`.

---

## 📦 Dependencies

```python
pandas       # Data loading, cleaning, groupby, merging
numpy        # Numerical operations
matplotlib   # Charts and visualizations
seaborn      # Statistical plotting, color palettes
```

Install all at once:
```bash
pip install pandas numpy matplotlib seaborn
```

---

## 👤 Author

<div align="center">

** Priya Sankar Mandal **

<br/>

⭐ *If you found this project useful, consider giving it a star!* ⭐

</div>
