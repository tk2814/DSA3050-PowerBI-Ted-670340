# DSA3050 ENDSEM EXAM

## 1. Project Overview

This project was developed as part of the DSA 3050A – Business Intelligence & Data Visualization End Semester Practical Examination.

The project uses Microsoft Power BI to transform a raw product sales dataset into an interactive Business Intelligence solution.

The complete workflow follows:

Dataset → Power Query → Data Model → DAX → Dashboard → Business Insights

The main objective is to analyze sales performance, profitability, customers, products, categories, geographical regions, and time trends to support data-driven business decisions.

---

## 2. Dataset

### Dataset Name

Product Sales Dataset 2023–2024

### Dataset Source

The dataset was obtained from Kaggle:

https://www.kaggle.com/datasets/yashyennewar/product-sales-dataset-2023-2024

### Dataset Size

- Records: 200,000
- Columns: 14
- Time Period: 2023–2024

### Dataset Description

The dataset contains product sales transactions with information about orders, customers, products, geographical locations, quantity, unit price, revenue, and profit.

The dataset was selected because it contains numerical and categorical variables, date information, geographical dimensions, and business measures that support meaningful Business Intelligence analysis.

---

## 3. Why This Dataset Was Selected

The dataset was selected because it provides sufficient complexity for Business Intelligence analysis and supports the requirements of the practical examination.

The dataset supports:

- Sales analysis
- Profitability analysis
- Product analysis
- Customer analysis
- Regional analysis
- Time-series analysis
- KPI development
- Interactive Power BI dashboards

---

## 4. Data Dictionary

| Field | Description | Data Type |
|---|---|---|
| Order_ID | Unique identifier for an order | Text |
| Order_Date | Date on which the order was placed | Date |
| Customer_Name | Name of the customer | Text |
| City | City associated with the transaction | Text |
| State | State associated with the transaction | Text |
| Region | Geographical region | Text |
| Country | Country associated with the transaction | Text |
| Category | Main product category | Text |
| Sub_Category | Product sub-category | Text |
| Product_Name | Name of the product | Text |
| Quantity | Number of units sold | Whole Number |
| Unit_Price | Price per unit | Decimal Number |
| Revenue | Revenue generated from the transaction | Decimal Number |
| Profit | Profit generated from the transaction | Decimal Number |

---

## 5. Business Problem

The business needs to understand its sales and profitability performance across products, customers, categories, geographical regions, and time periods.

The Power BI solution analyzes revenue, profit, quantity sold, and customer and product performance to identify trends, high-performing areas, and areas requiring management attention.

The analysis is intended to provide management with a clear understanding of overall performance and support data-driven decision-making.

---

## 6. Analytical Questions

The Power BI solution is designed to answer the following questions:

1. What is the total revenue generated?
2. What is the total profit generated?
3. How does revenue change over time?
4. Which product categories generate the most revenue?
5. Which products generate the highest profit?
6. Which customers contribute the most revenue?
7. Which geographical regions perform best?
8. Which products or regions have low profitability?
9. How does sales quantity relate to revenue and profit?
10. How has revenue changed compared with the previous year?

---

## 7. Power Query – Data Cleaning and Transformation

Power Query was used to prepare the raw dataset for analysis.

### 7.1 Rename and Clean Column Names

Problem:
Some field names contained unnecessary spaces or inconsistent naming.

Transformation:
Column names were renamed and standardized.

Reason:
Consistent column names improve readability and make the fields easier to reference in Power BI and DAX.

Result:
The dataset contains clear and consistent field names.

### 7.2 Correct Data Types

Problem:
Some columns required appropriate data types for analysis.

Transformation:
Data types were reviewed and corrected.

Reason:
Correct data types are necessary for accurate calculations, filtering, and time-based analysis.

Result:
Date, text, whole number, and decimal number fields were assigned appropriate data types.

### 7.3 Clean Text Fields

Problem:
Text fields can contain unnecessary leading or trailing spaces.

Transformation:
Trim and Clean transformations were applied to relevant text columns.

Reason:
This prevents values that should be identical from being treated as separate categories.

Result:
Text fields were standardized for analysis.

### 7.4 Check Missing Values

