[Previous](drop-domain.md) [Next](DROP-FLASHBACK-ARCHIVE.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP EDITION 

## DROP EDITION

Purpose

Use the `DROP` `EDITION` statement to drop an edition, along with all actual
editionable objects it contains. An actual editionable object is an
editionable object that has been created or modified in an edition.

See Also:

[CREATE EDITION](CREATE-
EDITION.md#GUID-6CF92CA1-CAF7-4967-9B34-C02D72C23617) for a listing of
editionable object types

Prerequisites

You must have the `DROP` `ANY` `EDITION` system privilege, granted either
directly or through a role.

Syntax

drop_edition::=

![Description of drop_edition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_edition.gif)  
[Description of the illustration drop_edition.eps](img_text/drop_edition.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing edition.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

Objects that are not editionable, or that are editionable but have not been
actualized in the current edition, are not dropped.

You must specify `CASCADE` if the specified edition contains any actual
editionable objects.

Restrictions

This statement is subject to the following conditions and restrictions:

  * The specified edition cannot have both a parent edition and a child edition.

  * `DROP` `EDITION` will fail if you attempt to drop the default edition. 

  * `DROP` `EDITION` will fail if you attempt to drop the root edition and the recycle bin contains at least one object that used to be in that edition before it was dropped. Under these circumstances, even `DROP` `EDITION` `CASCADE` will fail. In this case, you can purge all objects from the recycle bin with the `PURGE` `DBA_RECYCLEBIN` statement and then drop the edition. Refer to [PURGE](PURGE.md#GUID-9257F773-E019-4464-80F4-F5AB61D7D9B6) for more information. 

`DROP` `EDITION` will also fail if you attempt to drop the leaf edition and
the recycle bin contains at least one object that used to be in that edition
before it was dropped. However, under these circumstances, `DROP` `EDITION`
`CASCADE` will succeed.

The only type of editioned object that might be in the recycle bin is a
trigger.

See Also:

  * [Oracle Database Development Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS-GUID-E6DBE175-2598-430F-9D0A-AB22CAE7DDDA)

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS-GUID-40AD8944-D7E0-4ACA-9A05-3DC502F47D27)

Examples

For examples that use this statement, refer to [CREATE EDITION](CREATE-
EDITION.md#GUID-6CF92CA1-CAF7-4967-9B34-C02D72C23617).


[← Previous](drop-domain.md)

[Next →](DROP-FLASHBACK-ARCHIVE.md)
