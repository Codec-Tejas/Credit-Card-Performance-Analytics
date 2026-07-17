# Credit Card Performance Analysis Dashboard

## Project Overview

The **Credit Card Performance Analysis Dashboard** is a Business Intelligence project designed to analyze credit card customer behavior, transaction trends, revenue, and key business performance metrics.

The project follows a complete ETL and visualization workflow:

- Import CSV datasets into MySQL
- Create relational database tables
- Load data into MySQL
- Connect MySQL with Power BI
- Build an interactive two-page dashboard for business insights

---

# Project Architecture

```text
CSV Files
     │
     ▼
MySQL Database
(Create Tables)
     │
     ▼
Import CSV Data
     │
     ▼
Power BI
(MySQL Connector)
     │
     ▼
Interactive Dashboard
```

---

# Dataset

The project uses two CSV files:

- `credit_card.csv`
- `customer.csv`

These datasets contain customer details and credit card transaction information.

---

# Technologies Used

| Tool | Purpose |
|------|----------|
| MySQL | Database Storage |
| SQL | Table Creation & Data Management |
| Power BI | Dashboard & Visualization |
| CSV Files | Source Data |

---

# Step 1: Create Database

Create a new database in MySQL.

```sql
CREATE DATABASE credit_card_db;

USE credit_card_db;
```

---

# Step 2: Create Tables

Create the required tables before importing the CSV files.

Example:

```sql
CREATE TABLE customer (
    Client_Num INT PRIMARY KEY,
    Customer_Age INT,
    Gender VARCHAR(20),
    Dependent_Count INT,
    Education_Level VARCHAR(50),
    Marital_Status VARCHAR(30),
    Income_Category VARCHAR(50),
    Card_Category VARCHAR(50)
);
```

```sql
CREATE TABLE credit_card (
    Client_Num INT,
    Card_Category VARCHAR(50),
    Annual_Fees DECIMAL(10,2),
    Activation_30_Days INT,
    Customer_Acq_Cost DECIMAL(10,2),
    Week_Start_Date DATE,
    Week_Num VARCHAR(10),
    Qtr VARCHAR(10),
    Current_Year INT,
    Credit_Limit DECIMAL(12,2),
    Total_Revolving_Bal DECIMAL(12,2),
    Total_Trans_Amt DECIMAL(12,2),
    Total_Trans_Vol INT,
    Avg_Utilization_Ratio DECIMAL(10,4),
    Use_Chip VARCHAR(20),
    Exp_Type VARCHAR(50),
    Interest_Earned DECIMAL(12,2),
    Delinquent_Acc INT
);
```

---

# Step 3: Import CSV Files into MySQL

Import the CSV files using MySQL Workbench.

### Method

1. Open MySQL Workbench
2. Right-click the table
3. Select **Table Data Import Wizard**
4. Choose the CSV file
5. Map the columns
6. Finish the import process

Repeat the same process for both datasets.

---

# Step 4: Verify Imported Data

Run SQL queries to verify the imported records.

```sql
SELECT * FROM customer;

SELECT * FROM credit_card;
```

---

# Step 5: Connect MySQL with Power BI

1. Open Power BI Desktop.
2. Select **Get Data**.
3. Choose **MySQL Database**.
4. Enter:
   - Server Name
   - Database Name
5. Authenticate using MySQL credentials.
6. Load the required tables into Power BI.

---

# Step 6: Data Modeling

Create relationships between tables using the common key:

```text
Customer[Client_Num]
        │
        ▼
Credit_Card[Client_Num]
```

Relationship Type:

- One-to-Many
- Single Direction

---

# Dashboard Pages

## Page 1 — Credit Card Performance Overview

This dashboard provides an overview of business performance using key metrics.

### KPIs

- Total Revenue
- Total Interest Earned
- Total Transaction Amount
- Total Transaction Volume
- Total Customers

### Visualizations

- Revenue by Card Category
- Revenue by Expenditure Type
- Quarterly Revenue Trend
- Weekly Revenue Trend
- Revenue by Gender
- Revenue by Income Category
- Revenue by Education Level

---

## Page 2 — Customer Insights Dashboard

This dashboard focuses on customer segmentation and behavior.

### KPIs

- Customer Count
- Average Credit Limit
- Average Utilization Ratio
- Total Delinquent Accounts

### Visualizations

- Customer Distribution by Age Group
- Customer Distribution by Marital Status
- Revenue by State
- Revenue by Gender
- Revenue by Card Category
- Credit Limit Analysis
- Transaction Analysis

---

# Key Business Insights

The dashboard helps answer business questions such as:

- Which card category generates the highest revenue?
- Which customer segment contributes the most revenue?
- What is the transaction trend over time?
- Which expenditure type has the highest spending?
- How does revenue vary by gender and income category?
- Which regions generate the highest revenue?
- What is the customer utilization ratio?
- How many delinquent accounts exist?

---

# Power BI Features Used

- KPI Cards
- Bar Charts
- Column Charts
- Line Charts
- Donut Charts
- Map Visuals
- Slicers
- Matrix Tables
- Data Modeling
- DAX Measures
- Interactive Filters

---

# Project Workflow

```text
CSV Files
      │
      ▼
Create MySQL Database
      │
      ▼
Create SQL Tables
      │
      ▼
Import CSV Data
      │
      ▼
Validate Data
      │
      ▼
Connect MySQL to Power BI
      │
      ▼
Data Modeling
      │
      ▼
Build Dashboard
      │
      ▼
Generate Business Insights
```

---

# Folder Structure

```text
Credit-Card-Performance-Analysis/
│
├── Dataset/
│   ├── customer.csv
│   └── credit_card.csv
│
├── SQL/
│   ├── create_database.sql
│   ├── create_tables.sql
│   └── import_data.sql
│
├── PowerBI/
│   └── Credit_Card_Performance.pbix
│
├── Images/
│   ├── Dashboard_Page1.png
│   └── Dashboard_Page2.png
│
└── README.md
```

---

# Conclusion

This project demonstrates an end-to-end Business Intelligence workflow by integrating **MySQL** and **Power BI**. Raw CSV data is transformed into a structured relational database, connected to Power BI for interactive analysis, and presented through a two-page dashboard that delivers meaningful insights into credit card performance, customer behavior, revenue trends, and transaction analytics.

---

## Author

**Your Name**

Data Analyst | SQL | MySQL | Power BI | Business Intelligence