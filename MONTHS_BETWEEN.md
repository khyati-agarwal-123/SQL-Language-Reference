##  MONTHS_BETWEEN {#GUID-E4A1AEC0-F5A0-4703-9CC8-4087EB889952} 

Syntax 

![Description of months_between.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/months_between.gif)[ Description of the illustration months_between.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/months_between.md)

Purpose 

` MONTHS_BETWEEN ` returns number of months between dates *date1* and *date2* . The month and the last day of the month are defined by the parameter ` NLS_CALENDAR ` . If *date1* is later than *date2* , then the result is positive. If *date1* is earlier than *date2* , then the result is negative. If *date1* and *date2* are either the same days of the month or both last days of months, then the result is always an integer. Otherwise Oracle Database calculates the fractional portion of the result based on a 31-day month and considers the difference in time components *date1* and *date2* . 

Examples 

The following example calculates the months between two dates: 
    
    
    ```
    SELECT MONTHS_BETWEEN
           (TO_DATE('02-02-1995','MM-DD-YYYY'),
            TO_DATE('01-01-1995','MM-DD-YYYY') ) "Months"
      FROM DUAL;
    
        Months
    ----------
    1.03225806
    ```
