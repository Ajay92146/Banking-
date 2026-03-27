# Banking Data Analytics — Python, SQL & Power BI

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=flat&logo=powerbi&logoColor=black)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=flat&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=flat&logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-4C72B0?style=flat&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?style=flat&logo=numpy&logoColor=white)

---

## Problem Statement

> Develop a basic understanding of **risk analytics in banking and financial services** and understand how data is used to **minimise the risk of losing money while lending to customers**.

The goal is to build a dashboard system that helps a bank make loan approval decisions based on an applicant's financial profile — predicting whether the applicant is likely to repay the loan, and approving or rejecting accordingly.

---

## Solution

Interactive Power BI dashboards built using the latest Power BI tools that help banks make data-driven decisions based on each applicant's profile — including loan history, deposits, income band, risk weighting, and engagement length.

---

## Project Structure

```
Banking--main/
│
├── data/
│   ├── banking-clients.csv          # Main dataset — 3,000 clients, 25 columns
│   ├── banking-realtionships.csv    # Banking relationship types
│   ├── gender.csv                   # Gender reference table
│   └── investment-advisiors.csv     # Investment advisor mapping
│
├── notebooks/
│   ├── BankEDA_v1.ipynb             # Version 1 — initial exploration
│   └── BankEDA_v2.ipynb             # Version 2 — full analysis (main)
│
├── Dashboard/
│   └── Banking Dashboard (2025).pbix  # Final Power BI dashboard
│
├── designs/
│   ├── New Design/                  # Final dashboard screenshots
│   │   ├── Home.png
│   │   ├── Loan Analysis.png
│   │   ├── Deposit Analysis.png
│   │   ├── Summary.png
│   │   └── Drill Through.png
│   └── Demo Design/                 # Alternate design iteration
│
├── outputs/                         # All EDA chart exports (30+ PNGs)
│
├── reports/
│   ├── Banking Report.docx          # Full written project report
│   └── Banking.xlsx                 # Supporting data workbook
│
└── README.md
```

---

## About the Dataset

The dataset contains information about bank clients across **multiple interlinked tables** connected through primary and foreign keys.

| Table | Description |
|-------|-------------|
| Clients - Banking | Main table — 3,000 clients, 25 features |
| Banking Relationship | Relationship type per client |
| Gender | Gender reference data |
| Investment Advisor | Advisor assignments |
| Period | Time period reference |

**Key columns:** Client ID, Age, Nationality, Occupation, Estimated Income, Fee Structure, Loyalty Classification, Risk Weighting, Bank Loans, Business Lending, Credit Card Balance, Bank Deposits, Saving Accounts, Checking Accounts, Foreign Currency Account, Superannuation Savings, Properties Owned, Joined Bank

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy, Matplotlib, Seaborn) | Data cleaning, EDA, visualisation |
| Jupyter Notebook | Interactive analysis environment |
| Power BI (DAX) | Dashboard, KPIs, calculated measures |
| Microsoft Word | Final written report |

---

## Data Cleaning (Power BI & Python)

Four key transformations applied to the dataset:

1. **Engagement Timeframe** — New column showing the timeline of each client in the bank
2. **Engagement Days** — `DATEDIFF([Joined Bank], TODAY(), DAY)` — number of days since joining
3. **Income Band** — Estimated Income bucketed into three tiers:
   - Low → `< 100,000`
   - Mid → `100,000 – 300,000`
   - High → `> 300,000`
4. **Processing Fees** — Derived from Fee Structure column (e.g. High fee structure → 5% processing fee)

---

## DAX Measures & KPIs

| KPI | DAX Formula | Description |
|-----|-------------|-------------|
| Total Clients | `DISTINCTCOUNT('Clients - Banking'[Client ID])` | Total unique clients |
| Total Loan | `[Bank Loan] + [Business Lending] + [Credit Cards Balance]` | Combined loan exposure |
| Bank Loan | `SUM('Clients - Banking'[Bank Loans])` | Total bank loans |
| Business Lending | `SUM('Clients - Banking'[Business Lending])` | SME / business loans |
| Total Deposit | `[Bank Deposit] + [Savings Account] + [Foreign Currency Account] + [Checking Accounts]` | Total client deposits |
| Total Fees | `SUMX('Clients - Banking', [Total Loan] * 'Clients - Banking'[Processing Fees])` | Revenue from processing fees |
| Bank Deposit | `SUM('Clients - Banking'[Bank Deposits])` | Total bank deposits |
| Checking Accounts | `SUM('Clients - Banking'[Checking Accounts])` | Daily transaction accounts |
| Savings Account | `SUM('Clients - Banking'[Saving Accounts])` | Interest-bearing savings |
| Foreign Currency | `SUM('Clients - Banking'[Foreign Currency Account])` | Foreign currency holdings |
| Credit Cards Balance | `SUM('Clients - Banking'[Credit Card Balance])` | Outstanding CC balances |
| Total CC Amount | `SUM('Clients - Banking'[Amount of Credit Cards])` | Number of credit cards |
| Engagement Length | `SUM('Clients - Banking'[Engagement Days])` | Total client engagement days |

