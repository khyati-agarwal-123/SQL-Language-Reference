[Previous](USERENV.md) [Next](VALUE.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VALIDATE_CONVERSION 

## VALIDATE_CONVERSION

Syntax

![Description of validate_conversion.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/validate_conversion.gif)  
[Description of the illustration
validate_conversion.eps](img_text/validate_conversion.md)

Purpose

`VALIDATE_CONVERSION` determines whether `expr` can be converted to the
specified data type. If `expr` can be successfully converted, then this
function returns 1; otherwise, this function returns 0. If `expr` evaluates to
null, then this function returns 1. If an error occurs while evaluating
`expr`, then this function returns the error.

For `expr`, specify a SQL expression. The acceptable data types for `expr`,
and the purpose of the optional `fmt` and `nlsparam` arguments, depend on the
data type you specify for `type_name`.

For `type_name`, specify the data type to which you want to convert `expr`.
You can specify the following data types:

  * `BINARY_DOUBLE`

If you specify `BINARY_DOUBLE`, then `expr` can be any expression that
evaluates to a character string of `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2`
data type, or a numeric value of type `NUMBER`, `BINARY_FLOAT`, or
`BINARY_DOUBLE`. The optional `fmt` and `nlsparam` arguments serve the same
purpose as for the `TO_BINARY_DOUBLE` function. Refer to
[TO_BINARY_DOUBLE](TO_BINARY_DOUBLE.md#GUID-0BA2E065-8006-426C-A3CB-1F6B0C8F283C)
for more information.

  * `BINARY_FLOAT`

If you specify `BINARY_FLOAT`, then `expr` can be any expression that
evaluates to a character string of `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2`
data type, or a numeric value of type `NUMBER`, `BINARY_FLOAT`, or
`BINARY_DOUBLE`. The optional `fmt` and `nlsparam` arguments serve the same
purpose as for the `TO_BINARY_FLOAT` function. Refer to
[TO_BINARY_FLOAT](TO_BINARY_FLOAT.md#GUID-66A51BE2-BE4A-4B99-9C37-73B110452D27)
for more information.

  * `DATE`

If you specify `DATE`, then `expr` can be any expression that evaluates to a
character string of `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2` data type. The
optional `fmt` and `nlsparam` arguments serve the same purpose as for the
`TO_DATE` function. Refer to
[TO_DATE](TO_DATE.md#GUID-D226FA7C-F7AD-41A0-BB1D-BD8EF9440118) for more
information.

  * `INTERVAL` `DAY` `TO` `SECOND`

If you specify `INTERVAL` `DAY` `TO` `SECOND`, then `expr` can be any
expression that evaluates to a character string of `CHAR`, `VARCHAR2`,
`NCHAR`, or `NVARCHAR2` data type, and must contain a value in either the SQL
interval format or the ISO duration format. The optional `fmt` and `nlsparam`
arguments do not apply for this data type. Refer to
[TO_DSINTERVAL](TO_DSINTERVAL.md#GUID-DEBB41BD-9438-4558-A53E-428CE93C05D3)
for more information on the SQL interval format and the ISO duration format.

  * `INTERVAL` `YEAR` `TO` `MONTH`

If you specify `INTERVAL` `YEAR` `TO` `MONTH`, then `expr` can be any
expression that evaluates to a character string of `CHAR`, `VARCHAR2`,
`NCHAR`, or `NVARCHAR2` data type, and must contain a value in either the SQL
interval format or the ISO duration format. The optional `fmt` and `nlsparam`
arguments do not apply for this data type. Refer to
[TO_YMINTERVAL](TO_YMINTERVAL.md#GUID-5DEBA096-7AC3-4B18-A4BE-D36FC9BDB450)
for more information on the SQL interval format and the ISO duration format.

  * `NUMBER`

If you specify `NUMBER`, then `expr` can be any expression that evaluates to a
character string of `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2` data type, a
numeric value of type `NUMBER`, `BINARY_FLOAT`, or `BINARY_DOUBLE` or value of
type `BOOLEAN`. The optional `fmt` and `nlsparam` arguments serve the same
purpose as for the `TO_NUMBER` function. Refer to
[TO_NUMBER](TO_NUMBER.md#GUID-D4807212-AFD7-48A7-9AED-BEC3E8809866) for more
information.

If `expr` is a value of type `NUMBER`, then the `VALIDATE_CONVERSION` function
verifies that `expr` is a legal numeric value. If `expr` is not a legal
numeric value, then the function returns 0. This enables you to identify
corrupt numeric values in your database.

  * `TIMESTAMP`

If you specify `TIMESTAMP`, then `expr` can be any expression that evaluates
to a character string of `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2` data
type. The optional `fmt` and `nlsparam` arguments serve the same purpose as
for the `TO_TIMESTAMP` function. If you omit `fmt`, then `expr` must be in the
default format of the `TIMESTAMP` data type, which is determined by the
`NLS_TIMESTAMP_FORMAT` initialization parameter. Refer to
[TO_TIMESTAMP](TO_TIMESTAMP.md#GUID-57E09334-E3CC-4CA2-809E-F0909458BCFA)
for more information.

  * `TIMESTAMP` `WITH` `TIME` `ZONE`

If you specify `TIMESTAMP` `WITH` `TIME` `ZONE`, then `expr` can be any
expression that evaluates to a character string of `CHAR`, `VARCHAR2`,
`NCHAR`, or `NVARCHAR2` data type. The optional `fmt` and `nlsparam` arguments
serve the same purpose as for the `TO_TIMESTAMP_TZ` function. If you omit
`fmt`, then `expr` must be in the default format of the `TIMESTAMP` `WITH`
`TIME` `ZONE` data type, which is determined by the `NLS_TIMESTAMP_TZ_FORMAT`
initialization parameter. Refer to
[TO_TIMESTAMP_TZ](TO_TIMESTAMP_TZ.md#GUID-3999303B-89CA-4AA3-9817-458F36ADC9DC)
for more information.

  * `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`

If you specify `TIMESTAMP`, then `expr` can be any expression that evaluates
to a character string of `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2` data
type. The optional `fmt` and `nlsparam` arguments serve the same purpose as
for the `TO_TIMESTAMP` function. If you omit `fmt`, then `expr` must be in the
default format of the `TIMESTAMP` data type, which is determined by the
`NLS_TIMESTAMP_FORMAT` initialization parameter. Refer to
[TO_TIMESTAMP](TO_TIMESTAMP.md#GUID-57E09334-E3CC-4CA2-809E-F0909458BCFA)
for more information.

  * `BOOLEAN`

`BOOLEAN` is supported as a target type. It supports `NUMBER` type family,
`VARCHAR` type family, and `BOOLEAN` itself as input.

Examples

In each of the following statements, the specified value can be successfully
converted to the specified data type. Therefore, each of these statements
returns a value of 1.

    
    
    SELECT VALIDATE_CONVERSION(1000 AS BINARY_DOUBLE)
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('1234.56' AS BINARY_FLOAT)
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('July 20, 1969, 20:18' AS DATE,
        'Month dd, YYYY, HH24:MI', 'NLS_DATE_LANGUAGE = American')
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('200 00:00:00' AS INTERVAL DAY TO SECOND)
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('P1Y2M' AS INTERVAL YEAR TO MONTH)
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('$100,00' AS NUMBER,
        '$999D99', 'NLS_NUMERIC_CHARACTERS = '',.''')
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('29-Jan-02 17:24:00' AS TIMESTAMP,
        'DD-MON-YY HH24:MI:SS')
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('1999-12-01 11:00:00 -8:00'
        AS TIMESTAMP WITH TIME ZONE, 'YYYY-MM-DD HH:MI:SS TZH:TZM')
      FROM DUAL;
    
    SELECT VALIDATE_CONVERSION('11-May-16 17:30:00'
        AS TIMESTAMP WITH LOCAL TIME ZONE, 'DD-MON-YY HH24:MI:SS')
      FROM DUAL;

The following statement returns 0, because the specified value cannot be
converted to `BINARY_FLOAT`:

    
    
    SELECT VALIDATE_CONVERSION('$29.99' AS BINARY_FLOAT)
      FROM DUAL;

The following statement returns 1, because the specified number format model
enables the value to be converted to `BINARY_FLOAT`:

    
    
    SELECT VALIDATE_CONVERSION('$29.99' AS BINARY_FLOAT, '$99D99')
      FROM DUAL;


[← Previous](USERENV.md)

[Next →](VALUE.md)
