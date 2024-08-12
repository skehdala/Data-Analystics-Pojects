# SQL COMPLETE PROJECT
- [Project Overview](Project-Overview)
- [MySQL Forward Engineering](MySQL-Forward-Engineering)
- [Creating schema called helpdesk](creating-schema-called-helpdesk)
  
# SQL PROJECT PHASE 1
## PROJECT OVERVIEW
In this project, I will guide you step by step on how I created tables using MySQL from zero then join the tables and query the two tables.
After deep research, i created SQL code in 3 phases that will guide you follow along with my project.
Make sure the you have MySQL up and running.
## THE FIRST SQL FILE CREATION
I name this file as Helpdesk_setup
### MySQL Forward Engineering
In SQL, forward engineering involves converting a data model or design into an actual database schema by generating the SQL scripts needed to create tables, relationships, and other database structures
```SQL
SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';
```
### CREATING SCHEMA CALLED HELPDESK
Drop any schema having the same name
```SQL
DROP SCHEMA IF EXISTS `helpdesk` ;
```
Create a new schema called helpdesk and used it
```SQL
CREATE SCHEMA IF NOT EXISTS `helpdesk` DEFAULT CHARACTER SET utf8 ;
USE `helpdesk` ;
```
### CREATING THE FIRST TABLE EMPLOYEE
Drop any existing table with the name employee and create a new one
```SQL
DROP TABLE IF EXISTS `employee` ;

CREATE TABLE IF NOT EXISTS `employee` (
  `idEmployee` INT NOT NULL AUTO_INCREMENT,
  `FirstName` VARCHAR(45) NULL DEFAULT NULL,
  `LastName` VARCHAR(45) NULL DEFAULT NULL,
  `Location` VARCHAR(45) NULL DEFAULT NULL,
  PRIMARY KEY (`idEmployee`))
ENGINE = InnoDB
AUTO_INCREMENT = 1
DEFAULT CHARACTER SET = utf8;
```
### CREATING THE SECOND TABLE TICKETS
Drop any existing table with the name tickets and create a new one
```SQL
DROP TABLE IF EXISTS `tickets` ;

CREATE TABLE IF NOT EXISTS `tickets` (
  `idTickets` INT NOT NULL AUTO_INCREMENT,
  `Description` VARCHAR(45) NULL DEFAULT NULL,
  `Duration` INT NULL DEFAULT NULL,
  `Priority` VARCHAR(45) NULL DEFAULT NULL,
  `Status` VARCHAR(45) NULL DEFAULT NULL,
  `Employee_idEmployee` INT NULL DEFAULT NULL,
  PRIMARY KEY (`idTickets`),
  INDEX `fk_Orders_Employee_idx` (`Employee_idEmployee` ASC),
  CONSTRAINT `fk_Orders_Employee`
    FOREIGN KEY (`Employee_idEmployee`)
    REFERENCES `employee` (`idEmployee`))
ENGINE = InnoDB
AUTO_INCREMENT = 1
DEFAULT CHARACTER SET = utf8;
```
### RESTORING SETTINGS FOR MySQL MODE
This code restores the original settings for SQL mode, foreign key checks, and unique checks in a MySQL database. It assigns the previously saved values back to their respective system variables. This is typically done after temporarily modifying these settings for specific operations, such as bulk data imports, to ensure the database returns to its original configuration.
```SQL
SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
```
Congrats you just created two new table using SQL

