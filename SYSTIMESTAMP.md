[Previous](SYSDATE.md) [Next](TAN.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. SYSTIMESTAMP 

## SYSTIMESTAMP

Syntax

![Description of systimestamp.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/systimestamp.gif)  
[Description of the illustration systimestamp.eps](img_text/systimestamp.md)

Purpose

`SYSTIMESTAMP` returns the system date, including fractional seconds and time
zone, of the system on which the database resides. The return type is
`TIMESTAMP` `WITH` `TIME` `ZONE`.

In a multitenant setup existing PDBs and PDBs created later inherit the
timezone of the system.

If you want `SYSTIMESTAMP` to return the timezone of the PDB, then you must
set the initialization parameter `TIME_AT_DBTIMEZONE` to `TRUE` before
starting the PDB.

You can change the timezone using `ALTER SYSTEM SET TIME_ZONE` or `ALTER
DATABASE db_name SET TIME_ZONE`.

You can set `SYSTIMESTAMP` to return system time by setting the initialization
parameter `TIME_AT_DBTIMEZONE` to `FALSE` and restarting the database.

Note:

For more see
[TIME_AT_DBTIMEZONE](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN-GUID-493916F5-AFD7-4001-8FB4-02258E0AD595) of the
Oracle Database Reference.

Examples

The following example returns the system timestamp:

    
    
    SELECT SYSTIMESTAMP FROM DUAL;
    
    SYSTIMESTAMP
    ------------------------------------------------------------------
    28-MAR-00 12.38.55.538741 PM -08:00
    

The following example shows how to explicitly specify fractional seconds:

    
    
    SELECT TO_CHAR(SYSTIMESTAMP, 'SSSSS.FF') FROM DUAL;
    
    TO_CHAR(SYSTIME
    ---------------
    55615.449255
    

The following example returns the current timestamp in a specified time zone:

    
    
    SELECT SYSTIMESTAMP AT TIME ZONE 'UTC' FROM DUAL;
     
    SYSTIMESTAMPATTIMEZONE'UTC'
    ---------------------------------------------------------------------------
    08-07-21 20:39:52,743557 UTC
    

The output format in this example depends on the `NLS_TIMESTAMP_TZ_FORMAT` for
the session.


[← Previous](SYSDATE.md)

[Next →](TAN.md)
