Power Query Sales Data Cleaning & Customer Product Analysis

📊 Power Query Sales Data Cleaning & Transformation Project



📌 Project Overview

This project demonstrates a complete sales data cleaning and transformation workflow using Microsoft Excel Power Query.

The original dataset contains 10,000+ sales records with intentionally messy and inconsistent data. The purpose of the project is to transform this raw dataset into a clean, structured, analysis-ready dataset using Power Query.

The project covers:

Data cleaning

Text standardization

Name transformation

Product standardization

Price cleaning

Date transformation

Data type conversion

Duplicate handling

Grouping and aggregation

Customer-level product analysis

Quantity analysis

Custom columns

Power Query M transformations

🎯 Business Problem

Raw sales data often contains inconsistencies that make analysis difficult.

For example, the same product may appear as:

Laptop
laptop
LAPTOP

The same city may appear as:

Delhi
delhi
DELHI

Prices may appear as:

₹63,915
Rs 52896
50223
€8,067

Dates may appear in different formats:

02-27-2024
19/09/2025
2025-03-31
06/04/2025

Customer names are also stored separately as:

First Name = Rohan
Last Name  = Singh

This project solves these problems using Power Query transformations instead of manually editing thousands of rows.

📂 1. Dataset

The project uses a sales dataset containing 10,000+ records.

Main columns

Column

Description

Order ID

Unique order identifier

Product Name

Product purchased

First Name

Customer first name

Last Name

Customer last name

Quantity

Quantity purchased

Price

Sales price

Purchase Date

Date of purchase

City

Customer city

Payment Mode

Payment method

Email

Customer email

Raw Dataset

The following screenshot shows the original sales data before Power Query cleaning.



What can be observed?

The raw dataset contains:

Inconsistent capitalization

Mixed product names

Mixed city formats

Currency symbols

Commas in prices

Different date formats

First and last names in separate columns

Different payment-mode formats

Missing values in some fields

📝 2. Project Tasks

Before performing the transformation, a list of Power Query tasks was created.

The main tasks were:

Combine First Name and Last Name.

Standardize Product Name.

Standardize City.

Standardize Payment Mode.

Clean Price values.

Convert Price to numeric data type.

Convert Purchase Date to a proper date.

Standardize dates to Indian format.

Group customers by product.

Calculate total quantity for each customer-product combination.

Create a customer-level summary.

Combine products into a single cell.

Combine corresponding quantities into a single cell.

Ensure each customer appears only once.



🧹 3. Before Data Cleaning

Before cleaning, the dataset contains several types of inconsistencies.



Problems identified

Product Name

Examples:

Laptop
laptop
LAPTOP

These are actually the same product but would be treated as different values during analysis.

City

Examples:

Delhi
delhi
DELHI

Again, these should be standardized.

Payment Mode

Examples:

UPI
upi

These should be converted to one consistent value.

Price

Examples:

₹63,915
Rs 52896
₹27,989
50223
€8,067

These values need to be cleaned before numerical analysis.

Purchase Date

Examples:

02-27-2024
19/09/2025
2025-03-31
06/04/2025

The mixed formats require proper date conversion.

🔧 4. Data Cleaning in Power Query

The first major stage was cleaning the raw data using Power Query.



Transformations performed

4.1 Text Cleaning

Text values were standardized to avoid treating different capitalization as separate categories.

Example:

laptop
LAPTOP
Laptop

became:

Laptop

4.2 City Standardization

City names were standardized.

Example:

delhi
DELHI
Delhi

became:

Delhi

4.3 Payment Mode Standardization

Payment modes were standardized.

Example:

upi
UPI

became:

UPI

4.4 Removing Unwanted Characters

Unnecessary characters were removed from fields where required.

This makes the data suitable for calculations and grouping.

👤 5. Creating Full Name

The original dataset contains:

First Name
Last Name

For customer-level analysis, these fields were combined into a single column:

Full_Name

For example:

First Name = Rohan
Last Name  = Singh

Result:

Rohan Singh



Why create Full_Name?

A single customer identifier makes grouping and summarization much easier.

