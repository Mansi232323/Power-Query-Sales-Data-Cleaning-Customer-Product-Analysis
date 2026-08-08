# 📊 Power Query Sales Data Cleaning & Transformation Project

## 📌 Project Overview

This project demonstrates a complete **Sales Data Cleaning and Transformation workflow using Microsoft Excel Power Query**.

The dataset contains **10,000+ sales records** with messy and inconsistent data such as:

* Inconsistent product names
* Different customer name formats
* Mixed price formats
* Different date formats
* Inconsistent city names
* Inconsistent payment modes
* Duplicate customer-product combinations
* Different data types

The objective was to transform this raw dataset into a **clean, standardized, and analysis-ready dataset** using Power Query.

---

## 🎯 Project Objectives

The main objectives of this project were:

1. Clean the raw sales dataset.
2. Standardize text values.
3. Combine First Name and Last Name.
4. Clean and standardize Product Name.
5. Clean Price values.
6. Convert Price into numeric format.
7. Convert Purchase Date into a proper date.
8. Standardize date format to Indian format.
9. Standardize City and Payment Mode.
10. Group data by Customer and Product.
11. Calculate total quantity for each Customer-Product combination.
12. Remove duplicate Customer-Product combinations.
13. Create a Product List for every customer.
14. Create a corresponding Quantity List.
15. Create a final customer-level summary.

---

# 📂 1. Raw Dataset

The original dataset contains **10,000+ sales transactions**.

### Main Columns

| Column        | Description             |
| ------------- | ----------------------- |
| Order ID      | Unique order identifier |
| Product Name  | Product purchased       |
| First Name    | Customer first name     |
| Last Name     | Customer last name      |
| Quantity      | Quantity purchased      |
| Price         | Product price           |
| Purchase Date | Purchase date           |
| City          | Customer city           |
| Payment Mode  | Payment method          |
| Email         | Customer email          |

### Raw Data

![Raw Sales Data](Images/10k%2B%20SALES%20DATA.png)

The raw dataset intentionally contains inconsistent values so that different Power Query transformations can be performed.

---

# 📝 2. Power Query Tasks

The following tasks were performed on the dataset.

![Power Query Tasks](Images/TASKS.png)

### Tasks Performed

* Merge First Name and Last Name
* Create Full Name
* Standardize Product Name
* Standardize City
* Standardize Payment Mode
* Clean Price
* Remove currency symbols
* Remove commas from Price
* Convert Price to number
* Convert Purchase Date to date
* Standardize dates
* Group Customer + Product
* Sum Quantity
* Remove duplicate combinations
* Group by Customer
* Create Product List
* Create Quantity List
* Create final customer summary

---

# 🧹 3. Before Data Cleaning

The raw dataset contains several inconsistencies.

![Before Cleaning](Images/BEFORE%20CLEANING%20DATA%20IN%20PQ.png)

### Product Name

The same product appears in different formats:

```text
Laptop
laptop
LAPTOP
```

These values need to be standardized.

### City

```text
Delhi
delhi
DELHI
```

These should become one consistent value.

### Payment Mode

```text
UPI
upi
```

These also need standardization.

### Price

Prices appear in different formats:

```text
₹63,915
Rs 52896
₹27,989
50223
€8,067
```

These values cannot be directly used for numerical analysis.

### Purchase Date

Dates appear in different formats:

```text
02-27-2024
19/09/2025
2025-03-31
06/04/2025
```

These need to be converted into a proper date type.

---

# 🧼 4. Data Cleaning

Power Query was used to clean the raw dataset.

![After Cleaning](Images/AFTER%20CLEANING%20DATA%20IN%20PQ.png)

### Cleaning Operations

The following transformations were performed:

* Trimmed unnecessary spaces
* Standardized text
* Replaced inconsistent values
* Removed unwanted characters
* Cleaned currency values
* Converted data types
* Standardized dates
* Removed unnecessary columns
* Renamed columns
* Created custom columns

The main advantage of Power Query is that the entire process is **repeatable and refreshable**.

---

# 👤 5. Creating Full Name

Initially, the dataset had two separate columns:

```text
First Name
Last Name
```

For example:

```text
Rohan | Singh
```

These were merged into:

```text
Rohan Singh
```

![Adding New Column](Images/ADDING%20NEW%20COLUMN%20IN%20A%20DATA.png)

### Why Create Full Name?

