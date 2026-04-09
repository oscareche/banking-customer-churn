# Bank Customer Churn Analysis

## The Problem

Banks lose customers. That's not news. But understanding *why* they leave, and more importantly *who* is likely to leave next, is the difference between reactive damage control and proactive retention. Customer churn is expensive. Acquiring a new customer costs significantly more than keeping an existing one, and every departure represents lost revenue, lost cross-selling opportunities, and a signal that something in the experience isn't working.

This project takes a dataset of 10,000 bank customers and digs into the patterns behind churn. The goal isn't just to describe what happened. It's to surface actionable insight that a retention team could actually use.

## Business Objectives

1. Who is churning and why?
This profiles customers who leave the bank by their demographic (age, gender, country), financial (balance, credit score, salary), and behavioural (active status, product count, tenure) characteristics to identify the common traits of a churned customer.

2. Where is the risk concentrated?
We will try to quantify churn rates across key customer segments to identify which groups are most vulnerable and represent the greatest volume or financial exposure — so the retention team knows exactly where to focus first.

3. What are the early warning signs?
We will identify patterns and combinations of factors (such as zero balance paired with inactivity, or high product count with short tenure) that signal a customer is at risk of leaving before they actually do.

## The Dataset

Source: [Kaggle - Bank Customer Churn Dataset](https://www.kaggle.com/datasets/gauravtopre/bank-customer-churn-dataset)

10,000 rows. 12 columns. Each row is one customer.

| Column | Description | Type |
|--------|-------------|------|
| customer_id | Unique identifier | Numeric |
| credit_score | Customer's credit score | Numeric |
| country | Customer's country | Categorical |
| gender | Customer's gender | Categorical |
| age | Customer's age | Numeric |
| tenure | Years with the bank | Numeric |
| balance | Account balance | Numeric |
| products_number | Number of bank products held | Numeric |
| credit_card | Has a credit card (1 = yes, 0 = no) | Binary |
| active_member | Is an active member (1 = yes, 0 = no) | Binary |
| estimated_salary | Estimated annual salary | Numeric |
| churn | Left the bank (1 = yes, 0 = no) | Binary |

## Approach
This analysis follows the six phases of the data analysis process: Ask, Prepare, Process, Analyse, Share and Act.

For the **Process** phase, a full health audit was conducted follwoing a cleaning workflow as follows:

- Built a data_health_summary sheet with COUNTA and COUNTBLANK formulas referencing raw_data to assess completeness across all 12 columns
- Result: zero missing values across the entire dataset (100% complete on all columns)
- Checked for and confirmed no duplicate rows
- Removed 2 empty trailing rows (10002-10003) from cleaned_data
- Verified text consistency in categorical columns (country, gender) using filters
- Checked numeric ranges from impossible or suspicious values
- Standardised all column headers to snake_case
- Created derived columns: age_group, balance_salary_ratio, high_product_flag
- Added readable label columns for binary fields with conditional formatting
- Documented every cleaning decision in dedicated data_cleaning_log sheet

## Key Findings

Base churn rate: 20.37% (2,037 out of 10,000 customers left). Every finding below is measured against this benchmark.

**Finding 1: The 46-60 age group is the bank's biggest churn problem**

The 46-60 age bracket churns at 51.12%, which is 2.5 times the base rate. This isn't a single-market issue. It holds across all three countries: Germany (67.33%), France (45.79%), and Spain (40.66%). The 18-30 age group is the most loyal at just 7.52%. Something specific is pushing middle-aged customers away, and it's happening everywhere.

**Finding 2: Customers with 3-4 products churn at catastrophic rates**

82.71% of customers with 3 products left. 100% of customers with 4 products left. Every single one. And critically, even active customers with 3-4 products churn at 80.28%. Activity doesn't protect them. This means the problem is the products themselves, not a lack of engagement. Cross-selling beyond 2 products is actively associated with customer loss.

**Finding 3: Non-zero balance inactive customers are the highest-volume risk group**

Customers with money in their accounts who have gone inactive churn at 31.63%. This group contains 3,105 customers with 982 churners. In absolute terms, this is where the bank loses the most customers and the most revenue. These are people with actual balances who have disengaged and are taking their money elsewhere.

**Finding 4: Zero-balance customers are an opportunity, not a threat**

Zero-balance customers churn at 13.82%, below the base rate. Zero-balance active customers churn at just 9.61%. These customers aren't leaving because they're not losing anything by staying. But they're also not generating revenue. They represent a re-engagement and revenue opportunity rather than a retention risk.

## Business Recommendations

**1. Investigate the 46-60 age group experience**

Commission qualitative research (surveys, exit interviews) with 46-60 year old customers to understand why they're leaving at such elevated rates across all markets. This age group likely has specific financial needs (retirement planning, wealth management, mortgage changes) that the bank may not be serving well.

**2. Audit the 3-4 product portfolio**

Stop aggressive cross-selling beyond 2 products until the bank understands why multi-product customers are leaving at near-total rates. Conduct a product compatibility review to identify whether specific product combinations create friction, fees, or complexity that drives customers away.

**3. Build an inactivity early warning system**

Non-zero balance customers who become inactive represent the highest-volume risk group. The bank should monitor engagement metrics and trigger retention outreach when a customer with a positive balance shows declining activity. The intervention window is between "going quiet" and "formally leaving."

**4. Re-engage zero-balance customers for revenue growth**

Zero-balance customers are not at high risk of leaving, but they represent unrealised revenue. Design targeted campaigns to encourage savings, introduce them to fee-generating products, or offer incentives for account funding. Active zero-balance customers (9.61% churn) are especially receptive since they're already engaged with the bank.

## Limitations

**Snapshot data:** The dataset is a single point in time. There's no way to track how customer behaviour changed over time, when engagement declined, or what sequence of events led to churn. Time-series data would significantly strengthen the early warning analysis.

**Unknown product details:** The dataset tells you how many products a customer holds but not which products. Understanding which specific combinations drive the 3-4 product churn problem requires product-level data.

**Ambiguous "active member" definition:** The criteria for active vs inactive membership are not defined in the dataset. The findings about activity status are directionally useful but the exact threshold for "active" is unknown.

**Estimated salary.** The salary column is explicitly an estimate, not verified income. Salary-based conclusions carry this uncertainty.

**No causal data:** The analysis identifies associations and patterns but cannot determine causation. The 46-60 age group churns at high rates, but the data cannot tell you why. That requires qualitative research.

**Small sample sizes in composite segments:** Some cross-referenced segments (e.g., Germany + 46-60 + 3-4 products at 38 customers) have small sample sizes. Percentage-based findings for these groups should be treated as directional rather than definitive.

**Three countries only:** Findings are limited to France, Germany, and Spain. Patterns may not generalise to other markets.
