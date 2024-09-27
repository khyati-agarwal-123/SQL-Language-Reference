[Previous](KURTOSIS_SAMP.md) [Next](l2_distance.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. L1_DISTANCE

## L1_DISTANCE

Syntax

  

![Description of l1_distance.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/l1_distance.gif)  
[Description of the illustration l1_distance.eps](img_text/l1_distance.md)

  

Purpose

`L1_DISTANCE` is a shorthand version of the `VECTOR_DISTANCE` function that
calculates the distance between two vectors. It takes two vectors as input and
returns the distance between them as a `BINARY_DOUBLE`.

Parameters

  * `expr1` and `expr2` must evaluate to vectors and have the same number of dimensions. 

  * `L1_DISTANCE` returns NULL, if either `expr1` or `expr2` is NULL, or if the dimensions between the two vectors do not match up. 

See Also:

  * [VECTOR_DISTANCE](vector_distance.md#GUID-BA4BCFB2-D905-43DC-87B0-E53522CF07B7)

  * [COSINE_DISTANCE](cosine_distance.md#GUID-2128DC1D-612A-444F-87D8-3D249CD8F12D)

  * [INNER_PRODUCT](inner_product.md#GUID-6AE745CF-93E7-4192-8F80-7B9853DF5B72)

  * [L2_DISTANCE](l2_distance.md#GUID-2FD8BC27-7614-471F-A4F5-3ED52130A05A)

  * 


[← Previous](KURTOSIS_SAMP.md)

[Next →](l2_distance.md)
