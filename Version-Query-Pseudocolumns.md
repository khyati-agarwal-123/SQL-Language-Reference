[Previous](Sequence-Pseudocolumns.md) [Next](COLUMN_VALUE-Pseudocolumn.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Pseudocolumns](Pseudocolumns.md)
  3. Version Query Pseudocolumns 

## Version Query Pseudocolumns

The version query pseudocolumns are valid only in Oracle Flashback Version
Query, which is a form of Oracle Flashback Query. The version query
pseudocolumns are:

  * `VERSIONS_STARTSCN` and `VERSIONS_STARTTIME`: Starting System Change Number (SCN) or `TIMESTAMP` when the row version was created. This pseudocolumn identifies the time when the data first had the values reflected in the row version. Use this pseudocolumn to identify the past target time for Oracle Flashback Table or Oracle Flashback Query. If this pseudocolumn is `NULL`, then the row version was created before start. 

  * `VERSIONS_ENDSCN` and `VERSIONS_ENDTIME`: SCN or `TIMESTAMP` when the row version expired. If the pseudocolumn is `NULL`, then either the row version was current at the time of the query or the row corresponds to a `DELETE` operation. 

  * `VERSIONS_XID`: Identifier (a `RAW` number) of the transaction that created the row version. 

  * `VERSIONS_OPERATION`: Operation performed by the transaction: `I` for insertion, `D` for deletion, or `U` for update. The version is that of the row that was inserted, deleted, or updated; that is, the row after an `INSERT` operation, the row before a `DELETE` operation, or the row affected by an `UPDATE` operation. 

For user updates of an index key, Oracle Flashback Version Query might treat
an `UPDATE` operation as two operations, `DELETE` plus `INSERT`, represented
as two version rows with a `D` followed by an `I` `VERSIONS_OPERATION`.

See Also:

  * [flashback_query_clause](SELECT.md#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6__I2112818) for more information on version queries 

  * [Oracle Database Development Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADFNS01004) for more information on using Oracle Flashback Version Query 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation rules for values of the `VERSIONS_OPERATION` pseudocolumn 


[← Previous](Sequence-Pseudocolumns.md)

[Next →](COLUMN_VALUE-Pseudocolumn.md)
