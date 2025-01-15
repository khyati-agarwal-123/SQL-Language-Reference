##  ORA_INVOKING_USER {#GUID-FAE7B186-C40D-48BB-A2C9-AB7EE3878BF1} 

Syntax 

![Description of ora_invoking_user.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ora_invoking_user.gif)[ Description of the illustration ora_invoking_user.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/ora_invoking_user.md)

Purpose 

` ORA_INVOKING_USER ` returns the name of the database user who invoked the current statement or view. This function takes into account the ` BEQUEATH ` property of intervening views referenced in the statement. If this function is invoked from within a definer's rights context, then it returns the name of the owner of the definer's rights object. If the invoking user is a Real Application Security user, then it returns user ` XS$NULL ` . 

This function returns a ` VARCHAR2 ` value. 

> **note:** See Also: 

  * [ BEQUEATH ](CREATE-VIEW.md#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30__BABFIHJJ) clause of the ` CREATE ` ` VIEW ` statement 

  * Appendix C in [ *Oracle Database Globalization Support Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of ` ORA_INVOKING_USER `




Examples 

The following example returns the name of the database user who invoked the statement: 
    
    
    ```
    SELECT ORA_INVOKING_USER FROM DUAL;
    ```
