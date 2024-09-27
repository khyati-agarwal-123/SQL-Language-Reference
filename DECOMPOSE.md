[Previous](DECODE.md) [Next](DENSE_RANK.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. DECOMPOSE 

## DECOMPOSE

Syntax

![Description of decompose.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/decompose.gif)  
[Description of the illustration decompose.eps](img_text/decompose.md)

Purpose

`DECOMPOSE` takes as its first argument a character value `string` and returns
the result of applying one of the Unicode decompositions to it. The
decomposition to apply is determined by the second, optional parameter. If the
character set of the first argument is not one of the Unicode character sets,
`DECOMPOSE` returns the argument unmodified.

If the second argument to `DECOMPOSE` is the string `CANONICAL` (case-
insensitively), `DECOMPOSE` applies canonical decomposition, as described in
the Unicode Standard definition D68, and returns a string in the NFD
normalization form. If the second argument is the string `COMPATIBILITY`,
`DECOMPOSE` applies compatibility decomposition, as described in the Unicode
Standard definition D65, and returns a string in the NFKD normalization form.
The default behavior is to apply the canonical decomposition.

In a pessimistic case, the return value of `DECOMPOSE` may be a few times
longer than `string`. If a string to be returned is longer than the maximum
length `VARCHAR2` value in a given runtime environment, the value is silently
truncated to the maximum `VARCHAR2` length.

Both arguments to `DECOMPOSE` can be of any of the data types `CHAR`,
`VARCHAR2`, `NCHAR`, or `NVARCHAR2`. Other data types are allowed if they can
be implicitly converted to `VARCHAR2`or `NVARCHAR2`. The return value of
`DECOMPOSE` is in the same character set as its first argument.

`CLOB` and `NCLOB` values are supported through implicit conversion. If
`string` is a character LOB value, then it is converted to a `VARCHAR2` value
before the `DECOMPOSE` operation. The operation will fail if the size of the
LOB value exceeds the supported length of the `VARCHAR2` in the particular
execution environment.

See Also:

  * [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG014) for information on Unicode character sets and character semantics 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules, which define the collation assigned to the character return value of `DECOMPOSE`

  * [COMPOSE](COMPOSE.md#GUID-A16E7D53-E7F8-46A6-B3F8-BA322D129019)

Examples

The following example decomposes the string "`ChÃ¢teaux`" into its component
code points:

    
    
    SELECT DECOMPOSE ('ChÃ¢teaux')
      FROM DUAL; 
    
    DECOMPOSE
    ---------
    ChÃ¢teaux

Note:

The results of this example can vary depending on the character set of your
operating system.


[← Previous](DECODE.md)

[Next →](DENSE_RANK.md)
