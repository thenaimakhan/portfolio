# Sales-Dashboard

### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiNmI1OTM2MzktZjFhMy00NmUxLTkzMWEtYzgwNTYxYjA4N2NkIiwidCI6ImZlZTNiOTE2LTAxYzEtNDk4Ny1hNjQ2LWUxOTM0MzJiOWVhYSIsImMiOjl9

# Problem Statement

The goal is to analyze the sales data to identify trends, performance metrics, and key insights that can help the business make data-driven decisions. The focus is on understanding the selling value by various dimensions such as payment mode, sale type, product, category, month, and day.


# Data Description

The dataset comprises two sheets: "Input Data" and "Master Data."

### Input Data

This sheet contains the transactional details of sales, including:

    1. DATE: The date when the transaction occurred.
    2. PRODUCT ID: A unique identifier for each product.
    3. QUANTITY: The quantity of the product sold.
    4. SALE TYPE: The type of sale (e.g., Wholesaler, Online, Direct Sales).
    5. PAYMENT MODE: The payment method used for the transaction (e.g., Cash, Online).
    6. DISCOUNT %: The discount percentage applied to the sale.

### Master Data
This sheet provides detailed information about each product, including:

    1. PRODUCT ID: A unique identifier for each product.
    2. PRODUCT: The name of the product.
    3. CATEGORY: The category to which the product belongs.
    4. UOM: Unit of Measure (e.g., Kg, Lt, Ft).
    5. BUYING PRICE: The cost price of the product.
    6. SELLING PRICE: The selling price of the product.

### Data Integration Using Merged Queries

We used merged queries to join the "Input Data" sheet and the "Master Data" sheet. This integration allowed us to combine transactional details with product information:



    = Table.NestedJoin(#"Inserted Month1", {"PRODUCT ID"}, #"Master Data", {"PRODUCT ID"}, "Master Data", JoinKind.LeftOuter)

### Adding Calculated Columns Using DAX

We added two new calculated columns using DAX expressions in Power BI. The first column, 'Total Selling Value,' was created using the formula:

    Total Selling Value = 'Input Data'[Quantity]*'Input Data'[Master Data.SELLING PRICE]

The second column, 'Total Buying Value,' was created using the formula:

    Total Buying Value = ('Input Data'[Quantity]*'Input Data'[Master Data.BUYING PRIZE])*(1 - 'Input Data'[DISCOUNT %]/100)


### Power BI Measures

We created two measures to analyze profitability: Profit and Profit %:

    1. Profit = SUM('Input Data'[Total Selling Value])-SUM('Input Data'[Total Buying Value])
    2. Profit % = [Profit]/SUM('Input Data'[Total Buying Value])*100


### Snapshot of Power BI Dashboard


![Sample](https://github.com/thenaimakhan/portfolio/assets/112707772/bb949bd6-a220-4184-b4d0-6e4ffe3d3975)

        
# Visuals Description
### KPI Cards

- Sum of Quantity: Displays the total quantity sold, which is 4280 units.
- Profit %: Shows the profit percentage, which is 20.7%.
- Sum of Total Selling Value: Displays the total selling value, which is $401.4K.
- Sum of Total Buying Value: Shows the total buying value, which is $332.5K.
- Profit: Displays the total profit, which is $68.9K.
- Category: Highlights the top category, which is Category04.
- Product: Highlights the top product, which is Product41.

### Total Selling Value by Payment Mode

Donut chart showing the distribution of sales by payment mode: Cash (49.7%) and Online (50.3%).

### Total Selling Value by Sale Type

Donut chart showing the distribution of sales by sale type: Wholesaler (14.78%), Online (33.36%), and Direct Sales (51.86%).

### Total Selling Value by Product

Bar chart showing the selling value of the top products, with Product41 having the highest selling value.

### Total Selling Value by Category

Treemap displaying the selling value by category, with Category04 having the highest selling value.

### Total Selling Value and Profit by Month Name

Bar chart showing the monthly selling value and profit, with January having the highest selling value.

### Total Selling Value by Day

Line chart showing the daily selling value trends.

### Slicers

- Payment Mode: Allows filtering by different payment methods.
- Sale Type: Allows filtering by different sale types.
- Year: Allows filtering data by the year (2021 or 2022).
- Month: Allows filtering data by specific months.

# Insights

Following inferences can be drawn from the dashboard:

### [1] Total Sales and Profit
- Total Quantity Sold: 4280 units
- Total Selling Value: $401.4K
- Total Buying Value: $332.5K
- Total Profit: $68.9K
- Profit Percentage: 20.7%

### [2] Sales by Payment Mode
- Cash: 49.7% of total sales
- Online: 50.3% of total sales

Thus, the sales are almost evenly split between Cash and Online payment modes.

### [3] Sales by Sale Type
- Wholesaler: 14.78% of total sales
- Online: 33.36% of total sales
- Direct Sales: 51.86% of total sales

Thus, Direct Sales are the dominant sale type.

### [4] Top Product
Product41 with the highest selling value

### [5] Top Category
Category04 with the highest selling value ($95.3K)

### [6] Monthly Trends
- Highest Selling Month: January with $48.4K in sales
- Monthly Profit Trend: Consistent profit margins across months

### [7] Daily Trends

Fluctuations observed, with some days significantly outperforming others

# How It Helps the Client
By consolidating various sales metrics into a single interface, the dashboard helps users:

- Track Sales Performance: Users can monitor total sales value, quantity sold, and profitability, providing a clear picture of business performance.

- Identify Trends and Patterns: Visualizations such as line charts for monthly trends and bar charts for daily sales help in identifying seasonal patterns and peak sales periods, aiding in strategic planning and resource allocation.

- Understand Customer Behavior: Donut charts displaying sales distribution by payment mode and sale type provide insights into customer preferences and behaviors, helping tailor marketing and sales strategies.

- Analyze Product Performance: Detailed breakdowns of sales by product and category highlight the top-performing items, allowing clients to focus on key products and optimize inventory.