A single `Full_Name` column makes customer-level grouping easier.

Instead of using:

```text
First Name + Last Name
```

we can simply use:

```text
Full_Name
```

---

# 💰 6. Price Cleaning

The Price column contained values such as:

```text
₹63,915
Rs 52896
₹27,989
50223
€8,067
```

Currency symbols and separators were removed.

### Example

```text
₹63,915 → 63915
Rs 52896 → 52896
₹27,989 → 27989
€8,067 → 8067
```

After cleaning, the Price column was converted into a numeric data type.

This allows further calculations such as:

* Total Sales
* Average Price
* Minimum Price
* Maximum Price
* Revenue Analysis

---

# 📅 7. Purchase Date Cleaning

The Purchase Date column contained mixed formats.

Examples:

```text
02-27-2024
19/09/2025
2025-03-31
06/04/2025
```

Power Query was used to convert these values into a proper date type.

The required Indian date format is:

```text
DD-MM-YYYY
```

For example:

```text
31-03-2025
19-09-2025
06-04-2025
```

This makes the dataset suitable for:

* Year analysis
* Month analysis
* Quarter analysis
* Date filtering
* Sales trend analysis

---

# 🧩 8. Adding New Columns

Additional columns were created during the cleaning and transformation process.

![After Adding New Columns](Images/AFTER%20ADD%20NEW%20COLUMNS%20RESULTS%20IN%20PQ.png)

These include:

* `Full_Name`
* Cleaned Price
* Cleaned Date
* Custom/helper columns

---

# 🔄 9. Grouping Customer + Product

This is one of the most important steps in the project.

The data was grouped using:

```text
Full_Name
Product Name
```

Then Quantity was aggregated using:

```text
SUM
```

### Example

Before grouping:

| Full Name   | Product | Quantity |
| ----------- | ------- | -------: |
| Rohan Singh | Camera  |        1 |
| Rohan Singh | Camera  |        3 |
| Rohan Singh | Mobile  |        2 |
| Rohan Singh | Mobile  |        1 |

After grouping:

| Full Name   | Product | Total Quantity |
| ----------- | ------- | -------------: |
| Rohan Singh | Camera  |              4 |
| Rohan Singh | Mobile  |              3 |

This removes duplicate Customer-Product combinations while keeping the correct total quantity.

---

# 📊 10. Group By Result

![After Grouping](Images/AFTER%20GROUPING%20DATA.png)

The Group By operation creates a unique combination of:

```text
Full_Name + Product Name
```

and calculates:

```text
Total Quantity
```

For example:

```text
Rohan Singh | Camera | 4
Rohan Singh | Mobile | 3
Rohan Singh | Laptop | 5
```

---

# 🧱 11. Grouping by Customer

After calculating total quantity for each Customer-Product combination, the data was grouped again by:

```text
Full_Name
```

The grouped data contains a nested table for each customer.

For example:

```text
Rohan Singh
    ├── Camera → 4
    ├── Mobile → 3
    └── Laptop → 5
```

This structure allows us to create the final customer summary.

---

# 📋 12. Creating Product List

A Custom Column was created to combine all products purchased by a customer.

### Power Query M Code

```powerquery
Text.Combine(
    List.Transform([Data][Product Name], each Text.From(_)),
    ", "
)
```

### Result

Instead of:

```text
Rohan Singh | Camera
Rohan Singh | Mobile
Rohan Singh | Laptop
```

we get:

```text
Rohan Singh | Camera, Mobile, Laptop
```

---

# 🔢 13. Creating Quantity List

A second Custom Column was created for the corresponding quantities.

### Power Query M Code

```powerquery
Text.Combine(
    List.Transform([Data][Total Quantity], each Text.From(_)),
    ", "
)
```

### Result

```text
Product:
Camera, Mobile, Laptop

Quantity:
4, 3, 5
```

Therefore:

```text
Camera → 4
Mobile → 3
Laptop → 5
```

The position of each quantity corresponds to the product at the same position.

---

# 🎯 14. Final Output

The final requirement was:

> **Customer name should appear only once, with all products and their corresponding quantities.**

### Final Structure

| Full Name   | Product List           | Quantity |
| ----------- | ---------------------- | -------- |
| Rohan Singh | Camera, Mobile, Laptop | 4, 3, 5  |
| Neha Patel  | Laptop, Camera, Tablet | 7, 2, 5  |
| Priya Gupta | Tablet, Computer       | 5, 2     |

