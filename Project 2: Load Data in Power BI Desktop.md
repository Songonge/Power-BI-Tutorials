# Project #2: Load Data in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Configuration of Queries](#Configuration-of-Queries)
   * [Configuring the Salesperson query](Configuring-the-Salesperson-query)
   * [Configuring the SalespersonRegion query](#Configuring-the-SalespersonRegion-query)
   * [Configuring the Product query](Configuring-the-Product-query)
   * [Configuring the Reseller query](#Configuring-the-Reseller-query)
   * [Configuring the Region query](Configuring-the-Region-query)
   * [Configuring the Sales query](#Configuring-the-Sales-query)
   * [Configuring the Targets query](Configuring-the-Targets-query)
   * [Configuring the ColorFormats query](#Configuring-the-ColorFormats-query)
4. [Getting Data From SQL Server](#Getting-Data-From-SQL-Server)


## Introduction
This project is the continuation of the one on [**Get Data in Power BI Desktop**](https://github.com/Songonge/Learning-Power-BI/blob/main/Project%201%3A%20Get%20Data%20in%20Power%20BI%20Desktop.md). It involves using data cleansing and transformation techniques to shape the data model and applying queries to load all tables to the data model. 

## Project Objectives
* Apply various transformations
* Load queries to the data model

## Configuration of Queries
In this task, I used Power Query to configure each query (table). First, I opened Power Query by selecting **Transform Data** from inside the **Queries** group under the **Home** tab.

### Configuring the Salesperson query
1. Renamed the query to Salesperson.
  
2. Use the Go to Column feature by selecting Choose Columns under the Home tab inside the Manage Columns group.
  
3. Filtered rows in the table by a specific column (SalesPersonFlag) to retain only entries with TRUE in that specific column.
  
4. Removed other columns by selecting Choose Columns under the Home tab inside the Manage Columns group. The following columns were retained:
   * EmployeeKey 
   * EmployeeNationalIDAlternateKey
   * FirstName
   * LastName
   * Title
   * EmailAddress

5. Merged two columns (FirstName and LastName) to a column named Salesperson. This was completed as follows:
   * Selected both column headers
   * Right-clicked any of them and selected Merge Columns from the menu.
   * Specified Space as Separator

6. Renamed columns
   * EmployeeNationalIDAlternateKey to EmployeeID
   * EmailAddress to UPN (meaning User Principal Name)

> [!NOTE]
> This table was transformed from 3 columns and 292 rows to 5 columns and 18 rows.

### Configuring the SalespersonRegion query


### Configuring the Reseller query 

> [!NOTE]
> This table was transformed from 3 columns and 292 rows to 5 columns and 18 rows.

### Configuring the Region query

> [!NOTE]
> This table was transformed from 3 columns and 292 rows to 5 columns and 18 rows.

### Configuring the Sales query

> [!NOTE]
> This table was transformed from 3 columns and 292 rows to 5 columns and 18 rows.

### Configuring the Targets query

> [!NOTE]
> This table was transformed from 3 columns and 292 rows to 5 columns and 18 rows.

### Configuring the ColorFormats query

> [!NOTE]
> This table was transformed from 3 columns and 292 rows to 5 columns and 18 rows.


</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


