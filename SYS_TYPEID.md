[Previous](sys_row_etag.md) [Next](SYS_XMLAGG.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. SYS_TYPEID 

## SYS_TYPEID

Syntax

![Description of sys_typeid.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sys_typeid.gif)  
[Description of the illustration sys_typeid.eps](img_text/sys_typeid.md)

Purpose

`SYS_TYPEID` returns the typeid of the most specific type of the operand. This
value is used primarily to identify the type-discriminant column underlying a
substitutable column. For example, you can use the value returned by
`SYS_TYPEID` to build an index on the type-discriminant column.

You can use this function only on object type operands. All final root object
typesâfinal types not belonging to a type hierarchyâhave a null typeid.
Oracle Database assigns to all types belonging to a type hierarchy a unique
non-null typeid.

See Also:

[Oracle Database Object-Relational Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADOBJ002) for more information on typeids

Examples

The following examples use the tables `persons` and `books`, which are created
in "[Substitutable Table and Column Examples](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2090577)". The first
query returns the most specific types of the object instances stored in the
`persons` table.

    
    
    SELECT name, SYS_TYPEID(VALUE(p)) "Type_id" FROM persons p;
    
    NAME                      Type_id
    ------------------------- --------------------------------
    Bob                       01
    Joe                       02
    Tim                       03
    

The next query returns the most specific types of authors stored in the table
`books`:

    
    
    SELECT b.title, b.author.name, SYS_TYPEID(author)
       "Type_ID" FROM books b;
    
    TITLE                     AUTHOR.NAME          Type_ID
    ------------------------- -------------------- -------------------
    An Autobiography          Bob                  01
    Business Rules            Joe                  02
    Mixing School and Work    Tim                  03
    

You can use the `SYS_TYPEID` function to create an index on the type-
discriminant column of a table. For an example, see "[Indexing on
Substitutable Columns: Examples](CREATE-
INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE__I2089060)".


[← Previous](sys_row_etag.md)

[Next →](SYS_XMLAGG.md)
