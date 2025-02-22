---
aliases: 
date: 2017-03-06
dateModified: 2024-07-07
fileClass:
  - Page
image: 
share: true
stage: 🌿 Fern
title: 445 Consulting Database
---

Fully functional relational database design for a fictional consulting company. Includes multiple stored procedures, business rules, views, and calculated columns. Built using SQL Server.

<hr>

![database ERD](./assets/images/445_fullErd.png)

## Who it Was Built for

As a final project for *INFO 445, Advanced Database Design*, I was tasked with building a fully functional and complex database.
This database was built to fulfill the needs of a fictional consulting company (<em>445 Consulting</em>).

The database tracks projects (including tasks, skills, and assigned employees), as well as client companies, and employees (with their positions, wages, and skills). This allows the consulting company to easily track its projects, employees, and clients, making the most of their resources.

This database is fully normalized, with no data redundancy or possibility for 'infinite loops'.
The final submission included several Stored Procedures for insertion of complex data (such as assigning an employee to a project with specific tasks).
The DB also includes several business rules that automatically send out alerts after certain actions are flagged, such as redundant skills being added for an employee, or an employee being assigned to too many active projects

## Example Code Snippets

### Stored Procedure

Add a salary history (a salary the employee was paid at one point)

```SQL
CREATE PROC uspAddSalaryHistory
@Fname varchar(100),
@Lname varchar(100),
@DOB DATE,
@Position varchar(100),
@Company varchar(100),
@Amount MONEY,
@BeginDate DATE,
@EndDate DATE
AS
DECLARE @PositionID INT
DECLARE @CompanyID INT
DECLARE @EmpID INT
DECLARE @EmpHistoryID INT

BEGIN
SET @PositionID = (
	SELECT PositionID FROM [POSITION]
	WHERE PositionName = @Position
)
IF @PositionID IS NULL
	RAISERROR('Position name not valid', 12, 1)
SET @CompanyID = (
	SELECT CompanyID FROM [COMPANY]
	WHERE CompanyName = @Company
)
IF @CompanyID IS NULL
	RAISERROR('Company name not valid', 12, 1)
SET @EmpID = (
	SELECT EmployeeID FROM [EMPLOYEE]
	WHERE FName = @Fname
	AND LName = @Lname
	AND DOB = @DOB
)
IF @CompanyID IS NULL
	RAISERROR('Personal info not valid', 12, 1)
SET @EmpHistoryID = (
	SELECT EmploymentHistoryID FROM [EMPLOYMENT_HISTORY]
	WHERE EmployeeID = @EmpID
	AND PositionID = @PositionID
	AND CompanyID = @CompanyID
)
IF @EmpHistoryID IS NULL
	RAISERROR('Data mismatch (person not found to have that job at that company)', 12, 1)

BEGIN TRAN TranNewSalaryHistory
	INSERT INTO [SALARY_HISTORY]([EmploymentHistoryID], BeginDate, EndDate, Amount)
	VALUES (@EmpHistoryID, @BeginDate, @EndDate, @Amount)
	IF @@Error <> 0
		ROLLBACK TRAN TranNewSalaryHistory
	ELSE
		COMMIT TRAN TranNewSalaryHistory
END
```

### Check Constraint

Employees can't have two instances of the same skill

```SQL
CREATE FUNCTION fn_LimitEmployeeSkillDuplicates()
RETURNS INT
AS
BEGIN
DECLARE @RET INT = 0
IF EXISTS (SELECT COUNT(*), SE.EmployeeID, SE.SkillID FROM SKILL_EMPLOYEE SE
	GROUP BY SE.SkillID, SE.EmployeeID
	HAVING COUNT(*) > 1)
		SET @RET = 1
RETURN @RET
END
GO

ALTER TABLE SKILL_EMPLOYEE WITH NOCHECK
ADD CONSTRAINT ck_LimitEmployeeSkillDuplicates
CHECK (dbo.fn_LimitEmployeeSkillDuplicates() = 0)
```

### Computed Column

Number of employees assigned to a project

```SQL
CREATE FUNCTION dbo.getNumProjectEmployees(@ProjectID int)
RETURNS int
AS
BEGIN
    DECLARE @RET int
    SELECT @RET = COUNT(*) FROM PROJECT_EMPLOYEE PE WHERE PE.ProjectID = @ProjectID
    RETURN @RET
END

ALTER TABLE PROJECT ADD NumEmployeesAssigned AS (dbo.getNumProjectEmployees(ProjectID))
```

### View: Project Tasks

Artificial table with description of task & assigned employee

```SQL
CREATE VIEW taskView
AS
SELECT p.ProjectName AS 'Project Name', p.ProjectDescription AS 'Project Description', e.FullName AS 'Employee Name', t.TaskName AS 'Task Name', t.TaskDesc AS 'Task Description'
FROM TASK t
JOIN PROJECT_EMPLOYEE pe ON t.ProjectEmployeeID = pe.ProjectEmployeeID
JOIN EMPLOYEE e ON pe.EmployeeID = e.EmployeeID
JOIN PROJECT p ON pe.ProjectID = p.ProjectID
GO
```
