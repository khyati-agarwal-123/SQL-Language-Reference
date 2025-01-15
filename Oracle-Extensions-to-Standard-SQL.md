##  Oracle Extensions to Standard SQL {#GUID-7D3A5F6C-79D4-4B71-AEC3-7AB847DF0989} 

Oracle supports numerous features that extend beyond standard SQL. If you are concerned with the portability of your applications to other implementations of SQL, then use Oracle's FIPS Flagger to help identify the use of Oracle extensions to Entry SQL-92 in your embedded SQL programs. The FIPS Flagger is part of the Oracle precompilers and the SQL*Module compiler. The FIPS Flagger can also be enabled in SQL*Plus by using ` ALTER ` ` SESSION ` ` SET ` ` FLAGGER ` ` = ` ` ENTRY ` . While SQL-92 has been superseded by SQL:2016, there has been no conformance testing authority for any version of SQL since SQL-92; hence, Entry SQL-92 offers you the most assurance of portability. 

> **note:** See Also: 

[ *Pro*COBOL Programmer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPCB1075) and [ *Pro*C/C++ Programmer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=LNPCC3722) for information on how to use the FIPS Flagger 
