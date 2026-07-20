# Credit Card Customer & Transaction Analytics

A Power BI reporting solution built on a MySQL data warehouse, designed to give a credit card business a unified view of revenue, transaction activity, customer risk, and engagement.

## Business Problem

A credit card company has two kinds of data: information about its customers (age, income, job, location) and information about their card transactions (spending, revenue, missed payments). This data is usually stored in separate files, so it's hard to answer simple business questions like: Do high-income customers actually bring in more revenue? Which job types or states have the most missed payments? Which card type is really the most profitable? Every time someone wants to answer a question like this, they have to manually combine the two files and go through the numbers again. This project fixes that by loading both files into one database, connecting them by customer ID, and building a Power BI report on top. Now these questions can be answered by filtering a dashboard instead of redoing the work each time.

## Target Users

- Business and finance teams tracking revenue and interest performance
- Marketing and product teams segmenting customers by demographics, income, and card category
- Risk and credit teams monitoring activation and delinquency rates
- Leadership reviewing overall portfolio health

## Business Impact

- Replaces manual, spreadsheet-based reporting with a single connected data model, so the same numbers don't get recalculated by hand for every request
- Puts revenue, interest, and risk side by side across every segment a business would actually care about — state, card category, occupation, income group, age group, marital status, dependents, education level, and expenditure type — instead of exporting separate cuts of the data for each one
- Shows which segments carry the most delinquency risk (by occupation, in the current model) alongside their revenue contribution, so risk and revenue can be weighed together instead of looked at separately
- Breaks down revenue by payment method (swipe, chip, online) and by expenditure category (bills, grocery, travel, fuel, entertainment), which supports questions about where spending is concentrated, not just how much of it there is
- Turns recurring questions — "how is Blue vs Platinum performing," "which states drive revenue," "are high-income customers actually the most valuable ones" — into a filter click instead of a new analysis request each time
- Gives a single source of truth for customer and transaction numbers, so different teams aren't working off different exports of the same underlying data

## Key Objectives

- Centralize customer and transaction data in a relational database rather than flat files
- Build a data model that supports slicing revenue and risk by demographic and card attributes
- Deliver two focused report pages — customer analytics and transaction analytics — instead of one overloaded dashboard
- Keep the model simple enough (two tables, one relationship) to be maintainable and easy to extend

## Automation, Time Savings & Decision-Making Benefits

Moving from manual CSV analysis to a MySQL-to-Power BI pipeline automates the parts of reporting that would otherwise be repeated by hand:

- **Automation** — data is loaded once via `LOAD DATA INFILE` and refreshed through Power BI rather than re-processed in spreadsheets each time
- **Time savings** — filtering by quarter, card category, or gender is a slicer click instead of rebuilding a pivot table or query
- **Decision-making** — metrics like activation rate and delinquency rate are visible continuously rather than calculated on request, so trends can be caught earlier

Cost reduction and customer experience improvements would depend on how this is deployed inside an actual business (e.g., reduced analyst hours, faster response to at-risk segments) — this project demonstrates the reporting foundation those gains would be built on, rather than measuring them directly, since it runs on synthetic data.

## System Architecture & Data Flow

The pipeline has two layers: storage and reporting.

**1. Storage layer (MySQL)**
The data is held in two MySQL tables:
- `cust_detail` — one row per customer, holding demographic and profile attributes
- `credit_card_details` — one row per customer per week, holding card, credit, and transaction attributes

Both tables share `Client_Num` as a common key, giving a 1:1 relationship between a customer and their card/transaction record.

**2. Reporting layer (Power BI)**
Power BI connects directly to the MySQL database and imports both tables. The relationship on `Client_Num` is preserved in the model, and a calculated `AgeGroup` column is added on the customer table for demographic bucketing. From this model, two report pages are built:
- **Customer Analytics** — revenue and risk viewed through the customer lens (age, income, occupation, marital status, state)
- **Transaction Analytics** — revenue and volume viewed through the transaction lens (card category, payment method, expenditure type, quarter)

Shared slicers (quarter, week, card category, gender) let a user filter both the customer and transaction context consistently across either page.

As new weekly data is added to the MySQL database, the report reflects it on refresh, so the dashboards stay current without rebuilding the model.

```
MySQL database → Power BI (Import, 1:1 relationship on Client_Num) → Two report pages
```

## Tools Used

- MySQL — data storage and modeling
- Power BI — data connection, DAX, and visualization

## Repository Structure

```
dataset/    raw CSV files
sql/        database setup and import script
reports/    Power BI dashboard screenshots
README.md
```
