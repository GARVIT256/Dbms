# Experiment 14

**Title**: To understand the concepts of function and procedure in PL/SQL.

**Objective**: Students will be able to implement the Pl/SQL programs using function
and procedure.


1) PL/SQL Code to Accept Values A, B, & C and Display the Greatest Value:

```sql
DECLARE
    A NUMBER := 10;
    B NUMBER := 20;
    C NUMBER := 15;
BEGIN
    IF A > B AND A > C THEN
        DBMS_OUTPUT.PUT_LINE('A is the greatest with value: ' || A);
    ELSIF B > A AND B > C THEN
        DBMS_OUTPUT.PUT_LINE('B is the greatest with value: ' || B);
    ELSE
        DBMS_OUTPUT.PUT_LINE('C is the greatest with value: ' || C);
    END IF;
END;
/
```
Output:-

<img title="Exp" alt="Image" src="14_1.png">

2) PL/SQL Code to Display a Message 20 Times Using a Loop:
```sql

DECLARE
    i NUMBER := 1;
BEGIN
    WHILE i <= 20 LOOP
        DBMS_OUTPUT.PUT_LINE('Welcome to PL/SQL Programming');
        i := i + 1;
    END LOOP;
END;
/

```
Outut :-

<img title="Exp" alt="Image" src="14_2.png">

3) PL/SQL Code Block to Find the Factorial of a Number:
```sql

DECLARE
    num NUMBER := 5;
    fact NUMBER := 1;
    i NUMBER := 1;
BEGIN
    FOR i IN 1..num LOOP
        fact := fact * i;
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Factorial of ' || num || ' is: ' || fact);
END;
/
```
Output :-

<img title="Exp" alt="Image" src="14_3.png">

4) PL/SQL Program to Generate Fibonacci Series:
```sql

DECLARE
    n NUMBER := 10;
    a NUMBER := 0;
    b NUMBER := 1;
    temp NUMBER;
    i NUMBER := 1;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Fibonacci Series:');
    DBMS_OUTPUT.PUT_LINE(a);
    DBMS_OUTPUT.PUT_LINE(b);
    WHILE i <= n - 2 LOOP
        temp := a + b;
        DBMS_OUTPUT.PUT_LINE(temp);
        a := b;
        b := temp;
        i := i + 1;
    END LOOP;
END;
/
```
Output :-

<img title="Exp" alt="Image" src="14_4.png">

5) PL/SQL Code to Find the Sum of First N Numbers:
```sql

DECLARE
    N NUMBER := 10;
    sum NUMBER := 0;
    i NUMBER := 1;
BEGIN
    WHILE i <= N LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Sum of the first ' || N || ' numbers is: ' || sum);
END;
/
```
Output :- 

<img title="Exp" alt="Image" src="14_5.png">


# Experiment 15

**Title**: To understand the concepts of implicit and explicit cursor.

**Objective**: Students will be able to implement the concept of implicit and explicit
cursor.

## Setting up prerequisites

<img src="15_0-1.png">
<img src="15_0-2.png">
<img src="15_0-1.png">

1. Using implicit cursor update the salary by an increase of 10% for all the records in EMPLOYEES table, and finally display how many records have been updated. If no records exist display the message “No Change”.

```sql
DECLARE
    v_count NUMBER := 0;
BEGIN
    UPDATE EMPLOYEES
    SET SALARY = SALARY * 1.10;
    v_count := SQL%ROWCOUNT;

    IF v_count > 0 THEN
        DBMS_OUTPUT.PUT_LINE(v_count || ' records have been updated.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('No Change');
    END IF;
END;
```
<img src="15_1.png">

2. Using explicit cursor fetch the employee name, employee_id and salary of all the records from EMPLOYEES table.

```sql
DECLARE
    CURSOR emp_cursor IS
        SELECT employee_name, employee_id, salary FROM EMPLOYEES;
    emp_rec emp_cursor%ROWTYPE;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO emp_rec;
        EXIT WHEN emp_cursor%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.employee_name || 
                             ', ID: ' || emp_rec.employee_id || 
                             ', Salary: ' || emp_rec.salary);
    END LOOP;
    CLOSE emp_cursor;
END;
```
<img src="15_2.png">

3. Using explicit cursor Insert the records from EMPLOYEES table for the columns employee_id, Last_Name and salary for those records whose salary exceeds 2500 into a new table TEMP_EMP

```sql
DECLARE
    CURSOR emp_cursor IS
        SELECT employee_id, last_name, salary 
        FROM EMPLOYEES 
        WHERE salary > 2500;
    emp_rec emp_cursor%ROWTYPE;
BEGIN
    OPEN emp_cursor;
    
    LOOP
        FETCH emp_cursor INTO emp_rec;
        EXIT WHEN emp_cursor%NOTFOUND;
        
        INSERT ALL
            INTO TEMP_EMP (employee_id, last_name, salary) 
            VALUES (emp_rec.employee_id, emp_rec.last_name, emp_rec.salary)
        SELECT 1 FROM DUAL;
        
    END LOOP;
    
    CLOSE emp_cursor;
    
    COMMIT;  
END;
```
<img src="15_3.png">

--- 

# Garvit Gandhi | 500119058 | R292223005
