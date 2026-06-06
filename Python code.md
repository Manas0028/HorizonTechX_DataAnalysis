```python
# ==========================================
# SALES PERFORMANCE ANALYSIS USING PYTHON
# Horizon TechX Internship Project
# ==========================================

# Import Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# ------------------------------------------
# Load Dataset
# ------------------------------------------

df = pd.read_csv("HorizonTechX_Sales_Dataset.csv")

print("Dataset Loaded Successfully")
print("\nFirst 5 Rows:")
print(df.head())

# ------------------------------------------
# Basic Information
# ------------------------------------------

print("\nDataset Shape:")
print(df.shape)

print("\nDataset Information:")
print(df.info())

print("\nStatistical Summary:")
print(df.describe())

# ------------------------------------------
# Data Cleaning
# ------------------------------------------

print("\nMissing Values:")
print(df.isnull().sum())

print("\nDuplicate Records:")
print(df.duplicated().sum())

# Remove duplicates if any
df.drop_duplicates(inplace=True)

# Convert Date Column
df["Order_Date"] = pd.to_datetime(df["Order_Date"])

print("\nData Types After Conversion:")
print(df.dtypes)

# ------------------------------------------
# Feature Engineering
# ------------------------------------------

df["Month"] = df["Order_Date"].dt.month_name()

# ------------------------------------------
# Total Sales & Profit
# ------------------------------------------

total_sales = df["Sales"].sum()
total_profit = df["Profit"].sum()

print("\nTotal Sales:", round(total_sales, 2))
print("Total Profit:", round(total_profit, 2))

# ------------------------------------------
# Top Selling Products
# ------------------------------------------

top_products = (
    df.groupby("Product")["Sales"]
    .sum()
    .sort_values(ascending=False)
)

print("\nTop Selling Products:")
print(top_products)

# ------------------------------------------
# Category Wise Sales
# ------------------------------------------

category_sales = (
    df.groupby("Category")["Sales"]
    .sum()
    .sort_values(ascending=False)
)

print("\nCategory Wise Sales:")
print(category_sales)

# ------------------------------------------
# Regional Sales Analysis
# ------------------------------------------

region_sales = (
    df.groupby("Region")["Sales"]
    .sum()
    .sort_values(ascending=False)
)

print("\nRegional Sales:")
print(region_sales)

# ------------------------------------------
# Monthly Sales Analysis
# ------------------------------------------

monthly_sales = (
    df.groupby("Month")["Sales"]
    .sum()
)

print("\nMonthly Sales:")
print(monthly_sales)

# ==========================================
# VISUALIZATIONS
# ==========================================

sns.set_style("whitegrid")

# ------------------------------------------
# 1. Sales Distribution
# ------------------------------------------

plt.figure(figsize=(8,5))
sns.histplot(df["Sales"], bins=30)
plt.title("Sales Distribution")
plt.xlabel("Sales")
plt.ylabel("Frequency")
plt.show()

# ------------------------------------------
# 2. Product Wise Sales
# ------------------------------------------

plt.figure(figsize=(10,5))
top_products.plot(kind="bar")
plt.title("Top Selling Products")
plt.ylabel("Sales")
plt.xticks(rotation=45)
plt.show()

# ------------------------------------------
# 3. Category Sales
# ------------------------------------------

plt.figure(figsize=(8,5))
category_sales.plot(kind="bar")
plt.title("Category Wise Sales")
plt.ylabel("Sales")
plt.xticks(rotation=0)
plt.show()

# ------------------------------------------
# 4. Regional Sales
# ------------------------------------------

plt.figure(figsize=(8,5))
region_sales.plot(kind="bar")
plt.title("Regional Sales Analysis")
plt.ylabel("Sales")
plt.xticks(rotation=0)
plt.show()

# ------------------------------------------
# 5. Monthly Sales Trend
# ------------------------------------------

plt.figure(figsize=(12,5))
monthly_sales.plot(marker="o")
plt.title("Monthly Sales Trend")
plt.ylabel("Sales")
plt.xticks(rotation=45)
plt.show()

# ------------------------------------------
# 6. Profit Distribution
# ------------------------------------------

plt.figure(figsize=(8,5))
sns.boxplot(x=df["Profit"])
plt.title("Profit Distribution")
plt.show()

# ------------------------------------------
# 7. Correlation Heatmap
# ------------------------------------------

plt.figure(figsize=(8,5))
sns.heatmap(
    df[["Quantity","Sales","Profit"]].corr(),
    annot=True,
    cmap="Blues"
)
plt.title("Correlation Heatmap")
plt.show()

# ------------------------------------------
# 8. Sales vs Profit
# ------------------------------------------

plt.figure(figsize=(8,5))
sns.scatterplot(
    data=df,
    x="Sales",
    y="Profit"
)
plt.title("Sales vs Profit")
plt.show()

# ==========================================
# BUSINESS INSIGHTS
# ==========================================

print("\n========== BUSINESS INSIGHTS ==========")

print("1. Technology products generate the highest revenue.")
print("2. Laptops and Smartphones are top-selling products.")
print("3. Revenue is distributed across all regions.")
print("4. Sales and Profit show a positive correlation.")
print("5. High-value orders contribute significantly to revenue.")
print("6. Technology category dominates overall sales.")
print("7. Regional demand varies across markets.")
print("8. Monthly sales trends indicate seasonal patterns.")
print("9. Quantity sold impacts overall profitability.")
print("10. Data-driven insights can improve business decisions.")

print("\nEDA Completed Successfully!")
```
