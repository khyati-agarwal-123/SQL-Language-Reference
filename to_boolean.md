[Previous](TO_BLOB-raw.md) [Next](TO_CHAR-bfile-blob.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_BOOLEAN

## TO_BOOLEAN

Syntax

  

![Description of to_boolean.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_boolean.gif)  
[Description of the illustration to_boolean.eps](img_text/to_boolean.md)

  

Purpose

Use `TO_BOOLEAN` to explicitly convert character value expressions or numeric
value expressions to boolean values.

If `expr` is a string, it must evaluate to the allowed string inputs. See
[Table 2-6](Data-
Types.md#GUID-285FFCA8-390D-4FA9-9A51-47B84EF5F83A__TABLE_H3B_FXB_1VB
"String literals for true and false").

`expr` can take one of the following types, or null:

  * A character string of type `CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`

  * A numeric value of type `NUMBER`, `BINARY_FLOAT`, or `BINARY_DOUBLE`

  * A boolean value of type `BOOLEAN`. 

Examples

    
    
    SELECT TO_BOOLEAN(0), TO_BOOLEAN('true'), TO_BOOLEAN('no');

The output is:

    
    
    TO_BOOLEAN( TO_BOOLEAN( TO_BOOLEAN(
    ----------- ----------- -----------
    FALSE       TRUE        FALSE
    
    
    
    SELECT TO_BOOLEAN(1) FROM DUAL;

The output is:

    
    
    TO_BOOLEAN( 
    ----------- 
    TRUE      

See Also:

  * [CAST](CAST.md#GUID-5A70235E-1209-4281-8521-B94497AAEF75) for conversion rules. 

  * [Boolean Data Type](Data-Types.md#GUID-285FFCA8-390D-4FA9-9A51-47B84EF5F83A) for more details on the built-in boolean data type. 


[← Previous](TO_BLOB-raw.md)

[Next →](TO_CHAR-bfile-blob.md)
