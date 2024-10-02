# Project #3: Configure a Data Model in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Creating Model Relationships](#Creating-model-relationships)
4. [Creating Additional Relationships](#Creating-additional-relationships)
5. [Configuring the Product Table](#Configuring-the-Product-table)
   * [A. Creating a Hierarchy in the Product Table](#A-Creating-a-Hierarchy-in-the-Product-Table)
   * [B. Organizing Columns Into a Display Folder](#B-Organizing-Columns-Into-a-Display-Folder)
6. [Configuring the Region Table](#Configuring-the-region-table)
   * [A. Creating a Hierarchy in the Region Table](#A-Creating-a-Hierarchy-in-the-Region-Table)
   * [B. Updating a Category](#B-Updating-a-category)
7. [Configuring the Reseller Table](#Configuring-the-Reseller-table)
   * [A. Creating a Hierarchy in the Reseller Table](#A-Creating-a-Hierarchy-in-the-Reseller-Table)
   * [B. Updating a Category in the Reseller Table](#B-Updating-a-category-in-the-Reseller-Table)
8. [Configuring the Sales Table](#Configuring-the-Sales-table)
   * [A. Updating Description](#A-Updating-Description)
   * [B. Formatting Columns](#B-Formatting-Columns)
9. [Bulk Update Properties](#Bulk-Update-Properties)
   * [A. Hiding Columns from the Data Model](#A-Hiding-Columns-from-the-Data-Model)
   * [B. Formatting Columns](#B-Formatting-Columns)
10. [Exploring the Model Interface](#Exploring-the-model-interface)
11. [Creating Quick Measures](#Creating-quick-measures)
12. [Creating a Many-to-Many Relationship](#Creating-a-many-to-many-relationship)
13. [Relating the Targets Table](#Relating-the-Targets-table)

## Introduction
This project is the continuation of the one on [**Load Data in Power BI Desktop**](https://github.com/Songonge/Learning-Power-BI/blob/main/Project%202%3A%20Load%20Data%20in%20Power%20BI%20Desktop.md). It involves 
creating relationships between tables, and then configuring table and column properties to improve the friendliness and usability of the data model. In this project, I develop hierarchies and quick measures.

## Project Objectives
*	Create model relationships
*	Configure table and column properties
*	Create hierarchies

## Creating Model Relationships
In this task, I create relationships between the dimension tables and the fact table. This is to facilitate the output of each category. To do that, I
1. Selected the Model view. Then, I selected Manage Relationships under the Home tab.

2. In the Manage Relationships window, I selected the Product table and the Sales table. Then, a column named ProductKey on each table was automatically selected.
> [!NOTE]
>  When you select two tables for which you want to create relationships, Power BI automatically selects one column in each table that shares the same name and data type.
> In case column names are different, you may need to find columns with matching data types.

3. **Cardinality**: A One to Many `(1:*)` relationship was detected. 
> [!NOTE]
> The One to Many relationship is an ideal relationship when the column from one table contains unique values.

4. Selected Single for the Cross-filter direction. This was to ensure that the filters propagate from the _one side_ to the _many side_. In the present case, any filter applied to the Product table will propagate to the Sales table.

5. Made the relation active by checking the box. Then, clicked on Save.

## Creating Additional Relationships
The following additional relationships were created.  
* Reseller | ResellerKey to Sales | ResellerKey 
* Region | SalesTerritoryKey to Sales | SalesTerritoryKey
* Salesperson | EmployeeKey to Sales | EmployeeKey

## Configuring the Product Table 
In this task, I create a hierarchy and also a display folder in the product table. 

### A. Creating a Hierarchy in the Product Table
To do that, I switched to the model view. Then, in the Data pane, I  
* Right-clicked the Category column and selected Create Hierarchy from the menu.
* Renamed the hierarchy to Products.
* Added other levels to the hierarchy by selecting the following from the dropdown list:
  * Subcategory
  * Product
* Clicked on Apply Level Changes. This shows the hierarchy created in the Data pane. 

### B. Organizing Columns Into a Display Folder
To perform this task, in the Data pane, I  
* Selected the columns to include in the folder: Background Color Format and Font Color Format.
* In the Properties pane, I wrote Formatting in the Display Folder box.

## Configuring the Region Table
In this task, I create a hierarchy and updated categories. 

### A. Creating a Hierarchy in the Region Table
To create a hierarchy in the Region table, I  
* Right-clicked the Country column and selected Create Hierarchy from the menu.
* Renamed the hierarchy to Regions.
* Added the following two levels to the hierarchy:
  * Country
  * Region
* Clicked on Apply Level Changes. 

### B. Updating a Category
* To create an updated category, I
  * Selected the Country column.
  * Expanded the Advanced section in the Property pane.
  * Selected Country/Region in the Data Category dropdown list.
> [!NOTE]
> Categorizing the column as country or region provides more accurate information to Power BI when it renders a map visualization.

## Configuring the Reseller Table
In this task, I create a hierarchy and updated categories in the Reseller table. 

### A. Creating a Hierarchy in the Reseller Table
In this task, I create two hierarchies in the Reseller table. 

i. The first hierarchy named Resellers had the following two levels:  
   * Business Type
   * Reseller

ii. The second hierarchy named Geography had the following four levels:  
   * Country-Region
   * State-Province
   * City
   * Reseller
    
### B. Updating a Category in the Reseller Table
The Data Category for the following columns was set:
* Country-Region to Country/Region
* State-Province to State or Province
* City to City

## Configuring the Sales Table
In this task, I configure the Sales table with updated descriptions, formatting, and summarization.

## A. Updating Description
To configure the Sales table with updated descriptions, I
* Selected the Cost column in the Sales table.
* In the Description box under the Properties pane, I entered: **Based on standard cost** as a description.
> [!NOTE]
> This description will appear whenever I will hover the cursor over the Cost field.

### B. Formatting Columns
i. To apply formatting to the **Quantity** column in the Sales table, I  
   * Selected the Quantity column.
   * In the Properties pane, from inside the Formatting section, I slid the Thousands Separator property to Yes.

ii. To apply formatting to the **Unit Price** column in the Sales table, I  
   * Selected the Unit Price column.
   * In the Properties pane from inside the Formatting section, I set the Decimal Places property to 2.
   * In the Advanced group still under the Property pane, in the Summarize By dropdown list, I selected Average.
> [!NOTE]
> Setting the default summarization of the Unit Price to average will produce a meaningful result, unlike the default _summarize by summing values together_ that Power BI applies to any numeric column which is not suitable for certain columns. 

## Bulk Update Properties 
In this task, I update multiple columns using single bulk updates. Precisely, I use this approach to hide columns and format column values. 

### A. Hiding Columns from the Data Model
To do that,  
1. I switched to the Model view.
2. In the Data pane, I selected the ProductKey column from the Product table (Product | ProductKey).
3. While pressing the Ctrl key, I selected the following 13 columns (spanning multiple tables) to hide them:  
   * Region | SalesTerritoryKey
   * Reseller | ResellerKey
   * Sales | EmployeeKey
   * Sales | ProductKey
   * Sales | ResellerKey
   * Sales | SalesOrderNumber
   * Sales | SalesTerritoryKey
   * Salesperson | EmployeeID
   * Salesperson | EmployeeKey
   * Salesperson | UPN
   * SalespersonRegion | EmployeeKey
   * SalespersonRegion | SalesTerritoryKey
   * Targets | EmployeeID
4. In the Properties pane, I slid the Is Hidden property to **Yes**.
> [!NOTE]
> I hid these columns because they are either used by relationships or will later be used in row-level security configuration or calculation logic.

### B. Formatting Columns
To do that, in the Data pane, 
* I selected the following three columns:
  * Product | Standard Cost
  * Sales | Cost
  * Sales | Sales
* I set the Decimal Places property to 0 (zero).

## Exploring the Model Interface 




## Creating Quick Measures 




## Creating a Many-to-Many Relationship 




## Relating the Targets Table 



> [!NOTE]
>  

 

 

> [!IMPORTANT]
>  
 



This completed the lab.



</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


