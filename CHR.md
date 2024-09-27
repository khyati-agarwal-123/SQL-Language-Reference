[Previous](checksum.md) [Next](CLUSTER_DETAILS.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CHR 

## CHR

Syntax

![Description of chr.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/chr.gif)  
[Description of the illustration chr.eps](img_text/chr.md)

Purpose

`CHR` returns the character having the binary equivalent to `n` as a
`VARCHAR2` value in either the database character set or, if you specify
`USING` `NCHAR_CS`, the national character set.

For single-byte character sets, if `n` > 256, then Oracle Database returns the
binary equivalent of `n` `mod` `256`. For multibyte character sets, `n` must
resolve to one entire code point. Invalid code points are not validated, and
the result of specifying invalid code points is indeterminate.

This function takes as an argument a `NUMBER` value, or any value that can be
implicitly converted to `NUMBER`, and returns a character.

Note:

Use of the `CHR` function (either with or without the optional `USING`
`NCHAR_CS` clause) results in code that is not portable between ASCII- and
EBCDIC-based machine architectures.

See Also:

  * [NCHR](NCHR.md#GUID-3A1BDD54-6C0B-4067-99C5-A439C0F8D561) and [Table 2-9](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell indicates implicit conversion of the data types") for more information on implicit conversion 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `CHR`

Examples

The following example is run on an ASCII-based machine with the database
character set defined as WE8ISO8859P1:

    
    
    SELECT CHR(67)||CHR(65)||CHR(84) "Dog"
      FROM DUAL;
    
    Dog
    ---
    CAT
    

To produce the same results on an EBCDIC-based machine with the WE8EBCDIC1047
character set, the preceding example would have to be modified as follows:

    
    
    SELECT CHR(195)||CHR(193)||CHR(227) "Dog"
      FROM DUAL; 
    
    Dog 
    --- 
    CAT 
    

For multibyte character sets, this sort of concatenation gives different
results. For example, given a multibyte character whose hexadecimal value is
`a1a2` (`a1` representing the first byte and `a2` the second byte), you must
specify for `n` the decimal equivalent of '`a1a2`', or 41378:

    
    
    SELECT CHR(41378)
      FROM DUAL;
    

You cannot specify the decimal equivalent of a1 concatenated with the decimal
equivalent of a2, as in the following example:

    
    
    SELECT CHR(161)||CHR(162)
      FROM DUAL;
    

However, you can concatenate whole multibyte code points, as in the following
example, which concatenates the multibyte characters whose hexadecimal values
are `a1a2` and `a1a3`:

    
    
    SELECT CHR(41378)||CHR(41379)
      FROM DUAL;
    

The following example assumes that the national character set is UTF16:

    
    
    SELECT CHR (196 USING NCHAR_CS)
      FROM DUAL; 
    
    CH 
    -- 
    Ã 


[← Previous](checksum.md)

[Next →](CLUSTER_DETAILS.md)
