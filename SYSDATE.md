[Previous](SYS_XMLGEN.md) [Next](SYSTIMESTAMP.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. SYSDATE 

## SYSDATE

Syntax

![Description of sysdate.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sysdate.gif)  
[Description of the illustration sysdate.eps](img_text/sysdate.md)

Purpose

`SYSDATE` returns the current date and time set for the operating system on
which the database server resides. The data type of the returned value is
`DATE`, and the format returned depends on the value of the `NLS_DATE_FORMAT`
initialization parameter. The function requires no arguments. In distributed
SQL statements, this function returns the date and time set for the operating
system of your local database. You cannot use this function in the condition
of a `CHECK` constraint.

In a multitenant setup existing PDBs and PDBs created later inherit the
timezone of the system.

If you want `SYSDATE` to return the timezone of the PDB, then you must set the
initialization parameter `TIME_AT_DBTIMEZONE` to `TRUE` before starting the
PDB.

You can change the timezone using `ALTER SYSTEM SET TIME_ZONE` or `ALTER
DATABASE db_name SET TIME_ZONE`.

You can set `SYSTIMESTAMP` to return system time by setting the initialization
parameter `TIME_AT_DBTIMEZONE` to `FALSE` and restarting the database.

Note:

  * For more see [TIME_AT_DBTIMEZONE](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN-GUID-493916F5-AFD7-4001-8FB4-02258E0AD595) of the Oracle Database Reference. 

  * The `FIXED_DATE` initialization parameter enables you to set a constant date and time that `SYSDATE` will always return instead of the current date and time. This parameter is useful primarily for testing. Refer to [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN10062) for more information on the `FIXED_DATE` initialization parameter. 

Examples

The following example returns the current operating system date and time:

    
    
    SELECT TO_CHAR
        (SYSDATE, 'MM-DD-YYYY HH24:MI:SS') "NOW"
         FROM DUAL;
    
    NOW
    -------------------
    04-13-2001 09:45:51


[← Previous](SYS_XMLGEN.md)

[Next →](SYSTIMESTAMP.md)
