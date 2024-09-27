[Previous](DROP-ROLLBACK-SEGMENT.md) [Next](DROP-SYNONYM.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP SEQUENCE 

## DROP SEQUENCE

Purpose

Use the `DROP` `SEQUENCE` statement to remove a sequence from the database.

You can also use this statement to restart a sequence by dropping and then re-
creating it. For example, if you have a sequence with a current value of 150
and you would like to restart the sequence with a value of 27, then you can
drop the sequence and then re-create it with the same name and a `START`
`WITH` value of 27.

See Also:

[CREATE SEQUENCE](CREATE-
SEQUENCE.md#GUID-E9C78A8C-615A-4757-B2A8-5E6EFB130571) and [ALTER
SEQUENCE](ALTER-SEQUENCE.md#GUID-A6468B63-E7C9-4EF0-B048-82FE2449B26D) for
more information on creating and modifying a sequence

Prerequisites

The sequence must be in your own schema or you must have the `DROP` `ANY`
`SEQUENCE` system privilege.

Syntax

drop_sequence::=

![Description of drop_sequence.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_sequence.gif)  
[Description of the illustration
drop_sequence.eps](img_text/drop_sequence.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the sequence. If you omit `schema`, then Oracle
Database assumes the sequence is in your own schema.

sequence_name

Specify the name of the sequence to be dropped.

Examples

Dropping a Sequence: Example

The following statement drops the sequence `customers_seq` owned by the user
`oe`, which was created in "[Creating a Sequence: Example](CREATE-
SEQUENCE.md#GUID-E9C78A8C-615A-4757-B2A8-5E6EFB130571__I2092099)". To issue
this statement, you must either be connected as user `oe` or have the `DROP`
`ANY` `SEQUENCE` system privilege:

    
    
    DROP SEQUENCE oe.customers_seq; 


[← Previous](DROP-ROLLBACK-SEGMENT.md)

[Next →](DROP-SYNONYM.md)
