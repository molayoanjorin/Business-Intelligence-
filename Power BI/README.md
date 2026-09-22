# Business Performance Intelligence Dashboard

## Project Overview 

This project focuses on building an interactive Business Performance Intelligence Dashboard using Microsoft Power BI.

The objective was to transform raw sales data into an interactive business intelligence solution that allows management to understand:

* How the business is performing
* What is driving revenue and profitability
* Which products, categories, customers, regions, and salespeople are performing well
* Where performance is weaker
* Where management should focus its attention

Rather than simply displaying sales figures, the dashboard was designed to answer specific business questions and turn the analysis into meaningful business insights.

## Business Problem

Management needed a clearer view of the company’s sales and profitability performance.

The raw data contained information about sales transactions, products, customers, employees, dates, payment methods, and sales channels, but the information was not presented in a way that made it easy to identify trends or performance gaps.

The key business questions were:

#### Revenue & Sales Performance

* What is the total revenue generated?
* Which month recorded the highest sales?
* Which products generate the most revenue?
* Which product categories perform best?
* Which regions generate the most sales?

#### Profitability 

* Which categories are the most profitable?
* Which products have the highest profit margins?
* Are there products generating high revenue but relatively low profit?
* Are there salespeople generating strong sales but weaker profitability?

#### Customer Performance 

* Which customer segment generates the most revenue?
* Which region has the highest number of customers?
* What payment method is most commonly used?

#### Sales Performance 

* Who are the top-performing salespeople?
* Which salespeople have high sales but weaker profit?
* Which regions are underperforming?

The dashboard was therefore designed to provide management with a single interactive view of these areas.

## Tools & Technologies 

#### Microsoft Power BI

Used for:

* Data transformation
* Data modelling
* DAX calculations
* Interactive visualizations
* Dashboard development
* Business intelligence analysis

#### Power Query

Used for:

* Data cleaning
* Handling missing values
* Removing duplicates
* Standardizing categories
* Preparing the dataset for analysis

#### DAX

Used to create business metrics and calculations such as:

* Total Sales
* Total Quantity
* Total Cost
* Total Profit
* Profit Margin %
* Total Orders
* Total Products
* Average Order Value
* Sales Growth %
* Previous Month Sales
* Previous Year Sales
* Average Quantity per Order

#### Excel

The original dataset was provided in Excel format and contained the different fact and dimension tables used in the Power BI model.

## Dataset
The dataset was provided as an Excel workbook containing several related tables.

#### Fact_Sales

The main transactional table containing individual sales records.

Key fields included information such as:

* Order ID
* Order Date
* Product ID
* Customer ID
* Employee/Salesperson information
* Quantity
* Unit Price
* Discount
* Payment Method
* Sales Channel
* Order Status

#### Dim_Products

Contained product-related information including:

* Product ID
* Product Name
* Category
* Brand
* Unit Cost
* Unit Price

#### Dim_Customers

Contained customer information including:

* Customer ID
* Customer Type/Segment
* Region
* State
* City

#### Dim_Employees

* Employer ID
* Employee Name
* Department
* Job Level
* Region

#### Dim_Date

A dedicated date dimension used for time-based analysis such as:

* Year
* Quarter
* Month
* Month Number
* Month Name

The dataset covers sales activity across 2024–2026.

## Data Preparation 

Before building the dashboard, the dataset was cleaned to improve data quality and ensure that the analysis was reliable.

1. Checked Data Types

Columns were reviewed to make sure they had appropriate data types.

Examples included:

* Dates → Date
* Quantity → Whole Number
* Sales/Cost values → Decimal/Currency
* IDs → appropriate text/number formats

This was important because incorrect data types can affect calculations, relationships, filtering, and visualizations.

2. Removed Duplicate Records

Duplicate records were checked in the Fact_Sales table.

This prevented the same transaction from being counted more than once in the analysis.

3. Handled Missing Values

Blank values were identified across the dataset.

Examples included:

* Missing Discount values
* Missing City values
* Missing Brand values

These were reviewed and handled appropriately during the data preparation process so they would not unnecessarily distort the analysis.

4. Standardized Inconsistent Categories

Inconsistent category values were identified.

For example, payment/channel values appeared with different capitalization or spacing, such as:

* Sales
* sales

and:

* Online
* online

These categories were standardized so that the same category would not appear as separate values in Power BI slicers and charts.

5. Date Table

The Date Table was sorted to support time-based analysis.

The Date Table included:

* Date
* Year
* Quarter
* Month
* Month Number

A Month Number column was also used to ensure that months were displayed chronologically rather than alphabetically.

For example:

January → February → March → April

instead of:

April → August → December → February

## Data Model 

The project followed a star-schema style model, with Fact_Sales serving as the central fact table and the dimension tables providing descriptive information.

The main relationships were:

* Dim_Date[Date] → Fact_Sales[Order_Date]
* Dim_Customers[Customer_ID] → Fact_Sales[Customer_ID]
* Dim_Products[Product_ID] → Fact_Sales[Product_ID]
* Dim_Employees → Fact_Sales through the relevant employee/salesperson key

The dimension tables contain the descriptive attributes, while Fact_Sales contains the transactional records.

This structure allowed filters from dimensions such as Date, Product, Customer, Region, and Salesperson to affect the sales analysis.

## Key DAX Measures 
1. Total Sales
   Total Sales = SUM(Fact_Sales[Net_Sales])