Problem:
Missing or null values can affect calculations and visualizations.

Transformation:
Relevant columns were inspected for missing and null values.

Reason:
Missing values need to be identified before analysis to reduce the possibility of misleading results.

Result:
Missing values were reviewed and handled where necessary.

### 7.5 Check Duplicate Records

Problem:
Duplicate records can cause incorrect totals and inflated analytical results.

Transformation:
The dataset was checked for duplicate records.

Reason:
Checking for duplicates improves data quality and prevents duplicate transactions from affecting the analysis.

Result:
Duplicate records were reviewed and handled where appropriate.

### 7.6 Extract Year

Problem:
The original date field does not directly provide a convenient year dimension.

Transformation:
The year was extracted from Order_Date.

Reason:
Year is required for comparing sales and profit across different periods.

Result:
A Year field was created.

### 7.7 Extract Month

Problem:
Monthly sales trends need to be analyzed.

Transformation:
The month was extracted from Order_Date.

Reason:
This allows revenue and profit trends to be analyzed at monthly level.

Result:
A Month field was created.

### 7.8 Extract Quarter

Problem:
Quarterly performance was not directly available.

Transformation:
A quarter field was extracted from Order_Date.

Reason:
Quarterly analysis can help identify changes in performance throughout the year.

Result:
A Quarter field containing Q1, Q2, Q3, and Q4 was created.

### 7.9 Create Profit Status

Problem:
It is useful to distinguish profitable transactions from loss-making transactions.

Transformation:
A conditional column was created using the Profit field.

Reason:
This provides an additional classification for profitability analysis.

Result:
Transactions were classified according to their profitability.

### 7.10 Create Dimension Tables

Problem:
A single flat table is not ideal for analytical modelling.

Transformation:
Reference queries were used to create dimension tables.

Reason:
Dimension tables support a structured star-schema model and improve filtering and analytical organization.

Result:
Customer, Product, Location, and Date dimension tables were created.

---

## 8. Data Model

A Star Schema was developed for the Power BI data model.

### FactSales

The FactSales table contains transactional information such as:

- Order ID
- Order Date
- Customer
- Product
- Location
- Quantity
- Unit Price
- Revenue
- Profit

### DimDate

Contains:

- Date
- Year
- Quarter
- Month
- Month Number

### DimCustomer

Contains customer information used for customer-level analysis.

### DimProduct

Contains:

- Product
- Category
- Sub-Category

### DimLocation

Contains:

- City
- State
- Region
- Country

### Relationships

One-to-many relationships were established between the dimension tables and the FactSales table.

The dimensions filter the FactSales table using appropriate single-direction relationships.

The dedicated Date table supports time-based analysis and time-intelligence calculations.

---

## 9. DAX Measures

A minimum of 12 meaningful DAX measures were created to support the Business Intelligence analysis.

### 9.1 Total Revenue

Total Revenue = SUM(FactSales[Revenue])

Calculates the total revenue generated from sales transactions.

### 9.2 Total Profit

Total Profit = SUM(FactSales[Profit])

Calculates the total profit generated from sales.

### 9.3 Total Quantity

Total Quantity = SUM(FactSales[Quantity])

Calculates the total number of units sold.

### 9.4 Total Orders

Total Orders = DISTINCTCOUNT(FactSales[Order_ID])

Calculates the number of unique orders.

### 9.5 Average Revenue

Average Revenue = AVERAGE(FactSales[Revenue])

Calculates the average revenue per transaction.

### 9.6 Average Profit

Average Profit = AVERAGE(FactSales[Profit])

Calculates the average profit per transaction.

### 9.7 Profit Margin %

Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)

Measures profit as a percentage of total revenue.

### 9.8 Average Order Value

Average Order Value = DIVIDE([Total Revenue], [Total Orders], 0)

Measures the average revenue generated per order.

### 9.9 Profitable Orders

Profitable Orders = CALCULATE([Total Orders], FactSales[Profit] > 0)

Calculates the number of orders that generated positive profit.

### 9.10 Loss Orders

Loss Orders = CALCULATE([Total Orders], FactSales[Profit] < 0)

Calculates the number of orders that generated a loss.

### 9.11 Previous Year Revenue

