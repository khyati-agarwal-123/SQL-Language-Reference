##  JSON_ID Operator {#GUID-89A6BCC7-B500-429B-8299-A3F78D1D077F} 

Syntax 

  


![Description of json_id.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_id.gif)[ Description of the illustration json_id.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/json_id.md)

  


Purpose 

` JSON_ID ` takes a single argument, one of ` 'OID' ` or ` 'UUID' ` to create a value for a document-identifier field that you provide. 

` JSON_ID ` returns a value of SQL type ` RAW ` that is globally unique. The value returned is determined by the argument that you provide. With string ` 'OID' ` , a 12-byte ` RAW ` value is returned; with string ` 'UUID' ` , a 16-byte ` RAW ` value is returned. 

> **note:** See Also: 

[ JSON Collections ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN-GUID-F69A381E-7A6A-4D18-A148-B0C541C174BD) of the *JSON Developer's Guide* . 
