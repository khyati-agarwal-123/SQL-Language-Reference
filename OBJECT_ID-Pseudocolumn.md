[Previous](COLUMN_VALUE-Pseudocolumn.md) [Next](OBJECT_VALUE-
Pseudocolumn.md) JavaScript must be enabled to correctly display this
content

  1. [SQL Language Reference ](index.md)
  2. [ Pseudocolumns](Pseudocolumns.md)
  3. OBJECT_ID Pseudocolumn 

## OBJECT_ID Pseudocolumn

The `OBJECT_ID` pseudocolumn returns the object identifier of a column of an
object table or view. Oracle uses this pseudocolumn as the primary key of an
object table. `OBJECT_ID` is useful in `INSTEAD` `OF` triggers on views and
for identifying the ID of a substitutable row in an object table.

Note:

In earlier releases, this pseudocolumn was called `SYS_NC_OID$`. That name is
still supported for backward compatibility. However, Oracle recommends that
you use the more intuitive name `OBJECT_ID`.

See Also:

[Oracle Database Object-Relational Developer's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADOBJ7129) for examples of the use of this pseudocolumn


[← Previous](COLUMN_VALUE-Pseudocolumn.md)

[Next →](OBJECT_VALUE-Pseudocolumn.md)
