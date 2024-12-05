[Previous](CUME_DIST.html) [Next](CURRENT_TIMESTAMP.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)
  2. [Functions](Functions.html)
  3. CURRENT_DATE 



## CURRENT_DATE 

Syntax

![Description of current_date.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/current_date.gif)[Description of the illustration current_date.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/current_date.html)

Purpose

`CURRENT_DATE` returns the current date in the session time zone, in a value in the Gregorian calendar of data type `DATE`. 

Examples 

The following example illustrates that `CURRENT_DATE` is sensitive to the session time zone: 
    
    
    ALTER SESSION SET TIME_ZONE = '-5:0';
    ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY HH24:MI:SS';
    SELECT SESSIONTIMEZONE, CURRENT_DATE FROM DUAL;
    
    SESSIONTIMEZONE CURRENT_DATE
    --------------- --------------------
    -05:00          29-MAY-2000 13:14:03
    
    ALTER SESSION SET TIME_ZONE = '-8:0';
    SELECT SESSIONTIMEZONE, CURRENT_DATE FROM DUAL;
    
    SESSIONTIMEZONE CURRENT_DATE
    --------------- --------------------
    -08:00          29-MAY-2000 10:14:33

[← Previous](CUME_DIST.md)

[Next →](CURRENT_TIMESTAMP.md)
