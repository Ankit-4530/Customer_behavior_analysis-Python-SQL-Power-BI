#Customer Shopping Behaviour Analysis

A complete Data Analytics Project that analyzes customer purchasing behavior to extract meaningful business insights using Python, SQL, and Power BI.

This project demonstrates the full data analytics workflow: data cleaning, database analysis, and business intelligence visualization.

Dashboard Preview

Interactive dashboard built in Microsoft Power BI to analyze customer purchase behaviour and business insights.

#Project Overview

Understanding customer purchasing behaviour helps businesses improve marketing strategies, product positioning, and customer retention.

This project analyzes customer transaction data to identify:

Top performing products

Customer purchase patterns

Discount influence on sales

Customer segmentation

Category-wise purchasing trends

The final results are presented through an interactive business dashboard.

Tools & Technologies Used

Python

Pandas

Jupyter Notebook

PostgreSQL

Microsoft Power BI

Dataset Description

The dataset contains customer purchase records including demographic and transaction information.

Key Columns
Column	Description
customer_id	Unique customer identifier
age	Age of customer
gender	Customer gender
category	Product category
item_purchased	Product purchased
purchase_amount	Purchase amount
review_rating	Customer review rating
discount_applied	Indicates if discount was applied
previous_purchases	Number of previous purchases
Project Workflow
Raw Dataset
      ↓
Data Cleaning (Python & Pandas)
      ↓
Database Storage (PostgreSQL)
      ↓
SQL Business Analysis
      ↓
Dashboard Visualization (Power BI)
      ↓
Business Insights
Data Cleaning & Preparation

Data preprocessing was performed using Pandas.

Key steps included:

Standardizing column names

Handling missing values

Creating derived columns (age group segmentation)

Data validation and consistency checks

Example transformation:

data.columns = data.columns.str.lower()
data.columns = data.columns.str.replace(' ', '_')

Missing values in review_rating were filled using category-wise median values.

SQL Business Analysis

Data was loaded into PostgreSQL for querying and analysis.

Top Rated Products
SELECT item_purchased,
ROUND(AVG(review_rating)::numeric,2) AS avg_rating
FROM customer
GROUP BY item_purchased
ORDER BY avg_rating DESC
LIMIT 5;
Discount Usage by Product
SELECT item_purchased,
ROUND(100.0 * AVG(CASE WHEN discount_applied='Yes' THEN 1 ELSE 0 END),2) AS discount_rate
FROM customer
GROUP BY item_purchased
ORDER BY discount_rate DESC
LIMIT 5;
Customer Segmentation

Customers were segmented based on their purchase history.

WITH customer_type AS (
SELECT customer_id,
CASE
WHEN previous_purchases = 1 THEN 'New'
WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
ELSE 'Loyal'
END AS customer_segment
FROM customer
)

SELECT customer_segment, COUNT(*)
FROM customer_type
GROUP BY customer_segment;
Top Products per Category

Using SQL Window Functions:

ROW_NUMBER() OVER(PARTITION BY category ORDER BY COUNT(customer_id) DESC)

This identifies the Top 3 most ordered products in each category.

Power BI Dashboard

An interactive dashboard was created using Power BI to visualize the insights.

Dashboard Features

Category wise purchase analysis

Customer demographic insights

Discount impact analysis

Product performance comparison

Customer segmentation insights

Interactive Filters (Slicers)

Users can analyze data dynamically using:

Product Category

Gender

Age Group

Discount Applied

Product Type

Key Insights

Some key insights derived from the analysis:

Certain product categories drive the majority of sales.

Discounts significantly influence purchase behaviour for specific products.

Returning customers represent a major portion of transactions.

Some products consistently receive higher customer ratings.

Loyal customers contribute significantly to repeat purchases.

Skills Demonstrated

Data Cleaning & Preprocessing

Exploratory Data Analysis

SQL Querying

Window Functions

Customer Segmentation

Business Intelligence Dashboard Development

Project Structure
customer-shopping-analysis
│
├── data
│   └── customer_shopping_behavior.csv
│
├── notebooks
│   └── data_analysis.ipynb
│
├── sql_queries
│   └── analysis.sql
│
├── dashboard
│   ├── powerbi_dashboard.pbix
│   └── dashboard_preview.png
│
└── README.md
Future Improvements

Possible extensions for this project:

Predictive models for purchase behaviour

Recommendation systems

Customer lifetime value prediction

Real-time data integration

Author

Ankit Kumar

Aspiring Data Analyst passionate about using data to generate actionable business insights.
