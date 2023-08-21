# SQL_Table

CREATE TABLE Table_1(
Column_1 TYPE columnConstraint_1,
Column_2 TYPE columnConstraint_2,
...
Column_n TYPE columnConstraint_n)

' Where "TYPE"={NOT NULL, UNIQUE. CHECK, EXCLUSION, PRIMARY KEY, FOREIGN KEY)

' Where columnConstraint := {CHECK, REFERENCES, UNIQUE, PRIMARY KEY} *I will need to check this again*

## Example
>
>CREATE TABLE Persons( PersonID PRIMARY KEY int, LastName varchar(255)
