# Coffee Chain Management Database

**Relational Database Design & Advanced SQL | Oracle Database**

An end-to-end academic database project modeling the operations of a multi-location coffee shop franchise. Designed and implemented a relational schema to manage employees, shifts, customers, orders, menu items, recipes, ingredient inventory, suppliers, and deliveries.

The project emphasizes **relational data modeling, data integrity, advanced SQL querying, normalization, and query optimization**, with analytical queries designed around realistic business questions.

## Tech Stack

- **Database:** Oracle Database
- **Language:** SQL (Oracle SQL dialect)
- **Concepts:** ER modeling, relational algebra, normalization, constraints, joins, correlated subqueries, common table expressions (CTEs), views, and data manipulation

## Key Features

### Relational Database Architecture
- Designed a schema covering **19 tables**, including entity subtypes and associative tables.
- Modeled one-to-many, many-to-many, and ternary relationships using primary and foreign keys.
- Used entity specialization for employee roles (**Manager, Barista, Chef**) and menu categories (**Beverage, Brunch**).
- Defined integrity constraints with `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`, and default values.
- Documented entity-relationship and relational-schema diagrams.

### Operational Data Management
- **Staff and shifts:** employee assignments, shift attendance, hourly pay, and seniority-based compensation reporting.
- **Orders and customers:** order processing, order items, transaction totals, and customer purchase history.
- **Menu and recipes:** products, preparation instructions, ingredient quantities, and product categories.
- **Inventory and procurement:** ingredient stock, supplier relationships, purchase requests, and deliveries across locations.

### Advanced SQL and Business Analytics
- **Customer preference profiles:** identify frequently ordered products, preferred locations, customer tenure, and loyalty categories.
- **Branch performance:** summarize orders and revenue, compare branch sales against the overall average, and analyze sales by year.
- **Employee reporting:** combine job roles, completed shifts, and compensation calculations.
- **Menu analysis:** categorize products and analyze recipe complexity and preparation time.
- **Supplier reporting:** examine procurement activity and ingredient usage.

The SQL work demonstrates:
- Multi-table `JOIN` operations, including outer joins
- Correlated and non-correlated subqueries
- Aggregation with `GROUP BY` and `HAVING`
- Common table expressions using `WITH`
- Conditional expressions using `CASE` and `DECODE`
- Oracle functions including `NVL` and date/string functions
- Top-N analysis and relational division
- Subquery-based `UPDATE` and `DELETE` operations
- A reporting `VIEW` combining orders, customers, and employees

## Database Design and Optimization

**Normalization:** Analyzed the schema through **1NF, 2NF, 3NF**, with further exploration of **BCNF, 4NF, and 5NF** to evaluate dependencies and redundancy.

**Relational algebra:** Compared original and rewritten SQL queries using relational-algebra expressions and operator trees. Applied predicate pushdown and explicit joins to demonstrate logical query optimization.

**Denormalization trade-off:** Proposed a consolidated order-details structure for receipt/history retrieval, explaining the trade-off between repeated joins and controlled data redundancy.

> **Scope:** Query optimization is demonstrated conceptually through relational algebra and SQL rewrites; the project does not claim measured runtime improvements or a production deployment.

## Example: Branch Performance Analysis

One of the analytical tasks is to identify locations whose total sales exceed average branch sales, and report their order volume, revenue, and year-by-year sales figures. This illustrates how multi-table joins, grouped aggregates, and subqueries can answer a business question directly within the database.

## Repository Contents

The project documentation includes:
- Business requirements and integrity constraints
- Entity-relationship and relational-schema diagrams
- Table creation statements and sample-data inserts
- Advanced SQL queries and data modification examples
- View creation and examples of permitted/restricted modifications
- Relational-algebra optimization examples
- Normalization and denormalization analysis

## Running the SQL

Use an **Oracle Database** instance and an Oracle-compatible SQL client (such as Oracle SQL Developer). Execute the schema creation statements before inserting the sample data, then run the analysis queries. SQL examples use Oracle-specific syntax and may require changes for other database engines.

*For easier reproduction, the repository should include separate SQL scripts for schema creation, sample data, and analytical queries.*

## Academic Context

Developed independently for the **Databases** course, Faculty of Mathematics and Computer Science, **University of Bucharest** (June 2026).

**Author:** Eliza-Georgiana Boroș

## Skills Demonstrated

`Oracle SQL` · `Relational Database Design` · `Data Modeling` · `ER Diagrams` · `SQL Joins` · `Subqueries` · `CTEs` · `Aggregation` · `Views` · `Data Integrity` · `Database Normalization` · `Relational Algebra` · `Query Optimization`
