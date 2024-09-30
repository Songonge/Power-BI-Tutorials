# Project #1: Get Data in Power BI Desktop

# Introduction
This project is an introduction to the Power BI Desktop application. It explains how to connect to data and how to use data preview techniques to understand the characteristics and quality of the source data. 

## Project Objectives
* Open Power BI Desktop
* Connect to different data sources
* Preview source data  with Power Query
* Use data profiling features in Power Query

## Steps Completed Throughout the Project
To begin with, I downloaded the zip folder through the [link](https://github.com/MicrosoftLearning/PL-300-Microsoft-Power-BI-Data-Analyst/raw/Main/Allfiles/Labs/01-prepare-data-with-power-query-in-power-bi-desktop/01-prepare-data.zip) provided. Then, after I extracted 
everything, I opened the .pbix file. The following settings have been disabled:  
* Data Load > Import relationships from data sources on the first load
* Data Load > Autodetect new relationships after data is loaded  
This was done to avoid Power BI automatically creating relationships between the data (tables).

### Getting Data From SQL Server
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


Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Power BI](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


