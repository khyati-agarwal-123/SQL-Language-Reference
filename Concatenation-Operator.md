[Previous](COLLATE-Operator.md) [Next](Hierarchical-Query-Operators.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. Concatenation Operator

## Concatenation Operator

The concatenation operator manipulates character strings and `CLOB` data.
[Table 4-4](Concatenation-
Operator.md#GUID-08C10738-706B-4290-B7CD-C279EBC90F7E__CIHDBHCB "The first
column lists the single concatenation operators, the second column describes
it, and the third column provides an example.") describes the concatenation
operator.

Table 4-4 Concatenation Operator

Operator | Purpose | Example  
---|---|---  
|| |  Concatenates character strings and `CLOB` data.  | 
    
    
    SELECT 'Name is ' || last_name
      FROM employees
      ORDER BY last_name;  
  
The result of concatenating two character strings is another character string.
If both character strings are of data type `CHAR`, then the result has data
type `CHAR` and is limited to 2000 characters. If either string is of data
type `VARCHAR2`, then the result has data type `VARCHAR2` and is limited to
32767 characters if the initialization parameter `MAX_STRING_SIZE` `=`
`EXTENDED` and 4000 characters if `MAX_STRING_SIZE` `=` `STANDARD`. Refer to
[Extended Data Types](Data-
Types.md#GUID-8EFA29E9-E8D8-40A6-A43E-954908C954A4) for more information. If
either argument is a `CLOB`, the result is a temporary `CLOB`. Trailing blanks
in character strings are preserved by concatenation, regardless of the data
types of the string or `CLOB`.

On most platforms, the concatenation operator is two solid vertical bars, as
shown in [Table 4-4](Concatenation-
Operator.md#GUID-08C10738-706B-4290-B7CD-C279EBC90F7E__CIHDBHCB "The first
column lists the single concatenation operators, the second column describes
it, and the third column provides an example."). However, some IBM platforms
use broken vertical bars for this operator. When moving SQL script files
between systems having different character sets, such as between ASCII and
EBCDIC, vertical bars might not be translated into the vertical bar required
by the target Oracle Database environment. Oracle provides the `CONCAT`
character function as an alternative to the vertical bar operator for cases
when it is difficult or impossible to control translation performed by
operating system or network utilities. Use this function in applications that
will be moved between environments with differing character sets.

Although Oracle treats zero-length character strings as nulls, concatenating a
zero-length character string with another operand always results in the other
operand, so null can result only from the concatenation of two null strings.
However, this may not continue to be true in future versions of Oracle
Database. To concatenate an expression that might be null, use the `NVL`
function to explicitly convert the expression to a zero-length string.

See Also:

  * [Character Data Types](Data-Types.md#GUID-1BABC478-FB47-4962-9B0C-8B8BD059E733) for more information on the differences between the `CHAR` and `VARCHAR2` data types 

  * The functions [CONCAT](CONCAT.md#GUID-D8723EA5-C93A-45C3-83FB-1F3D2A4CEAF2) and [NVL](NVL.md#GUID-3AB61E54-9201-4D6A-B48A-79F4C4A034B2)

  * [Oracle Database SecureFiles and Large Objects Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADLOB001) for more information about `CLOB`s 

  * [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules for the concatenation operator 

Concatenation Example

This example creates a table with both `CHAR` and `VARCHAR2` columns, inserts
values both with and without trailing blanks, and then selects these values
and concatenates them. Note that for both `CHAR` and `VARCHAR2` columns, the
trailing blanks are preserved.

    
    
    CREATE TABLE tab1 (col1 VARCHAR2(6), col2 CHAR(6),
                       col3 VARCHAR2(6), col4 CHAR(6));
    
    INSERT INTO tab1 (col1,  col2,     col3,     col4)
              VALUES ('abc', 'def   ', 'ghi   ', 'jkl');
    
    SELECT col1 || col2 || col3 || col4 "Concatenation"
      FROM tab1;
    
    Concatenation
    ------------------------
    abcdef   ghi   jkl


[← Previous](COLLATE-Operator.md)

[Next →](Hierarchical-Query-Operators.md)
