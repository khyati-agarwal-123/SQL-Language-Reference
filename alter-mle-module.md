[Previous](alter-mle-env.md) [Next](ALTER-OPERATOR.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER MLE MODULE

## ALTER MLE MODULE

Purpose

Use `ALTER MLE MODULE` to add metadata to existing MLE modules in the
database.

Prerequisites

To alter MLE modules in another schema you need the `ALTER ANY MLE` system
privilege. No privileges are required to alter MLE modules in your own schema.

Syntax

  

![Description of alter_mle_module.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_mle_module.gif)  
[Description of the illustration
alter_mle_module.eps](img_text/alter_mle_module.md)

  

Semantics

IF EXISTS

The `ALTER MLE MODULE` statement raises an `ORA-04103` error if the module
does not exist, or an `ORA-00922` error if an invalid attribute is specified.

schema

Specify the schema containing the MLE module. If you do not specify the
schema, then Oracle Database assumes that the module is in your own schema.

module_name

`module_name` refers to the name of the MLE module.

CLOB

`CLOB` refers to the text you can attach to an MLE module. You can use it to
refer to a commit in a version control system or as a part of a Software Bill
of Materials. The `CLOB` contents are freeform metadata that can be attached
to the MLE module. The metadata does not impact module functionality in any
way. Oracle recommends that the metadata be used to record version information
for the MLE module, e.g., the commit in a version control system that
corresponds to the deployed version of the module, or a Software Bill of
Materials for the module, for example the contents of `package-lock.json` for
a bundled JavaScript module.

Examples

The following example attaches metadata as `JSON` to MLE module `myMLEModule`:

    
    
    ALTER MLE MODULE myMLEModule 
    SET METADATA USING CLOB (
    SELECT JSON(
      '{
           "name": "value",
           "version": "1.2.0",
           "commitHash": "23fas4h",
           "projectName": "Database Backend"
      }')
    )
    

See Also:

  * [MLE JavaScript Modules and Environments](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MLEJS-GUID-32E2D1BB-37A0-4BA8-AD29-C967A8CA0CE1)

  * [CREATE MLE MODULE](create-mle-module.md#GUID-EF8D8EBC-2313-4C6C-A76E-1A739C304DCC)

  * [DROP MLE MODULE](drop-mle-module.md#GUID-1E3DEB27-76D6-4564-BC3F-B11DB02609A7)


[← Previous](alter-mle-env.md)

[Next →](ALTER-OPERATOR.md)
