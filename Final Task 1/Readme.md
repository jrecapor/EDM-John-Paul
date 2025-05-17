# Final Lab Task 1 - MySQL Basics

## Task 1: Create a table named employee with the following fields:
- employee_id: Unique integer, auto-increment, primary key.
- employee_name: String (VARCHAR) with up to 255 characters, not null.
- manager_id: Integer, foreign key referencing employee_id in the same table (employees).
## Task 2: Create a table named departments with the following fields:
- department_id: Unique interger, auto-increment,primary key.
- department_name: String (VARCHAR) with up to 255 characters, not null.
## Task 3: Create a table named employee departments with the following fields:
- employee_id: Interger, foreign key referencing employee_id in employees.
- department_id: Interger, foreign key referencing department_id in **departments.
- Composite primary key (employee_id, department_id).
## Task 4: Create a table named employee projects with the following fields:
- employee_id: Interger, foreign key referencing employee_id in employees.
- project_name: String (VARCHAR) with up to 255 characters, not null.
## Task 5: Create a table named managers with the following fields:
- manager_id: Unique interger, auto_increment, primary key.
- employee_id: Interger, foreign key referencing employee_id in employees.

## Query Statements & Table Structure:
### Task 1:
#### Query:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/TASK1.PNG)
#### Table:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/TAble1.PNG)
### Task 2:
#### Query:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/task2.PNG)
#### Table:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/Table2.PNG)
### Task 3:
#### Query:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/task3.PNG)
#### Table:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/TAble3.PNG)
### Task 4:
#### Query:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/task4.PNG)
#### Table:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/TAble4.PNG)
### Task 5:
#### Query:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/task5.PNG)
#### Table:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/table5.PNG)
## ER Diagram:
![screenshot](https://github.com/jrecapor/EDM-John-Paul/blob/main/Final%20Task%201/Images/er.PNG)
