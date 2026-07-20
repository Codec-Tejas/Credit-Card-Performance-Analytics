# Credit Card Customer & Transaction Analytics

A Power BI reporting solution built on a MySQL data warehouse, designed to give a credit card business a unified view of revenue, transaction activity, customer risk, and engagement.

## Business Problem

Credit card issuers generate two separate streams of data: customer demographic/profile information and weekly card transaction activity. Kept in separate systems, this data can't answer basic business questions — which customer segments drive revenue, which card categories are underperforming, where delinquency risk is concentrated — without manual, repeated effort. This project consolidates both data streams into a single database and reporting layer so those questions can be answered on demand.

## Target Users

- Business and finance teams tracking revenue and interest performance
- Marketing and product teams segmenting customers by demographics, income, and card category
- Risk and credit teams monitoring activation and delinquency rates
- Leadership reviewing overall portfolio health

## Business Impact

- Replaces manual, spreadsheet-based reporting with a single connected data model
- Surfaces revenue and risk by segment (state, occupation, card category, income group) in one place instead of separate exports
- Makes recurring questions ("how is Blue vs Platinum performing," "which states drive revenue") self-service instead of one-off requests

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
