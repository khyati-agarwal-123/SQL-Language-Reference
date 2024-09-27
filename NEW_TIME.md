[Previous](NCHR.md) [Next](NEXT_DAY.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NEW_TIME 

## NEW_TIME

Syntax

![Description of new_time.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/new_time.gif)  
[Description of the illustration new_time.eps](img_text/new_time.md)

Purpose

`NEW_TIME` returns the date and time in time zone `timezone2` when date and
time in time zone `timezone1` are `date`. Before using this function, you must
set the `NLS_DATE_FORMAT` parameter to display 24-hour time. The return type
is always `DATE`, regardless of the data type of `date`.

Note:

This function takes as input only a limited number of time zones. You can have
access to a much greater number of time zones by combining the `FROM_TZ`
function and the datetime expression. See
[FROM_TZ](FROM_TZ.md#GUID-84384FF7-6462-480C-BC40-60087016857B) and the
example for "[Datetime Expressions](Datetime-
Expressions.md#GUID-F72A753A-98A4-4EBD-84E9-C014CE058384)".

The arguments `timezone1` and `timezone2` can be any of these text strings:

  * AST, ADT: Atlantic Standard or Daylight Time

  * BST, BDT: Bering Standard or Daylight Time 

  * CST, CDT: Central Standard or Daylight Time 

  * EST, EDT: Eastern Standard or Daylight Time 

  * GMT: Greenwich Mean Time

  * HST, HDT: Alaska-Hawaii Standard Time or Daylight Time. 

  * MST, MDT: Mountain Standard or Daylight Time 

  * NST: Newfoundland Standard Time

  * PST, PDT: Pacific Standard or Daylight Time

  * YST, YDT: Yukon Standard or Daylight Time 

Examples

The following example returns an Atlantic Standard time, given the Pacific
Standard time equivalent:

    
    
    ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY HH24:MI:SS';
    
    SELECT NEW_TIME(TO_DATE('11-10-09 01:23:45', 'MM-DD-YY HH24:MI:SS'), 'AST', 'PST')
             "New Date and Time"
      FROM DUAL;
    
    New Date and Time
    --------------------
    09-NOV-2009 21:23:45


[← Previous](NCHR.md)

[Next →](NEXT_DAY.md)