2. Total Quantity
   Total Quantity = SUM(Fact_Sales[Quantity])

3. Total Profit
   Total Profit = [Total Sales] - [Total Cost]

4. Total Orders
   Total Orders = DISTINCTCOUNT(Fact_Sales[Order_ID])

5. Total Product
   Total Products = DISTINTCOUNT(Dim_Products[Product_Name])

6. Total Cost
   Total Cost = SUMX(Fact_Sales,Fact_Sales[Quantity] * RELATED(Dim_Products[Unit_Cost]))

7. Total Customers
   Total Customers = DISTINCTCOUNT(Fact_Sales[Customer_ID])

8. Profit Margin
   Profit Margin % = DIVIDE([Total Profit],[Total Sales])

9. Average Order Value
   Average Order Value = DIVIDE([Total Sales],[Total Orders])

10. Average Quantity per Order
   Average Quantity per Order = DIVIDE([Total Quantity],[Total Orders])

11. Previous Month Sales
   Previous Month Sales = CALCULATE([Total Sales],DATEADD(Dim_Date[Date], -1, MONTH))

12. Previous Year Sales
    Previous Year Sales = CALCULATE([Total Sales], DATEADD(Dim_Date[Date], -1, YEAR))

13. Sales Growth %
    Sales Growth % = DIVIDE([Total Sales] - [Previous Month Sales],[Previous Month Sales])

## Dashboard Design

The dashboard was divided into three main pages.

#### 1. Executive Overview

The first page provides a high-level view of overall business performance.

#### KPI Cards

The page includes key metrics such as:

* Total Sales
* Total Profit
* Total Orders
* Total Customers
* Total Quantity 
* Average Quantity per Order

#### Visualizations

The page also includes:

* Monthly and Yearly Sales Trend
* Sales by Product
* Sales by Category
* Sales by Region
* Sales by Segment
* Orders by Payment Method

#### Slicers

Interactive slicers were added for dimensions such as:

* Year
* Channel
* Region
* Category

This allows management to explore the overall performance from different perspectives.

#### 2. Sales & Profit Analysis

The second page focuses on understanding what is driving business performance.

#### KPI Cards

The page includes key metrics such as:

* Total Sales
* Total Profit
* Profit Margin %
* Total Orders
* Average Order Value
* Total Products

The analysis includes:

* Sales vs Profit (Monthly Trend)
* Top 10 Salesperson by Sales
* Top 10 Customers by Sales
* Customers by Region
* Sales vs Profit by Salesperson 
* Product Performance Summary highlighting the products sold, category, total sales, total orders, total profit, and profit margin %

The same slicers were used to allow users to filter the analysis.

This page moves beyond simply asking “What are sales?” and focuses on “What is driving those sales and how profitable they are.”

#### 3. Management Analysis

The third page translates the analysis into areas that management can focus on.

The page highlights:

* Biggest opportunities
* Biggest problem 
* Strong-performing segments
* Weak-performing segments 
* Products requiring attention
* Recommended business actions

The goal of this page was to move from data → insight → potential management action.

## Key Business Insights

The analysis produced several important findings:

Overall Business Performance:
The business generated approximately 183.09B in sales and 42.71B in profit, resulting in an overall 23.33% profit margin.

Revenue Performance:
Computers emerged as the leading revenue-generating product category, while the South South recorded the strongest regional sales performance.

Customer Performance:
Retail customers contributed 17.3 billion to the sales, making them a key customer segment for the business.

Sales Trends: 
January 2025 recorded the highest monthly sales, highlighting a period of particularly strong business activity.

Product Performance:
Flash Drive emerged as the top revenue-generating individual product, followed by other high-performing products such as Mini PC Headset, Scanner, Modem, and Keyboard.

Profitability:
The analysis showed that high revenue does not necessarily mean high profitability. Some products and salespeople generated strong sales while requiring further investigation from a profit-margin perspective.

This was particularly important because management decisions should not be based on revenue alone.

## Dashboard Features

The dashboard also included several interactive features.

#### Slicers

Users can filter the dashboard by relevant business dimensions.

#### Tooltips

A dedicated report-page tooltip was created to provide additional information when hovering over products.

The tooltip displays metrics such as:

* Sales
* Profit
* Profit Margin
* Quantity
* Orders

#### Page Navigation

Navigation buttons were added to make it easier to move between:

* Executive Overview
* Sales & Profit Analysis
* Management Analysis

This created a more structured dashboard experience rather than treating each page as a separate report.

## Skills Demonstrated

Through this project, I developed and demonstrated skills in:

* Microsoft Power BI
* Power Query
* DAX
* Data Cleaning
* Data Transformation
* Data Modelling
* Star Schema Design
* Relationship Management
* KPI Development
* Data Visualization
* Business Intelligence
* Exploratory Data Analysis
* Dashboard Design
* Business Storytelling

## Conclusion

The Business Performance Intelligence Dashboard demonstrates how raw data can be transformed into an interactive business intelligence solution.

By combining data preparation, modelling, DAX, visualization, and business analysis, the dashboard provides management with a clearer understanding of sales performance, profitability, customers, products, regions, and areas requiring further attention.

The goal was to build a report that helps answer:

* What is happening?
* Why is it happening?
* Where are the opportunities or problems?
* What should management investigate or focus on next?

This project is part of my ongoing data analytics journey, where I am focused on developing practical skills by working through real-world business problems and learning how to communicate data-driven insights effectively.

