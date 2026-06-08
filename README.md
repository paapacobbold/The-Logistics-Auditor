# Veridi Logistics — Delivery Performance Audit
### An Analysis of the Olist Brazilian E-Commerce Dataset

---

## A. Executive Summary

Veridi Logistics is over-promising and under-delivering on customer expectations. This audit reveals that **8.1% of all delivered orders arrived after the estimated delivery date**, and these delays are directly damaging customer sentiment. Super Late deliveries (>5 days late) receive an average review score of just **1.79/5 — a 2.51 point drop** compared to On Time deliveries (4.29/5). While remote northern states (AL, MA, PI) show the highest late percentages, **São Paulo generates the most customer damage** due to its sheer order volume, making it the #1 priority for logistics intervention. The CEO's gut feeling is correct: late deliveries are the primary driver behind the rise in negative customer reviews.

---

## B. Project Links

- **Notebook:** [https://github.com/paapacobbold/The-Logistics-Auditor/blob/main/delivery_audit.ipynb] 
- **Dashboard:** [https://app.powerbi.com/view?r=eyJrIjoiZTUxNmZlNDUtNDQyNy00YjU5LThhZDYtNTY5ZjNhZWI0YjEyIiwidCI6IjEwNGQ4MDQ4LWZkMGMtNDNkNS1hNjMwLWZjNjI5ZTVkYWI1OSJ9]
- **Presentation:** [https://knustedugh-my.sharepoint.com/:p:/g/personal/pkandamcobbold_st_knust_edu_gh/IQCt81ZHZhtYR6JDVsk8ElDvAcBgvll8Kou4MQGGjlQA3M0?e=Sly1n5]


---

## C. Technical Explanation

### Data Cleaning Approach
The analysis joined 6 raw CSV files (orders, reviews, customers, products, order items, and translations) into a single master dataset using `pandas.merge`. Three key cleaning steps were applied:

1. **Avoiding row duplication** — Order items were aggregated to order-level before joining, preventing the 1-to-many relationship from inflating row counts.
2. **Filtering undelivered orders** — Orders with statuses like `cancelled` or `unavailable` were excluded from delay analysis, as they lack delivery dates.
3. **Date parsing** — Date columns were converted from strings to datetime objects to enable arithmetic for delay calculation.

The final dataset contained ~97,000 delivered orders enriched with customer location, review scores, and product categories.

### Candidate's Choice: The "Damage Score" Metric

**The Problem with Simple Late % Rankings:**
A state with a 30% late rate but only 100 orders is less damaging to the business than a state with a 10% late rate and 10,000 orders. Yet a naive ranking by late percentage would prioritise the smaller market.

**The Solution — Damage Score:**
Damage Score = (Number of Late Orders) × (5 - Average Review Score)

This metric weights two factors that matter most to the business:
- **Volume of affected customers** — how many people had a bad experience
- **Severity of dissatisfaction** — how unhappy those customers were

**The Key Insight This Revealed:**
São Paulo (SP) appears to perform reasonably well at 5.9% late rate. However, with 2,393 late orders, it generates the highest Damage Score of all states — significantly more than Rio de Janeiro (RJ) which has a much higher 13.5% late rate. This means the CEO's repair efforts should focus on **São Paulo first**, not the states with the highest late percentages.

This insight would be invisible to standard reporting and demonstrates the value of designing business-aligned metrics.

---

## D. Repository Structure
The-Logistics-Auditor/
├── data/                          # Raw CSVs (gitignored)
├── charts/                        # Exported visualisations
├── delivery_audit.ipynb           # Main analysis notebook
├── delivery_audit.html            # HTML export of notebook
├── README.md                      # This file
└── .gitignore

### How to Reproduce
1. Clone this repository
2. Download the Olist dataset from [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) into a `data/` folder
3. Open `delivery_audit.ipynb` in Jupyter
4. Run all cells top to bottom

---

## E. Tools Used
- **Python** (pandas, numpy) — data manipulation
- **Matplotlib & Seaborn** — visualisations in notebook
- **Power BI** — interactive dashboard
- **Jupyter Notebook** — analysis environment
- **GitHub** — version control & hosting

---
