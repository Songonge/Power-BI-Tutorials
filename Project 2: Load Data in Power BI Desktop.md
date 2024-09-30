# Project #2: Load Data in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Configuration of Queries](#Configuration-of-Queries)
4. [Getting Data From SQL Server](#Getting-Data-From-SQL-Server)


## Introduction
This project is the continuation of the one on [**Get Data in Power BI Desktop**](https://github.com/Songonge/Learning-Power-BI/blob/main/Project%201%3A%20Get%20Data%20in%20Power%20BI%20Desktop.md). It involves using data cleansing and transformation techniques to shape the data model and applying queries to load all tables to the data model. 

## Project Objectives
* Apply various transformations
* Load queries to the data model

## Configuration of Queries
In this task, I used Power Query to configure each query (table). First, 

## Getting Data From SQL Server
1. To complete this step, first I installed SQL Server on my computer. Then, using the backup file (.bak file) provided, I was able to extract the database containing all the tables and load it into Microsoft SQL Server Management Studio. The steps are given [here](https://github.com/Songonge/Learning-Power-BI/blob/main/Import%20a%20backup%20file%20in%20SQL%20Server.md).

2. Once the database was up and functioning, I went back to Power BI to connect to the SQL Server database. On the Home tab, I selected SQL Server from inside the Data group.

3. In the pop-up window, I entered my server and database details. Then, I clicked on OK. This pulled the database and showed it in the Navigator pane.

4. I selected the following tables:
   * DimEmployee (3 columns, 292 rows)
   * DimEmployeeSalesTerritory (4 columns, 39 rows)
   * DimProduct (40 columns, 606 rows)
   * DimReseller (22 columns, 701 rows)
   * DimSalesTerritory (10 columns, 11 rows)
   * FactResellerSales (21 columns, 57851 rows)

5. Then, I clicked on Transform Data. This opened Power Query. In Power Query, the following were completed.
   * Assessed column quality by checking the box for Column Quality under View within Data Preview. This was to note columns with valid, empty, and error data.
   * Assessed column distribution by checking the box for Column Distribution under View within Data Preview. This allowed to note unique and distinct values in each column.
   * Viewed column values by checking the box for Column Profile under View within Data Preview. This allowed to notice if there were issues with the data quality. For example, spelling errors for the same category of data in a column. From here, it is easy to note if values will be replaced in some columns/rows.

6. Got other data from external files using the Home tab -> New Source from inside the New Query group -> selecting Text/CSV:
   * ResellerSalesTargets (14 columns, 81 rows)
   * ColorFormats (3 columns, 11 rows)

7. In total, there were 8 tables loaded.

8. This completed the lab.


</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


