[Previous](LNNVL.md) [Next](LOG.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. LOCALTIMESTAMP 

## LOCALTIMESTAMP

Syntax

![Description of localtimestamp.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/localtimestamp.gif)  
[Description of the illustration
localtimestamp.eps](img_text/localtimestamp.md)

Purpose

`LOCALTIMESTAMP` returns the current date and time in the session time zone in
a value of data type `TIMESTAMP`. The difference between this function and
`CURRENT_TIMESTAMP` is that `LOCALTIMESTAMP` returns a `TIMESTAMP` value while
`CURRENT_TIMESTAMP` returns a `TIMESTAMP` `WITH` `TIME` `ZONE` value.

The optional argument `timestamp_precision` specifies the fractional second
precision of the time value returned.

See Also:

[CURRENT_TIMESTAMP](CURRENT_TIMESTAMP.md#GUID-
CBD42B84-869D-45C7-9FFC-001DD7712097), "[TIMESTAMP Data Type](Data-
Types.md#GUID-94A82966-D380-4583-9AF1-AEE681881E64)", and "[TIMESTAMP WITH
TIME ZONE Data Type](Data-Types.md#GUID-
BE23545B-469A-4A57-8D13-505F2F5DB706)"

Examples

This example illustrates the difference between `LOCALTIMESTAMP` and
`CURRENT_TIMESTAMP`:

    
    
    ALTER SESSION SET TIME_ZONE = '-5:00';
    SELECT CURRENT_TIMESTAMP, LOCALTIMESTAMP FROM DUAL;
    
    CURRENT_TIMESTAMP                    LOCALTIMESTAMP
    -------------------------------------------------------------------
    04-APR-00 01.27.18.999220 PM -05:00  04-APR-00 01.27.19 PM
    
    ALTER SESSION SET TIME_ZONE = '-8:00';
    SELECT CURRENT_TIMESTAMP, LOCALTIMESTAMP FROM DUAL;
    
    CURRENT_TIMESTAMP                    LOCALTIMESTAMP
    -----------------------------------  ------------------------------
    04-APR-00 10.27.45.132474 AM -08:00  04-APR-00 10.27.451 AM
    

When you use the `LOCALTIMESTAMP` with a format mask, take care that the
format mask matches the value returned by the function. For example, consider
the following table:

    
    
    CREATE TABLE local_test (col1 TIMESTAMP WITH LOCAL TIME ZONE);
    

The following statement fails because the mask does not include the `TIME`
`ZONE` portion of the return type of the function:

    
    
    INSERT INTO local_test
      VALUES (TO_TIMESTAMP(LOCALTIMESTAMP, 'DD-MON-RR HH.MI.SSXFF'));
    

The following statement uses the correct format mask to match the return type
of `LOCALTIMESTAMP`:

    
    
    INSERT INTO local_test
      VALUES (TO_TIMESTAMP(LOCALTIMESTAMP, 'DD-MON-RR HH.MI.SSXFF PM'));


[← Previous](LNNVL.md)

[Next →](LOG.md)
