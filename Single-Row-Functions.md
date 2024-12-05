[Previous](OLAP-Functions.html) [Next](ABS.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. Single-Row Functions 



## Single-Row Functions 

Single-row functions return a single result row for every row of a queried table or view. These functions can appear in select lists, `WHERE` clauses, `START` `WITH` and `CONNECT` `BY` clauses, and `HAVING` clauses. 

### Numeric Functions 

Numeric functions accept numeric input and return numeric values. Most numeric functions return `NUMBER` values that are accurate to 38 decimal digits. The transcendental functions `COS`, `COSH`, `EXP`, `LN`, `LOG`, `SIN`, `SINH`, `SQRT`, `TAN`, and `TANH` are accurate to 36 decimal digits. The transcendental functions `ACOS`, `ASIN`, `ATAN`, and `ATAN2` are accurate to 30 decimal digits. The numeric functions are: 

  * [ABS](ABS.html#GUID-D8D3489A-44EA-4FEC-A6F0-B5E312FFC231)* [ACOS](ACOS.html#GUID-B4C70DD5-B908-4130-975A-6CFD5C1AC1F9)
  * [ASIN](ASIN.html#GUID-809ACB4E-9FDA-4943-B234-DDB32522A523)* [ATAN](ATAN.html#GUID-12E8F1AA-54D0-4A19-8648-27094946C588)
  * [ATAN2](ATAN2.html#GUID-D34E671B-F3C0-4390-A2D8-ABB702B4B5D3)* [BITAND](BITAND.html#GUID-EADBED75-6AC5-4FBE-991A-E3B4D260F73B)
  * [CEIL (number)](CEIL.html#GUID-6DCC9AFB-9B80-4C27-AF63-5AA3B1E43660)* [COS](COS.html#GUID-C008F067-C6DC-4C13-9B7F-5A385415363A)
  * [COSH](COSH.html#GUID-A48CD625-5238-4259-9A1F-0FDBFD19841E)* [EXP](EXP.html#GUID-414FB4AE-03B5-41AD-AE33-E3755EFED0A0)
  * [FLOOR (number)](FLOOR.html#GUID-67F61AC7-C097-4397-A122-213157BF584F)* [LN](LN.html#GUID-DCC9EDAA-D308-4145-8E05-8D06A5EF5F6F)
  * [LOG](LOG.html#GUID-3739F356-A4A0-4D0D-A4EB-9725ACA05CD1)* [MOD](MOD.html#GUID-E12A3928-2C50-45B0-B8C3-82432C751B8C)
  * [NANVL](NANVL.html#GUID-3C094646-2A70-41F5-984C-9BC0FB31494A)* [POWER](POWER.html#GUID-D280B322-D2C3-46D0-8076-C88F16CBEDC2)
  * [REMAINDER](REMAINDER.html#GUID-430D4C4A-5779-4EBB-90C5-4D7CA7E73556)* [ROUND (number)](ROUND-number.html#GUID-849F6C45-0D72-4464-9C0F-8B6822BA85E1)
  * [SIGN](SIGN.html#GUID-08B75521-B5F5-4658-A005-4B4441C82945)* [SIN](SIN.html#GUID-2AF4895F-5D23-4165-89D5-B1D404ED99BF)
  * [SINH](SINH.html#GUID-1EB8626B-4D84-4EAD-BD23-1A97F186FD4A)* [SQRT](SQRT.html#GUID-E28C0B65-AAD8-4077-A82E-2FB4CD261CCA)
  * [TAN](TAN.html#GUID-473E2008-5951-4FC8-A356-14D3D085B8AA)* [TANH](TANH.html#GUID-8DD0B75F-1BDB-4E41-8C6D-FB5B2908AF80)
  * [TRUNC (number)](TRUNC-number.html#GUID-911AE7FE-E04A-471D-8B0E-9C50EBEFE07D)* [WIDTH_BUCKET](WIDTH_BUCKET.html#GUID-5E9058E5-A91F-45ED-A90D-E21355D19A88)



### Character Functions Returning Character Values 

Character functions that return character values return values of the following data types unless otherwise documented:

  * If the input argument is `CHAR` or `VARCHAR2`, then the value returned is `VARCHAR2`. 

  * If the input argument is `NCHAR` or `NVARCHAR2`, then the value returned is `NVARCHAR2`. 




The length of the value returned by the function is limited by the maximum length of the data type returned.

  * For functions that return `CHAR` or `VARCHAR2`, if the length of the return value exceeds the limit, then Oracle Database truncates it and returns the result without an error message. 

  * For functions that return `CLOB` values, if the length of the return values exceeds the limit, then Oracle raises an error and returns no data. 




The character functions that return character values are:

  * [CHR](CHR.html#GUID-35FEE007-D49C-4562-A904-041186AC8928)* [CONCAT](CONCAT.html#GUID-D8723EA5-C93A-45C3-83FB-1F3D2A4CEAF2)
  * [INITCAP](INITCAP.html#GUID-9FE9E0EE-D6B6-4C2C-BDEF-4FF4E1314560)* [LOWER](LOWER.html#GUID-C8682D4C-9BED-48AC-B73A-1D70BF307F48)
  * [LPAD](LPAD.html#GUID-0C27B59A-A6CF-43D3-BF4B-07A3D0F2CE20)* [LTRIM](LTRIM.html#GUID-81B3D53C-0BBC-4485-B057-C8012CD6E40F)
  * [NCHR](NCHR.html#GUID-3A1BDD54-6C0B-4067-99C5-A439C0F8D561)* [NLS_INITCAP](NLS_INITCAP.html#GUID-42C1581B-B5AA-4D4C-A489-BC5B38A754FD)
  * [NLS_LOWER](NLS_LOWER.html#GUID-96944213-377E-461C-9F02-2DC4EC2B1649)* [NLS_UPPER](NLS_UPPER.html#GUID-91D6302F-4DE2-49FA-8837-D46D3FD58DF8)
  * [NLSSORT](NLSSORT.html#GUID-781C6FE8-0924-4617-AECB-EE40DE45096D)* [REGEXP_REPLACE](REGEXP_REPLACE.html#GUID-EA80A33C-441A-4692-A959-273B5A224490)
  * [REGEXP_SUBSTR](REGEXP_SUBSTR.html#GUID-2903904D-455F-4839-A8B2-1731EF4BD099)* [REPLACE](REPLACE.html#GUID-1A79BDDF-2D3B-4AD4-98E7-985B2E59DA6B)
  * [RPAD](RPAD.html#GUID-064CFCAE-5902-49F9-800E-0AF311AEF595)* [RTRIM](RTRIM.html#GUID-95A7DAFB-F7AB-48F4-BE24-64B3C7A840AA)
  * [SOUNDEX](SOUNDEX.html#GUID-9C43625B-70CA-4B43-AE22-5EC2A02192F8)* [SUBSTR](SUBSTR.html#GUID-C8A20B57-C647-4649-A379-8651AA97187E)
  * [TRANSLATE](TRANSLATE.html#GUID-80F85ACB-092C-4CC7-91F6-B3A585E3A690)* [TRANSLATE ... USING](TRANSLATE-USING.html#GUID-EC8DE4D2-4F24-456D-A2E7-AD8F82E3A148)
  * [TRIM](TRIM.html#GUID-00D5C77C-19B1-4894-828F-066746235B03)* [UPPER](UPPER.html#GUID-0518FB26-7FE5-43B9-AB31-9352F9F6029C)



### Character Functions Returning Number Values 

Character functions that return number values can take as their argument any character data type. The character functions that return number values are:

  * [ASCII](ASCII.html#GUID-871D4171-FF70-475E-BC82-9B8F46239A5D)* [INSTR](INSTR.html#GUID-47E3A7C4-ED72-458D-A1FA-25A9AD3BE113)
  * [LENGTH](LENGTH.html#GUID-8F97F652-5AE8-4457-AFD7-7A6F25551E0C)* [REGEXP_COUNT](REGEXP_COUNT.html#GUID-5148AF2E-9CED-497D-A78D-3A7847A45276)
  * [REGEXP_INSTR](REGEXP_INSTR.html#GUID-D21B53A1-83E2-4722-9BBB-638470715DD6)



### Character Set Functions 

The character set functions return information about the character set. The character set functions are:

  * [NLS_CHARSET_DECL_LEN](NLS_CHARSET_DECL_LEN.html#GUID-5F0939C0-4AFB-4CEA-9899-BDE85B9B2F11)* [NLS_CHARSET_ID](NLS_CHARSET_ID.html#GUID-733B03A0-CD66-4645-A323-401A176499E3)
  * [NLS_CHARSET_NAME](NLS_CHARSET_NAME.html#GUID-5DCFB255-92AD-4E94-9344-73B7918C106C)



### Collation Functions 

The collation functions return information about collation settings. The collation functions are:

  * [COLLATION](COLLATION.html#GUID-70A694BA-C1A0-4F5A-9492-58A5943D9BDD)* [NLS_COLLATION_ID](NLS_COLLATION_ID.html#GUID-69EA3869-28E3-4CF8-9678-CD4F9878EE99)
  * [NLS_COLLATION_NAME](NLS_COLLATION_NAME.html#GUID-24848987-2A02-4B09-A690-D3C87308FB3A)



### Datetime Functions 

Datetime functions operate on date (`DATE`), timestamp (`TIMESTAMP`, `TIMESTAMP` `WITH` `TIME` `ZONE`, and `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`), and interval (`INTERVAL` `DAY` `TO` `SECOND`, `INTERVAL` `YEAR` `TO` `MONTH`) values. 

Some of the datetime functions were designed for the Oracle `DATE` data type (`ADD_MONTHS`, `CURRENT_DATE`, `LAST_DAY`, `NEW_TIME`, and `NEXT_DAY`). If you provide a timestamp value as their argument, then Oracle Database internally converts the input type to a `DATE` value and returns a `DATE` value. The exceptions are the `MONTHS_BETWEEN` function, which returns a number, and the `ROUND` and `TRUNC` functions, which do not accept timestamp or interval values at all. 

The remaining datetime functions were designed to accept any of the three types of data (date, timestamp, and interval) and to return a value of one of these types.

All of the datetime functions that return current system datetime information, such as `SYSDATE`, `SYSTIMESTAMP`, `CURRENT_TIMESTAMP`, and so forth, are evaluated once for each SQL statement, regardless how many times they are referenced in that statement. 

The datetime functions are:

  * [ADD_MONTHS](ADD_MONTHS.html#GUID-B8C74443-DF32-4B7C-857F-28D557381543)* [CEIL (datetime)](ceil-datetime.html#GUID-666629BE-AA15-4EA6-86A0-DF321AEFF3C0)
  * [CURRENT_DATE](CURRENT_DATE.html#GUID-96795097-D6F0-4288-90E7-9D7C49B4F6E5)* [CURRENT_TIMESTAMP](CURRENT_TIMESTAMP.html#GUID-CBD42B84-869D-45C7-9FFC-001DD7712097)
  * [DBTIMEZONE](DBTIMEZONE.html#GUID-F2368F72-7065-462F-80B9-E115F5A48025)* [EXTRACT (datetime)](EXTRACT-datetime.html#GUID-36E52BF8-945D-437D-9A3C-6860CABD210E)
  * [FLOOR (datetime)](floor-datetime.html#GUID-3EB4F1BA-9D18-437C-96BA-D3B0282DDE97)* [FROM_TZ](FROM_TZ.html#GUID-84384FF7-6462-480C-BC40-60087016857B)
  * [LAST_DAY](LAST_DAY.html#GUID-296C7C02-7FB9-4AAC-8927-6A79320CE0C6)* [LOCALTIMESTAMP](LOCALTIMESTAMP.html#GUID-3C3D1F29-5F53-41F2-B2D6-A3767DFB22CA)
  * [MONTHS_BETWEEN](MONTHS_BETWEEN.html#GUID-E4A1AEC0-F5A0-4703-9CC8-4087EB889952)* [NEW_TIME](NEW_TIME.html#GUID-1D1CC7DE-CA2A-4BEC-B404-89FD19EE36AC)
  * [NEXT_DAY](NEXT_DAY.html#GUID-01B2CC7A-1A64-4A74-918E-26158C9096F6)* [NUMTODSINTERVAL](NUMTODSINTERVAL.html#GUID-5A7392A8-7976-4465-8839-A65EFF1A80B6)
  * [NUMTOYMINTERVAL](NUMTOYMINTERVAL.html#GUID-B98B21AA-44F7-4A9D-A646-6775A1D5F46D)* [ORA_DST_AFFECTED](ORA_DST_AFFECTED.html#GUID-EE288E4B-DE55-4104-813C-11E28F7B474A)
  * [ORA_DST_CONVERT](ORA_DST_CONVERT.html#GUID-3A991FB0-0E98-48F5-902F-55C6FCA8DA13)* [ORA_DST_ERROR](ORA_DST_ERROR.html#GUID-02FAF3EC-D90A-42FB-A212-513314AD774A)
  * [ROUND (datetime)](ROUND-date.html#GUID-C6D342D0-6068-4986-A759-70EF4599EC41)* [SESSIONTIMEZONE](SESSIONTIMEZONE.html#GUID-2A243878-C1C5-4B7C-81DE-D8B024796EAB)
  * [SYS_EXTRACT_UTC](SYS_EXTRACT_UTC.html#GUID-C540A8C8-72B1-46AF-A9AA-18D011763AD8)* [SYSDATE](SYSDATE.html#GUID-807F8FC5-D72D-4F4D-B66D-B0FE1A8FA7D2)
  * [SYSTIMESTAMP](SYSTIMESTAMP.html#GUID-FCED18CE-A875-4D5D-9178-3DE4FA956516)* [TO_CHAR (datetime)](TO_CHAR-datetime.html#GUID-0C3EEFD1-AE3D-452D-BF23-2FC95664E78F)
  * [TO_DSINTERVAL](TO_DSINTERVAL.html#GUID-DEBB41BD-9438-4558-A53E-428CE93C05D3)* [TO_TIMESTAMP](TO_TIMESTAMP.html#GUID-57E09334-E3CC-4CA2-809E-F0909458BCFA)
  * [TO_TIMESTAMP_TZ](TO_TIMESTAMP_TZ.html#GUID-3999303B-89CA-4AA3-9817-458F36ADC9DC)* [TO_YMINTERVAL](TO_YMINTERVAL.html#GUID-5DEBA096-7AC3-4B18-A4BE-D36FC9BDB450)
  * [TRUNC (datetime)](TRUNC-date.html#GUID-BC82227A-2698-4EC8-8C1A-ABECC64B0E79)* [TZ_OFFSET](TZ_OFFSET.html#GUID-D2007072-34C2-4971-BD2B-64D93A3D7A31)



### General Comparison Functions 

The general comparison functions determine the greatest and or least value from a set of values. The general comparison functions are:

  * [GREATEST](GREATEST.html#GUID-06B88B22-8466-44B6-93C7-50B222122ECE)* [LEAST](LEAST.html#GUID-0198D71B-051A-41D9-8E9C-599E24692556)



### Conversion Functions 

Conversion functions convert a value from one data type to another. Generally, the form of the function names follows the convention `datatype` `TO` `datatype`. The first data type is the input data type. The second data type is the output data type. The SQL conversion functions are: 

  * [ASCIISTR](ASCIISTR.html#GUID-B6128485-4E86-4851-860F-AC03981E2388)* [BIN_TO_NUM](BIN_TO_NUM.html#GUID-BF061402-D7F0-4557-B7D4-1CEE6E80F3B2)
  * [CAST](CAST.html#GUID-5A70235E-1209-4281-8521-B94497AAEF75)* [CHARTOROWID](CHARTOROWID.html#GUID-F9C63933-F680-465D-AB22-6B8B882B5CF7)
  * [COMPOSE](COMPOSE.html#GUID-A16E7D53-E7F8-46A6-B3F8-BA322D129019)* [CONVERT](CONVERT.html#GUID-C8BA0657-61C8-4964-A4CB-9292390853F6)
  * [DECOMPOSE](DECOMPOSE.html#GUID-3E772756-F12C-4827-99A5-F7CF4F11A25A)* [HEXTORAW](HEXTORAW.html#GUID-8571556F-C219-4814-A854-9F01581FFBDF)
  * [NUMTODSINTERVAL](NUMTODSINTERVAL.html#GUID-5A7392A8-7976-4465-8839-A65EFF1A80B6)* [NUMTOYMINTERVAL](NUMTOYMINTERVAL.html#GUID-B98B21AA-44F7-4A9D-A646-6775A1D5F46D)
  * [RAWTOHEX](RAWTOHEX.html#GUID-F86E3B5B-7FEE-47FD-A0C2-2FC55DC21C9E)* [RAWTONHEX](RAWTONHEX.html#GUID-5657B113-24CE-4DC6-BD11-63135B7DB009)
  * [ROWIDTOCHAR](ROWIDTOCHAR.html#GUID-67998E5B-376A-45B5-B20B-1A87E5D370C1)* [ROWIDTONCHAR](ROWIDTONCHAR.html#GUID-3178A4DA-2534-4A93-A819-7C14208AE9B5)
  * [SCN_TO_TIMESTAMP](SCN_TO_TIMESTAMP.html#GUID-BCB0C8EE-0E03-4A61-A41A-69975FAC1803)* [TIMESTAMP_TO_SCN](TIMESTAMP_TO_SCN.html#GUID-58796E1A-9943-4966-96E6-78B636BD2859)
  * [TO_BINARY_DOUBLE](TO_BINARY_DOUBLE.html#GUID-0BA2E065-8006-426C-A3CB-1F6B0C8F283C)* [TO_BINARY_FLOAT](TO_BINARY_FLOAT.html#GUID-66A51BE2-BE4A-4B99-9C37-73B110452D27)
  * [TO_BLOB (bfile)](TO_BLOB-bfile.html#GUID-232A1599-53C9-464B-904F-4DBA336B4EBC)* [TO_BLOB (raw)](TO_BLOB-raw.html#GUID-C4308DB1-5BFE-48F0-99E5-9E03B80B4585)
  * [TO_CHAR (bfile|blob)](TO_CHAR-bfile-blob.html#GUID-F12F3C5A-8E3C-4FE1-BD7D-4AC0B79EA5A5)* [TO_CHAR (character)](TO_CHAR-character.html#GUID-EC078E16-11FE-4ABE-AE05-DA9AC1B4BEBC)
  * [TO_CHAR (datetime)](TO_CHAR-datetime.html#GUID-0C3EEFD1-AE3D-452D-BF23-2FC95664E78F)* [TO_CHAR (number)](TO_CHAR-number.html#GUID-00DA076D-2468-41AB-A3AC-CC78DBA0D9CB)
  * [TO_CLOB (bfile|blob)](TO_CLOB-bfile-blob.html#GUID-FD7D58FE-B97C-4B75-85A9-5F82FB1DE96A)* [TO_CLOB (character)](TO_CLOB-character.html#GUID-82E2FAD3-B0C8-4A06-A882-26211EE0524C)
  * [TO_DATE](TO_DATE.html#GUID-D226FA7C-F7AD-41A0-BB1D-BD8EF9440118)* [TO_DSINTERVAL](TO_DSINTERVAL.html#GUID-DEBB41BD-9438-4558-A53E-428CE93C05D3)
  * [TO_LOB](TO_LOB.html#GUID-35810313-029E-4CB8-8C27-DF432FA3C253)* [TO_MULTI_BYTE](TO_MULTI_BYTE.html#GUID-58A9F91A-5B1E-4C14-8F48-046F176E2F4A)
  * [TO_NCHAR (character)](TO_NCHAR-character.html#GUID-539E9F5C-CB47-4BCE-B468-C34CF6BABDC5)* [TO_NCHAR (datetime)](TO_NCHAR-datetime.html#GUID-C40DBBC2-B9F2-49D8-8775-DDA99FF41EAC)
  * [TO_NCHAR (number)](TO_NCHAR-number.html#GUID-B0FA1B2F-3285-46C4-96DA-3C7AED48987C)* [TO_NCLOB](TO_NCLOB.html#GUID-56CEB237-8515-4030-A5D5-016CBC5FA6BB)
  * [TO_NUMBER](TO_NUMBER.html#GUID-D4807212-AFD7-48A7-9AED-BEC3E8809866)* [TO_SINGLE_BYTE](TO_SINGLE_BYTE.html#GUID-36364630-C62C-46C5-B29B-EFE3DFB5AA6D)
  * [TO_TIMESTAMP](TO_TIMESTAMP.html#GUID-57E09334-E3CC-4CA2-809E-F0909458BCFA)* [TO_TIMESTAMP_TZ](TO_TIMESTAMP_TZ.html#GUID-3999303B-89CA-4AA3-9817-458F36ADC9DC)
  * [TO_YMINTERVAL](TO_YMINTERVAL.html#GUID-5DEBA096-7AC3-4B18-A4BE-D36FC9BDB450)* [TREAT](TREAT.html#GUID-037C0CD3-C256-4A02-80E0-C6F15147C5BF)
  * [UNISTR](UNISTR.html#GUID-AAF757DB-6E5D-4548-9E36-6B36BB0BD83E)* [VALIDATE_CONVERSION](VALIDATE_CONVERSION.html#GUID-DC485EEB-CB6D-42EF-97AA-4487884CB2CD)



### Large Object Functions 

The large object functions operate on LOBs. The large object functions are:

  * [BFILENAME](BFILENAME.html#GUID-1F767077-7C26-4962-9833-1433F1749621)* [EMPTY_BLOB, EMPTY_CLOB](EMPTY_BLOB-EMPTY_CLOB.html#GUID-551B5A7C-A03B-4B2E-80EF-DAA8574CF160)



### Collection Functions 

The collection functions operate on nested tables and varrays. The SQL collection functions are:

  * [CARDINALITY](CARDINALITY.html#GUID-11F978F8-1DD9-4D82-9FCF-2FC633D1C100)* [COLLECT](COLLECT.html#GUID-A0A74602-2A97-449B-A3EC-847D38D3DA90)
  * [POWERMULTISET](POWERMULTISET.html#GUID-34F3B1D1-4089-4A5B-AA2C-9C69A5C36E6D)* [POWERMULTISET_BY_CARDINALITY](POWERMULTISET_BY_CARDINALITY.html#GUID-57423B5C-CD16-4B3C-A796-AAA0910EF261)
  * [SET](SET.html#GUID-533164AC-B4F0-4FCE-ADA4-85C925CB8D14)



### Hierarchical Functions 

Hierarchical functions applies hierarchical path information to a result set. The hierarchical function is:

  * [SYS_CONNECT_BY_PATH](SYS_CONNECT_BY_PATH.html#GUID-D25A0F86-B559-4090-9164-7A2C84D1E11E)



### Oracle Machine Learning for SQL Functions 

The Oracle Machine Learning for SQL functions use analytics to score data. The functions can apply a mining model schema object to the data, or they can dynamically mine the data by executing an analytic clause. The OML4SQL functions can be applied to models built using the native algorithms of Oracle, as well as those built using R through the extensibility mechanism.

The Oracle Machine Learning for SQL functions are:

  * [CLUSTER_DETAILS](CLUSTER_DETAILS.html#GUID-6E47A5A7-B73A-4D79-BAA5-BB7E3C173D0F)* [CLUSTER_DISTANCE](CLUSTER_DISTANCE.html#GUID-21E611E3-2F15-4DF1-B648-9A36E8D5CE4D)
  * [CLUSTER_ID](CLUSTER_ID.html#GUID-1B0D0954-5A57-409C-9E84-F3EE12712040)* [CLUSTER_PROBABILITY](CLUSTER_PROBABILITY.html#GUID-999A15BA-FEDD-4FA6-8F1B-C847C2FE51CD)
  * [CLUSTER_SET](CLUSTER_SET.html#GUID-7B44CB7A-4783-4FE0-80D8-26AE88D6B060)* [FEATURE_COMPARE](FEATURE_COMPARE.html#GUID-3D4E179F-F5D2-4FCF-AB42-4D0C8CC7D514)
  * [FEATURE_DETAILS](FEATURE_DETAILS.html#GUID-A42F313B-22C1-4CAC-BA3F-C418178D743F)* [FEATURE_ID](FEATURE_ID.html#GUID-BA187F80-5F51-49F6-BB69-64422FB9FD90)
  * [FEATURE_SET](FEATURE_SET.html#GUID-55582346-F1D6-447E-851A-D4912982EB28)* [FEATURE_VALUE](FEATURE_VALUE.html#GUID-EC0E44D0-BE01-49F8-9E5A-72B500119877)
  * [ORA_DM_PARTITION_NAME](ORA_DM_PARTITION_NAME.html#GUID-F9ADE9AD-C306-42D1-8274-3F73C2FBAC19)* [PREDICTION](PREDICTION.html#GUID-DA66A1C3-BFB2-43A1-A3FF-93D4A3DAB9C6)
  * [PREDICTION_BOUNDS](PREDICTION_BOUNDS.html#GUID-C9478C25-8D31-4A39-99B8-AB66A6614795)* [PREDICTION_COST](PREDICTION_COST.html#GUID-2E58222D-FB7E-4CA2-BCAA-C932FCDEE890)
  * [PREDICTION_DETAILS](PREDICTION_DETAILS.html#GUID-D7261A56-E729-4882-B48D-CDD343C53810)* [PREDICTION_PROBABILITY](PREDICTION_PROBABILITY.html#GUID-0F309771-40A3-4E23-9A96-CD134C80F584)
  * [PREDICTION_SET](PREDICTION_SET.html#GUID-25AE84A7-C733-4BC5-8C57-2E5574C49AFC)* [VECTOR_EMBEDDING](vector_embedding.html#GUID-5ED78260-6D21-4B6B-86E0-A1E70EFA11CA "Use VECTOR_EMBEDDING to generate a single vector embedding for different data types using embedding or feature extraction machine learning models.")



See Also:

  * [Oracle Machine Learning for SQL Concepts](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMCON) to learn about Oracle Machine Learning for SQL 

  * [Oracle Machine Learning for SQL Userâs Guide](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DMPRG004) for information about scoring 




### XML Functions 

The XML functions operate on or return XML documents or fragments. These functions use arguments that are not defined as part of the ANSI/ISO/IEC SQL Standard but are defined as part of the World Wide Web Consortium (W3C) standards. The processing and operations that the functions perform are defined by the relevant W3C standards. The table below provides a link to the appropriate section of the W3C standard for the rules and guidelines that apply to each of these XML-related arguments. A SQL statement that uses one of these XML functions, where any of the arguments does not conform to the relevant W3C syntax, will result in an error. Of special note is the fact that not every character that is allowed in the value of a database column is considered legal in XML.

Syntax Element | W3C Standard URL  
---|---  
value_expr | http://www.w3.org/TR/2006/REC-xml-20060816  
Xpath_string | http://www.w3.org/TR/1999/REC-xpath-19991116  
XQuery_string | http://www.w3.org/TR/2007/REC-xquery-semantics-20070123/ http://www.w3.org/TR/xquery-update-10/  
namespace_string | http://www.w3.org/TR/2006/REC-xml-names-20060816/  
identifier | http://www.w3.org/TR/2006/REC-xml-20060816/#NT-Nmtoken  
  
For more information about selecting and querying XML data using these functions, including information on formatting output, refer to [Oracle XML DB Developerâs Guide](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDB0400)

The SQL XML functions are:

  * [DEPTH](DEPTH.html#GUID-C0107BE4-0003-4329-9CCE-D0671B3F3538)* [EXISTSNODE](EXISTSNODE.html#GUID-71731B1A-99E5-4B82-8243-DEEE6704796F)
  * [EXTRACT (XML)](EXTRACT-XML.html#GUID-593295AA-4F46-4D75-B8DC-E7BCEDB1D4D7)* [EXTRACTVALUE](EXTRACTVALUE.html#GUID-20AB974B-7544-4F44-B539-787FB6145680)
  * [PATH](PATH.html#GUID-91937F98-7718-4F39-9225-1E0229F11F0D)* [SYS_DBURIGEN](SYS_DBURIGEN.html#GUID-ABA33BEB-F7B7-477B-9FF2-028D62768797)
  * [SYS_XMLAGG](SYS_XMLAGG.html#GUID-BEDD241D-360A-46A2-AEBF-C8B70E465D75)* [SYS_XMLGEN](SYS_XMLGEN.html#GUID-1AC25984-F4AB-468E-BF53-561275AD44E8)
  * [XMLAGG](XMLAGG.html#GUID-BCD1D755-5E26-4F73-BA22-521C30D275DA)* [XMLCAST](XMLCAST.html#GUID-06563B93-1247-4F0C-B6BE-42DB3B1DB069)
  * [XMLCDATA](XMLCDATA.html#GUID-FB517A52-6F1A-4D8D-B632-F91EFA606691)* [XMLCOLATTVAL](XMLCOLATTVAL.html#GUID-AE3B6441-74D8-4033-900B-A578A79E5F0A)
  * [XMLCOMMENT](XMLCOMMENT.html#GUID-AECB7BCC-C60F-4E0C-BD9A-E52D8F1599C4)* [XMLCONCAT](XMLCONCAT.html#GUID-CEEEF777-4C7D-41E4-9F69-69DE6D1B07C2)
  * [XMLDIFF](XMLDIFF.html#GUID-B7746C15-27FD-4CAF-87EA-49C0DFA1E935)* [XMLELEMENT](XMLELEMENT.html#GUID-DEA75423-00EA-4034-A246-4A774ADC988E)
  * [XMLEXISTS](XMLEXISTS.html#GUID-3D0D90DB-3D4F-4685-AFF6-72B6250624B9)* [XMLFOREST](XMLFOREST.html#GUID-68E5C67E-CE97-4BF8-B7FF-2365E062C363)
  * [XMLISVALID](XMLISVALID.html#GUID-012BB50C-30E4-46BA-8199-A8480453F79E)* [XMLPARSE](XMLPARSE.html#GUID-39A93E58-F06E-4633-A7BF-6CF27A53D9B6)
  * [XMLPATCH](XMLPATCH.html#GUID-C52DA494-2840-475B-871F-1EA071299894)* [XMLPI](XMLPI.html#GUID-142604E3-7999-4803-9DF5-28BDC0701571)
  * [XMLQUERY](XMLQUERY.html#GUID-9E8D3220-2CF5-4C63-BDC2-0526D57B9CDB)* [XMLSEQUENCE](XMLSEQUENCE.html#GUID-BE0837A9-7D85-4621-8C22-1FECAD17E569)
  * [XMLSERIALIZE](XMLSERIALIZE.html#GUID-F2D5ECE7-3838-4DD5-BE8F-2AEE7890AA1C)* [XMLTABLE](XMLTABLE.html#GUID-C4A32C58-33E5-4CF1-A1FE-039550D3ECFA)
  * [XMLTRANSFORM](XMLTRANSFORM.html#GUID-3B74EED2-E79F-4333-8C0B-02989DF5EEAA)



### JSON Functions

JavaScript Object Notation (JSON) functions allow you to query and generate JSON data.

The following SQL/JSON functions allow you to query JSON data:

  * [JSON_QUERY](JSON_QUERY.html#GUID-6D396EC4-D2AA-43D2-8F5D-08D646A4A2D9)* [JSON_TABLE](JSON_TABLE.html#GUID-3C8E63B5-0B94-4E86-A2D3-3D4831B67C62)
  * [JSON_VALUE](JSON_VALUE.html#GUID-C7F19D36-1E75-4CB2-AE67-ADFBAD23CBC2)



The following SQL/JSON functions allow you to generate JSON data:

  * [JSON_ARRAY](JSON_ARRAY.html#GUID-46CDB3AF-5795-455B-85A8-764528CEC43B)* [JSON_ARRAYAGG](JSON_ARRAYAGG.html#GUID-6D56077D-78DE-4CC0-9498-225DDC42E054)
  * [JSON_OBJECT](JSON_OBJECT.html#GUID-1EF347AE-7FDA-4B41-AFE0-DD5A49E8B370)* [JSON_OBJECTAGG](JSON_OBJECTAGG.html#GUID-09422D4A-936C-4D38-9991-C64101283D98)
  * [JSON Type Constructor](json-type-constructor.html#GUID-2B598841-A327-4610-91B9-602F480A8314)* [JSON_SCALAR](json_scalar.html#GUID-F05BD523-F827-4A5F-9A82-8CBC2DB04E2E)
  * [JSON_SERIALIZE](JSON_SERIALIZE.html#GUID-01B769C6-A7B3-4136-977F-63CA05963D21)* [JSON_TRANSFORM](JSON_TRANSFORM.html#GUID-DD2A821B-C688-4310-81B5-5F45090B9366)



The following Oracle SQL function creates a JSON data guide:

  * [JSON_DATAGUIDE](JSON_DATAGUIDE.html#GUID-4CF32887-0F46-4925-8381-AE2B74343933)



### Encoding and Decoding Functions 

The encoding and decoding functions let you inspect and decode data in the database. The encoding and decoding functions are:

  * [DECODE](DECODE.html#GUID-39341D91-3442-4730-BD34-D3CF5D4701CE)* [DUMP](DUMP.html#GUID-A05793C9-B35D-4BA7-B68C-E3693BCF47A5)
  * [ORA_HASH](ORA_HASH.html#GUID-0349AFF5-0268-43CE-8118-4F96D752FDE6)* [STANDARD_HASH](STANDARD_HASH.html#GUID-4A68DACE-CFCF-443B-8651-B6CEAA7C4FD7)
  * [VSIZE](VSIZE.html#GUID-CDDB2A17-9398-4AF8-96FB-4297DDA2665B)



### NULL-Related Functions 

The `NULL`-related functions facilitate null handling. The `NULL`-related functions are: 

  * [COALESCE](COALESCE.html#GUID-3F9007A7-C0CA-4707-9CBA-1DBF2CDE0C87)* [LNNVL](LNNVL.html#GUID-FBCCE9B1-614E-45FA-8EE1-DFAA4F936867)
  * [NANVL](NANVL.html#GUID-3C094646-2A70-41F5-984C-9BC0FB31494A)* [NULLIF](NULLIF.html#GUID-445FC268-7FFA-4850-98C9-D53D88AB2405)
  * [NVL](NVL.html#GUID-3AB61E54-9201-4D6A-B48A-79F4C4A034B2)* [NVL2](NVL2.html#GUID-414D6E81-9627-4163-8AC2-BD24E57742AE)



### Environment and Identifier Functions 

The environment and identifier functions provide information about the instance and session. The environment and identifier functions are:

  * [CON_DBID_TO_ID](CON_DBID_TO_ID.html#GUID-9F38A14F-8E6A-4A4A-96D5-52E4480A8926)* [CON_GUID_TO_ID](CON_GUID_TO_ID.html#GUID-F93F257F-BB58-427D-9E19-A22E43DB288F)
  * [CON_NAME_TO_ID](CON_NAME_TO_ID.html#GUID-714E0914-5018-4E32-AB1E-134FDD0B28FE)* [CON_UID_TO_ID](CON_UID_TO_ID.html#GUID-14BE69F3-8519-4676-90CD-374152981901)
  * [ORA_INVOKING_USER](ORA_INVOKING_USER.html#GUID-FAE7B186-C40D-48BB-A2C9-AB7EE3878BF1)* [ORA_INVOKING_USERID](ORA_INVOKING_USERID.html#GUID-91F09A40-96CD-4759-8EDF-4C54219E8E83)
  * [SYS_CONTEXT](SYS_CONTEXT.html#GUID-B9934A5D-D97B-4E51-B01B-80C76A5BD086)* [SYS_GUID](SYS_GUID.html#GUID-761E36B4-32DA-497D-8829-3D4653381F9B)
  * [SYS_TYPEID](SYS_TYPEID.html#GUID-4E3D45A1-7433-495D-9062-88505A1496E0)* [UID](UID.html#GUID-DFDC8E24-B911-4C42-B4B1-853E964D3644)
  * [USER](USER.html#GUID-AD0B927B-EFD4-4246-89B4-2D55AB3AF531)* [USERENV](USERENV.html#GUID-AC3C8AEF-A988-41C4-9242-69B54E5941D2)



### Domain Functions

Purpose

Use the following domain functions to work with SQL domains more efficiently: 

  * [DOMAIN_DISPLAY](domain_display.html#GUID-BF1D853F-5BA8-4E9E-B8EB-BF7502F11D20)* [DOMAIN_ORDER](domain_order.html#GUID-FC34F669-0BCA-4F8A-B911-4ACAA1F8F11D)

  * [DOMAIN_NAME](domain_name.html#GUID-BFF71A4E-8FF2-407A-8661-C0A24D4E5487)* [DOMAIN_CHECK](domain_check.html#GUID-599390A5-1B96-4465-82CE-DBC2345A018B)

  * [DOMAIN_CHECK_TYPE](domain_check_type.html#GUID-9ED35142-A66C-4511-9DE1-B8BB4350DE41)




### Vector Functions

Purpose

You can use the following vector functions in Oracle AI Vector Search to create and manipulate vectors:

Vector Distance Functions

  * [VECTOR_DISTANCE](vector_distance.html#GUID-BA4BCFB2-D905-43DC-87B0-E53522CF07B7 "VECTOR_DISTANCE is the main function that you can use to calculate the distance between two vectors.")

  * [L1_DISTANCE](vector_distance.html#GUID-604A5B68-10AF-48F3-A84F-ED0B90624059 "L1_DISTANCE is a shorthand version of the VECTOR_DISTANCE function that calculates the distance between two vectors. It takes two vectors as input and returns the distance between them as a BINARY_DOUBLE.")

  * [L2_DISTANCE](vector_distance.html#GUID-2FD8BC27-7614-471F-A4F5-3ED52130A05A "L2_DISTANCE is a shorthand version of the VECTOR_DISTANCE function that calculates the distance between two vectors. It takes two vectors as input and returns the distance between them as a BINARY_DOUBLE.")

  * [COSINE_DISTANCE](vector_distance.html#GUID-2128DC1D-612A-444F-87D8-3D249CD8F12D "COSINE_DISTANCE is a shorthand version of the VECTOR_DISTANCE function that calculates the distance between two vectors. It takes two vectors as input and returns the distance between them as a BINARY_DOUBLE.")

  * [INNER_PRODUCT](vector_distance.html#GUID-6AE745CF-93E7-4192-8F80-7B9853DF5B72 "INNER_PRODUCT calculates the inner product of two vectors. It takes two vectors as input and returns the inner product as a BINARY_DOUBLE. INNER_PRODUCT\(<expr1>, <expr2>\) is equivalent to -1 * VECTOR_DISTANCE\(<expr1>, <expr2>, DOT\).")




Vector Constructors

  * [TO_VECTOR](to_vector.html#GUID-2CCAB607-A28B-43F7-A71D-9800C0B9A380 "TO_VECTOR is a constructor that takes a string of type VARCHAR2, CLOB, BLOB, or JSON as input, converts it to a vector, and returns a vector as output. TO_VECTOR also takes another vector as input, adjusts its format, and returns the adjusted vector as output. TO_VECTOR is synonymous with VECTOR.")

  * [VECTOR](vector.html#GUID-8A63005B-5512-4D20-954C-7A9DA877FE4B "VECTOR is synonymous with TO_VECTOR.")




Vector Serializers

  * [FROM_VECTOR](from_vector.html#GUID-AA60B3CB-FCB7-4944-9E06-976C272855B1 "FROM_VECTOR takes a vector as input and returns a string of type VARCHAR2 or CLOB as output.")

  * [VECTOR_SERIALIZE](vector_serialize.html#GUID-9E3FFB34-F924-4C02-B35D-30B9FA1DA1A3 "VECTOR_SERIALIZE is synonymous with FROM_VECTOR.")




Other Common Vector Functions

  * [VECTOR_CHUNKS](vector_chunks.html#GUID-5927E2FA-6419-4744-A7CB-3E62DBB027AD "Use VECTOR_CHUNKS to split plain text into smaller chunks to generate vector embeddings that can be used with vector indexes or hybrid vector indexes.")

  * [VECTOR_DIMS](vector_dims.html#GUID-010349D7-190D-430B-A798-ACC486E1036A "VECTOR_DIMS returns the number of dimensions of a vector as a NUMBER. VECTOR_DIMS is synonymous with VECTOR_DIMENSION_COUNT.")

  * [VECTOR_DIMENSION_COUNT](vector_dimension_count.html#GUID-C3D937E0-7F9F-4C21-A214-0CFA31472E67 "VECTOR_DIMENSION_COUNT returns the number of dimensions of a vector as a NUMBER.")

  * [VECTOR_DIMENSION_FORMAT](vector_dimension_format.html#GUID-354ACE80-7120-4D45-B2B0-AB1D86E3D37D "VECTOR_DIMENSION_FORMAT returns the storage format of the vector. It returns a VARCHAR2, which can be one of the following values: INT8, FLOAT32, FLOAT64, or BINARY.")

  * [VECTOR_EMBEDDING](vector_embedding.html#GUID-5ED78260-6D21-4B6B-86E0-A1E70EFA11CA "Use VECTOR_EMBEDDING to generate a single vector embedding for different data types using embedding or feature extraction machine learning models.")

  * [VECTOR_NORM](vector_norm.html#GUID-41554068-9EB8-49E8-A771-4E666674DDA8 "VECTOR_NORM returns the Euclidean norm of a vector \(SQRT\(SUM\(\(xi-yi\)2\)\)\) as a BINARY_DOUBLE. This value is also called magnitude or size and represents the Euclidean distance between the vector and the origin.")




See Also:

[AI Vector Search User's Guide](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-746EAA47-9ADA-4A77-82BB-64E8EF5309BE)

[← Previous](OLAP-Functions.md)

[Next →](Single-Row-Functions.md)
