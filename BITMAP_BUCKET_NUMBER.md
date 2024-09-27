[Previous](BITMAP_BIT_POSITION.md) [Next](BITMAP_CONSTRUCT_AGG.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. BITMAP_BUCKET_NUMBER

## BITMAP_BUCKET_NUMBER

Syntax

  

![Description of bitmap_bucket_number.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/bitmap_bucket_number.gif)  
[Description of the illustration
bitmap_bucket_number.eps](img_text/bitmap_bucket_number.md)

  

Purpose

Use `BITMAP_BUCKET_NUMBER` to construct a one-to-one mapping between a number
and a bit position in a bitmap.

The argument `expr` is of type `NUMBER`. It represents the absolute bit
position in the bitmap.

`BITMAP_BUCKET_NUMBER` returns a `NUMBER`. It represents the relative bit
position.

If `expr` is NULL, the function returns NULL.

If `expr` is not an integer, you will see the following error message:

    
    
    Invalid value has been passed to a BITMAP COUNT DISTINCT related operator.


[← Previous](BITMAP_BIT_POSITION.md)

[Next →](BITMAP_CONSTRUCT_AGG.md)
