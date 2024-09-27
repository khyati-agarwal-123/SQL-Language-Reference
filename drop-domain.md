[Previous](DROP-DISKGROUP.md) [Next](DROP-EDITION.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP DOMAIN

## DROP DOMAIN

Purpose

Use this statement to drop a domain, thereby disassociating the domain from
all its dependent objects.

Prerequisites

The domain must be in your own schema or you must have the `DROP ANY DOMAIN`
system privilege.

Syntax

drop_domain::=

  

![Description of drop_domain.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_domain.gif)  
[Description of the illustration drop_domain.eps](img_text/drop_domain.md)

  

Semantics

USECASE

This keyword is optional and is provided for semantic clarity. It indicates
that the domain is to describe a data use case.

IF EXISTS

Specify `IF EXISTS` to drop a domain that exists.

You cannot specify `IF NOT EXISTS` with `DROP DOMAIN`. This results in the
following error: `ORA-11544:Incorrect IF EXISTS clause for ALTER/DROP
statement`.

You can drop a domain by specifying its domain name and disassociate it from
all its dependent columns. In the following example `email` is the name of a
domain name:

    
    
    DROP DOMAIN email;

If a domain is associated with columns, `DROP DOMAIN` `domain_name` fails with
`ORA-11502:The domain <domain_name> to be dropped has dependent objects.`This
includes any tables in the recyclebin.

You can additionally drop a domain by specifying two optional keywords: either
`FORCE` or `FORCE PRESERVE` which have different meanings:

FORCE

`DROP DOMAIN domain_name FORCE ` disassociates the domain from all its
dependent columns. This includes dropping all constraints on columns that were
inherited from the domain. Defaults inherited from the domain are also dropped
unless these defaults were set specifically on columns.

If you must drop a domain and have dependent tables in the recyclebin, you
must use the `FORCE` option.

FORCE PRESERVE

Use `DROP DOMAIN domain_name FORCE PRESERVE` if you want to preserve domain
defaults and domain constraints on columns inherited from the domain. You must
first specify `FORCE`, in order to specify the `PRESERVE` option. Use this
option if you want to temporarily drop the domain and recreate it later with
new data and the former dependent columns. In this case you want to ensure
that the table data continues to be consistent with the domain definition with
all the constraints and defaults on columns inherited from the domain
preserved. If you drop a domain with `FORCE PRESERVE` and later recreate the
domain and reassociate the column with it, you can end up with a second
constraint. In this case, use `ALTER TABLE DROP CONSTRAINT` to drop the second
constraint.

If there are no tables or materialized views with columns of the given domain,
then `DROP DOMAIN` will invalidate any SQL dependent statements and remove the
domain object from the catalog. In this case you can specify `FORCE` and
`FORCE PRESERVE` without affecting the domain or the domain's dependent
objects.

If there are tables or materialized views with columns of the given domain,
`DROP DOMAIN` without the `FORCE` option will fail without affecting the
domain or domain's dependent objects.

If there are tables or materialized views with columns of the given domain,
`DROP DOMAIN FORCE` will do the following:

  * Remove the default expression from any dependent column, if the column has a default expression that was only set as a domain default. If the default expression was added on the column and set as domain default, then default on the column is preserved.

  * Remove the domain annotations from all dependent columns

  * Preserve collation on any domain dependent columns

  * Invalidate all SQL dependent statements in the cursor cache.

  * Materialized views (MVs) that reference domain functions like `DOMAIN_DISPLAY`, `DOMAIN_ORDER`, `DOMAIN_NAME` will be invalidated so they can be fully refreshed. MVs that reference columns of a given domain will not be invalidated . 

  * Remove the domain successfully.

If there are flexible domains referencing the domain, then `DROP DOMAIN`
without the `FORCE` option will raise an error, while `DROP DOMAIN FORCE` will
drop all flexible dependent domains in `FORCE` mode also.

Examples

The following example drops the `domain day_of_week`. If there are any columns
associated with the domain the statement will raise `ORA-11502` and the domain
will still be present:

    
    
    DROP DOMAIN day_of_week;

The following statement drops the `domain day_of_week`. If there are any
columns associated with it, the columns will inherit any defaults and
constraints from the domain:

    
    
    DROP DOMAIN day_of_week FORCE PRESERVE;


[← Previous](DROP-DISKGROUP.md)

[Next →](DROP-EDITION.md)
