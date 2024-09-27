[Previous](TO_NCLOB.md) [Next](TO_SINGLE_BYTE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_NUMBER 

## TO_NUMBER

Syntax

![Description of to_number.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_number.gif)  
[Description of the illustration to_number.eps](img_text/to_number.md)

Purpose

`TO_NUMBER` converts `expr` to a value of `NUMBER` data type.

`expr` can be any expression that evaluates to a character string of type
`CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2`, a numeric value of type `NUMBER`,
`BINARY_FLOAT`, or `BINARY_DOUBLE`, `BOOLEAN`, or null. If `expr` is `NUMBER`,
then the function returns `expr`. If `expr` evaluates to null, then the
function returns null. Otherwise, the function converts `expr` to a `NUMBER`
value.

  * If you specify an `expr` of `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2` data type, then you can optionally specify the format model `fmt`. 

  * If you specify an `expr` of `BINARY_FLOAT` or `BINARY_DOUBLE` data type, then you cannot specify a format model because a float can be interpreted only by its internal representation. 

  * If you specify an `expr` of type `BOOLEAN`, then `TRUE` will be converted to 1 and `FALSE` will be converted to 0. You cannot specify a format model with inputs of type `BOOLEAN`. 

Refer to "[Format Models](Format-Models.md#GUID-DFB23985-2943-4C6A-96DF-
DF0F664CED96)" for information on number formats.

The `'nlsparam'` argument in this function has the same purpose as it does in
the `TO_CHAR` function for number conversions. Refer to [TO_CHAR
(number)](TO_CHAR-number.md#GUID-00DA076D-2468-41AB-A3AC-CC78DBA0D9CB) for
more information.

This function does not support `CLOB` data directly. However, `CLOB`s can be
passed in as arguments through implicit data conversion.

See Also:

"[Data Type Comparison Rules](Data-Type-Comparison-
Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187)" for more information.

Examples

The following examples convert character string data into a number:

    
    
    UPDATE employees SET salary = salary + 
       TO_NUMBER('100.00', '9G999D99')
       WHERE last_name = 'Perkins';
    
    
    
    SELECT TO_NUMBER('-AusDollars100','L9G999D99',
       ' NLS_NUMERIC_CHARACTERS = '',.''
         NLS_CURRENCY            = ''AusDollars''
       ') "Amount"
         FROM DUAL;
    
        Amount
    ----------
          -100

The following example returns the default value of `0` because the specified
expression cannot be converted to a `NUMBER` value:

    
    
    SELECT TO_NUMBER('2,00' DEFAULT 0 ON CONVERSION ERROR) "Value"
      FROM DUAL;
    
       Value
    --------
           0
    


[← Previous](TO_NCLOB.md)

[Next →](TO_SINGLE_BYTE.md)
