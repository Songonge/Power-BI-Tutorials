# Part #3: Configure a Data Model in Power BI Desktop

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
In this task, I switch to Report view, review the data model interface, and configure the auto date/time setting.

1. When I switched to Report view and explored the tables, I noticed that:
   * Tables with all columns hidden do not appear on the Data pane
   * Columns, hierarchies, and their levels are fields, which can be used to configure report visuals
   * Only fields relevant to report authoring are visible
   * Spatial fields in the Region and Reseller table are adorned with a spatial icon
   * Fields adorned with the sigma symbol (Ʃ) will summarize, by default
   * A tooltip appears when hovering the cursor over the Sales | Cost field

2. I expanded the Sales | OrderDate field and noticed that it reveals a Date Hierarchy. On the other hand, the Targets | TargetMonth field delivered a similar hierarchy. Since these hierarchies were not created by me and had a problem, I proceeded as follows to turn them off:
   * To turn off the Auto date/time setting, I navigated to File > Options and Settings > Options.
   * Under the Current File section, I navigated to Data Load > Time Intelligence, and unchecked Auto Date/Time.
   * This made the date hierarchies disappear from the Data pane.

## Creating Quick Measures 
In this task, I create two quick measures to calculate profit and profit margin. 
> [!NOTE]
> A quick measure creates the calculation formula for the report designer.
> Quick measures are easy and fast to create for simple and common calculations.

To create the first Quick Measure by Subtraction,   
1. In the Data pane, I right-clicked the Sales table and selected New Quick Measure.
2. In the Quick Measures window, I selected Subtraction in the Calculation dropdown list from inside the Mathematical Operations group.
3. Dragged the Sales field into the Base Value box and the Cost field into the Value to Subtract box.
4. Selected **Add**.
5. Renamed the measure as Profit.

To create the second Quick Measure by Division, 
1. In the Data pane, I right-clicked the Sales table and selected New Quick Measure.
2. In the Quick Measures window, I selected Division in the Calculation dropdown list from inside the Mathematical Operations group.
3. Set the Numerator to Sales | Profit and the Denominator to Sales | Sales.
4. Selected **Add**.
5. Renamed the measure as Profit Margin.
6. Set the format of the Profit Margin measure to Percentage with two decimal places.
   
## Creating a Many-to-Many Relationship 
In this task, I create a many-to-many relationship between the Salesperson table and the Sales table. To do that,  
1. I Switched to the Report view.
2. In the Data pane, I checked the following two fields to create a new table visual:
   * Salesperson | Salesperson
   * Sales | Sales
> [!NOTE]
> There is another relationship between salespeople and sales that was created earlier. Moreover, note that some salespeople belong to one, two, or possibly more sales regions and that sales regions can have multiple salespeople assigned to them.
> Therefore, from a performance management perspective, a salesperson’s sales (based on their assigned territories) need to be analyzed and compared with sales targets.

To create relationships to support this analysis, I  
1. Switched to Model view.
2. Dragged the SalespersonRegion table to position it between the Region and Salesperson tables.
3. Used the drag-and-drop technique to create the following two model relationships:
   * Salesperson | EmployeeKey to SalespersonRegion | EmployeeKey
   * Region | SalesTerritoryKey to SalespersonRegion | SalesTerritoryKey
> [!NOTE]
> Considering that the Salesperson table filters the Sales table and the SalespersonRegion table but does not continue by propagating filters to the Region table (the arrowhead is pointing in the wrong direction), I must edit the relationship.

To edit the relationship between the Region and SalespersonRegion tables, I  
1. Double-clicked the relationship.
2. In the Edit Relationship window, in the Cross Filter Direction dropdown list, I selected Both.
3. Checked the Apply Security Filter in Both Directions checkbox. Then, I selected OK. This updated the relationship with a double arrowhead.
4. Made one of the relationships between the Salesperson and Sales tables inactive by:
   * Double-clicking the relationship between the Salesperson and Sales tables.
   * Unchecking the Make This Relationship Active checkbox in the Edit Relationship window and selecting OK.

5. Renamed the Salesperson table to Salesperson (Performance). That is because the table is used to report and analyze the performance of salespeople based on the sales of their assigned sales regions.

## Relating the Targets Table 
In this task, I create a relationship to the Targets table. To do that, I  
1. Created a relationship between the following columns:
   * Salesperson (Performance) | EmployeeID column and the Targets | EmployeeID column.
2. I could now visualize sales and targets in one table with appropriate values.

This completed the project.




</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


