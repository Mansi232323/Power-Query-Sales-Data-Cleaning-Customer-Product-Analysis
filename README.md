Power Query Sales Data Cleaning & Customer Product Analysis

📌 Project Overview

This project demonstrates how Microsoft Excel Power Query can be used to clean, transform, standardize, and summarize a messy sales dataset containing 10,000+ sales records.

The project focuses on transforming raw sales data into a structured dataset that is easier to analyze and use for reporting.

🎯 Objectives

The main objectives of this project are:

Clean inconsistent and messy sales data.

Combine first and last names into a single customer name.

Standardize product, city, and payment-mode values.

Clean currency values and convert prices into numeric values.

Convert mixed date formats into a consistent Indian date format.

Handle duplicate customer-product combinations.

Calculate total quantity purchased by each customer for each product.

Create a customer-level summary where each customer appears only once.

Combine products and their corresponding quantities into readable lists.

📂 Dataset

The dataset contains 10,000+ sales records with fields such as:

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

Product/order price

Purchase Date

Date of purchase

City

Customer city

Payment Mode

Payment method

Email

Customer email

Raw Dataset

The Excel workbook used for this project is:

Messy_Sales_Data_10000_PowerQuery.xlsx

🧹 Data Cleaning Performed

1. Name Transformation

First Name and Last Name were combined to create:

Full_Name

Example:

Rohan + Singh → Rohan Singh

2. Product Name Standardization

Inconsistent values such as:

laptop

Laptop

LAPTOP

were standardized to:

Laptop

3. City Standardization

City names with inconsistent capitalization were cleaned.

Example:

delhi, DELHI, Delhi → Delhi

4. Payment Mode Standardization

Payment modes were standardized.

Example:

upi, UPI → UPI

5. Price Cleaning

Currency symbols and unnecessary characters were removed from the Price column.

Examples:

₹63,915 → 63915

Rs 52896 → 52896

€8,067 → 8067

The cleaned Price column was converted into a numeric data type.

6. Date Transformation

Mixed date formats were converted into valid dates and standardized to the Indian date format:

DD-MM-YYYY

7. Duplicate Product Handling

Customer and product combinations were grouped together.

For example:

Rohan Singh | Camera | 1
Rohan Singh | Camera | 3

was transformed into:

Rohan Singh | Camera | 4

where the quantity was calculated using Sum.

🔄 Customer Product Summary

After cleaning and grouping the data, a second grouping operation was performed using Full_Name.

The final structure contains:

Full_Name

Product_List_Names

Quantity_of_Product

Example:

Full_Name

Product_List_Names

Quantity_of_Product

Rohan Singh

Camera, Mobile, Laptop

4, 3, 5

Neha Patel

Laptop, Camera, Tablet

7, 2, 5

The customer name appears only once, while products and their corresponding quantities are displayed together.

🛠️ Power Query Techniques Used

This project uses the following Power Query features:

Change Data Type

Trim Text

Replace Values

Merge Columns

Reorder Columns

Remove Columns

Group By

Sum Aggregation

All Rows

Custom Column

Text.Combine()

List.Transform()

List.Distinct()

Date Transformation

Numeric Transformation

Data Standardization

📊 Transformation Logic

The main customer-product transformation follows this process:

Raw Sales Data
      ↓
Clean & Standardize Data
      ↓
Create Full_Name
      ↓
Group By Full_Name + Product Name
      ↓
Sum Quantity
      ↓
Group By Full_Name
      ↓
Create Product List
      ↓
Create Quantity List
      ↓
Final Customer Summary

📸 Project Screenshots

Raw Sales Data



Before Cleaning



Cleaning Process



Adding New Columns



Before Grouping



Grouping Data



Final Power Query Result



Query Performed



Tasks



💡 Key Learning

This project helped demonstrate how Power Query can automate repetitive data-cleaning tasks instead of manually editing thousands of rows.

The most important transformation was converting transaction-level data into a customer-level product summary while preserving the relationship between products and their quantities.

🚀 Tools Used

Microsoft Excel

Power Query

Power Query M Language

