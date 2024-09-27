[Previous](VARIANCE.md) [Next](vector_chunks.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VECTOR

## VECTOR

Syntax

  

![Description of vector.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector.gif)  
[Description of the illustration vector.eps](img_text/vector.md)

  

Purpose

`VECTOR` is a contructor that takes a string of type `VARCHAR2` or `CLOB` as
input and returns a vector as output.

`VECTOR` is synonymous with `TO_VECTOR`.

See Also:

  * [TO_VECTOR](to_vector.md#GUID-2CCAB607-A28B-43F7-A71D-9800C0B9A380)

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)

Parameters

  * `expr` must evaluate to a vector or a string that represents a vector. The function returns NULL if `expr` is NULL. 

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

Note:

Applications using Oracle Client 23ai libraries or Thin mode drivers can
insert vector data directly as a string or a `CLOB`. For example:

    
    
    INSERT INTO vecTab VALUES ('[1.1, 2.9, 3.14]');


[← Previous](VARIANCE.md)

[Next →](vector_chunks.md)
