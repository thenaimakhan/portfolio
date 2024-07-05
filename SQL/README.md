# Data Manipulation in SQL


# Problem Statement

The goal of this project is to analyze and integrate multiple data sources related to Adidas' sales, products, and retailers to generate insights about the brand through the creation of two key performance indicators (KPIs).


# Data Description

The Addidas data in contained in three separate files as below:

### Retailers.csv
*Columns*:

     1. Retailers: Names of the retailers.
     2. IDs: Unique identifiers for the retailers.
     3. Latest sales volume (in billions): Recent sales volume in billions.
     4. Website: Indicates if the retailer has a website.
     5. App: Indicates if the retailer has an app.
     6. Physical Stores: Number of physical stores.
     7. Loyalty Program: Indicates if the retailer has a loyalty program.
   

### Products.csv
*Columns*:

      1. Product_ID: Unique identifier for the products.
      2. Product: Name of the product.
      3. min_price: Minimum price of the product.
      4. max_price: Maximum price of the product.
      5. Type: Type of product (e.g., Footwear, Clothing).
      6. Material: Material of the product.
      7. min_size: Minimum size available.
      8. max_size: Maximum size available.
      9. colors: Number of available colors.
     10. rating: Product rating.
     11. Season: Applicable season for the product.
     12. gender: Target gender for the product.


### Addidas.csv
 *Columns*:

     1. Retailer ID: Identifier for the retailer.
     2. Invoice Date: Date of the invoice.
     3. Region: Geographical region of the sale.
     4. State: State where the sale occurred.
     5. City: City where the sale occurred.
     6. Product_Category_ID: Identifier for the product category.
     7. Price per Unit: Price per unit of the product.
     8. Units Sold: Number of units sold.
     9. Total Sales: Total sales value.
    10. Operating Profit: Profit from operations.
    11. Operating Margin: Margin from operations.
    12. Sales Method: Method of sales (e.g., Online, Outlet).

# Data Manipulation

### Data Cleaning

I used pandas profiling to assess the need for data cleaning. Since no data cleaning was required, I skipped this step. I removed any duplicate rows identified in Excel.

### Data Loading and Joins
   - I loaded the cleaned data into SQL and performed joins between the three tables: 
    1. Addidas_Cleaned
    2. Products
    3. Retailers.

   - *Full Join*:

     
    SELECT * 
    INTO AdidasData
    FROM Addidas_Cleaned
    FULL JOIN Products ON Products.Product_ID = Addidas_Cleaned.Product_Category_ID
    FULL JOIN Retailers ON Retailers.IDs = Addidas_Cleaned.Retailer_ID;
 
This query combined all records from Addidas_Cleaned, Products, and Retailers, including records with no matching entries in other tables.

   - *Inner Join*:
     
    SELECT * 
    INTO Joined_Data
    FROM Addidas_Cleaned
    JOIN Products ON Products.Product_ID = Addidas_Cleaned.Product_Category_ID
    JOIN Retailers ON Retailers.IDs = Addidas_Cleaned.Retailer_ID;

This query combined only the records with matching entries in all three tables.

# KPI Calculations in SQL

### Sales Method Distribution
     
     SELECT Sales_Method AS "Sales Method", COUNT() AS "Sales Count",(COUNT() * 100.0 / (SELECT COUNT(*) FROM AdidasData)) AS "Sales Percentage"
     INTO Sales_Method_Distribution
     FROM AdidasData
     GROUP BY Sales_Method;
This KPI calculates the distribution of sales methods, showing the count and percentage of sales for each method.

### Revenue Contribution by Top Selling Material
     
     SELECT TOP 3 Material, SUM(Total_Sales) AS "TotalSalesRevenue"
     INTO Top_Selling_Material
     FROM AdidasData
     GROUP BY Material
     ORDER BY TotalSalesRevenue DESC;

This KPI identifies the top three materials contributing the most to total sales revenue.



# Snapshot of SQL Queries

### Joins

![2024-07-05 (9)](https://github.com/thenaimakhan/portfolio/assets/112707772/5cc7e71b-945c-495f-b62d-86dade47cb3b)

### KPIs

![2024-07-05 (10)](https://github.com/thenaimakhan/portfolio/assets/112707772/aaff6345-7d83-45eb-83e2-0a60176e94f0)

# Output of KPI Queries

### Sales Method Distribution

![2024-07-05 (11)](https://github.com/thenaimakhan/portfolio/assets/112707772/50326e94-2e8e-4461-bfb1-bc900870fe1c)

### Revenue Contribution by Top Selling Material

![2024-07-05 (12)](https://github.com/thenaimakhan/portfolio/assets/112707772/18f1d0db-b219-4fdf-889b-b683297d0fbd)
