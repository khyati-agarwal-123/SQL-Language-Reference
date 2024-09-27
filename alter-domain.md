[Previous](ALTER-DISKGROUP.md) [Next](ALTER-FLASHBACK-ARCHIVE.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER DOMAIN

## ALTER DOMAIN

Purpose

Use this statement to make changes to a domain. When you alter a domain note
that checks and catalog changes are made on objects dependent on the domain.

Prerequisites

The domain must be in your own schema, or you must have `ALTER` object
privilege on the domain, or you must have `ALTER ANY DOMAIN` system privilege.

Syntax

alter_domain ::=

  

![Description of alter_domain.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_domain.gif)  
[Description of the illustration alter_domain.eps](img_text/alter_domain.md)

  

[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052)

For the full syntax and semantics of the `annotations_clause `see
[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052).

Semantics

USECASE

This keyword is optional and is provided for semantic clarity. It indicates
that the domain is to describe a data use case.

IF EXISTS

Specify `IF EXISTS` to alter an existing domain.

Specifying `IF NOT EXISTS` with `ALTER DOMAIN` results in the error: `
Incorrect IF EXISTS clause for ALTER/DROP statement`.

ADD DISPLAY

Adds the `display_expression` to the domain. Raises an error if the domain
already has a `display_expression` .

Invalidates all SQL statements referencing `DOMAIN_DISPLAY` for an expression
of the given domain.

For domain functions see [Domain Functions](Single-Row-Functions.md#GUID-
AEF8F898-493F-4BE8-86E6-06241BB78AB0)

MODIFY DISPLAY

Changes the domain's display expression to `display_expression` and
invalidates all SQL statements referencing `DOMAIN_DISPLAY` for an expression
of the given domain.

Raises an error if the domain does not have an associated display expression

Invalidates all SQL statements referencing `DOMAIN_DISPLAY` for an expression
of the given domain.

Both `ALTER DOMAIN ADD DISPLAY` and `ALTER DOMAIN MODIFY DISPLAY` type-check
the display expression against all the allowed data types of the domain.

DROP DISPLAY

Raises an error if the domain does not have a display expression. Raises an
error If the domain has dependent flexible domain.

Otherwise it removes the display expression from the domain's description, and
invalidates all SQL statements referencing `DOMAIN_DISPLAY` for an expression
of the given domain.

ADD MODIFY DROP ORDER

The semantics of these DDLs are the same as for `DISPLAY`, when translated to
the `ORDER` expression and `DOMAIN_ORDER` function.

annotations_clause

See Also:

  * For the full semantics of the annotations clause see [annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052). 

  * [CREATE DOMAIN](create-domain.md#GUID-17D3A9C6-D993-4E94-BF6B-CACA56581F41)

Examples

The following statement changes the display expression of the domain
`day_of_week`. It raises an error if the domain does not have a display
expression:

    
    
    ALTER DOMAIN day_of_week
          MODIFY DISPLAY LOWER(day_of_week);

The following statement removes the display expression from the domain
`day_of_week`. It raises an error if the domain does not have a display
expression:

    
    
    ALTER DOMAIN day_of_week
          DROP DISPLAY;

The following statement an display expression to the domain `day_of_week`. It
raises an error if the domain already has a display expression:

    
    
    ALTER DOMAIN day_of_week
          ADD DISPLAY INITCAP(day_of_week);

The following statement changes the order expression of the domain
`year_of_birth`. It raises an error if the domain does not have an order
expression:

    
    
    ALTER DOMAIN year_of_birth
          MODIFY ORDER MOD(year_of_birth,100);

The following statement removes the order expression from the domain
`year_of_birth`. It raises an error if the domain does not have an order
expression:

    
    
    ALTER DOMAIN year_of_birth
          DROP ORDER;

The following statement an order expression to the domain `year_of_birth`. It
raises an error if the domain already has an order expression:

    
    
    ALTER DOMAIN year_of_birth
          ADD ORDER FLOOR(year_of_birth/100);

The following example adds the annotation `Display` with the value
"`day_of_week`" to the domain. If the domain already has the `Display`
annotation it raises an error:

    
    
    ALTER DOMAIN day_of_week
          ANNOTATIONS(Display 'Day of week');


[← Previous](ALTER-DISKGROUP.md)

[Next →](ALTER-FLASHBACK-ARCHIVE.md)
