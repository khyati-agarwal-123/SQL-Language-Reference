[Previous](OBJECT_ID-Pseudocolumn.md) [Next](ORA_ROWSCN-Pseudocolumn.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Pseudocolumns](Pseudocolumns.md)
  3. OBJECT_VALUE Pseudocolumn 

## OBJECT_VALUE Pseudocolumn

The `OBJECT_VALUE` pseudocolumn returns system-generated names for the columns
of an object table, `XMLType` table, object view, or `XMLType` view. This
pseudocolumn is useful for identifying the value of a substitutable row in an
object table and for creating object views with the `WITH` `OBJECT`
`IDENTIFIER` clause.

Note:

In earlier releases, this pseudocolumn was called `SYS_NC_ROWINFO$`. That name
is still supported for backward compatibility. However, Oracle recommends that
you use the more intuitive name `OBJECT_VALUE`.

See Also:

  * [object_table](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159410) and [object_view_clause](CREATE-VIEW.md#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30__I2164765) for more information on the use of this pseudocolumn 

  * [Oracle Database Object-Relational Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADOBJ7129) for examples of the use of this pseudocolumn 


[← Previous](OBJECT_ID-Pseudocolumn.md)

[Next →](ORA_ROWSCN-Pseudocolumn.md)
