# SQL PROJECT 1
## CREATING TWO TABLES FROM SCRATCH (EMPLOYEE & TICKETS)
In this project, I will guide you step by step on how I created this project using MySQL from zero.
I spent a lot of time researching to create the two SQL code files that will help you follow along with my project.
Make sure the you have DBMS up and running.
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
