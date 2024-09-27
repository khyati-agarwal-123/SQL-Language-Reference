[Previous](NEXT_DAY.md) [Next](NLS_CHARSET_ID.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. NLS_CHARSET_DECL_LEN 

## NLS_CHARSET_DECL_LEN

Syntax

![Description of nls_charset_decl_len.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nls_charset_decl_len.gif)  
[Description of the illustration
nls_charset_decl_len.eps](img_text/nls_charset_decl_len.md)

Purpose

`NLS_CHARSET_DECL_LEN` returns the declaration length (in number of
characters) of an `NCHAR` column. The `byte_count` argument is the width of
the column. The `char_set_id` argument is the character set ID of the column.

Examples

The following example returns the number of characters that are in a 200-byte
column when you are using a multibyte character set:

    
    
    SELECT NLS_CHARSET_DECL_LEN(200, nls_charset_id('ja16eucfixed')) 
      FROM DUAL; 
    
    NLS_CHARSET_DECL_LEN(200,NLS_CHARSET_ID('JA16EUCFIXED'))
    --------------------------------------------------------
                                                         100


[← Previous](NEXT_DAY.md)

[Next →](NLS_CHARSET_ID.md)
