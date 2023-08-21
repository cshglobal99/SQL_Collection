# SQL_Table
This document lists the general Syntax rules for SQL and some examples.

## Table Creation Syntax
CREATE TABLE Table_1(  
Column_1 datatype_1 columnConstraint_1,  
Column_1 datatype_2 columnConstraint_2,  
...,  
Column_1 datatype_n columnConstraint_n);

' Where datatype_1 := {String Data Types, Numeric Data Types, Date and Time Data Types, Other Data Types, MS Access Data Types}

' Where columnConstraint_1 := {NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, DEFAULT, CREATE INDEX, **AUTO_INCREMENT**)

### Example
>CREATE TABLE Persons( PersonID int AUTO_INCREMENT,  
> LastName varchar(255),  
> FirstName varchar(255),
> MiddleName varchar(255),   
> Number int); *-Number is vague, so later on we will rename this header*  

>CREATE TABLE SkillSet( PersonID int,  
> Software varchar(255) NOT NULL,  
> Software Type varchar(255),
> Description varchar(255),  
>Ability TINYINT,  
>FOREIGN KEY (PersonID) REFERENCES YourParentTable(PersonID) *- This enables a connection between Table_1 & Table_2*  
>);

## Table_1 Adjustment
ALTER TABLE Table_1  
ADD COLUMN Column_add columnConstraint_add  
DROP COLUMN Column_delete  
RENAME COLUMN Column_i to Column_j;  

### Example
>ALTER TABLE Table_1  
ADD COLUMN EmailAddress varchat(255)  
DROP COLUMN MiddleName  
RENAME COLUMN Number to Phone;  

## Add Values into Table_1
INSERT INTO Table_1(*if empty it will include all columns*)  
VALUES(  
 (Value_11, Value_12,..., Value_1n),  
 (Value_21, Value_22,..., Value_2n),  
 ...,  
 (Value_n1, Value_n2,..., Value_nn));  


### Example
> INSERT INTO Persons(LastName,FirstName, Phone, EmailAddress)  
VALUES('Hickman',  
'Christopher',  
96893455,  
cshglobal99@gmail.com');  
