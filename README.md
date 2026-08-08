# 📊 Power Query Sales Data Cleaning & Transformation Project

## 📌 Project Overview

This project demonstrates a complete Sales Data Cleaning and Transformation workflow using **Microsoft Excel Power Query**.

The dataset contains **10,000+ sales records** with inconsistent product names, customer names, prices, dates, cities, payment modes, and other data-quality issues.

The objective is to transform the messy raw sales data into a clean, standardized, and analysis-ready dataset.

---

## 🎯 Project Objectives

The main objectives of this project are:

1. Clean the raw sales dataset.
2. Standardize text values.
3. Merge First Name and Last Name.
4. Standardize Product Name.
5. Clean Price values.
6. Convert Price into numeric format.
7. Convert Purchase Date into proper date format.
8. Standardize City and Payment Mode.
9. Group data by Customer and Product.
10. Calculate Total Quantity.
11. Remove duplicate Customer-Product combinations.
12. Create Product and Quantity lists for each customer.

---

# 📂 1. Raw Sales Dataset

The project starts with a **10,000+ row messy sales dataset** containing customer, product, quantity, price, date, city, payment mode, and email information.

![Raw Sales Data](Images/10k%2B%20SALES%20DATA.png)

### Dataset Columns

| Column | Description |
|---|---|
| Order ID | Unique order identifier |
| Product Name | Product purchased |
| First Name | Customer first name |
| Last Name | Customer last name |
| Quantity | Quantity purchased |
| Price | Product price |
| Purchase Date | Purchase date |
| City | Customer city |
| Payment Mode | Payment method |
| Email | Customer email |

---

# 📝 2. Power Query Tasks

The following data-cleaning and transformation tasks were performed using Power Query.

![Power Query Tasks](Images/TASKS.png)

### Tasks Performed

- Trim text
- Clean customer names
- Merge First Name and Last Name
- Standardize Product Name
- Standardize City
- Standardize Payment Mode
- Clean Price
- Remove currency symbols
- Remove commas
- Convert Price to number
- Handle different date formats
- Convert Purchase Date to date
- Add custom columns
- Group Customer + Product
- Calculate Total Quantity
- Remove duplicate combinations
- Group data by customer
- Create Product List
- Create Quantity List

---

# 🧹 3. Before Cleaning the Data

The original dataset contains several inconsistencies.

![Before Cleaning](Images/BEFORE%20CLEANING%20DATA%20IN%20PQ.png)

### Examples of Data Issues

#### Product Name

```text
Laptop
laptop
LAPTOP
````

These represent the same product but have different capitalization.

#### City

```text
Delhi
delhi
DELHI
```

#### Payment Mode

```text
UPI
upi
```

#### Price

```text
₹63,915
Rs 52896
₹27,989
50223
€8,067
```

#### Purchase Date

```text
02-27-2024
19/09/2025
2025-03-31
06/04/2025
```

These inconsistencies need to be cleaned before analysis.

---

# 🧼 4. Data Cleaning Using Power Query

Power Query was used to clean and standardize the raw dataset.

![After Cleaning](Images/AFTER%20CLEANING%20DATA%20IN%20PQ.png)

### Cleaning Operations

* Removed unnecessary spaces
* Standardized text values
* Replaced inconsistent values
* Cleaned currency symbols
* Removed commas from prices
* Converted Price to numeric data type
* Converted Purchase Date to date type
* Standardized categories
* Removed unnecessary columns
* Renamed columns

The Power Query workflow is **repeatable and refreshable**, meaning the same transformation can automatically be applied when new data is added.

---

# 👤 5. Creating Full Name

The original dataset contained:

```text
First Name
Last Name
```

For example:

```text
Rohan | Singh
```

These columns were merged to create:

```text
Rohan Singh
```

![Adding New Column](Images/ADDING%20NEW%20COLUMN%20IN%20A%20DATA.png)

### Why Full Name?

Creating a single `Full_Name` column makes customer-level grouping and analysis easier.

---

# ➕ 6. Results After Adding New Columns

After creating the required custom columns and transformations, the dataset contains additional cleaned information.

![After Adding New Columns](Images/AFTER%20ADD%20NEW%20COLUMNS%20RESULTS%20IN%20PQ.png)

The newly created columns are used in later transformation steps such as:

* Grouping
* Aggregation
* Product List creation
* Quantity List creation

---

# 💰 7. Price Cleaning

The Price column contained different formats such as:

```text
₹63,915
Rs 52896
₹27,989
50223
```

Currency symbols and unnecessary separators were removed.

### Example

```text
₹63,915 → 63915
Rs 52896 → 52896
₹27,989 → 27989
```

The final Price column was converted into a numeric data type.

This makes it possible to calculate:

* Total Sales
* Average Price
* Minimum Price
* Maximum Price
* Revenue

---

# 📅 8. Purchase Date Cleaning

The dataset contained different date formats:

```text
02-27-2024
19/09/2025
2025-03-31
06/04/2025
```

These values were converted into a proper date data type.

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

---

# 🔄 9. Grouping Customer + Product

The next important step was grouping the data using:

```text
Full_Name
Product Name
```

Quantity was aggregated using **Sum**.

![Before Grouping](Images/BEFORE%20GROUPING%20DATA.png)

### Example Before Grouping

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

This removes duplicate Customer-Product combinations while preserving the total quantity.

---

# 📊 10. After Grouping

After applying the Group By transformation, each Customer + Product combination becomes unique.

![After Grouping](Images/AFTER%20GROUPING%20DATA.png)

### Grouping Logic

```text
Full_Name + Product Name
          ↓
      Group Rows
          ↓
    Sum Quantity
          ↓
  Total Quantity
