##  BITMAP_BUCKET_NUMBER {#GUID-6368CC51-B7C5-4BD9-9276-DE449BBC2CF3} 

Syntax 

  


![Description of bitmap_bucket_number.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/bitmap_bucket_number.gif)[ Description of the illustration bitmap_bucket_number.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/bitmap_bucket_number.md)

  


Purpose 

Use ` BITMAP_BUCKET_NUMBER ` to construct a one-to-one mapping between a number and a bit position in a bitmap. 

The argument ` expr  ` is of type ` NUMBER ` . It represents the absolute bit position in the bitmap. 

` BITMAP_BUCKET_NUMBER ` returns a ` NUMBER ` . It represents the relative bit position. 

If ` expr  ` is NULL, the function returns NULL. 

If ` expr  ` is not an integer, you will see the following error message: 
    
    
    ```
    Invalid value has been passed to a BITMAP COUNT DISTINCT related operator.
    ```