Instead of grouping separately by:

First Name
Last Name

we can simply use:

Full_Name

💰 6. Cleaning the Price Column

The Price column contains different currency representations.

Examples:

₹63,915
Rs 52896
₹27,989
50223
€8,067

These values cannot reliably be used for calculations until they are converted into a consistent numeric format.

Transformation

Unwanted currency symbols and separators were removed.

Examples:

₹63,915 → 63915
Rs 52896 → 52896
₹27,989 → 27989
€8,067 → 8067

The cleaned column was then converted to a numeric data type.

Why?

Once Price is numeric, we can perform:

SUM

AVERAGE

MIN

MAX

Grouped sales analysis

Revenue calculations

📅 7. Cleaning the Purchase Date

The dataset contains mixed date formats.

Examples:

02-27-2024
19/09/2025
2025-03-31
06/04/2025

Power Query was used to convert these values into proper dates.

The final date representation is intended to follow the Indian format:

DD-MM-YYYY

Example:

31-03-2025
19-09-2025
06-04-2025

Why is this important?

Correct date types allow us to perform:

Month analysis

Year analysis

Quarterly analysis

Date filtering

Time-series analysis

Sales trends

🧩 8. Adding and Transforming Columns

After the initial cleaning, additional columns were created to make the dataset easier to analyze.



Examples include:

Full_Name

Clean Price

Clean Date

Other calculated/helper columns

Power Query allows these transformations to be performed consistently across the entire dataset.

🔄 9. Grouping Customer + Product

This is one of the most important steps in the project.

The requirement is:

For every customer, identify each unique product and calculate the total quantity purchased.

Therefore, the data was first grouped by:

Full_Name
+
Product Name

Then:

Quantity → Sum

Example

Original data:

Full_Name

Product

Quantity

Rohan Singh

Camera

1

Rohan Singh

Camera

3

Rohan Singh

Mobile

2

Rohan Singh

Mobile

1

Rohan Singh

Laptop

5

After grouping:

Full_Name

Product

Total Quantity

Rohan Singh

Camera

4

Rohan Singh

Mobile

3

Rohan Singh

Laptop

5



📊 10. Group By + Sum Quantity

The first grouping operation uses:

Group By:
Full_Name
Product Name

and:

Operation:
Sum
Column:
Quantity

This prevents duplicate customer-product combinations from appearing multiple times.



Example from the transformation

Instead of:

Rohan Singh | Camera | 1
Rohan Singh | Camera | 3

the result becomes:

Rohan Singh | Camera | 4

This preserves the quantity while eliminating duplicate customer-product combinations.

🧱 11. Creating a Customer-Level Summary

After calculating the total quantity for each customer-product combination, the data is grouped again by:

Full_Name

The operation used is:

All Rows

This creates a nested table for each customer.

For example:

Rohan Singh
    ├── Camera → 4
    ├── Mobile → 3
    └── Laptop → 5

This nested structure is then used to create the final product and quantity lists.

📋 12. Creating Product List

A Custom Column is used to combine the products into one cell.

The Power Query expression is:

Text.Combine(
    List.Transform([Data][Product Name], each Text.From(_)),
    ", "
)

Result

Instead of:

Rohan Singh | Camera
Rohan Singh | Mobile
Rohan Singh | Laptop

we get:

Rohan Singh | Camera, Mobile, Laptop

This makes the customer summary much more compact.

🔢 13. Creating Quantity List

A second Custom Column is created for the corresponding quantities.

Text.Combine(
    List.Transform([Data][Total Quantity], each Text.From(_)),
    ", "
)

Result

If the products are:

Camera, Mobile, Laptop

the corresponding quantities are:

4, 3, 5

The position of each quantity corresponds to the product in the same position.

Therefore:

Camera → 4
Mobile → 3
Laptop → 5

🎯 14. Final Customer-Level Output

The final output contains one row per customer.

Final structure

Full_Name

Product_List_Names

Quantity_of_Product

Rohan Singh

Camera, Mobile, Laptop

4, 3, 5

Neha Patel

Laptop, Camera, Tablet

