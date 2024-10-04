# Project #2: Load Data in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Configuration of Queries](#Configuration-of-Queries)
   * [A. Configuring the Salesperson query](#A-Configuring-the-Salesperson-query)
   * [B. Configuring the SalespersonRegion query](#B-Configuring-the-SalespersonRegion-query)
   * [C. Configuring the Product query](#C-Configuring-the-Product-query)
   * [D. Configuring the Reseller query](#D-Configuring-the-Reseller-query)
   * [E. Configuring the Region query](#E-Configuring-the-Region-query)
   * [F. Configuring the Sales query](#F-Configuring-the-Sales-query)
   * [G. Configuring the Targets query](#G-Configuring-the-Targets-query)
   * [H. Configuring the ColorFormats query](#H-Configuring-the-ColorFormats-query)
4. [Updating the Product Query](#Updating-the-Product-Query)
5. [Updating the ColorFormats Query](#Updating-the-ColorFormats-Query)
6. [Loading the Data in Power BI Desktop](#Loading-the-Data-in-Power-BI-Desktop)


## Introduction
This project is the continuation of the one on [**Get Data in Power BI Desktop**](https://github.com/Songonge/Learning-Power-BI/blob/main/Project%201%3A%20Get%20Data%20in%20Power%20BI%20Desktop.md). It involves using data cleansing and transformation techniques to shape the data model and applying queries to load all tables to the data model. 

## Project Objectives
* Apply various transformations
* Load queries to the data model

## Configuration of Queries
In this task, I used Power Query to configure each query (table). First, I opened Power Query by selecting **Transform Data** from inside the **Queries** group under the **Home** tab.

### A. Configuring the Salesperson query
1. Renamed the DimEmployee query (table) to Salesperson.
  
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

### B. Configuring the SalespersonRegion Query
1. Renamed the DimEmployeeSalesTerritory query (table) to SalespersonRegion.
2. Removed the last two columns by selecting both headers, right-clicking, and choosing Remove Columns from the menu.

> [!NOTE]
> This table was transformed from 4 columns, 39 rows to 2 columns and 39 rows.

### C. Configuring the Product Query 
1. Renamed the DimProduct query (table) to Product.

2. Filtered rows in the table by a specific column (FinishedGoodsFlag) to retain only entries with TRUE in that specific column.

3. Removed other columns except the following:
   *	ProductKey
   * EnglishProductName
   * StandardCost
   * Color
   * DimProductSubcategory

4. Expanded the DimProductSubcategory column and selected only EnglishProductSubcategoryName and DimProductCategory. Then, I unchecked the **Use Original Column Name as Prefix** to avoid that it prefixes each column with the expanded column name. Performed the same process on the DimProductCategory column to include only the EnglishProductCategoryName column.

5. Renamed several columns:
   * EnglishProductName to Product
   * StandardCost to Standard Cost (include a space)
   * EnglishProductSubcategoryName to Subcategory
   * EnglishProductCategoryName to Category

> [!NOTE]
> This table was transformed from 40 columns and 606 rows to 6 columns and 397 rows.

### D. Configuring the Reseller Query 
1. Renamed the DimReseller query (table) to Reseller.

2. Removed all columns, except the following:  
   * ResellerKey
   * BusinessType
   * ResellerName
   * DimGeography

3. Expanded the DimGeography column and selected only:    
   * City
   * StateProvinceName
   * EnglishCountryRegionName

4. Replaced values in this table in the BusinessType column. To do that,    
   * I right-clicked the Business column header.
   * Selected Replace Values from the menu.
   * In the pop-up window, I put Ware House in the Value to Find box and Warehouse in the Replace With box.

5. Renamed the following columns:
   * BusinessType to Business Type (include a space)
   * ResellerName to Reseller
   * StateProvinceName to State-Province
   * EnglishCountryRegionName to Country-Region

> [!NOTE]
> This table was transformed from 22 columns and 701 rows to 6 columns and 701 rows.

### E. Configuring the Region Query
1. Renamed the DimSalesTerritory query (table) to Region.
  
2. Filtered the SalesTerritoryAlternateKey column to remove a row with a 0 entry.

3. Removed all columns, except the following:  
   * SalesTerritoryKey
   * SalesTerritoryRegion
   * SalesTerritoryCountry
   * SalesTerritoryGroup

4. Renamed columns as follows:  
   * SalesTerritoryRegion to Region
   * SalesTerritoryCountry to Country
   * SalesTerritoryGroup to Group

> [!NOTE]
> This table was transformed from 10 columns and 11 rows to 4 columns and 10 rows.

### F. Configuring the Sales Query
1. Renamed the FactResellerSales query (table) to Sales.

2. Removed other columns in the table to keep only the following:  
   * SalesOrderNumber
   * OrderDate
   * ProductKey
   * ResellerKey
   * EmployeeKey
   * SalesTerritoryKey
   * OrderQuantity
   * UnitPrice
   * TotalProductCost
   * SalesAmount
   * DimProduct

3. Expanded the DimProduct column and selected only StandardCost. This column was to be used to fix missing (null) values in the TotalProductCost column. 

4. Created a new column. To do that, I  
   * Selected Custom Column on the Add Column tab inside the General group.
   * Named the column **Cost**
   * In the Custom column formula box, I wrote
     ```
     if [TotalProductCost] = null then [OrderQuantity] * [StandardCost] else [TotalProductCost]
     ```

> [!IMPORTANT]
> The formula above tests if the TotalProductCost value is missing. If missing, it produces a value by multiplying the OrderQuantity value by the StandardCost value. Otherwise, it uses the existing TotalProductCost value.

5. Removed the following columns:  
   * TotalProductCost
   * StandardCost

6. Renamed the following columns:  
   * OrderQuantity to Quantity
   * UnitPrice to Unit Price (include a space)
   * SalesAmount to Sales

7. Changed the data type of the Quantity column. To do that, I  
   * Selected the 1.2 icon at the left of the column header and chose Whole Number from the menu.

9. Modified the Unit Price, Sales, and Cost column types to Fixed Decimal Number.

> [!NOTE]
> This table was transformed from 21 columns and 57851 rows to 10 columns and 57851 rows.

### G. Configuring the Targets Query
1. Renamed the ResellerSalesTargets query (table) to Targets.

2. Unpivoted other columns. To do that, I  
   * Multi-selected the Year and EmployeeID column headers.
   * Right-clicked any of the selected column headers and chose Unpivot Other Columns from the menu.

3. Filtered rows by removing those with a hyphen in the Value column.

4. Renamed the following columns:  
   * Attribute to MonthNumber 
   * Value to Target

5. Replaced values in the MonthNumber column to remove the M preceding each month. To do that,  
   * I right-clicked the MonthNumber column header.
   * Selected Replace Values from the menu.
   * In the pop-up window, I put **M** in the Value to Find box and left the Replace With box empty.

6. Changed the data type of the MonthNumber column to a Whole Number. To do that, I  
   * Selected the ABC icon at the left of the column header and chose Whole Number from the menu.

7. Added a new column in the table. To do that, I  
   * Selected **Column From Examples** under the Add Column tab from inside the General group. This created an empty column.
   * In the first row, I wrote `7/1/2017` and I pressed Enter. This automatically populated the remaining rows in this column.
   * Renamed this column to TargetMonth

8. Removed the following columns (since these were used to create the TargetMonth column):  
   * Year
   * MonthNumber

9. Changed the data type of the following columns:  
   * Target as a fixed decimal number
   * TargetMonth as date

10. Multiplied the Target column by 1000 since they were stored as thousands. To do that, I  
    * Selected the Target column header.
    * Selected Standard and then Multiply under the Transform tab from inside the Number Column group.
    * In the pop-up window, I entered 100 and clicked on OK.

> [!NOTE]
> This table was transformed from 14 columns and 81 rows to 3 columns and 809 rows. We now have many rows because the unpivoted columns significantly increased the number of rows. 

### H. Configuring the ColorFormats Query
1. Promoted headers by selecting Use First Row as Headers under the Home tab.

> [!NOTE]
> This table was transformed from 3 columns and 11 rows to 3 columns and 10 rows.

## Updating the Product Query
This is done by merging the product table with the ColorFormats table.  
1. Selected the Product query (table)

2. Selected Merge Queries under the Home tab from inside the Combine group.

3. In the pop-up window, I  
   * Selected the **Color** header from the Product table.
   * Selected ColorFormats as the second table. Then, selected the Color header. left other options as is.
   * Clicked on OK.

4. Expanded the ColorFormats column to retain only the following columns:
   * Background Color Format
   * Font Color Format

> [!NOTE]
> This transformed the Product table from 6 columns and 397 rows to 8 columns and 397 rows.

## Updating the ColorFormats Query
This task is to update the ColorFormats query to disable it to load when I load data to Power BI since it was already merged with the Product table. To do that, I
1. Selected the ColorFormats query.
2. In the Query Settings pane, I selected the All Properties link.
3. In the Query Properties window, I unchecked the Enable Load To Report checkbox.
4. Clicked on OK to confirm.

## Loading the Data in Power BI Desktop
After completing the above steps, I clicked on **Close & Apply** under the Home tab to load the data to the model and close the Power Query Editor window.

In total, 7 tables were loaded in Power BI Desktop.

This completed the project.

</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