```

For example:

```text
Rohan Singh | Camera | 4
Rohan Singh | Mobile | 3
Rohan Singh | Laptop | 5
```

---

# 🧮 11. Creating Product List

After grouping the data by customer, a Product List was created using Power Query M.

### M Code

```powerquery
Text.Combine(
    List.Transform(
        [Data][Product Name],
        each Text.From(_)
    ),
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

the result becomes:

```text
Rohan Singh | Camera, Mobile, Laptop
```

---

# 🔢 12. Creating Quantity List

A corresponding Quantity List was created using:

```powerquery
Text.Combine(
    List.Transform(
        [Data][Total Quantity],
        each Text.From(_)
    ),
    ", "
)
```

### Result

```text
Rohan Singh
Camera, Mobile, Laptop
4, 3, 5
```

Meaning:

```text
Camera → 4
Mobile → 3
Laptop → 5
```

The position of the quantity corresponds to the position of the product.

---

# 👤 13. Final Customer-Level Summary

The final requirement was:

> **Customer name should not repeat.**

Instead of having multiple rows for Rohan Singh:

```text
Rohan Singh | Camera | 4
Rohan Singh | Mobile | 3
Rohan Singh | Laptop | 5
```

the final output becomes:

```text
Rohan Singh | Camera, Mobile, Laptop | 4, 3, 5
```

This creates a clean customer-level summary.

---

# 🔍 14. Complete Query Transformation

The complete sequence of Power Query transformations can be viewed through the Applied Steps panel.

![Query Performed](Images/QUERY%20PERFORMED.png)

### Transformation Flow

```text
Source
   ↓
Changed Type
   ↓
Trimmed Text
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

---

# 📋 15. Final Clean Dataset

After completing all Power Query transformations, the final dataset is clean, standardized, and ready for analysis.

![Final Clean Data](Images/SALES_CLEAN_DATA%20AFTER%20USING%20PQ.png)

### Final Output Example

| Full Name   | Product List           | Quantity |
| ----------- | ---------------------- | -------- |
| Rohan Singh | Camera, Mobile, Laptop | 4, 3, 5  |
| Neha Patel  | Laptop, Camera, Tablet | 7, 2, 5  |
| Priya Gupta | Tablet, Computer       | 5, 2     |

---

# 🧠 16. Power Query Functions Used

### `Text.Combine`

Combines multiple text values.

```powerquery
Text.Combine(List, ", ")
```

### `List.Transform`

Transforms each value inside a list.

```powerquery
List.Transform(
    [Data][Product Name],
    each Text.From(_)
)
```

### `Text.From`

Converts a value into text.

```powerquery
Text.From(_)
```

### `Table.Group`

Groups rows and performs aggregation.

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

# 🛠️ 17. Tools & Technologies

### Tools

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

---

# 📁 18. Repository Structure

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

# 🚀 19. Future Improvements

This project can be extended into a complete Sales Analytics Dashboard.

Possible future analysis:

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

# ⭐ 20. Project Summary

```text
10,000+ Raw Sales Records
          ↓
      Data Cleaning
          ↓
 Text Standardization
          ↓
    Price Cleaning
          ↓
    Date Cleaning
          ↓
    Full Name
          ↓
Customer + Product Grouping
          ↓
   Quantity Aggregation
          ↓
    Remove Duplicates
          ↓
   Product List Creation
          ↓
   Quantity List Creation
          ↓
Final Customer-Level Summary
```

### Final Result

> **One customer → Multiple products → Corresponding quantities**

Example:

```text
Rohan Singh
Camera, Mobile, Laptop
4, 3, 5
```

---



The README above now includes **all 10 images** in the appropriate sections.
