[Previous](ROLLBACK.md) [Next](SELECT.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: MERGE to UPDATE](SQL-Statements-MERGE-to-UPDATE.md)
  3. SAVEPOINT 

## SAVEPOINT

Purpose

Use the `SAVEPOINT` statement to create a name for a system change number
(SCN), to which you can later roll back.

See Also:

  * [Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT016) for information on savepoints. 

  * [ROLLBACK](ROLLBACK.md#GUID-94551F0C-A47F-43DE-BC68-9B1C1ED38C93) for information on rolling back transactions 

  * [SET TRANSACTION](SET-TRANSACTION.md#GUID-F11E1E30-5871-48D1-8266-F80A1DF126A1) for information on setting characteristics of the current transaction 

Prerequisites

None.

Syntax

savepoint::=

![Description of savepoint.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/savepoint.gif)  
[Description of the illustration savepoint.eps](img_text/savepoint.md)

Semantics

savepoint

Specify the name of the savepoint to be created.

Savepoint names must be distinct within a given transaction. If you create a
second savepoint with the same identifier as an earlier savepoint, then the
earlier savepoint is erased. After a savepoint has been created, you can
either continue processing, commit your work, roll back the entire
transaction, or roll back to the savepoint.

Examples

Creating Savepoints: Example

To update the salary for `Banda` and `Greene` in the sample table
`hr.employees`, check that the total department salary does not exceed
314,000, then reenter the salary for `Greene`:

    
    
    UPDATE employees 
        SET salary = 7000 
        WHERE last_name = 'Banda';
    SAVEPOINT banda_sal;
    
    UPDATE employees 
        SET salary = 12000 
        WHERE last_name = 'Greene';
    SAVEPOINT greene_sal;
    
    SELECT SUM(salary) FROM employees;
    
    ROLLBACK TO SAVEPOINT banda_sal;
     
    UPDATE employees 
        SET salary = 11000 
        WHERE last_name = 'Greene';
     
    COMMIT; 


[← Previous](ROLLBACK.md)

[Next →](SELECT.md)
