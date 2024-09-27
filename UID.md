[Previous](TZ_OFFSET.md) [Next](UNISTR.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. UID 

## UID

Syntax

![Description of uid.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/uid.gif)  
[Description of the illustration uid.eps](img_text/uid.md)

Purpose

`UID` returns an integer that uniquely identifies the session user (the user
who logged on).

See Also:

[USER](USER.md#GUID-AD0B927B-EFD4-4246-89B4-2D55AB3AF531) to learn how
Oracle Database determines the session user

Examples

The following example returns the UID of the session user:

    
    
    SELECT UID FROM DUAL;


[← Previous](TZ_OFFSET.md)

[Next →](UNISTR.md)
