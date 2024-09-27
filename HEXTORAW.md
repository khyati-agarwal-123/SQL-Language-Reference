[Previous](GROUPING_ID.md) [Next](INITCAP.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. HEXTORAW 

## HEXTORAW

Syntax

![Description of hextoraw.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/hextoraw.gif)  
[Description of the illustration hextoraw.eps](img_text/hextoraw.md)

Purpose

`HEXTORAW` converts `char` containing hexadecimal digits in the `CHAR`,
`VARCHAR2`, `NCHAR`, or `NVARCHAR2` data type to a raw value.

This function does not support `CLOB` data directly. However, `CLOB`s can be
passed in as arguments through implicit data conversion.

See Also:

"[Data Type Comparison Rules](Data-Type-Comparison-
Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187)" for more information.

Examples

The following example creates a simple table with a raw column, and inserts a
hexadecimal value that has been converted to `RAW`:

    
    
    CREATE TABLE test (raw_col RAW(10));
    
    INSERT INTO test VALUES (HEXTORAW('7D'));
    

The following example converts hexadecimal digits to a raw value and casts the
raw value to `VARCHAR2`:

    
    
    SELECT UTL_RAW.CAST_TO_VARCHAR2(HEXTORAW('4041424344'))
      FROM DUAL;
    
    UTL_RAW.CAST_TO_VARCHAR2(HEXTORAW('4041424344'))
    ------------------------------------------------
    @ABCD

See Also:

"[RAW and LONG RAW Data Types](Data-
Types.md#GUID-4FD497DD-3331-4C25-9147-3CEBEFDBFF22)" and
[RAWTOHEX](RAWTOHEX.md#GUID-F86E3B5B-7FEE-47FD-A0C2-2FC55DC21C9E)


[← Previous](GROUPING_ID.md)

[Next →](INITCAP.md)
