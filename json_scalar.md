##  JSON_SCALAR {#GUID-F05BD523-F827-4A5F-9A82-8CBC2DB04E2E} 

Syntax 

  


![Description of json_scalar.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_scalar.gif)[ Description of the illustration json_scalar.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/json_scalar.md)

  


Purpose 

` JSON_SCALAR ` accepts a SQL scalar value as input and returns a corresponding JSON scalar value as a ` JSON ` type instance. The value can be an Oracle-specific JSON-language type, such as a date, which is not part of the JSON standard. 

To use ` JSON_SCALAR ` you must set the database initialization parameter ` compatible ` is at least ` 20 ` . Otherwise it raises an error. 

The argument to ` JSON_SCALAR ` can be an instance of any of these SQL data types: ` BINARY_DOUBLE ` , ` BINARY_FLOAT ` , ` BLOB ` , ` CLOB ` , ` DATE ` , ` INTERVAL YEAR TO MONTH ` , ` INTERVAL DAY TO SECOND ` , ` JSON ` , ` NUMBER ` , ` RAW ` , ` TIMESTAMP ` , ` VARCHAR ` , ` VARCHAR2 ` , or ` VECTOR ` . 

The returned ` JSON ` type instance is a JSON-language scalar value supported by Oracle. 

If the argument to ` JSON_SCALAR ` is a SQL NULL value, then you can obtain a return value as follows: 

  * SQL ` NULL ` , the default behavior 

  * JSON ` null ` , using keywords ` NULL ON NULL `

  * An empty JSON string, " ", using keywords ` EMPTY STRING ON NULL `




The default behavior of returning SQL ` NULL ` is the only exception to the rule that a JSON scalar value is returned. 

> **note:** See Also: 

See [ Oracle SQL Function JSON_SCALAR ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN-GUID-5EAC1ADD-E138-4488-9FB0-7C245F87CBFD) of the *JSON Developer's Guide* . 
