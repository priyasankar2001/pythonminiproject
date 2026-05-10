# pythonminiproject
# Customer Data Analysis for Business Insights

A Python-based data analytics project that cleans, processes, and analyzes retail customer transaction data to generate actionable business insights using RFM (Recency, Frequency, Monetary) segmentation.

---

## Project Overview

A mid-sized Indian retail company wants to improve targeted marketing, retain valuable customers, and detect patterns in customer behavior. This project analyzes customer demographics and transaction data to segment customers and identify high-value groups.

---

## Dataset Description

Two CSV datasets are used:

### 1. `Customer_Master_Data2.csv` — 1,000 unique customers

| Column | Description |
|---|---|
| CustomerID | Unique identifier for each customer |
| Name | Customer's full name |
| Email | Customer's email ID |
| Gender | Male, Female, or Not Disclosed |
| Age | Customer age (18–75) |
| City | Indian metro/tier-2 city |
| MaritalStatus | Single, Married, Divorced, Widowed |
| NumChildren | Number of children in household |
| JoinDate | Date customer first registered |

### 2. `Customer_Transactions2.csv` — 23,050 transactions

| Column | Description |
|---|---|
| CustomerID | Links to customer master dataset |
| TransactionDate | Date of transaction |
| TransactionAmount | Amount spent in ₹ |

---

## Project Structure

```
├── miniproject_complete.ipynb   # Main analysis notebook
├── Customer_Master_Data2.csv    # Customer demographic data
├── Customer_Transactions2.csv   # Transaction history
└── README.md                    # Project documentation
```

---

## Steps Performed

### Step 1 — Load the Data
- Load both CSVs into Pandas DataFrames
- Check shape, structure (`.info()`), and preview (`.head()`)

### Step 2 — Clean the Data
- Convert `JoinDate` and `TransactionDate` to `datetime`
  - Note: `TransactionDate` format is `%m/%d/%y` (e.g. `7/31/23`)
- Check for null values in both datasets
- Validate uniqueness of `CustomerID` in master dataset
- Verify all transaction `CustomerID`s exist in master data

### Step 3 — Merge Datasets
- Left join `Customer_Transactions` with `Customer_Master_Data` on `CustomerID`
- Resulting merged DataFrame (`df`) has 23,050 rows × 11 columns

### Step 4 — RFM Calculation
- **Reference date**: max `TransactionDate` + 1 day → `2025-07-30`
- **Recency**: days between reference date and each customer's last transaction
- **Frequency**: total number of transactions per customer
- **Monetary**: total spend per customer
- Combined into a single `df_rfm` DataFrame

### Step 5 — RFM Scoring (1–5 scale)
- `R_Score`: lower recency = higher score (5 = most recent)
- `F_Score`: higher frequency = higher score (rank-based to handle ties)
- `M_Score`: higher spend = higher score
- Scored using `pd.qcut()` into 5 quantile bins

### Step 6 — Combined RFM Segment
- Scores concatenated into a string e.g. `"555"` (Champion) or `"111"` (Lost)
- Numeric `RFM_Score` = R + F + M (range: 3–15)

### Step 7 — Business Segment Labels

| Segment | Rule Logic | Strategy |
|---|---|---|
| Champions | R 4–5, F 4–5, M 4–5 | Early access, premium offers |
| Loyal Customers | F 4–5, R 2–5 | Reward points, upsell |
| Potential Loyalist | R 4–5, F 2–3 | Welcome packs, onboarding |
| At Risk | R 1–2, F 3–5 | Reactivation campaigns |
| Big Spenders | M 4–5, F 2–3, R 3–4 | Nurture for loyalty |
| Lost | R 1, F 1–2, M 1–2 | Exit surveys / cut losses |
| Others | Mixed | General campaigns |

### Step 8 — Visualizations

1. **Customer Count per Segment** — bar chart showing distribution across segments
2. **Revenue Contribution per Segment** — bar chart with % labels
3. **Recency vs Monetary Scatter Plot** — colored by segment to spot patterns
4. **Pareto Analysis** — dual-axis chart showing how top 20% of customers drive ~80% of revenue

---

## How to Run

1. Clone or download the repository
2. Place both CSV files in the same directory as the notebook
3. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
4. Open `miniproject_complete.ipynb` in Jupyter Notebook or JupyterLab
5. Update the file paths in cells 1 and 4 to match your local directory
6. Run all cells top to bottom (`Kernel → Restart & Run All`)

---

## Key Findings

- **1,000 unique customers** across Indian metro and tier-2 cities
- **23,050 transactions** analyzed over the dataset period
- Reference date set to **2025-07-30** (max transaction date + 1 day)
- Recency ranges from **1 to 524 days**
- Frequency ranges from **6 to 38 transactions** per customer
- Monetary value ranges from **₹5,052 to ₹44,785** per customer
- Largest segment: **Others (260 customers)**
- Highest-value segment: **Champions (131 customers)**

---

## Dependencies

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Plotting and visualization |
| `seaborn` | Statistical data visualization |

---

## Author

**Course:** Data Analytics with GenAI — Python Project Assessment  
**Topic:** Customer Data Analysis for Business Insights  
**Institution:** Career 247 (An Adda Education Company)
