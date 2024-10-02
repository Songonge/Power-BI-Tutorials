# Project #3: Configure a Data Model in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Creating Model Relationships](#Creating-model-relationships)
4. [Creating Additional Relationships](#Creating-additional-relationships)
   * [A. Configuring the Product Table](#C-Configuring-the-Product-table)
     * [1. Creating a Hierarchy in the Product Table](#1-Creating-a-Hierarchy-in-the-Product-Table)
     * [2. Organizing Columns Into a Display Folder](#2-Organizing-Columns-Into-a-Display-Folder)
   * [B. Configuring the Region Table](#A-Configuring-the-region-table)
     * [1. Creating a Hierarchy in the Region Table](#1-Creating-a-Hierarchy-in-the-Region-Table)
     * [2. Updating a Category](#2-Updating-a-category)
   * [C. Configuring the Reseller Table](#D-Configuring-the-Reseller-table)
     * [1. Creating a Hierarchy in the Reseller Table](#1-Creating-a-Hierarchy-in-the-Reseller-Table)
     * [2. Updating a Category in the Reseller Table](#2-Updating-a-category-in-the-Reseller-Table)
   * [D. Configuring the Sales Table](#F-Configuring-the-Sales-table)
6. [Bulk Update Properties](#Bulk-Update-Properties)
7. [Exploring the Model Interface](#Exploring-the-model-interface)
8. [Creating Quick Measures](#Creating-quick-measures)
9. [Creating a Many-to-Many Relationship](#Creating-a-many-to-many-relationship)
10. [Relating the Targets Table](#Relating-the-Targets-table)

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

### A. Configuring the Product Table 
In this task, I create a hierarchy and also a display folder in the product table. 

#### 1. Creating a Hierarchy in the Product Table
To do that, I switched to the model view. Then, in the Data pane, I  
* Right-clicked the Category column and selected Create Hierarchy from the menu.
* Renamed the hierarchy to Products.
* Added other levels to the hierarchy by selecting the following from the dropdown list:
  * Subcategory
  * Product
* Clicked on Apply Level Changes. This shows the hierarchy created in the Data pane. 

#### 2. Organizing Columns Into a Display Folder
To perform this task, in the Data pane, I  
* Selected the columns to include in the folder: Background Color Format and Font Color Format.
* In the Properties pane, I wrote Formatting in the Display Folder box.

### B. Configuring the Region Table
In this task, I create a hierarchy and updated categories. 

#### 1. Creating a Hierarchy in the Region Table
To create a hierarchy in the Region table, I  
* Right-clicked the Country column and selected Create Hierarchy from the menu.
* Renamed the hierarchy to Regions.
* Added the following two levels to the hierarchy:
  * Country
  * Region
* Clicked on Apply Level Changes. 

#### 2. Updating a Category
* To create an updated category, I
  * Selected the Country column.
  * Expanded the Advanced section in the Property pane.
  * Selected Country/Region in the Data Category dropdown list.
> [!NOTE]
> Categorizing the column as country or region provides more accurate information to Power BI when it renders a map visualization.

### C. Configuring the Reseller Table
In this task, I create a hierarchy and updated categories in the Reseller table. 

#### 1. Creating a Hierarchy in the Reseller Table
In this task, I create two hierarchies in the Reseller table. 

i. The first hierarchy named Resellers had the following two levels:  
   * Business Type
   * Reseller

ii. The second hierarchy named Geography had the following four levels:  
    * Country-Region
    * State-Province
    * City
    * Reseller
    

#### 2. Updating a Category in the Reseller Table
* To create an updated category, I
  * Selected the Country column.
  * Expanded the Advanced section in the Property pane.
  * Selected Country/Region in the Data Category dropdown list.


### D. Configuring the Sales Table




## Bulk Update Properties 




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