Previous Year Revenue = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(DimDate[Date]))

Calculates revenue for the corresponding period in the previous year.

### 9.12 YoY Revenue Growth %

YoY Revenue Growth % = DIVIDE([Total Revenue] - [Previous Year Revenue], [Previous Year Revenue], 0)

Measures the percentage change in revenue compared with the previous year.

---

## 10. Important DAX Measures

The six most important DAX measures selected for detailed documentation are:

1. Total Revenue
2. Total Profit
3. Profit Margin %
4. Average Order Value
5. Previous Year Revenue
6. YoY Revenue Growth %

These measures were selected because they provide important information about sales performance, profitability, order value, and changes in performance over time.

The main DAX functions used include:

- SUM()
- AVERAGE()
- DISTINCTCOUNT()
- DIVIDE()
- CALCULATE()
- SAMEPERIODLASTYEAR()

The results of these measures change according to the filter context created by dimensions such as Date, Product, Customer, Category, and Location.

---

## 11. Dashboard Design

Three interactive Power BI report pages were developed.

The dashboard structure follows:

Overview → Detailed Analysis → Deeper Insights

### 11.1 Page 1 – Executive Overview

The Executive Overview provides management with a quick understanding of overall business performance.

KPI Cards:

- Total Revenue
- Total Profit
- Total Orders
- Profit Margin %

Visualizations:

- Monthly Revenue Trend
- Revenue by Category
- Profit by Region
- Revenue by Sub-Category

Slicers:

- Year
- Region
- Category

Main Question:

What happened?

### 11.2 Page 2 – Product and Customer Analysis

This page provides detailed analysis of product and customer performance.

Visualizations:

- Top 10 Products by Revenue
- Top 10 Customers by Revenue
- Profit by Category
- Quantity versus Revenue
- Category and Sub-Category Performance Matrix

Slicers:

- Category
- Sub-Category
- Region

Main Question:

Where is the sales performance coming from?

### 11.3 Page 3 – Regional and Diagnostic Analysis

This page investigates regional performance and profitability.

Visualizations:

- Revenue by geographical location
- Profit by Region
- Revenue and Profit over time
- Bottom 10 Products by Profit
- Regional Performance Matrix

Additional Analysis:

Conditional formatting is used to highlight strong and weak profitability.

Main Question:

Why are some areas performing better or worse, and what requires attention?

---

## 12. Power BI Interactivity

The report uses several interactive features, including:

- Slicers
- Cross-filtering
- Drill-down
- Interactive charts
- Filter context
- Dashboard navigation

These features allow users to explore different aspects of the dataset and interact with the analytical results.

---

## 13. Key Insights

The final business insights are based on the results generated by the completed Power BI dashboard.

The analysis focuses on:

- Highest-performing products
- Highest-performing categories
- Most profitable regions
- Top customers
- Revenue trends
- Profitability trends
- Loss-making products or regions
- Year-over-year revenue changes

Specific numerical findings will be added after the final dashboard has been completed and validated.

---

## 14. Business Recommendations

The recommendations are based on the findings from the Power BI analysis.

Potential recommendations include:

1. Focus on high-performing products and categories.
2. Investigate products generating low or negative profit.
3. Strengthen performance in high-potential regions.
4. Monitor customers contributing significant revenue.
5. Monitor monthly and yearly sales trends.
6. Use profitability analysis when making product and regional decisions.

Final recommendations will be updated according to the actual results obtained from the dashboard.

---

## 15. Project Screenshots

Screenshots are included to demonstrate the progressive development of the Business Intelligence solution.

The screenshots include:

- Raw dataset
- Power Query transformations
- Completed data model
- DAX measures
- Executive dashboard
- Detailed analysis dashboard
- Diagnostic insights dashboard


---

## 16. Conclusion

This project demonstrates the complete Business Intelligence workflow from raw sales data to an interactive Power BI solution.

The final solution integrates:

- Data acquisition
- Data cleaning
- Power Query transformations
- Data modelling
- DAX calculations
- Interactive dashboards
- Business analysis
- GitHub documentation

The resulting Business Intelligence solution provides a structured approach to analyzing sales, profitability, customers, products, regions, and time-based performance and supports data-driven business decision-making.
