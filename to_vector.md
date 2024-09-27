[Previous](TO_UTC_TIMESTAMP_TZ.md) [Next](TO_YMINTERVAL.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TO_VECTOR

## TO_VECTOR

Syntax

  

![Description of to_vector.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/to_vector.gif)  
[Description of the illustration to_vector.eps](img_text/to_vector.md)

  

Purpose

`TO_VECTOR` is a contructor that takes a string of type `VARCHAR2` or `CLOB`
as input, converts it to a vector, and returns a vector as output. `TO_VECTOR`
also takes another vector as input, adjusts its format, and returns the
adjusted vector as output.

`TO_VECTOR` is synonymous with `VECTOR`.

Parameters

  * `expr` must evaluate to one of: 

    * A string that represents a vector. Accepted input data types for the string are character data types, `JSON`, `CLOB`, and `BLOB` . 

If a `BLOB` is used as the input parameter, it must represent the vector
binary bytes.

    * A vector. If the input is a vector, then the function converts it to the format specified or to the default format if the format is not specified.

If `expr` is NULL, the result is NULL.

The string representation of the vector must be in the form of an array of
non-null numbers enclosed with a bracket and separated by commas, such as `[1,
3.4, -05.60, 3e+4]`. `TO_VECTOR` converts a valid string representation of a
vector to a vector in the format specified. If no format is specified the
default format is used.

  * `number_of_dimensions` must be a numeric value that describes the number of dimensions of the vector to construct. The number of dimensions may also be specified as an asterisk (*), in which case the dimension is determined by `expr`. 

  * `format` must be one of the following tokens: `INT8`, `FLOAT32`, `FLOAT64`, or `*`. This is the target internal storage format of the vector. If `*` is used, the format will be `FLOAT32`. 

Note that this behavior is different from declaring a vector column. When you
declare a column of type `VECTOR(3, *)`, then all inserted vectors will be
stored as is without a change in format.

Examples

    
    
    SELECT TO_VECTOR('[34.6, 77.8]');
    SELECT TO_VECTOR('[34.6, 77.8]', 2, FLOAT32);
    
    SELECT TO_VECTOR('[34.6, 77.8]', 2, FLOAT32) FROM dual;
    
    TO_VECTOR('[34.6,77.8]',2,FLOAT32)
    ---------------------------------------------------------
    [3.45999985E+001,7.78000031E+001]
    
    1 row selected.
    
    SELECT TO_VECTOR('[34.6, 77.8, -89.34]', 3, FLOAT32);
    
    TO_VECTOR('[34.6,77.8,-89.34]',3,FLOAT32)
    -----------------------------------------------------------
    [3.45999985E+001,7.78000031E+001,-8.93399963E+001]
    
    1 row selected.

Note:

  * For applications using Oracle Client libraries prior to 23ai connected to Oracle Database 23ai, use the `TO_VECTOR` function to insert vector data. For example: 
    
        INSERT INTO vecTab VALUES(TO_VECTOR('[1.1, 2.9, 3.14]'));

  * Applications using Oracle Client 23ai libraries or Thin mode drivers can insert vector data directly as a string or a `CLOB`. For example: 
    
        INSERT INTO vecTab VALUES ('[1.1, 2.9, 3.14]');
    

See Also:

  * [VECTOR](vector.md#GUID-8A63005B-5512-4D20-954C-7A9DA877FE4B)

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)


[← Previous](TO_UTC_TIMESTAMP_TZ.md)

[Next →](TO_YMINTERVAL.md)
