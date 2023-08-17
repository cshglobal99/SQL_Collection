# SQL_Collection
# This repository will showcase my development in SQL
Date: 17/08/2023

# Creates a table of Crowd Control abilities	CREATE TABLE Crowd_Control(
Spell_Name VARCHAR(30) PRIMARY KEY,
Class VACHAR(15) NOT NULL,
Specialization VACHAR(15) NOT NULL,
Duration TINYINT,
CoolDown TINYINT,
CC_Type TINYTEXT,
Dispellable Boolean
);
	
# Add/Remove extra column
ALTER TABLE Crowd_Control
ADD Column Damange_Break Boolean
DROP Column Character_Race
RENAME Column CoolDown to Cooldown;
	In case you make a typo, you can rename columns.

# Add data values into the table	
INSERT INTO Crowd_Control (Spell_Name, Class, Specialization, Cooldown, CC_Type)
VALUES
(‘Freezing Trap’, ‘Hunter’, ‘All’, 24, ‘Incapacitate’),
(‘Fear’, ‘Warlock’, ‘All’, 0, ‘Fear’),
(‘Polymorph’, ‘Mage’, ‘All’, 0, ‘Incapacitate’)
('Sap', 'Rogue', 'All', 0, 'Incapacitate'),
('Cheap Shot', 'Rogue', 'All', 0,'Stun')
(‘Trap’, ‘Hunter’, ‘All’, 24, ‘Incapacitate’)
;

# Delete wrong input from table	DELETE FROM Crowd_Control
WHERE Spell_Name=’Trap’	
Update Columns/Data	Update [Crowd_Control]
Set Dispellable = 0
Where Spell_Name = 'Cheap Shot';
# If no “WHERE” is added, it will add the value 0 for all rows.

# Data Query
SELECT Class, CC_Type, Count(CC_Type) FROM [Crowd_Control]
Group by CC_Type	
