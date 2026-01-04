# ecommerce-analysis-sql
End-to-end SQL analysis on e-commerce data
Olist E-commerce SQL Analysis

# Project Overview
This project analyzes the Brazilian Olist e-commerce dataset using SQL Server to derive business insights related to growth, product performance, customer behavior, and delivery operations.

# Dataset
- Source: Olist (Brazilian e-commerce marketplace)
- Tables used: customers, orders, order_items, products, payments, reviews

# Key Objectives
- Analyze monthly growth in orders and revenue
- Identify top-performing product categories and products
- Segment customers into new, repeat, and loyal groups
- Evaluate the impact of delivery time on customer review scores

# Data Cleaning
- Filtered to delivered orders only
- Created a reusable `clean_orders` view
- Handled NULL values and inconsistent data types

# Key Insights
- Revenue is concentrated in a small number of product categories
- Majority of customers are one-time buyers
- Delivery delays correlate with higher low-star review counts
- Fast deliveries (0–2 days) receive consistently higher ratings

# Tools Used
- SQL Server (SSMS)
- SQL (joins, CTEs, window functions, aggregations)

# Files
- `sql/` → All analysis queries
- `insights.md` → Business findings and recommendations
