# Project #4: Create DAX Calculations in Power BI Desktop

## Table of content
1. [Introduction](#Introduction)
2. [Project Objectives](#Project-Objectives)
3. [Creating the Salesperson Calculated Table](#Creating-the-Salesperson-Calculated-Table)
   * [Creating the Table](#Creating-the-Table)
   * [Creating Relationships Between the Salesperson Table and Other Tables in the Model](#Creating-Relationships-Between-the-Salesperson-Table-and-Other-Tables-in-the-Model)
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

### Creating the Table
In Power BI Desktop, to create the Salesperson calculated table, I proceed as follows:  
1. In Report view I selected **New Table** on the Modeling ribbon from inside the Calculations group.
2. In the formula bar, I typed `Salesperson = 'Salesperson (Performance)'`.
3. This adds a new table named **Salesperson** in the Data pane.
> [!NOTE]
> The outcome of this DAX formula will create a copy of the Salesperson (Performance) table and assign it to a new name **Salesperson**. However, it copies the data only and discards model properties like formatting.

### Creating Relationships Between the Salesperson Table and Other Tables in the Model
In this task, I create a relationship from the Salesperson | EmployeeKey column to the Sales | EmployeeKey column by:
* dragging the Salesperson | EmployeeKey to Sales | EmployeeKey
* Then, I deleted the inactive relationship between the Salesperson (Performance) and Sales tables.
* Next, I added a description to the Salesperson table as **Salesperson related to Sales**.
* For the Salesperson (Performance) table, I set the description to **Salesperson related to region(s)**. This is to differentiate between the two Salesperson tables.

## Creating the Date Table


### A. Creating Calculated Columns in the Date Table


### B. Completing the Date Table
 

### C. Marking the Date Table


## Creating Simple Measures



## Creating Additional Measures






This completed the project.




</br></br>

Author [Edwige Songong](https://github.com/Songonge) powered by [Microsoft Certified: Power BI Data Analyst Associate](https://learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/?practice-assessment-type=certification)


