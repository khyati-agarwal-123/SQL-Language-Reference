##  RAWTOHEX {#GUID-F86E3B5B-7FEE-47FD-A0C2-2FC55DC21C9E} 

Syntax 

![Description of rawtohex.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rawtohex.gif)[ Description of the illustration rawtohex.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/rawtohex.md)

Purpose 

` RAWTOHEX ` converts *raw* to a character value containing its hexadecimal representation. 

As a SQL built-in function, ` RAWTOHEX ` accepts an argument of any scalar data type other than ` LONG ` , ` LONG ` ` RAW ` , ` CLOB ` , ` NCLOB ` , ` BLOB ` , or ` BFILE ` . If the argument is of a data type other than ` RAW ` , then this function converts the argument value, which is represented using some number of data bytes, into a ` RAW ` value with the same number of data bytes. The data itself is not modified in any way, but the data type is recast to a ` RAW ` data type. 

This function returns a ` VARCHAR2 ` value with the hexadecimal representation of bytes that make up the value of *raw* . Each byte is represented by two hexadecimal digits. 

> **note:** 

` RAWTOHEX ` functions differently when used as a PL/SQL built-in function. Refer to [ *Oracle Database Development Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS00308) for more information. 

> **note:** See Also: 

Appendix C in [ *Oracle Database Globalization Support Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of ` RAWTOHEX `

Examples 

The following hypothetical example returns the hexadecimal equivalent of a ` RAW ` column value: 
    
    
    ```
    SELECT RAWTOHEX(raw_column) "Graphics"
       FROM graphics;
    
    Graphics
    --------
    7D  
    ```

> **note:** See Also: 

" [ RAW and LONG RAW Data Types ](Data-Types.md#GUID-4FD497DD-3331-4C25-9147-3CEBEFDBFF22) "  and [ HEXTORAW ](HEXTORAW.md#GUID-8571556F-C219-4814-A854-9F01581FFBDF)
