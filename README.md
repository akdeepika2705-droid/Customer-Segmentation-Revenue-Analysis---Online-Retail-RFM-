# Customer Segmentation & Revenue Analysis — Online Retail (RFM)

## Overview
This project analyzes ~2 years of transaction data (Dec 2009 – Dec 2011) from a UK-based online retailer to segment customers using **RFM analysis** (Recency, Frequency, Monetary) and uncover actionable business insights around revenue concentration, customer retention, and market dependence.

## Dataset
- **Source**: Online Retail II (UCI/Kaggle)
- **Size**: ~1M+ raw transactions, reduced to **5,878 unique customers** after cleaning
- **Columns**: Invoice, StockCode, Description, Quantity, InvoiceDate, Price, Customer ID, Country

## Data Cleaning
- Removed 243,007 rows with missing `Customer ID` (required for customer-level analysis)
- Identified 18,744 cancelled orders (Invoice starting with 'C'), all matching negative `Quantity` values — removed
- Removed 71 rows with zero/negative `Price` as invalid entries
- Result: clean dataset of valid, positive-value sales transactions

## Methodology: RFM Analysis
- **Recency**: Days since last purchase (relative to a snapshot date = max invoice date + 1 day)
- **Frequency**: Number of distinct orders per customer
- **Monetary**: Total amount spent per customer (`Quantity × Price`)
- Each metric scored into quartiles (1–4) using `pd.qcut()`; scores summed into an `RFM_Score` (3–12)
- Customers mapped into four segments: **Champions, Loyal, At Risk, Lost**

## Key Insights

**1. Revenue is highly concentrated in top customers**
Champions (19% of customers) generate **71% of total revenue**, averaging ₹10,770/customer vs. ₹382/customer for Lost — a ~28x gap.

**2. Retention gap**
27.6% of customers made only one purchase and never returned, closely matching the 38% "Lost" segment.

**3. Heavy UK dependence**
United Kingdom accounts for ~91% of customers and ₹1.47 crore in revenue — over 23x the next-largest market (EIRE). International diversification is minimal.

**4. Product performance: revenue vs. volume**
Top revenue products (Regency Cakestand, White Hanging Heart T-Light Holder) differ from top volume products (World War 2 Gliders), showing that high sales volume doesn't always mean high revenue.

## Business Recommendations
- Prioritize retention campaigns for **At Risk** customers before they become **Lost**
- Investigate onboarding experience — nearly 1 in 4 customers never returns after their first order
- Explore international market expansion given the UK's heavy concentration risk
- Use revenue **and** volume together when evaluating product performance

## Tools Used
`pandas`, `Jupyter Notebook`

## Future Extensions
- Visualizations (bar/line charts) for segment and revenue trends
- Cohort/retention analysis over time
- Predictive modeling (e.g., churn risk scoring)