# SQL PROJECT PHASE 2
## Now we inserts values into the table that were created in PROJECT1
We start with employee table
```SQL
INSERT INTO `helpdesk`.`employee` (`FirstName`, `LastName`, `Location`) VALUES 
('Will', 'Smith','MD'),
('Ben', 'Johnson','MD'),
('Charlie', 'Jackson','MD'),
('Diamond', 'Lee','CA'),
('Elena', 'Gomez','CA'),
('Fabian', 'Williams','CA'),
('Giriraj', 'Patel','CA');
```
We can read the tale 
```SQL
select * from employee;
```
We insert values into the second table tickets
```SQL
INSERT INTO `helpdesk`.`tickets` (`Description`, `Duration`, `Priority`, `Status`, `Employee_idEmployee`) VALUES 
('Malware', '33','3-Low', 'Completed','1'),
('Virus', '17','1-High', 'In Progress','7'),
('Hardware', Null,'3-Low', 'Not Started',Null),
('Malware', '28','1-High', 'Completed','7'),
('Virus', '14','2-Medium', 'Completed','5'),
('Virus', '20','2-Medium', 'Completed','2'),
('Virus', Null,'3-Low', 'Not Started',Null),
('Malware', '27','2-Medium', 'In Progress','7'),
('Malware', '18','3-Low', 'Completed','1'),
('Hardware', '63','2-Medium', 'Completed','7'),
('Malware', '7','3-Low', 'Completed','2'),
('Malware', '8','1-High', 'In Progress','2'),
('Virus', '40','3-Low', 'Completed','7'),
('Software', '42','3-Low', 'Completed','7'),
('Virus', Null,'1-High', 'Not Started',Null),
('Hardware', '12','3-Low', 'Completed','2'),
('Malware', '33','3-Low', 'Completed','2'),
('Virus', '53','2-Medium', 'Completed','4'),
('Malware', '15','1-High', 'Completed','2'),
('Hardware', '16','2-Medium', 'In Progress','7'),
('Malware', '16','3-Low', 'Completed','2'),
('Hardware', '11','3-Low', 'Completed','7'),
('Virus', '27','3-Low', 'Completed','7'),
('Malware', Null,'1-High', 'Not Started',Null),
('Internet', '36','2-Medium', 'In Progress','4'),
('Internet', '40','2-Medium', 'Completed','2'),
('Malware', '39','2-Medium', 'Completed','5'),
('Malware', '39','3-Low', 'Completed','2'),
('Malware', Null,'1-High', 'Not Started',Null),
('Hardware', '20','1-High', 'Completed','1')
;
```
We can read the tale 
```SQL
select * from tickets;
```
Congrats, now we have two databases created

# QUESTIONS AND ANSWERS PHASE 3

