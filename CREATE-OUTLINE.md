[Previous](CREATE-OPERATOR.md) [Next](CREATE-PACKAGE.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE OUTLINE 

## CREATE OUTLINE

Purpose

Note:

Stored outlines are deprecated. They are still supported for backward
compatibility. However, Oracle recommends that you use SQL plan management
instead. SQL plan management creates SQL plan baselines, which offer superior
SQL performance stability compared with stored outlines.

You can migrate existing stored outlines to SQL plan baselines by using the
`MIGRATE_STORED_OUTLINE` function of the `DBMS_SPM` package or Enterprise
Manager Cloud Control. When the migration is complete, the stored outlines are
marked as migrated and can be removed. You can drop all migrated stored
outlines on your system by using the `DROP_MIGRATED_STORED_OUTLINE` function
of the `DBMS_SPM` package.

See Also:â[Oracle Database SQL Tuning
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=TGSQL615) for more information about SQL plan management
and [Oracle Database PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS150) for information about the `DBMS_SPM` package

Use the `CREATE` `OUTLINE` statement to create a stored outline, which is a
set of attributes used by the optimizer to generate an execution plan. You can
then instruct the optimizer to use a set of outlines to influence the
generation of execution plans whenever a particular SQL statement is issued,
regardless of changes in factors that can affect optimization. You can also
modify an outline so that it takes into account changes in these factors.

Note:

The SQL statement you want to affect must be an exact string match of the
statement specified when creating the outline.

See Also:

  * [Oracle Database SQL Tuning Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=TGSQL615) for information on execution plans 

  * [ALTER OUTLINE](ALTER-OUTLINE.md#GUID-49F25C82-0783-4407-88BB-613F986C2FEC) for information on modifying an outline 

  * [ALTER SESSION](ALTER-SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B) and [ALTER SYSTEM](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB) for information on the `USE_STORED_OUTLINES` and `USE_PRIVATE_OUTLINES` parameters 

Prerequisites

To create a public or private outline, you must have the `CREATE` `ANY`
`OUTLINE` system privilege.

If you are creating a clone outline from a source outline, then you must also
have the `SELECT_CATALOG_ROLE` role.

You can enable or disable the use of stored outlines dynamically for an
individual session or for the system:

  * Enable the `USE_STORED_OUTLINES` parameter to use public outlines. 

  * Enable the `USE_PRIVATE_OUTLINES` parameter to use private stored outlines. 

Syntax

create_outline::=

![Description of create_outline.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_outline.gif)  
[Description of the illustration
create_outline.eps](img_text/create_outline.md)

Note:

None of the clauses after `outline` are required. However, you must specify at
least one clause after `outline`, and it must be either the `FROM` clause or
the `ON` clause.

Semantics

OR REPLACE

Specify `OR` `REPLACE` to replace an existing outline with a new outline of
the same name.

PUBLIC | PRIVATE

Specify `PUBLIC` if you are creating an outline for use by `PUBLIC`. This is
the default.

Specify `PRIVATE` to create an outline for private use by the current session
only. The data of this outline is stored in the current schema.

outline

Specify the unique name to be assigned to the stored outline. The name must
satisfy the requirements listed in "[Database Object Naming Rules](Database-
Object-Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".
If you do not specify `outline`, then the database generates an outline name.

See Also:

"[Creating an Outline: Example](CREATE-OUTLINE.md#GUID-7CC033AF-
DB19-4616-87D9-8173939FD627__I2119940)"

FROM source_outline Clause

Use the `FROM` clause to create a new outline by copying an existing one. By
default, Oracle Database looks for `source_category` in the public area. If
you specify `PRIVATE`, then the database looks for the outline in the current
schema.

Restriction on Copying an Outline

If you specify the `FROM` clause, then you cannot specify the `ON` clause.

See Also:

"[Creating a Private Clone Outline: Example](CREATE-
OUTLINE.md#GUID-7CC033AF-DB19-4616-87D9-8173939FD627__I2119956)" and
"[Publicizing a Private Outline to the Public Area: Example](CREATE-
OUTLINE.md#GUID-7CC033AF-DB19-4616-87D9-8173939FD627__I2119967)"

FOR CATEGORY Clause

Specify an optional name used to group stored outlines. For example, you could
specify a category of outlines for end-of-week use and another for end-of-
quarter use. If you do not specify `category`, then the outline is stored in
the `DEFAULT` category.

ON Clause

Specify the SQL statement for which the database will create an outline when
the statement is compiled. This clause is optional only if you are creating a
copy of an existing outline using the `FROM` clause.

You can specify any one of the following statements: `SELECT`, `DELETE`,
`UPDATE`, `INSERT` ... `SELECT`, `CREATE` `TABLE` ... `AS` `SELECT`.

Restrictions on the ON Clause

This clause is subject to the following restrictions:

  * If you specify the `ON` clause, then you cannot specify the `FROM` clause. 

  * You cannot create an outline on a multitable `INSERT` statement. 

  * The SQL statement in the `ON` clause cannot include any DML operation on a remote object. 

Note:

In subsequent statements, you can specify additional outlines for the same SQL
statement, but each outline for the same statement must specify a different
category in the `CATEGORY` clause.

Examples

Creating an Outline: Example

The following statement creates a stored outline by compiling the `ON`
statement. The outline is called `salaries` and is stored in the category
`special`.

    
    
    CREATE OUTLINE salaries FOR CATEGORY special
       ON SELECT last_name, salary FROM employees;
    

When this same `SELECT` statement is subsequently compiled, if the
`USE_STORED_OUTLINES` parameter is set to `special`, the database generates
the same execution plan as was generated when the outline `salaries` was
created.

Creating a Private Clone Outline: Example

The following statement creates a stored private outline `my_salaries` based
on the public category `salaries` created in the preceding example.

    
    
    CREATE OR REPLACE PRIVATE OUTLINE my_salaries
       FROM salaries;

Publicizing a Private Outline to the Public Area: Example

The following statement copies back (publicizes) a private outline to the
public area after private editing:

    
    
    CREATE OR REPLACE OUTLINE public_salaries 
       FROM PRIVATE my_salaries;


[← Previous](CREATE-OPERATOR.md)

[Next →](CREATE-PACKAGE.md)
