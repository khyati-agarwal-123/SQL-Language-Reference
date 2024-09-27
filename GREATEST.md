[Previous](from_vector.md) [Next](GROUP_ID.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. GREATEST 

## GREATEST

Syntax

![Description of greatest.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/greatest.gif)  
[Description of the illustration greatest.eps](img_text/greatest.md)

Purpose

`GREATEST` returns the greatest of a list of one or more expressions. Oracle
Database uses the first `expr` to determine the return type. If the first
`expr` is numeric, then Oracle determines the argument with the highest
numeric precedence, implicitly converts the remaining arguments to that data
type before the comparison, and returns that data type. If the first `expr` is
not numeric, then each `expr` after the first is implicitly converted to the
data type of the first `expr` before the comparison.

Oracle Database compares each `expr` using nonpadded comparison semantics. The
comparison is binary by default and is linguistic if the `NLS_COMP` parameter
is set to `LINGUISTIC` and the `NLS_SORT` parameter has a setting other than
`BINARY`. Character comparison is based on the numerical codes of the
characters in the database character set and is performed on whole strings
treated as one sequence of bytes, rather than character by character. If the
value returned by this function is character data, then its data type is
`VARCHAR2` if the first `expr` is a character data type and `NVARCHAR2` if the
first `expr` is a national character data type.

See Also:

  * "[Data Type Comparison Rules](Data-Type-Comparison-Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187)" for more information on character comparison 

  * [Table 2-9](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell indicates implicit conversion of the data types") for more information on implicit conversion and "[Floating-Point Numbers](Data-Types.md#GUID-F579F4B8-EF13-4CAF-9B06-03B076861C41)" for information on binary-float comparison semantics 

  * "[LEAST](LEAST.md#GUID-0198D71B-051A-41D9-8E9C-599E24692556)", which returns the least of a list of one or more expressions 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `GREATEST` uses to compare character values for `expr`, and for the collation derivation rules, which define the collation assigned to the return value of this function when it is a character value 

Examples

The following statement selects the string with the greatest value:

    
    
    SELECT GREATEST('HARRY', 'HARRIOT', 'HAROLD') "Greatest"
      FROM DUAL;
     
    Greatest
    --------
    HARRY
    

In the following statement, the first argument is numeric. Oracle Database
determines that the argument with the highest numeric precedence is the second
argument, converts the remaining arguments to the data type of the second
argument, and returns the greatest value as that data type:

    
    
    SELECT GREATEST (1, '3.925', '2.4') "Greatest"
      FROM DUAL;
    
    Greatest
    --------
       3.925


[← Previous](from_vector.md)

[Next →](GROUP_ID.md)
