# SuperStore Sales Analysis

**Domain:** Retail / E-commerce  
**Tools:** Python, pandas, NumPy, matplotlib, seaborn, scipy  
**Dataset:** Sample Superstore — 9,994 orders across 4 years (2014–2017)  
**Status:** Complete

---

## Business Problem

SuperStore is experiencing **declining average order value (AOV) year-on-year** despite growing order volumes. High-discount orders are generating negative profit margins. This analysis identifies which **categories, regions, and discount bands are destroying margin** to inform a targeted pricing and retention strategy.

---

## Analysis Structure

| Section | Focus |
|---|---|
| 1. Setup & Understanding | Load data, inspect shape, nulls, types |
| 2. Cleaning & Feature Engineering | Derived columns, bins, type fixes |
| 3. Observations | Who, what, where — top-level findings |
| 4. Trend Analysis | How metrics change over time |
| 5. Root Cause Analysis | Why profit is declining |
| 6. Recommendations | Priority interventions with scores |
| 7. Executive Summary | 4-bullet decision-ready output |

---

## Key Findings

**1. Discounts above 25% destroy margin**  
14.7% of all orders carry a discount above 25%. These orders average **−22% margin**. Orders at 50%+ discount average **−77% margin**. The 25% threshold is a hard cliff.

**2. Three sub-categories are structurally loss-making**  
Tables (−8.6% avg margin), Bookcases (−3.9%), and Supplies (−2.5%) lose money on every average order despite generating significant revenue.

**3. AOV declining despite order growth**  
Orders grew 66% from 2014–2017, but AOV fell from $243 → $221. The business is growing by volume but losing value per customer.

**4. Home Office is the healthiest, most under-invested segment**  
Highest margin (14.3%), lowest average discount (13%), but fewest orders (1,783 vs 5,191 Consumer). Best unit economics with most room to grow.

---

## Recommendations

| Priority | Action | Owner | Impact |
|---|---|---|---|
| P1 | Cap all discounts at 25%; require VP approval above | Pricing team | High |
| P1 | Audit Tables, Bookcases, Supplies costs — reprice or discontinue | Category team | High |
| P2 | Set minimum order value threshold for free shipping to lift AOV | Marketing | Medium |
| P2 | Launch targeted Home Office acquisition campaign | Sales team | Medium |

---

## Statistical Methods Used

- Descriptive statistics (mean, median, std dev, IQR)
- Feature engineering (profit margin %, discount bins, loss flags)
- Grouped aggregations (Region × Category, Segment health scorecard)
- Time series trend analysis (YoY orders, AOV, margin)
- Min-max normalisation for composite scoring
- Root cause analysis via discount band segmentation

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/yourusername/da-projects.git
cd da-projects/01-superstore-sales-analysis

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scipy

# 3. Add the dataset
# Download from: https://www.kaggle.com/datasets/vivek468/superstore-dataset-final
# Place superstore.csv in this folder

# 4. Open the notebook
jupyter notebook SuperStore.ipynb
```

---

## Dataset

**Source:** [Kaggle — Sample Superstore](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)  
**Size:** 9,994 rows × 21 columns  
**Columns:** Order ID, Order Date, Ship Date, Customer, Segment, Region, Category, Sub-Category, Sales, Quantity, Discount, Profit

> The dataset file (`superstore.csv`) is not included in this repo. Download it from Kaggle and place it in this folder before running the notebook.

---

## Project Structure

```
01-superstore-sales-analysis/
├── SuperStore.ipynb     ← Full analysis notebook
└── README.md            ← This file
```
