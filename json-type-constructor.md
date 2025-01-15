##  JSON Type Constructor {#GUID-2B598841-A327-4610-91B9-602F480A8314} 

Syntax 

  


![Description of json_constructor.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_constructor.gif)[ Description of the illustration json_constructor.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/json_constructor.md)

  


Purpose 

The JSON data type constructor, JSON, takes as input a textual JSON value (a scalar, object, or array), parses it, and returns the value as an instance of JSON type. Alternatively, the input can be an instance of SQL type VECTOR, a user-defined PL/SQL type, or a SQL aggregate type. 

You can use the JSON data type constructor ` JSON ` to parse textual JSON input ( a scalar, object, or array), and return it as an instance of type ` JSON ` . 

Input values must pass the ` IS JSON ` test. Input values that fail the ` IS JSON ` test are rejected with a syntax error. 

To filter out duplicate input values, you must run the ` IS JSON (WITH UNIQUE KEYS) ` check on the textual JSON input before using the ` JSON ` constructor. 

Prerequisites 

You can use the constructor ` JSON ` only if database initialization parameter ` compatible ` is atleast ` 20 ` . 

> **note:** See Also: 

[ JSON Data Type Constructor ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADJSN-GUID-F04556DD-B435-425E-8EA6-FBE636FEEA2C) of the *JSON Developer's Guide* . 

*expr* 

The input in ` expr ` must be a syntactically valid textual representation of type ` VARCHAR2 ` , ` CLOB ` and ` BLOB ` . It can also be a literal SQL string. A SQL ` NULL ` input value results in a JSON type instance of SQL ` NULL ` . 
