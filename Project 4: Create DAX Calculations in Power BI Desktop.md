# Project #4: Create DAX Calculations in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Creating the Salesperson Calculated Table](#Creating-the-Salesperson-Calculated-Table)
   * [A. Creating the Table](#A-Creating-the-Table)
   * [B. Creating Relationships Between the Salesperson Table and Other Tables in the Model](#B-Creating-Relationships-Between-the-Salesperson-Table-and-Other-Tables-in-the-Model)
4. [Creating the Date Table](#Creating-the-Date-table)
   * [A. Creating Calculated Columns in the Date Table](#A-Creating-Calculated-Columns-in-the-Date-Table)
     * [Creating the Year Column](#Creating-the-Year-Column)
     * [Creating the Quarter Column](#Creating-the-Quarter-Column)
     * [Creating the Month Columns](#Creating-the-Month-Column)
   * [B. Completing the Date Table](#B-Completing-the-Date-Table)
   * [C. Marking the Date Table](#C-Marking-the-Date-table)
6. [Creating Simple Measures](#Creating-simple-measures)
7. [Creating Additional Measures](#Creating-additional-measures)

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
> * A calculated table is created by entering the table name, the equals symbol (=), and a DAX formula that returns a table. The table name can't already exist in the data model.
> * The formula bar supports entering a valid DAX formula. It includes features like auto-complete, Intellisense, and color-coding, enabling you to quickly and accurately enter the formula.

### A. Creating the Table
In Power BI Desktop, to create the Salesperson calculated table, I proceed as follows:  
1. In Report view I selected **New Table** on the Modeling ribbon from inside the Calculations group.
2. In the formula bar, I typed  
   `Salesperson = 'Salesperson (Performance)'`.
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
3. Entered the following DAX in the formula bar:  
   `Date = CALENDARAUTO(6)`
> [!NOTE]
> The CALENDARAUTO() function returns a single-column table consisting of date values. The “auto” behavior scans all the data model date columns to determine the earliest and latest date values stored in the present data model. It then creates one row for each date within this range, extending the range in either direction to ensure full years of data is stored.

### A. Creating Calculated Columns in the Date Table
In this task, I added more columns to the date table to enable filtering and grouping by different time periods. I also created a calculated column to control the sort order of other columns. 

#### Creating the Year Column
To create the Year column, I  
1. Selected New Column on the Table Tools contextual ribbon from inside the Calculations group.
2. In the formula bar, I wrote the following DAX:  
   `Year = "FY" & YEAR('Date'[Date]) + IF(MONTH('Date'[Date]) > 6, 1)`
> [!NOTE]
> * The above formula is used to calculate the fiscal year (FY) based on the date column or DAX. The formula assumes the fiscal year starts in July (which is the Adventure Work Fiscal year).
> * The YEAR('Date'[Date]) function extracts the calendar year from the date in the 'Date'[Date] column. "FY" adds the prefix "FY" to the year. This means the result will start with "FY" followed by the year (e.g., "FY2023").  
> * The MONTH('Date'[Date]) function extracts the month from the date. Then, the formula checks if the month is greater than 6 (i.e., July or later).
>   * If the condition is true (the month is July or later), it adds 1 to the year, signifying the start of the next fiscal year.
>   * If the condition is false (the month is January to June), it keeps the same year.  
> * **Example**: For a date in April 2023, the formula will return "FY2023", whereas for a date in August 2023, the formula will return "FY2024" because the fiscal year advances after June.

#### Creating the Quarter Column
To create the Quarter column, we should first bear in mind that the fiscal quarters are as follows:
* Fiscal Q1: July to September.
* Fiscal Q2: October to December.
* Fiscal Q3: January to March.
* Fiscal Q4: April to June.
  
So, I proceeded as follows to create that column:  
1. Selected New Column on the Table Tools contextual ribbon from inside the Calculations group.
2. In the formula bar, I wrote the following DAX:
```
Quarter =
'Date'[Year] & " Q"
    & IF(
        MONTH('Date'[Date]) <= 3,
        3,
        IF(
            MONTH('Date'[Date]) <= 6,
            4,
            IF(
                MONTH('Date'[Date]) <= 9,
                1,
                2
            )
        )
    )
```
> [!NOTE]
> * This DAX formula is used to calculate the fiscal quarter (Q) for each date in the 'Date' table. The formula shifts the calendar quarters to align with a fiscal year that starts in July.  
> * The `'Date'[Year] & " Q"` extracts the year from the 'Date'[Year] column. `" Q"` is concatenated to the year to indicate that the result will represent a fiscal quarter (e.g., "2023 Q").
> * In the next line of the formula `IF(MONTH('Date'[Date]) <= 3, 3, ...)`:
>   * The `MONTH('Date'[Date])` function extracts the month from the date in the `'Date'[Date]` column.
>   * The `IF` statements assign a fiscal quarter based on the month of the date. Since the fiscal year starts in July, the quarters are reassigned accordingly: If the month is January, February, or March `(<= 3)`, it's assigned fiscal quarter 3.  
> * In the next line of the formula `IF(MONTH('Date'[Date]) <= 6, 4, ...)`, if the month is April, May, or June `(<= 6)`, it’s assigned fiscal quarter 4.  
> * Then, in the following line of the formula `IF(MONTH('Date'[Date]) <= 9, 1, ...)`, if the month is July, August, or September `(<= 9)`, it’s assigned fiscal quarter 1.
> * Else, fiscal quarter 2 for October, November, and December (which are not covered by the earlier conditions).
> * **Example**: `MONTH('Date'[Date]) <= 3, 3)` will output `"2023 Q3"` if the fiscal year is 2023 and the month is January, February, or March.

#### Creating the Month Column
1. Selected New Column on the Table Tools contextual ribbon from inside the Calculations group.
2. In the formula bar, I wrote the following DAX:
   ```
   Month =
   FORMAT('Date'[Date], "yyyy MMM")
   ```
> [!NOTE]
> * This DAX formula is used to format the date into a specific year and month format for each entry in the 'Date' table. It is used to create a more readable and concise representation of the date.  
> * In the formula `FORMAT('Date'[Date], "yyyy MMM")`, the `FORMAT` function is used to convert the value of `'Date'[Date]` into a custom text format.
>   * The first argument `'Date'[Date]` is the date column in the 'Date' table.
>   * The second argument, `"yyyy MMM"` specifies the desired format:
>     * `"yyyy"` represents the full year (4 digits) and
>     * `"MMM"` represents the abbreviated month name (3 letters). 

### B. Completing the Date Table
 

### C. Marking the Date Table


## Creating Simple Measures



## Creating Additional Measures






This completed the project.




</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


