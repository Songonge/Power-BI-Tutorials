# Project #4: Create DAX Calculations in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Creating the Salesperson Calculated Table](#Creating-the-Salesperson-Calculated-Table)
   * [A. Creating the Table](#A-Creating-the-Table)
   * [B. Creating Relationships Between the Salesperson Table and Other Tables in the Model](#B-Creating-Relationships-Between-the-Salesperson-Table-and-Other-Tables-in-the-Model)
4. [Creating the Date Table](#Creating-the-Date-table)
   * [A. Creating Calculated Columns in the Date Table](#A-Creating-Calculated-Columns-in-the-Date-Table)
   * [B. Completing the Date Table](#B-Completing-the-Date-Table)
   * [C. Marking the Date Table](#C-Marking-the-Date-table)
5. [Creating Simple Measures](#Creating-simple-measures)
6. [Creating Additional Measures](#Creating-additional-measures)

## Introduction
This project is the continuation of the one on [**Configure a Data Model in Power BI Desktop**](https://github.com/Songonge/Learning-Power-BI/blob/main/Project%203%3A%20Configure%20a%20data%20model%20in%20Power%20BI%20Desktop.md). It involves 
creating calculated tables, calculated columns, and simple measures using Data Analysis Expressions (DAX).

## Project Objectives
*	Create calculated tables
*	Create calculated columns
*	Create measures

## Creating the Salesperson Calculated Table
In this task, I created the Salesperson calculated table directly related to Sales.
> [!NOTE]
> A calculated table is created by entering the table name, the equals symbol (=), and a DAX formula that returns a table. The table name can't already exist in the data model.
> The formula bar supports entering a valid DAX formula. It includes features like auto-complete, Intellisense, and color-coding, enabling you to quickly and accurately enter the formula.

### A. Creating the Table
In Power BI Desktop, to create the Salesperson calculated table, I proceed as follows:  
1. In Report view I selected **New Table** on the Modeling ribbon from inside the Calculations group.
2. In the formula bar, I typed `Salesperson = 'Salesperson (Performance)'`.
3. This adds a new table named **Salesperson** in the Data pane.
> [!NOTE]
> The outcome of this DAX formula will create a copy of the Salesperson (Performance) table and assign it to a new name **Salesperson**. However, it copies the data only and discards model properties like formatting.

### B. Creating Relationships Between the Salesperson Table and Other Tables in the Model
In this task, I create a relationship from the Salesperson | EmployeeKey column to the Sales | EmployeeKey column by:
* dragging the Salesperson | EmployeeKey to Sales | EmployeeKey
* Then, I deleted the inactive relationship between the Salesperson (Performance) and Sales tables.
* Next, I added a description to the Salesperson table as **Salesperson related to Sales**.
* For the Salesperson (Performance) table, I set the description to **Salesperson related to region(s)**. This is to differentiate between the two Salesperson tables.

## Creating the Date Table
This task involved creating the Date table. To do that, I  
1. Switched to the Table view.
2. Selected New Table on the Home tab from inside the Calculations group.
3. Entered the following DAX in the formula bar: `Date = CALENDARAUTO(6)`
> [!NOTE]
> The CALENDARAUTO() function returns a single-column table consisting of date values. The “auto” behavior scans all the data model date columns to determine the earliest and latest date values stored in the present data model. It then creates one row for each date within this range, extending the range in either direction to ensure full years of data is stored.

### A. Creating Calculated Columns in the Date Table
In this task, I added more columns to the date table to enable filtering and grouping by different time periods. I also created a calculated column to control the sort order of other columns. To do that, I
1. Selected New Column on the Table Tools contextual ribbon from inside the Calculations group.
2. In the formula bar, I wrote the following DAX: `Year = "FY" & YEAR('Date'[Date]) + IF(MONTH('Date'[Date]) > 6, 1)`
> [!NOTE]
> * The above formula is used to calculate the fiscal year (FY) based on the date column or DAX. The formula assumes the fiscal year starts in July (which is the Adventure Work Fiscal year).
> * The YEAR('Date'[Date]) function extracts the calendar year from the date in the 'Date'[Date] column. "FY" adds the prefix "FY" to the year. This means the result will start with "FY" followed by the year (e.g., "FY2023").  
> The MONTH('Date'[Date]) function extracts the month from the date. Then, the formula checks if the month is greater than 6 (i.e., July or later). If the condition is true (the month is July or later), it adds 1 to the year, signifying the start of the next fiscal year. If the condition is false (the month is January to June), it keeps the same year.  
> For example: For a date in April 2023, the formula will return "FY2023", whereas for a date in August 2023, the formula will return "FY2024" because the fiscal year advances after June.




### B. Completing the Date Table
 

### C. Marking the Date Table


## Creating Simple Measures



## Creating Additional Measures






This completed the project.




</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


