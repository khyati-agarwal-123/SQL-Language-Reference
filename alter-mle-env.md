[Previous](ALTER-MATERIALIZED-ZONEMAP.md) [Next](alter-mle-module.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER MLE ENV

## ALTER MLE ENV

Purpose

Use `ALTER MLE ENV` to alter an exisiting MLE environment. You can add,
remove, and alter mappings for import names and set language options.

Prerequisites

You must have the `ALTER ANY MLE` privilege to alter an environment in schemas
other than your own. No privilege is needed to alter an environment in your
own schema.

Syntax

  

![Description of alter_mle_env.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_mle_env.gif)  
[Description of the illustration
alter_mle_env.eps](img_text/alter_mle_env.md)

  

Semantics

IF EXISTS

The `ALTER MLE MODULE` statement raises an `ORA-04103` error if the module
does not exist, or an `ORA-00922` error if an invalid attribute is specified.

schema

Specify the schema containing the MLE module. If you do not specify the
schema, then Oracle Database assumes that the module is in your own schema.

ADD IMPORTS Clause

Use `ADD IMPORTS` to add new mappings from import names to MLE module schema
objects. Mappings to be added are specified as a comma-separated list enclosed
in parentheses. Each element in the list is of the form: `import-name MODULE
[schema]. mle-module-name`.

The following cases produce errors:

  * If the environment already contains one or more of the import names, an `ORA-04109` error is thrown. 

  * If one or more of the MLE modules does not reside in the same schema as the environment, an `ORA-01031` error is thrown. 

DROP IMPORTS Clause

Use `DROP IMPORTS` to remove import names from the environment.

If the environment does nnot contain one or more of the specified import
names, an `ORA -04110` error is thrown.

ALTER IMPORTS Clause

Use `ALTER IMPORTS` to update import mappings for each of the specified import
names.

The following cases produce errors:

  * If the environment does not contain one or more of the import names, an `ORA-04110` error is thrown. 

  * If one or more of the new MLE modules does not reside in the same schema as the environment, an `ORA-01031` error is thrown. 

SET LANGUAGE OPTIONS Clause

Use `LANGUAGE OPTIONS` to specify language options for all execution contexts
created with this environment. Language options are specified as a string
literal consisting of comma-separated key-value pairs. Language options are
only parsed at runtime when an execution context is created using the MLE
environment.

If at context creation the language options string turns out to be invalid
(invalid format, unsupported options), an `ORA-04152` error is thrown.

Example

The following example modifies an exisiting environment myenv by enabling
JavaScript in strict mode:

    
    
    ALTER MLE ENV scott."myenv" SET LANGUAGE OPTIONS âjs.strict=
    true â;

COMPILE Clause

Use `COMPILE` to explicitly recompile an MLE environment. You can use this
clause to revalidate an environment that has become invalid and thereby catch
errors before run time.

See Also:

  * [MLE JavaScript Modules and Environments](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MLEJS-GUID-32E2D1BB-37A0-4BA8-AD29-C967A8CA0CE1)

  * [CREATE MLE ENV](create-mle-env.md#GUID-419C81FD-338D-495F-85CD-135D4D316718)

  * [DROP MLE ENV](drop-mle-env.md#GUID-19AD5DA2-10B0-46D7-BBEF-6313B6A79425)


[← Previous](ALTER-MATERIALIZED-ZONEMAP.md)

[Next →](alter-mle-module.md)
