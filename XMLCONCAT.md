##  XMLCONCAT {#GUID-CEEEF777-4C7D-41E4-9F69-69DE6D1B07C2} 

Syntax 

![Description of xmlconcat.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/xmlconcat.gif)[ Description of the illustration xmlconcat.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/xmlconcat.md)

Purpose 

` XMLConcat ` takes as input a series of ` XMLType ` instances, concatenates the series of elements for each row, and returns the concatenated series. ` XMLConcat ` is the inverse of ` XMLSequence ` . 

Null expressions are dropped from the result. If all the value expressions are null, then the function returns null. 

> **note:** See Also: 

[ XMLSEQUENCE ](XMLSEQUENCE.md#GUID-BE0837A9-7D85-4621-8C22-1FECAD17E569)

Examples 

The following example creates XML elements for the first and last names of a subset of employees, and then concatenates and returns those elements: 
    
    
    ```
    SELECT XMLCONCAT(XMLELEMENT("First", e.first_name),
       XMLELEMENT("Last", e.last_name)) AS "Result"
       FROM employees e
       WHERE e.employee_id > 202;
    
    Result
    ----------------------------------------------------------------
    Susan
    Mavris
    
    Hermann
    Baer
    
    Shelley
    Higgins
    
    William
    Gietz
    
    4 rows selected.
    ```
