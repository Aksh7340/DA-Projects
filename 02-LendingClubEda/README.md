# 🏦 Lending Club — Loan Default EDA

> **Can we identify which borrowers are most likely to default before they do?**  
> An exploratory data analysis of 10,000 Lending Club loans using Python, pandas, and seaborn.

---

## Overview

This project performs end-to-end exploratory data analysis on a Lending Club peer-to-peer lending dataset. The goal is to uncover borrower characteristics and financial signals most strongly associated with loan default (Charged Off status), providing a data-driven foundation for credit risk profiling.

The analysis spans univariate distributions, bivariate comparisons against loan outcome, and multivariate hypothesis testing — with every finding grounded in sample-size-aware interpretation.

---

## Repository Structure

```
lending-club-eda/
│
├── Project1_EDA.ipynb               # Raw EDA notebook (data wrangling + exploration)
├── Lending_Club_EDA_Portfolio.ipynb # Portfolio-grade notebook (clean narrative + insights)
├── result.csv                       # Processed dataset (19 columns, 10,000 loans)
└── README.md
```

---

## Dataset

| Property | Value |
|---|---|
| Source | Lending Club Loan Dataset |
| Raw rows | 10,000 loans |
| Columns selected | 19 |
| After cleaning | 9,976 rows (24 invalid income rows dropped) |
| Closed loans (analysis base) | 452 (Fully Paid + Charged Off only) |

**Selected columns:**
`emp_title`, `emp_length`, `state`, `homeownership`, `annual_income`, `verified_income`, `debt_to_income`, `delinq_2y`, `months_since_last_delinq`, `total_credit_lines`, `account_never_delinq_percent`, `loan_amount`, `term`, `interest_rate`, `installment`, `grade`, `loan_purpose`, `application_type`, `loan_status`

---

## Loan Status Distribution

| Status | Count |
|---|---|
| Current | 9,354 |
| Fully Paid | 445 |
| In Grace Period | 66 |
| Late (31–120 days) | 66 |
| Late (16–30 days) | 38 |
| **Charged Off** | **7** |

> ⚠️ Only **Fully Paid** and **Charged Off** loans have a known final outcome and are used in default analysis. This gives a closed loan sample of 452 — with a 1.55% default rate.

---

## Tech Stack

- **Python 3**
- **pandas** — data wrangling, null handling, groupby
- **numpy** — numerical operations
- **matplotlib** — base charting
- **seaborn** — statistical visualizations (histplot, boxplot)

---

## Analysis Structure

### 1. Data Cleaning
- Dropped 24 rows where `annual_income <= 1` (invalid entries causing DTI nulls)
- `emp_title` → filled nulls with `'NA'` (too high cardinality to group)
- `emp_length` → filled nulls with `'Unknown'` (null = no job record)
- `months_since_last_delinq` → filled nulls with `-1` (informative missingness — null means never delinquent)

### 2. Univariate Analysis
Distribution, skewness, outlier detection, and descriptive stats for:
- Annual income (strong right skew, skewness = 9.07)
- Debt-to-income ratio
- Delinquency history
- Loan grade, purpose, term, installment

### 3. Bivariate Analysis
Each feature compared against `loan_status` (Fully Paid vs Charged Off) using stacked bar charts normalised to percentage within each group.

**Binning strategy:** Continuous variables (annual income, DTI, loan amount, interest rate, installment) were manually binned into business-interpretable ranges rather than quantiles — e.g. income brackets aligned to common salary tiers (<25K, 25K–50K, 50K–75K, etc.), DTI bands reflecting common lending thresholds (<10%, 10–20%, 20–30%, 30–40%, >40%). These cutoffs are not statistically derived and a different binning scheme could produce different patterns.

Key findings:

| Feature | Finding |
|---|---|
| **Debt-to-Income** | Strongest signal — DTI 30–40% defaults at 2.86% vs 0.55% for DTI 10–20% |
| **Income Verification** | Not Verified borrowers default at 1.94% vs 1.09% for Source Verified |
| **Homeownership** | Minimal impact — all groups default within a 1.30–1.75% band |
| **Loan Grade** | No consistent pattern; Grade D highest at 2.67% but sample too small |
| **Annual Income** | No directional trend across income brackets |
| **Interest Rate** | No reliable pattern given sample constraints |

### 4. Multivariate Analysis
Five cross-variable hypotheses tested:

1. **Annual Income × Loan Amount** — No consistent pattern found
2. **DTI × Interest Rate** — Largest sub-group (DTI 10–20% + rate 10–20%) had 0 defaults out of 110 loans; hypothesis not supported
3. **Employment Length × Loan Term** — Sub-groups too small; no reliable conclusion
4. **Loan Grade × Loan Amount** — Most combinations had 0 Charged Off cases
5. **Annual Income × DTI** — No consistent pattern; sample insufficient

---

## Key Findings

*Ordered by strength and consistency of the observed signal.*

**1. DTI showed the clearest directional tendency among the variables analysed.**  
Borrowers in the 30–40% DTI band defaulted at nearly 5× the rate of the 10–20% band (2.86% vs 0.55%), although the limited number of default cases prevents firm conclusions. Of all variables tested, DTI produced the most consistent directional pattern and is the most actionable signal for a credit risk team.

**2. Income verification status is associated with different observed default rates.**  
Source Verified borrowers defaulted at roughly half the rate of Not Verified borrowers (1.09% vs 1.94%), suggesting greater uncertainty associated with unverified applications. The dataset does not measure the cause of this difference — it only captures the observed outcome by verification type.

**3. Loan grade showed a weak and inconsistent pattern.**  
Grade D had the highest observed default rate (2.67%), but differences across grades were small and sample sizes per grade were limited. No reliable monotonic trend emerged — the platform's internal grade alone is not a strong standalone predictor in this sample.

**4. Interest rate and annual income showed no reliable directional signal.**  
Default rates across interest rate brackets and income groups were inconsistent, with several sub-groups having zero defaults. Neither variable alone produced a pattern robust enough to act on.

**5. The sample is too small for a reliable risk model.**  
With only 7 confirmed defaults in the closed loan pool, no multivariate pattern is statistically robust — most sub-group combinations contain zero Charged Off cases. A substantially larger number of default observations would be required before building a reliable predictive model.

**6. Next steps for modelling.**  
The [Lending Club full dataset (2.2M rows)](https://www.kaggle.com/datasets/wordsforthewise/lending-club) or the [Home Credit Default Risk dataset (307K rows)](https://www.kaggle.com/competitions/home-credit-default-risk) would be appropriate for building a production-grade default classifier.

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone https://github.com/Aksh7340/DA-Projects.git
```

### 2. Navigate to the Lending Club project

```bash
cd DA-Projects/02-LendingClubEda

# Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# Launch
jupyter notebook Lending_Club_EDA_Portfolio.ipynb
```

> The notebook expects `result.csv` in the same directory. The raw `loans_full_schema.csv` is not included due to size — the cleaned `result.csv` is the working dataset.

---

## Author

**Akshay Kumar Gurjar**  
Data Analyst | Python · SQL · EDA · Visualization

---

## License

This project is for portfolio and educational purposes.