1. Print the first name, last name, ticket ID, ticket description, and duration of the employees who are assigned with a ticket(s). Sort them first alphabetically by first name (starting with letter A at the top) and then ascending by Duration.
```SQL
SELECT employee.FirstName, employee.LastName, tickets.idTickets, tickets.Description, tickets.Duration
FROM employee
INNER JOIN tickets
ON employee.idEmployee = tickets.Employee_idEmployee
ORDER BY employee.FirstName ASC, tickets.Duration ASC;
```
![image](https://github.com/user-attachments/assets/419c27ef-be86-4928-b299-6957ad73fc3d)

2. We want to get a workload by employee printout.  For every employee, print the first name, last name, all ticket ID numbers assigned to that employee, the ticket description, and ticket duration of our records.  Include only tickets which have been assigned to an employee.  Include all employees, even if that person doesn’t have any tickets in the current database. Sort them first alphabetically by first name (starting with letter A at the top) and then ascending by ticket duration.
```SQL
SELECT employee.FirstName, employee.LastName, tickets.idTickets, tickets.Description, tickets.Duration
FROM employee
LEFT JOIN tickets
ON employee.idEmployee = tickets.Employee_idEmployee
ORDER BY employee.FirstName ASC, tickets.Duration ASC;
```
![image](https://github.com/user-attachments/assets/f3ae4339-2403-41ca-adeb-b209b97978e8)

3. We want to get an idea of how many tickets we have and what our issues are.  Print the ticket ID number, ticket description, ticket priority, ticket status, and if the information is available, employee first name assigned to it for our records.  Include all tickets regardless of whether they have been assigned to an employee or not.  Sort it alphabetically by ticket status, and then numerically by ticket ID, with lower ticket IDs on top.
```SQL
SELECT tickets.idTickets, tickets.Description, tickets.Priority, tickets.Status, employee.FirstName
FROM employee
RIGHT JOIN tickets
ON employee.idEmployee = tickets.Employee_idEmployee
ORDER BY tickets.Status ASC, tickets.idTickets ASC;
```
![image](https://github.com/user-attachments/assets/d05936b9-9188-499e-a9bc-573e49a93a3c)

4. Management wants to pay special attention to calls which are in progress and for which the duration is currently 20 minutes or longer (include calls of exactly 20 minutes duration).  Print the ticket ID number, description, duration, priority, status, and the employee first name for all of these calls.
```SQL
SELECT tickets.idTickets, tickets.Description, tickets.Duration, tickets.Priority, tickets.Status, employee.FirstName
FROM employee
RIGHT JOIN tickets
ON employee.idEmployee = tickets.Employee_idEmployee
WHERE tickets.Duration>=20 AND tickets.Status='In Progress';
```
![image](https://github.com/user-attachments/assets/a1cc1c74-a09a-4862-ba3a-6d26455fc3e2)

5. You suspect there has been a malware breach at the Maryland facility.  They’re not sure if it’s an inside job (involving one of your employees) or an outside job (involving an outside attack.)  Make a listing of all high priority helpdesk tickets which have either been identified as malware, or which were taken by an employee whose location is in the Maryland facility.  Print the description, duration, ticket ID number, ticket status, employee first name, employee location, and priority of ticket.    Sort it alphabetically by description, then by duration (longest duration on top), then ascending by ticket ID number.
```SQL
SELECT tickets.Description, tickets.Duration, tickets.idTickets, tickets.Status, employee.FirstName, employee.Location, tickets.Priority
FROM employee
INNER JOIN tickets
ON employee.idEmployee=tickets.Employee_idEmployee
WHERE tickets.Priority='1-High' AND (tickets.Description='Malware' OR employee.Location='MD')
ORDER BY tickets.Description ASC, tickets.Duration DESC, tickets.idTickets ASC;
```
![image](https://github.com/user-attachments/assets/0780c9af-c869-453e-bd86-0faf3d9ead18)

6. We want to see the total duration for completed helpdesk calls by employee.   Only include employees who have completed helpdesk tickets; if an employee doesn’t have any completed tickets, their name should not show up in this report.   Generate a report for which the 
-	First column contains the employee’s first and last name (don’t use two columns for this – put the first and last name together)
-	Second column contains the total duration of all completed tickets by that employee.  If an employee had more than one ticket, add the durations together.
-	Report is sorted so the largest total duration is on the top, and then alphabetically by employee name (sort it using the “First Last” combination, so that “Mickey Mouse” would come before “Nancy Mouse”.)
-	Only include completed tickets; don’t include those in progress or not yet started.
```SQL
SELECT CONCAT_WS(" ", FirstName, LastName) AS EmployeeName, SUM(tickets.Duration) AS TotalDuration
FROM employee
RIGHT JOIN tickets
ON employee.idEmployee=tickets.Employee_idEmployee
WHERE tickets.Status='Completed'
GROUP BY EmployeeName
ORDER BY TotalDuration DESC, EmployeeName ASC;
```
![image](https://github.com/user-attachments/assets/b8de7f8c-0825-4d1a-9dfd-d1f4edce8191)

7. Do the same as Problem 6 above, except in addition to the sum of the ticket durations, also include an additional column to give us the number of completed tickets as well.  Now sort your database so the largest number of completed tickets is on the top.

Here's a sample of the output for Mr. Duck and Mr. Mouse.
![image](https://github.com/user-attachments/assets/1da441d6-1e39-4705-af76-d34d89289791)
```SQL
SELECT CONCAT_WS(" ", FirstName, LastName) AS EmployeeName, SUM(tickets.Duration) AS TotalDuration, COUNT(tickets.Status) AS TotalCompletedTickets
FROM employee
RIGHT JOIN tickets
ON employee.idEmployee=tickets.Employee_idEmployee
WHERE tickets.Status='Completed'
GROUP BY EmployeeName
ORDER BY TotalCompletedTickets DESC;
```
![image](https://github.com/user-attachments/assets/2c038c40-2927-4127-9d15-6d10798162ed)

8. You want to learn more about the average duration of all tickets taken by employees in California.  Include all tickets which have been completed or are in progress by employees in California.  Sort them alphabetically by priority, and then alphabetically by ticket description.  Additionally, group them first by priority (highest on top), then alphabetically by description.  So your final report will look something like this (your data may vary).
![image](https://github.com/user-attachments/assets/9c1963f6-67bb-4d5f-9af1-151bc8581755)
```SQL
SELECT tickets.Priority, tickets.Description, AVG(tickets.Duration)
FROM employee
RIGHT JOIN tickets
ON employee.idEmployee=tickets.Employee_idEmployee
WHERE employee.Location='CA' AND (tickets.Status='In Progress' OR tickets.Status='Completed')
GROUP BY tickets.Priority, tickets.Description
ORDER BY tickets.Priority ASC, tickets.Description ASC;
```
![image](https://github.com/user-attachments/assets/4cc69904-2365-494c-85e6-646db686c600)

9. Your management wants to know what the different types of tickets are.  Write a query that uniquely identifies ticket type based on the ticket description.
```SQL
SELECT DISTINCT tickets.Description AS TicketType FROM tickets;
```
![image](https://github.com/user-attachments/assets/d6284cca-d8b2-40df-8471-81a0dbe25928)