### Final Clean Dataset

![Final Clean Data](Images/SALES_CLEAN_DATA%20AFTER%20USING%20PQ.png)

---

# 🔍 15. Power Query Applied Steps

The entire transformation process is visible in the **Applied Steps** section.

![Query Performed](Images/QUERY%20PERFORMED.png)

### Transformation Flow

```text
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
Product List
 ↓
Quantity List
 ↓
Final Customer Summary
```

This makes the transformation process easy to understand, reproduce, and refresh.

---

# 🧠 16. Power Query M Functions Used

### Text.Combine

Used to combine multiple values into one text string.

```powerquery
Text.Combine(List, ", ")
```

### List.Transform

Used to transform each value inside a list.

```powerquery
List.Transform(
    [Data][Product Name],
    each Text.From(_)
)
```

### Text.From

Converts a value into text.

```powerquery
Text.From(_)
```

### Table.Group

Used to group rows and perform aggregation.

```powerquery
Table.Group(
    Source,
    {"Full_Name", "Product Name"},
    {
        {
            "Total Quantity",
            each List.Sum([Quantity]),
            Int64.Type
        }
    }
)
```

---

# 📈 17. Business Value

This cleaned dataset can help answer important business questions.

### Customer Analysis

* What products does each customer purchase?
* How many units did each customer purchase?
* Which customers purchased multiple products?

### Product Analysis

* Which products have the highest quantity?
* Which products are purchased most frequently?
* Which products are purchased by the same customers?

### Sales Analysis

The cleaned data can also be used for:

* Revenue analysis
* Monthly sales analysis
* City-wise sales
* Payment mode analysis
* Product performance
* Customer segmentation

---

# 🛠️ 18. Tools & Technologies

### Tools Used

* Microsoft Excel
* Power Query
* Power Query M

### Skills Demonstrated

* Data Cleaning
* Data Transformation
* Data Standardization
* Data Aggregation
* Group By
* Custom Columns
* Text Transformation
* List Transformation
* Date Transformation
* Numeric Transformation
* Data Type Conversion
* Customer-Level Analysis

---

# 📁 19. Repository Structure

```text
Power-Query-Sales-Data/
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
│
└── README.md
```

---

# 🔄 20. Complete Transformation Workflow

```text
10,000+ Raw Sales Records
          ↓
      Data Profiling
          ↓
     Data Cleaning
          ↓
 Text Standardization
          ↓
     Merge Names
          ↓
    Clean Prices
          ↓
    Clean Dates
          ↓
   Change Data Types
          ↓
Group Customer + Product
          ↓
    Sum Quantity
          ↓
 Remove Duplicate
 Customer-Product Rows
          ↓
   Group by Customer
          ↓
  Create Product List
          ↓
  Create Quantity List
          ↓
Final Customer Summary
```

---

# ⭐ 21. Key Learning Outcomes

Through this project, I gained practical experience in:

* Working with messy sales data
* Building a repeatable Power Query workflow
* Cleaning inconsistent text
* Standardizing categories
* Cleaning currency values
* Handling mixed date formats
* Merging columns
* Creating custom columns
* Grouping data
* Aggregating quantities
* Working with nested tables
* Using Power Query M
* Creating customer-level summaries
* Preparing data for dashboards

---

# 🚀 22. Future Improvements

This project can be extended into a complete **Sales Analytics Dashboard**.

Future analysis can include:

* 💰 Total Revenue
* 📦 Total Quantity Sold
* 🏆 Top Products
* 👤 Top Customers
* 📅 Monthly Sales Trend
* 🌍 City-wise Sales
* 💳 Payment Mode Analysis
* 📊 Product-wise Revenue
* 🔎 Customer Segmentation
* 📈 Excel Dashboard
* 📊 Power BI Dashboard

---

# 👩‍💻 Author

## Mansi Kushwaha

**Aspiring Data Analyst | Excel | Power Query | SQL | Python | Power BI**

This project demonstrates practical experience in **data cleaning, transformation, aggregation, and analysis using Microsoft Excel Power Query**.

---

## ⭐ Project Highlights

> **10,000+ Raw Records → Cleaned → Standardized → Grouped → Aggregated → Customer-Level Sales Summary**

If you found this project useful, feel free to explore the Excel workbook and transformation screenshots in this repository.