**DAX functions used:** `SUM`, `SUMX`, `DISTINCTCOUNT`, `SWITCH`, `DATEDIFF`

---

## Python EDA — Analysis Performed

### 1. Data Cleaning
- Converted `Joined Bank` to datetime format
- Created `Income Band` feature using `pd.cut()` with three tiers
- Checked for missing values across all 25 columns
- Generated descriptive statistics for all numerical columns

### 2. Univariate Analysis
Distribution analysis across all key columns — histograms and count plots for: Age, Estimated Income, Superannuation Savings, Credit Card Balance, Bank Loans, Bank Deposits, Checking Accounts, Saving Accounts, Risk Weighting, Nationality, Occupation, Loyalty Classification, Fee Structure, Income Band.

### 3. Cross-Analysis by Nationality
Every major variable broken down by Nationality to identify demographic-level patterns in financial behaviour.

### 4. Correlation Analysis
Full correlation matrix across 11 numerical variables with heatmap. Key findings:

- **Bank Deposits ↔ Saving Accounts** — high positive correlation; clients who deposit actively also maintain savings
- **Age ↔ Superannuation Savings** — older clients accumulate more retirement funds (financial lifecycle pattern)
- **Estimated Income ↔ Checking Accounts** — higher earners maintain larger current account balances
- **Bank Loans ↔ Credit Card Balance** — debt behaviour clusters together; useful for risk profiling

### 5. Scatter Plot Pair Analysis

| Pair | Insight |
|------|---------|
| Bank Deposits vs Saving Accounts | Strong linear relationship |
| Checking Accounts vs Saving Accounts | Moderate positive correlation |
| Age vs Superannuation Savings | Financial lifecycle confirmed |
| Estimated Income vs Checking Accounts | Income-driven account usage |
| Bank Loans vs Credit Card Balance | Debt clustering pattern |
| Business Lending vs Bank Loans | Overlapping borrower profiles |

---

## Power BI Dashboard

The interactive dashboard includes four report pages:

**Home** — Executive summary with all KPI cards (Total Clients, Total Loan, Total Deposit, Total Fees, Engagement Length)

**Loan Analysis** — Loan distribution by nationality, investor type, gender, and risk weighting

**Deposit Analysis** — Deposit trends and savings behaviour across client segments

**Summary** — Overall client demographics combining financial behaviour, income bands, loyalty classification, and engagement metrics

### Dashboard Previews

| Home | Loan Analysis |
|------|--------------|
| ![Home](designs/New%20Design/Home.png) | ![Loan](designs/New%20Design/Loan%20Analysis.png) |

| Deposit Analysis | Summary |
|-----------------|---------|
| ![Deposit](designs/New%20Design/Deposit%20Analysis.png) | ![Summary](designs/New%20Design/Summary.png) |

---

## How to Run

### Python Notebook
```bash
git clone https://github.com/Ajay92146/Banking-.git
cd Banking-
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook notebooks/BankEDA_v2.ipynb
```
Ensure the `data/` folder is present with all CSV files before running.

### Power BI Dashboard
1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. Open `Dashboard/Banking Dashboard (2025).pbix`
3. All visuals and DAX measures load automatically

---

## Conclusion

Power BI dashboards are among the most effective tools for the banking sector. This project demonstrates how a banking operations dashboard can be built with key financial metrics and KPIs to support data-driven lending and risk decisions.

---

## Future Work

- **Loan approval prediction** — Add Machine Learning model (Logistic Regression / Random Forest) to automate risk classification
- **Nationality-level lending insights** — Identify which nationalities carry the highest bank loans to enable targeted risk policies
- **Bank type strategy** — Private banks show the highest client count; insights can help other banks build strategies to grow their client base
- **Deploy online** — Publish dashboard to Power BI Service for live stakeholder access
- **Automate pipeline** — Connect live data sources to Power BI for real-time refresh

---

## Author

**Ajay Yadav**
[GitHub](https://github.com/Ajay92146)

---

*If you found this project useful, please give it a star on GitHub!*
