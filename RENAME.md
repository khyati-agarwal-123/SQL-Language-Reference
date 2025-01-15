##  RENAME {#GUID-573347CE-3EB8-42E5-B4D5-EF71CA06FAFC} 

Purpose 

> **note:** 

You cannot roll back a ` RENAME ` statement. 

Use the ` RENAME ` statement to rename a table, view, sequence, private synonym, or property graph. 

  * Oracle Database automatically transfers integrity constraints, indexes, and grants on the old object to the new object. 

  * Oracle Database invalidates all objects that depend on the renamed object, such as views, synonyms, and stored procedures and functions that refer to a renamed table. 




> **note:** See Also: 

[ CREATE SYNONYM ](CREATE-SYNONYM.md#GUID-A806C82F-1171-478E-A910-F9C6C42739B2) and [ DROP SYNONYM ](DROP-SYNONYM.md#GUID-C7293D40-83B8-4E60-9E90-CB907F2CA6C7)

Prerequisites 

The object must be in your own schema. 

Syntax 

*rename* ::= 

![Description of rename.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rename.gif)[ Description of the illustration rename.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/rename.md)

Semantics 

*old_name* 

Specify the name of an existing table, view, sequence, or private synonym. 

*new_name* 

Specify the new name to be given to the existing object. The new name must not already be used by another schema object in the same namespace and must follow the rules for naming schema objects. 

Restrictions on Renaming Objects 

Renaming objects is subject to the following restrictions: 

  * You cannot rename a public synonym. Instead, drop the public synonym and then re-create the public synonym with the new name. 

  * You cannot rename a type synonym that has any dependent tables or dependent valid user-defined object types. 




> **note:** See Also: 

" [ Database Object Naming Rules ](Database-Object-Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA) " 

Examples 

Renaming a Database Object: Example 

The following example uses a copy of the sample table ` hr.departments ` . To change the name of table ` departments_new ` to ` emp_departments ` , issue the following statement: 
    
    
    ```
    RENAME departments_new TO emp_departments;
    
    ```

You cannot use this statement directly to rename columns. However, you can rename a column using the ` ALTER ` ` TABLE ` ... *rename_column_clause* . 

> **note:** See Also: 

*rename_column_clause* 

Another way to rename a column is to use the ` RENAME ` statement together with the ` CREATE ` ` TABLE ` statement with ` AS ` *subquery* . This method is useful if you are changing the structure of a table rather than only renaming a column. The following statements re-create the sample table ` hr.job_history ` , renaming a column from ` department_id ` to ` dept_id ` : 
    
    
    ```
    CREATE TABLE temporary 
       (employee_id, start_date, end_date, job_id, dept_id) 
    AS SELECT 
         employee_id, start_date, end_date, job_id, department_id
    FROM job_history; 
    
    DROP TABLE job_history; 
    
    RENAME temporary TO job_history; 
    
    ```

Any integrity constraints defined on table ` job_history ` will be lost in the preceding example. You will have to redefine them on the new ` job_history ` table using an ` ALTER ` ` TABLE ` statement. 
