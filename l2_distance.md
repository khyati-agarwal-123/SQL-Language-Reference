[Previous](l1_distance.md) [Next](LAG.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. L2_DISTANCE

## L2_DISTANCE

Syntax

  

![Description of l2_distance.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/l2_distance.gif)  
[Description of the illustration l2_distance.eps](img_text/l2_distance.md)

  

Purpose

`L2_DISTANCE` is a shorthand version of the `VECTOR_DISTANCE` function that
calculates the distance between two vectors. It takes two vectors as input and
returns the distance between them as a `BINARY_DOUBLE`.

Parameters

  * `expr1` and `expr2` must evaluate to vectors and have the same number of dimensions. 

  * `L2_DISTANCE` returns NULL, if either `expr1` or `expr2` is NULL, or if the dimensions between the two vectors do not match up. 

See Also:

  * [VECTOR_DISTANCE](vector_distance.md#GUID-BA4BCFB2-D905-43DC-87B0-E53522CF07B7)

  * [COSINE_DISTANCE](cosine_distance.md#GUID-2128DC1D-612A-444F-87D8-3D249CD8F12D)

  * [INNER_PRODUCT](inner_product.md#GUID-6AE745CF-93E7-4192-8F80-7B9853DF5B72)

  * [L1_DISTANCE](l1_distance.md#GUID-604A5B68-10AF-48F3-A84F-ED0B90624059)

  * 


[← Previous](l1_distance.md)

[Next →](LAG.md)
