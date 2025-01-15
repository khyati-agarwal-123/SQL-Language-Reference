##  TO_NCHAR (datetime) {#GUID-C40DBBC2-B9F2-49D8-8775-DDA99FF41EAC} 

Syntax 

*to_nchar_date* ::= 

![Description of to_nchar_date.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_nchar_date.gif)[ Description of the illustration to_nchar_date.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/to_nchar_date.md)

Purpose 

` TO_NCHAR ` (datetime) converts a datetime or interval value of ` DATE ` , ` TIMESTAMP ` , ` TIMESTAMP ` ` WITH ` ` TIME ` ` ZONE ` , ` TIMESTAMP ` ` WITH ` ` LOCAL ` ` TIME ` ` ZONE ` , ` INTERVAL ` ` MONTH ` ` TO ` ` YEAR ` , or ` INTERVAL ` ` DAY ` ` TO ` ` SECOND ` data type from the database character set to the national character set. 

> **note:** See Also: 

  * " [ Security Considerations for Data Conversion ](Data-Type-Comparison-Rules.md#GUID-6A02902A-1EF1-41E4-9494-381488BD272F) " 

  * Appendix C in [ *Oracle Database Globalization Support Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of this function 




Examples 

The following example converts the ` order_date ` of all orders whose status is ` 9 ` to the national character set: 
    
    
    ```
    SELECT TO_NCHAR(ORDER_DATE) AS order_date
       FROM ORDERS
       WHERE ORDER_STATUS > 9
       ORDER BY order_date;
    
    ORDER_DATE
    --------------------------------------------------------------------------
    06-DEC-99 02.22.34.225609 PM
    13-SEP-99 10.19.00.654279 AM
    14-SEP-99 09.53.40.223345 AM
    26-JUN-00 10.19.43.190089 PM
    27-JUN-00 09.53.32.335522 PM
    ```
