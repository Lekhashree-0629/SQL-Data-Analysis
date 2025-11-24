# Zepto Product Data Analysis (SQL Project)

This project contains SQL scripts for cleaning, exploring, and analyzing product-level data from a Zepto-style e-commerce inventory dataset.
The goal is to understand pricing, discounts, inventory, and product performance using SQL.

# Project Overview

The dataset contains product information including:

- SKU ID

- Category

- Product Name

- MRP

- Discount %

- Selling Price

- Available Quantity

- Weight

- Stock Status

The project includes:
-  Data Exploration
- Data Cleaning
- Business Insights
- SQL Transformations

## 1. Table Schema

A table named zepto is created with product-level details:

CREATE TABLE zepto (
    sku_id SERIAL PRIMARY KEY,
    category VARCHAR(120),
    name VARCHAR(150) NOT NULL,
    mrp NUMERIC(8,2),
    discountPercent NUMERIC(5,2),
    availableQuantity INTEGER,
    discountedSellingPrice NUMERIC(8,2),
    weightInGms INTEGER,
    outOfStock BOOLEAN,	
    quantity INTEGER
);

## 2. Data Exploration (EDA)

The project performs basic exploration such as:

- Count Total Rows
SELECT COUNT(*) FROM zepto;

- View Sample Data
SELECT * FROM zepto LIMIT 10;

- Check for NULL Values

Identifies missing values across all fields.

- List All Categories
SELECT DISTINCT category FROM zepto;

- Stock Status Summary
SELECT outOfStock, COUNT(sku_id)
FROM zepto
GROUP BY outOfStock;

- Duplicate Product Names

Detects repeated products with multiple SKUs.

## 3. Data Cleaning

Key cleaning tasks include:

- Remove Items with Invalid Prices

Products with zero MRP or selling price are deleted.

- Convert Paise to Rupees

Price fields are corrected by dividing by 100.

UPDATE zepto
SET mrp = mrp / 100.0,
    discountedSellingPrice = discountedSellingPrice / 100.0;

## 4. Data Analysis & Business Insights
### Q1. Top 10 Best Value Products by Discount %

Identifies highly discounted products.

### Q2. High-MRP Products That Are Out of Stock

Useful for demand planning.

### Q3. Estimated Revenue by Category
SELECT category,
SUM(discountedSellingPrice * availableQuantity) AS total_revenue
FROM zepto
GROUP BY category;

### Q4. Premium Low-Discount Products

MRP > 500 but discount < 10%.

### Q5. Top 5 Categories With Highest Avg Discount

Shows customer-attracting categories.

### Q6. Price Per Gram for Value Comparison

Useful for groceries, snacks, FMCG products.

### Q7. Categorizing Products by Weight

Classification into:

Low (< 1 kg)

Medium (1–5 kg)

Bulk (> 5 kg)

### Q8. Total Inventory Weight by Category

Helps with logistics & warehouse optimization.

## Key Insights From the Analysis

- Identify high-demand items that are out of stock
- Understand revenue contribution by each category
- Detect duplicate SKUs and potential catalog issues
- Find most discounted product segments
- Evaluate product value using price-per-gram
- Estimate total inventory weight for supply chain planning
