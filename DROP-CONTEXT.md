[Previous](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md) [Next](DROP-
DATABASE.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP CONTEXT 

## DROP CONTEXT

Purpose

Use the `DROP` `CONTEXT` statement to remove a context namespace from the
database.

Removing a context namespace does not invalidate any context under that
namespace that has been set for a user session. However, the context will be
invalid when the user next attempts to set that context.

See Also:

[CREATE CONTEXT](CREATE-CONTEXT.md#GUID-
FDF62812-A884-479C-9C1B-5BD6DDEFE7FA) and [Oracle Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG70071) for more information on contexts

Prerequisites

You must have the `DROP` `ANY` `CONTEXT` system privilege.

Syntax

drop_context::=

![Description of drop_context.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_context.gif)  
[Description of the illustration drop_context.eps](img_text/drop_context.md)

Semantics

namespace

Specify the name of the context namespace to drop. You cannot drop the built-
in namespace `USERENV`.

See Also:

[SYS_CONTEXT](SYS_CONTEXT.md#GUID-B9934A5D-D97B-4E51-B01B-80C76A5BD086) for
information on the `USERENV` namespace

Examples

Dropping an Application Context: Example

The following statement drops the context created in [CREATE CONTEXT](CREATE-
CONTEXT.md#GUID-FDF62812-A884-479C-9C1B-5BD6DDEFE7FA):

    
    
    DROP CONTEXT hr_context;


[← Previous](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)

[Next →](DROP-DATABASE.md)
