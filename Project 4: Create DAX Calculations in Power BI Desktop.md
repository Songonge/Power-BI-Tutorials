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
     * [Creating the Month Column](#Creating-the-Month-Column)
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
   ```
   Salesperson = 'Salesperson (Performance)'
   ```
4. This adds a new table named **Salesperson** in the Data pane.
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
   ```
   Date = CALENDARAUTO(6)
   ```
> [!NOTE]
> The CALENDARAUTO() function returns a single-column table consisting of date values. The “auto” behavior scans all the data model date columns to determine the earliest and latest date values stored in the present data model. It then creates one row for each date within this range, extending the range in either direction to ensure full years of data is stored.

### A. Creating Calculated Columns in the Date Table
In this task, I added more columns to the date table to enable filtering and grouping by different time periods. I also created a calculated column to control the sort order of other columns. 

#### Creating the Year Column
To create the Year column, I  
1. Selected New Column on the Table Tools contextual ribbon from inside the Calculations group.
2. In the formula bar, I wrote the following DAX:  
   ```
   Year = "FY" & YEAR('Date'[Date]) + IF(MONTH('Date'[Date]) > 6, 1)
   ```
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
1. Added a new column to the table.
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
1. Added a New Column to the Date table.
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

> [!IMPORTANT]
> By default, Power BI orders text alphabetically, numbers from smallest to largest, and dates from earliest to latest. For that reason, if you construct a matrix in Power BI Desktop with the current **Date** table adding the following columns: Date, Year, Quarter, and Month, you will realize that the Month column is sorted alphabetically (starting with August) instead of chronologically (starting from January). So you need to customize the Month column.

To customize the Month column, I  
1. Added a new column to the Date table.
2. Wrote the following DAX in the formula bar:
   ```
   MonthKey =
   (YEAR('Date'[Date]) * 100) + MONTH('Date'[Date])
   ```
> [!NOTE]
> * This DAX formula is used to create a MonthKey that uniquely identifies each year and month in a numeric format. The MonthKey is commonly used for sorting or grouping in time-series analysis because it provides a unique numeric value that easily differentiates between different months and years. It is especially useful when you need a continuous sequence of months for easier calculations or comparisons, like when dealing with fiscal calendars, rolling averages, or time-based visualizations.
> * In the formula,
>   * the `YEAR('Date'[Date])` function extracts the year from the date in the 'Date'[Date] column.
>   * the `MONTH('Date'[Date])` function extracts the month from the date.
>   * In the term `YEAR('Date'[Date]) * 100`, the extracted year is multiplied by 100 to shift the year to the left by two decimal places, creating space for the month to follow.  
>   * `(YEAR('Date'[Date]) * 100) + MONTH('Date'[Date])` adds the month to the year-multiplied-by-100 value, creating a unique numeric key for each year and month combination. For example:
> * **Example**: 202300 + 4 = 202304 represents April 2023 in a compact numeric format.

3. The Month column should be sorted using the MonthKey column. To do that,   
   * On the Column Tools contextual ribbon, from inside the Sort group, I Selected Sort by Column.
   * I Chose MonthKey from the list. 

### B. Completing the Date Table
In this task, I completed the design of the Date table by hiding a column and creating a hierarchy. Then, I created relationships to the Sales and Targets tables. To do that, I  
1. Switched to Model view.
2. In the Date table, I hid the MonthKey column since I did not need it during my analysis.
3. On the Data right side pane, I
   * Selected the Date table.
   * Right-clicked and selected the Year column
   * Selected create hierarchy from the menu.
   * Renamed it to Fiscal.
   * Right-clicked Quarter and Month and selected Add to hierarchy -> Fiscal.
4. Created the following two relationships in the Model:
   * Date | Date to Sales | OrderDate
   * Date | Date to Targets | TargetMonth
5. Hid the following two columns:
   * Sales | OrderDate
   * Targets | TargetMonth

### C. Marking the Date Table
To mark the **Date** table as a date table, I  
1. Switched to Report view.
2. Selected the Date table In the Data pane (not the date field).
3. Selected Mark as Date Table on the Table Tools contextual ribbon from inside the Calendars group.
4. In the Mark as a Date Table window, I slid the Mark as a Date Table property to Yes, and in the Choose a date column dropdown list, I selected Date. Then, I clicked on Save.

## Creating Simple Measures
In this task, I created simple measures. 
> [!NOTE]
> Simple measures aggregate values in a single column or count rows of a table.  

### Creating Measures
To create a measure, in the Data pane, I  
1. Right-clicked the Sales table.
2. Selected New Measure.
3. I added the following measure in the formula bar:
   ```
   Avg Price =
   AVERAGE(Sales[Unit Price])
   ```
4. I also created the following measures:  
   * Median Price
     ```
     Median Price =
     MEDIAN(Sales[Unit Price])
     ```
   * Min Price  
     ```
     MIN Price =
     MIN(Sales[Unit Price])
     ```
   * Max Price  
     ```
     Max Price =
     MAX(Sales[Unit Price])
     ```
   * Orders  
     ```
     Orders =
     DISTINCTCOUNT(Sales[SalesOrderNumber])
     ```
> [!NOTE]
> The `DISTINCTCOUNT()` function counts orders only once (ignoring duplicates).  
   * Order Lines
     ```
     Order Lines =
     COUNTROWS(Sales)
     ```
> [!NOTE]
> The `COUNTROWS()` function operates over a table. It summarizes a table by returning the number of rows.

### Configuring and Assigning Folders to the New Measures Created
In this task, I configured the new measures created. To do that, I  
1. Switched to Model view.
2. Multi-selected the four price measures above created: Avg Price, Max Price, Median Price, and Min Price. Then, I  
   * Set their format to two decimal places.
   * Assigned them a display folder named **Pricing**  
   * hid the Unit Price column since the **Avg Price** values are the same as that of the **Unit Price** column and will be used instead.
3. Multi-selected the **Order Lines** and **Orders** measures and configured the following requirements:  
   * Set their format to use the thousands separator.
   * Assigned both measures to a display folder named **Counts**.

## Creating Additional Measures
I created a new measure for the Targets table. 
1. First, I renamed the Targets | Target column as Targets | TargetAmount. Then,
2. I created the following measure:
```
Target =
IF(
HASONEVALUE('Salesperson (Performance)'[Salesperson]),
SUM(Targets[TargetAmount])
)
```
> [!NOTE]
> The `HASONEVALUE()` function tests whether a single value in the Salesperson column is filtered. When true, the expression returns the sum of target amounts (for just that salesperson). When false, BLANK is returned.
3. I format the Target measure for zero decimal places.
4. Hid the TargetAmount column since the Target column I just created will be used instead.

I also created the following two measures:
* Variance
```
Variance =
IF(
	HASONEVALUE('Salesperson (Performance)'[Salesperson]),
	SUM(Sales[Sales]) - [Target]
)
```
* Variance Margin
```
Variance Margin =
DIVIDE([Variance], [Target])
```
Then, I 
* Formatted the Variance measure for zero decimal places.
* Formatted the Variance Margin measure as percentage with zero decimal places.

> [!NOTE]
> * The function `DIVIDE()` Achieves division. You must pass in numerator and denominator expressions. Optionally, you can pass in a value that represents an alternate result. It handles division by zero cases.  
> * It is advised to use the DIVIDE function whenever the denominator is an expression that could return zero or BLANK.  
> * When BLANKs create unexpected results, consider using the IF and ISBLANK DAX functions to test for BLANK, and then respond appropriately.

</br></br>

This completed the project.




</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


