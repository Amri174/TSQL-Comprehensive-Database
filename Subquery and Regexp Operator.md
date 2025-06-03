## SUBQUERY AND REGEXP OPERATOR

### TABLE

**Departments Table:**
````
create table Departments (
  DepartmentID number not null,
  Name Varchar2(100) not null,
  LocationID number
);
````
**Employee Table:**
````
create table Employees (
  EmployeeID number not null,
  Firstname Varchar2(50) not null,
  Lastname Varchar2(50) not null,
  Email Varchar2(100) unique not null,
  HireDate date not null default sysdate,
  Salary number(10, 2) check (salary > 0),
  DepartmentID number,
  primary key (EmployeeID)
);
````


### ALTER QUERY USECASES

````
alter table Employees add (Phone Varchar(20));
alter table Departments add (ManagerID number);

alter table Employees add (Address Varchar2(100), City Varchar2(50));
alter table Departments add (Floor number, Extension Varchar2(10));

alter table Employees drop (Phone);
alter table Departments drop (Extension);

alter table Employees drop (Address, City);
alter table Departments drop (Floor, ManagerID);

alter table Employees modify Salary number(12, 2) after HireDate;
alter table Departments modify Name Varchar2(150);

alter table Employees modify HireDate default SYSDATE;
alter table Departments modify LocationID default 100;

alter table Employees rename column Firstname to FirstName;
alter table Employees rename column Lastname to LastName;

alter table Employees rename to Staff;
alter table Departments rename to Divisions;

alter table Departments add primary key (DepartmentID);

alter table Employees add constraint fkdept foreign key (DepartmentID) references Departments(DepartmentID);

alter table Employees drop constraint fkdept; 
alter table Employees drop constraint UniqueEmail;

alter table Employees drop constraint UniqueEmail;
alter table Departments drop index UniqueDepartmentName;
````


### SUBQUERY
**Scalar:**
````
select Name, (select MAX(Salary) from Employees) Max_Salary
from Departments;
````
**Row:**
````
select name
from Employees
where (DepartmentID, Salary) in (select DepartmentID, MAX(Salary) from Employees
group by DepartmentID);
````
**Column:**
````
select Name
from Employees
where DepartmentID in (select DepartmentID from Departments where LocationID = 1000);
````
**Table:**
````
select *
from (select Name, Salary from Employees where Salary > 50000) High_Salary_Employees;
````
**Correlated:**
````
select e1.name
from Employees e1
where e1.Salary > (select AVG(e2.salary) from Employees e2 where e2.DepartmentID
= e1.DepartmentID);
````


### REGEXP OPERATOR

* Match Firstname starting with 'A'

&nbsp;&nbsp; ````select FirstName from Employees where REGEXP_LIKE(FirstName, '^A', 'i');````

* Match Lastname ending with 'y'

&nbsp;&nbsp; ````select LastName from Employees where REGEXP_LIKE(LastName, 'y$');````

* Match Firstname containing 'e' (case-sensitive)

&nbsp;&nbsp; ````select FirstName from Employees where REGEXP_LIKE(FirstName, 'e');````

* Match Firstname with exactly three characters

&nbsp;&nbsp; ````select FirstName from Employees where REGEXP_LIKE(FirstName, '^.{3}$');````

* Match Firstname starting with 'M' or 'N'

&nbsp;&nbsp; ````select FirstName from Employees where REGEXP_LIKE(FirstName, '^[MN]');````

* Match Lastname containing two consecutive 'a's

&nbsp;&nbsp; ````select LastName from Employees where REGEXP_LIKE(LastName, 'aa');````

* Match Email containing digits

&nbsp;&nbsp; ````select Email from Employees where REGEXP_LIKE(Email, '[0-9]');````

* Match Firstname without vowels

&nbsp;&nbsp; ````select FirstName from Employees where REGEXP_LIKE(FirstName, '^[^AEIOUaeiou]*$');````

* Match Firstname starting with a capital letter

&nbsp;&nbsp; ````select FirstName from Employees where REGEXP_LIKE(FirstName, '^[A-Z]');````

* Validate Email format

&nbsp;&nbsp; ````select Email from Employees where REGEXP_LIKE(Email, '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');````

* Match phone numbers in format 123-456-7890

&nbsp;&nbsp; ````select Phone from Employees where REGEXP_LIKE(Phone, '^[0-9]{3}-[0-9]{3}-[0-9]{4}$');````

* Match dates in YYYY-MM-DD format

&nbsp;&nbsp; ````select HireDate from Employees where REGEXP_LIKE(TO_CHAR(HireDate, 'YYYY-MM-DD'), '^[0-9]{4}-[0-9]{2}-[0-9]{2}$');````

* Match Firstname with special characters

&nbsp;&nbsp; ````select FirstName from Employees where REGEXP_LIKE(FirstName, '[!@#$%^&*()]');````

* Match Lastname with only alphabets

&nbsp;&nbsp; ````select LastName from Employees where REGEXP_LIKE(LastName, '^[A-Za-z]+$');````

* Match Address containing whitespace

&nbsp;&nbsp; ````select Address from Employees where REGEXP_LIKE(Address, '\s');````

* Match Department names starting with 'Dev'

&nbsp;&nbsp; ````select Name from Departments where REGEXP_LIKE(Name, '^Dev');````

* Match Job titles ending with 'Manager'

&nbsp;&nbsp; ```` select JobTitle from Employees where REGEXP_LIKE(JobTitle, 'Manager$');````

* Validate alphanumeric EmployeeID (if stored as string)

&nbsp;&nbsp; ```` select EmployeeID from Employees where REGEXP_LIKE(EmployeeID, '^[A-Za-z0-9]+$');````

* Match non-alphabetic characters in Address

&nbsp;&nbsp; ````select Address from Employees where REGEXP_LIKE(Address, '[^A-Za-z]');````

* Validate ID format A12345678 (if applicable)

&nbsp;&nbsp; ````select EmployeeID from Employees where REGEXP_LIKE(EmployeeID, '^A[0-9]{8}$');````



