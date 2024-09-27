[Previous](boolean_or_agg.md) [Next](CAST.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CARDINALITY 

## CARDINALITY

Syntax

![Description of cardinality.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cardinality.gif)  
[Description of the illustration cardinality.eps](img_text/cardinality.md)

Purpose

`CARDINALITY` returns the number of elements in a nested table. The return
type is `NUMBER`. If the nested table is empty, or is a null collection, then
`CARDINALITY` returns `NULL`.

Examples

The following example shows the number of elements in the nested table column
`ad_textdocs_ntab` of the sample table `pm.print_media`:

    
    
    SELECT product_id, CARDINALITY(ad_textdocs_ntab) cardinality
      FROM print_media
      ORDER BY product_id;
    
    PRODUCT_ID CARDINALITY
    ---------- -----------
          2056           3
          2268           3
          3060           3
          3106           3


[← Previous](boolean_or_agg.md)

[Next →](CAST.md)
