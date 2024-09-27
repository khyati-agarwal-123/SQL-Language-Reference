[Previous](COSH.md) [Next](COUNT.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. COSINE_DISTANCE

## COSINE_DISTANCE

Syntax

  

![Description of cosine_distance.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cosine_distance.gif)  
[Description of the illustration
cosine_distance.eps](img_text/cosine_distance.md)

  

Purpose

`COSINE_DISTANCE` is a shorthand version of the `VECTOR_DISTANCE` function
that calculates the distance between two vectors. It takes two vectors as
input and returns the distance between them as a `BINARY_DOUBLE`.

Parameters

  * `expr1` and `expr2` must evaluate to vectors and have the same number of dimensions. 

  * `COSINE_DISTANCE` returns NULL, if either `expr1` or `expr2` is NULL, or if the dimensions between the two vectors do not match up. 

See Also:

  * [VECTOR_DISTANCE](vector_distance.md#GUID-BA4BCFB2-D905-43DC-87B0-E53522CF07B7)

  * [INNER_PRODUCT](inner_product.md#GUID-6AE745CF-93E7-4192-8F80-7B9853DF5B72)

  * [L1_DISTANCE](l1_distance.md#GUID-604A5B68-10AF-48F3-A84F-ED0B90624059)

  * [L2_DISTANCE](l2_distance.md#GUID-2FD8BC27-7614-471F-A4F5-3ED52130A05A)

  * 


[← Previous](COSH.md)

[Next →](COUNT.md)
