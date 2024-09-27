[Previous](Oracle-SQL-Reserved-Words-and-Keywords.md) [Next](Oracle-SQL-
Keywords.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Oracle SQL Reserved Words and Keywords](Oracle-SQL-Reserved-Words-and-Keywords.md)
  3. Oracle SQL Reserved Words

## Oracle SQL Reserved Words

This section lists Oracle SQL reserved words. You cannot use Oracle SQL
reserved words as nonquoted identifiers. Quoted identifiers can be reserved
words, although this is not recommended.

Note:

In addition to the following reserved words, Oracle uses system-generated
names beginning with "`SYS_`" for implicitly generated schema objects and
subobjects. Oracle discourages you from using this prefix in the names you
explicitly provide to your schema objects and subobjects to avoid possible
conflict in name resolution.

The `V$RESERVED_WORDS` data dictionary view provides additional information on
each reserved word, including whether it is always reserved or is reserved
only for particular uses. Refer to [Oracle Database
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30204) for more information.

Words followed by an asterisk (*) are also ANSI reserved words.

  * `ACCESS`
  * `ADD`
  * `ALL *`
  * `ALTER *`
  * `AND *`
  * `ANY *`
  * `AS *`
  * `ASC`
  * `AUDIT`
  * `BETWEEN *`
  * `BY *`
  * `CHAR *`
  * `CHECK *`
  * `CLUSTER`
  * `COLUMN` * 
  * `COLUMN_VALUE` (See Note 1 at the end of this list) 
  * `COMMENT`
  * `COMPRESS`
  * `CONNECT *`
  * `CREATE *`
  * `CURRENT *`
  * `DATE *`
  * `DECIMAL *`
  * `DEFAULT *`
  * `DELETE *`
  * `DESC`
  * `DISTINCT *`
  * `DROP *`
  * `ELSE *`
  * `EXCLUSIVE`
  * `EXISTS` * 
  * `FILE`
  * `FLOAT *`
  * `FOR *`
  * `FROM *`
  * `GRANT *`
  * `GROUP *`
  * `HAVING *`
  * `IDENTIFIED`
  * `IMMEDIATE`
  * `IN *`
  * `INCREMENT`
  * `INDEX`
  * `INITIAL`
  * `INSERT *`
  * `INTEGER *`
  * `INTERSECT *`
  * `INTO *`
  * `IS *`
  * `LEVEL`
  * `LIKE *`
  * `LOCK`
  * `LONG`
  * `MAXEXTENTS`
  * `MINUS`
  * `MLSLABEL`
  * `MODE`
  * `MODIFY`
  * `NESTED_TABLE_ID` (See Note 1 at the end of this list) 
  * `NOAUDIT`
  * `NOCOMPRESS`
  * `NOT *`
  * `NOWAIT`
  * `NULL *`
  * `NUMBER`
  * `OF *`
  * `OFFLINE`
  * `ON *`
  * `ONLINE`
  * `OPTION`
  * `OR *`
  * `ORDER *`
  * `PCTFREE`
  * `PRIOR`
  * `PUBLIC`
  * `RAW`
  * `RENAME`
  * `RESOURCE`
  * `REVOKE *`
  * `ROW` * 
  * `ROWID` (See Note 2 at the end of this list) 
  * `ROWNUM`
  * `ROWS *`
  * `SELECT *`
  * `SESSION`
  * `SET *`
  * `SHARE`
  * `SIZE`
  * `SMALLINT *`
  * `START` * 
  * `SUCCESSFUL`
  * `SYNONYM`
  * `SYSDATE`
  * `TABLE *`
  * `THEN *`
  * `TO *`
  * `TRIGGER` * 
  * `UID`
  * `UNION *`
  * `UNIQUE *`
  * `UPDATE *`
  * `USER *`
  * `VALIDATE`
  * `VALUES *`
  * `VARCHAR *`
  * `VARCHAR2`
  * `VIEW`
  * `WHENEVER *`
  * `WHERE` * 
  * `WITH *`
  * 

Note 1: This keyword is only reserved for use as an attribute name.

Note 2: You cannot use the uppercase word `ROWID`, either quoted or nonquoted,
as a column name. However, you can use the uppercase word as a quoted
identifier that is not a column name, and you can use the word with one or
more lowercase letters (for example, "Rowid" or "rowid") as any quoted
identifier, including a column name.


[← Previous](Oracle-SQL-Reserved-Words-and-Keywords.md)

[Next →](Oracle-SQL-Keywords.md)
