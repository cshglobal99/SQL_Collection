# SQL_Constraints
[SQL_Collection](https://github.com/cshglobal99/SQL_Collection/blob/main/INTRODUCTION.md)

Welcome to my SQL Constraints Markdown.  
This document lists the general Syntax rules for SQL and some examples.

## Column Constrains for Tables
| id | Product | Description |
|  :---:         |     :---:      |           :---:   |
| 1 | Product_1 | Description_1 |
| 2 | Product_2 | Description_2 |

White creating Constraints for tables we can make so that the id is not needed to be recorded, id est its automatic. This was you have no duplicate id's and therefore is legitabely a primarey key that can be used for referncing.

### 1) PostgreSQL - SERIAL Constrains
>CREATE TABLE Example (  
    id SERIAL PRIMARY KEY,  
    Product VARCHAR(50),  
    Description VARCHART(255)  
);  

*SERIAL is a data type in PostgreSQL that automatically generates a unique integer value for each new row inserted into the table.*  

### 2) MySQL - AUTO_INCREMENT Constrains
>CREATE TABLE Example (  
    id INT AUTO_INCREMENT PRIMARY KEY,  
    Product VARCHAR(50),  
    Description VARCHART(255)  
);  

*AUTO_INCREMENT is a keyword used in MySQL to specify that a column should automatically generate a unique value for each new row.*


| Previous | Home | Next |
|  :---:         |     :---:      |           :---:   |
| [SQL_Database](https://github.com/cshglobal99/SQL_Collection/blob/main/SQL_Database.md) |    [SQL Collection](https://github.com/cshglobal99/SQL_Collection/blob/main/INTRODUCTION.md) | [SQL_Queries](https://github.com/cshglobal99/SQL_Collection/blob/main/SQL_Queries.md)   |