7, 2, 5

Priya Gupta

Tablet, Computer

5, 2

The customer name is no longer repeated.



🔍 15. Query Steps

The project was performed using a sequence of Power Query transformations.



The query includes operations such as:

Source
↓
Changed Type
↓
Trim Text
↓
Removed Columns
↓
Replaced Values
↓
Merged Columns
↓
Reordered Columns
↓
Added Custom Columns
↓
Changed Data Types
↓
Grouped Rows
↓
Added Custom Columns
↓
Final Clean Dataset

The Applied Steps panel makes the entire transformation process reproducible.

🧠 16. Power Query M Logic

The project also uses Power Query's M language for custom transformations.

Product combination

Text.Combine(
    List.Transform([Data][Product Name], each Text.From(_)),
    ", "
)

Quantity combination

Text.Combine(
    List.Transform([Data][Total Quantity], each Text.From(_)),
    ", "
)

These expressions convert list values into readable comma-separated text.

📈 17. Business Value

This transformation can help businesses answer questions such as:

What products does each customer purchase?

How many units of each product did a customer purchase?

Which customers purchased multiple products?

Which products are frequently purchased together?

How much quantity has each customer purchased?

How can customer purchase history be summarized?

The cleaned dataset can then be used for further analysis in:

Excel

Pivot Tables

Power Pivot

Power BI

SQL

Python

🛠️ 18. Tools & Technologies

Tools

Microsoft Excel

Power Query

Power Query M

Skills Demonstrated

Data Cleaning

Data Transformation

Data Standardization

Data Aggregation

Group By

Custom Columns

Text Transformation

Date Transformation

Numeric Transformation

Data Preparation

Customer-Level Analysis

📁 19. Repository Structure

Power-Query-Sales-Data-Analysis/
│
├── Images/
│   ├── 10k+ SALES DATA.png
│   ├── ADDING NEW COLUMN IN A DATA.png
│   ├── AFTER ADD NEW COLUMNS RESULTS IN PQ.png
│   ├── AFTER CLEANING DATA IN PQ.png
│   ├── AFTER GROUPING DATA.png
│   ├── BEFORE CLEANING DATA IN PQ.png
│   ├── BEFORE GROUPING DATA.png
│   ├── QUERY PERFORMED.png
│   ├── SALES_CLEAN_DATA AFTER USING PQ.png
│   └── TASKS.png
│
├── Messy_Sales_Data_10000_PowerQuery.xlsx
└── README.md

📸 20. Complete Transformation Flow

The complete project can be summarized as:

10,000+ Raw Sales Records
             ↓
       Data Profiling
             ↓
       Data Cleaning
             ↓
     Text Standardization
             ↓
       Name Merging
             ↓
       Price Cleaning
             ↓
       Date Cleaning
             ↓
    Data Type Conversion
             ↓
 Group by Customer + Product
             ↓
       Sum Quantity
             ↓
      Group by Customer
             ↓
    Product List Creation
             ↓
    Quantity List Creation
             ↓
      Clean Customer Summary

⭐ Key Learning Outcomes

Through this project, I learned how to use Power Query to:

Work with messy real-world-style data.

Build repeatable data-cleaning workflows.

Standardize inconsistent text values.

Convert mixed data types.

Clean currency values.

Handle mixed date formats.

Merge columns.

Group and aggregate records.

Calculate total quantities.

Work with nested tables.

Use Power Query M functions.

Convert lists into readable text.

Build customer-level summaries.

🚀 Future Improvements

The cleaned dataset can be extended into a complete sales analytics project by adding:

Total Revenue

Average Order Value

Top Products

Top Customers

Monthly Sales Trends

City-wise Sales

Payment Mode Analysis

Product-wise Revenue

Customer Segmentation

Excel Dashboard

Power BI Dashboard

👩‍💻 Author

Mansi Kushwaha

Aspiring Data Analyst | Excel | Power Query | SQL | Python | Power BI

This project is part of my practical data analytics portfolio and demonstrates hands-on experience with Excel Power Query and data transformation.

⭐ If you found this project useful
