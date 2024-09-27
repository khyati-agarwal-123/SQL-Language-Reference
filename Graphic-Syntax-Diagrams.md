[Previous](How-to-Read-Syntax-Diagrams.md) [Next](Backus-Naur-Form-
Syntax.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ How to Read Syntax Diagrams](How-to-Read-Syntax-Diagrams.md)
  3. Graphic Syntax Diagrams

## Graphic Syntax Diagrams

Syntax diagrams are drawings that illustrate valid SQL syntax. To read a
diagram, trace it from left to right, in the direction shown by the arrows.

Commands and other keywords appear in UPPERCASE inside rectangles. Type them
exactly as shown in the rectangles. Parameters appear in lowercase inside
ovals. Variables are used for the parameters. Punctuation, operators,
delimiters, and terminators appear inside circles.

If the syntax diagram has more than one path, then you can choose any path.
For example, in the following syntax you can specify either `NOPARALLEL` or
`PARALLEL`:

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

If you have the choice of more than one keyword, operator, or parameter, then
your options appear in a vertical list. For example, in the following syntax
diagram, you can specify one or more of the four parameters in the stack:

physical_attributes_clause::=

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

The following table shows parameters that appear in the syntax diagrams and
provides examples of the values you might substitute for them in your
statements:

Table A-1 Syntax Parameters

Parameter | Description | Examples  
---|---|---  
`table` |  The substitution value must be the name of an object of the type specified by the parameter. For a list of all types of objects, see the section, "[Schema Objects](Database-Objects.md#GUID-1B1818AD-6A70-4C2A-8E86-98BECA723FB8)".  |  `employees`  
`c` |  The substitution value must be a single character from your database character set.  |  `T` `s `  
`'text'` |  The substitution value must be a text string in single quotation marks. See the syntax description of '`text`' in "[Text Literals](Literals.md#GUID-1824CBAA-6E16-4921-B2A6-112FB02248DA)".  |  `'Employee records'`  
`char` |  The substitution value must be an expression of data type `CHAR` or `VARCHAR2` or a character literal in single quotation marks.  |  `last_name` `'Smith' `  
`condition` |  The substitution value must be a condition that evaluates to `TRUE` or `FALSE`. See the syntax description of `condition` in [Conditions](Conditions.md#GUID-C2E3ED44-16E7-4924-9125-E1693B1022A8).  |  `last_name >'A' `  
`date` `d` |  The substitution value must be a date constant or an expression of `DATE` data type.  |  `TO_DATE(` `'01-Jan-2002',` `'DD-MON-YYYY')`  
`expr` |  The substitution value can be an expression of any data type as defined in the syntax description of expr in "[About SQL Expressions](About-SQL-Expressions.md#GUID-68789A5C-B142-496F-ADEE-837F75F95B2B)".  |  `salary + 1000 `  
`integer` |  The substitution value must be an integer as defined by the syntax description of integer in "[Integer Literals](Literals.md#GUID-A0B9C440-5C3C-407B-8C8B-0553293C7983)".  |  `72`  
`number` `m` `n` |  The substitution value must be an expression of `NUMBER` data type or a number constant as defined in the syntax description of number in "[Numeric Literals](Literals.md#GUID-F521FBA0-FFED-4079-ABC4-9052218B3FD5)".  |  `AVG(salary)` `15 * 7 `  
`raw` |  The substitution value must be an expression of data type `RAW`.  |  `HEXTORAW('7D') `  
`subquery ` |  The substitution value must be a `SELECT` statement that will be used in another SQL statement. See [SELECT](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6).  |  `SELECT last_name ` `FROM employees`  
`db_name` |  The substitution value must be the name of a nondefault database in an embedded SQL program.  |  `sales_db`  
`db_string` |  The substitution value must be the database identification string for an Oracle Net database connection. For details, see the user's guide for your specific Oracle Net protocol.  |  â  
  
### Required Keywords and Parameters

Required keywords and parameters can appear singly or in a vertical list of
alternatives. Single required keywords and parameters appear on the main path,
which is the horizontal line you are currently traveling. In the following
example, `library_name` is a required parameter:

drop_library::=

![Description of drop_library.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_library.gif)  
[Description of the illustration drop_library.eps](img_text/drop_library.md)

If there is a library named `HQ_LIB`, then, according to the diagram, the
following statement is valid:

    
    
    DROP LIBRARY hq_lib;
    

If multiple keywords or parameters appear in a vertical list that intersects
the main path, then one of them is required. You must choose one of the
keywords or parameters, but not necessarily the one that appears on the main
path. In the following example, you must choose `ALL`, `STANDBY`, or `NONE`:

security_clause::=

![Description of security_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/security_clause.gif)  
[Description of the illustration
security_clause.eps](img_text/security_clause.md)

### Optional Keywords and Parameters

If keywords and parameters appear in a vertical list above the main path, then
they are optional. In the following example, instead of traveling down a
vertical line, you can continue along the main path:

deallocate_unused_clause::=

![Description of deallocate_unused_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/deallocate_unused_clause.gif)  
[Description of the illustration
deallocate_unused_clause.eps](img_text/deallocate_unused_clause.md)

size_clause::=

![Description of size_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/size_clause.gif)  
[Description of the illustration size_clause.eps](img_text/size_clause.md)

According to the diagrams, all of the following statements are valid:

    
    
    DEALLOCATE UNUSED;
    DEALLOCATE UNUSED KEEP 1000;
    DEALLOCATE UNUSED KEEP 10G;
    DEALLOCATE UNUSED 8T; 

### Syntax Loops

Loops let you repeat the syntax within them as many times as you like. In the
following example, after choosing one value expression, you can go back
repeatedly to choose another, separated by commas.

query_partition_clause::=

![Description of query_partition_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/query_partition_clause.gif)  
[Description of the illustration
query_partition_clause.eps](img_text/query_partition_clause.md)

### Multipart Diagrams

Read a multipart diagram as if all the main paths were joined end to end. The
following example is a three-part diagram:

alter_java::=

![Description of alter_java.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_java.gif)  
[Description of the illustration alter_java.eps](img_text/alter_java.md)

According to the diagram, the following statement is valid:

    
    
    ALTER JAVA SOURCE jsource_1 COMPILE; 


[← Previous](Graphic-Syntax-Diagrams.md)

[Next →](Backus-Naur-Form-Syntax.md)
