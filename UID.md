[Previous](TZ_OFFSET.html) [Next](UNISTR.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. UID 



## UID 

Syntax

![Description of uid.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/uid.gif)[Descriptionof the illustration uid.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/uid.md)

Purpose

`UID` returns an integer that uniquely identifies the session user (the user who logged on). 

See Also:

[USER](USER.html#GUID-AD0B927B-EFD4-4246-89B4-2D55AB3AF531) to learn how Oracle Database determines the session user 

Examples

The following example returns the UID of the session user:
    
    
    SELECT UID FROM DUAL;

[← Previous](TZ_OFFSET.md)

[Next →](UNISTR.md)
