##  TO_MULTI_BYTE {#GUID-58A9F91A-5B1E-4C14-8F48-046F176E2F4A} 

Syntax 

![Description of to_multi_byte.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_multi_byte.gif)[ Description of the illustration to_multi_byte.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/to_multi_byte.md)

Purpose 

` TO_MULTI_BYTE ` returns *char* with all of its single-byte characters converted to their corresponding multibyte characters. *char* can be of data type ` CHAR ` , ` VARCHAR2 ` , ` NCHAR ` , or ` NVARCHAR2 ` . The value returned is in the same data type as *char* . 

Any single-byte characters in *char* that have no multibyte equivalents appear in the output string as single-byte characters. This function is useful only if your database character set contains both single-byte and multibyte characters. 

This function does not support ` CLOB ` data directly. However, ` CLOB ` s can be passed in as arguments through implicit data conversion. 

> **note:** See Also: 

  * " [ Data Type Comparison Rules ](Data-Type-Comparison-Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187) "  for more information. 

  * Appendix C in [ *Oracle Database Globalization Support Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of ` TO_MULTI_BYTE `




Examples 

The following example illustrates converting from a single byte ` A ` to a multibyte ` A ` in UTF8: 
    
    
    ```
    SELECT dump(TO_MULTI_BYTE( 'A')) FROM DUAL; 
    
    DUMP(TO_MULTI_BYTE('A')) 
    ------------------------ 
    Typ=1 Len=3: 239,188,161
    ```
