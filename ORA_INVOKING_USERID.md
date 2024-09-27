[Previous](ORA_INVOKING_USER.md) [Next](PATH.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ORA_INVOKING_USERID

## ORA_INVOKING_USERID

Syntax

![Description of ora_invoking_userid.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ora_invoking_userid.gif)  
[Description of the illustration
ora_invoking_userid.eps](img_text/ora_invoking_userid.md)

Purpose

`ORA_INVOKING_USERID` returns the identifier of the database user who invoked
the current statement or view. This function takes into account the `BEQUEATH`
property of intervening views referenced in the statement.

This function returns a `NUMBER` value.

See Also:

  * [ORA_INVOKING_USER](ORA_INVOKING_USER.md#GUID-FAE7B186-C40D-48BB-A2C9-AB7EE3878BF1) to learn how Oracle Database determines the database user who invoked the current statement or view 

  * [BEQUEATH](CREATE-VIEW.md#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30__BABFIHJJ) clause of the `CREATE` `VIEW` statement 

Examples

The following example returns the identifier of the database user who invoked
the statement:

    
    
    SELECT ORA_INVOKING_USERID FROM DUAL;


[← Previous](ORA_INVOKING_USER.md)

[Next →](PATH.md)
