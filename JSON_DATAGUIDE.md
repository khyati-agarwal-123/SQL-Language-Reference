[Previous](JSON_ARRAYAGG.md) [Next](JSON_MERGEPATCH.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. JSON_DATAGUIDE

## JSON_DATAGUIDE

Syntax

![Description of json_dataguide.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/json_dataguide.gif)  
[Description of the illustration
json_dataguide.eps](img_text/json_dataguide.md)

Purpose

The aggregate function `JSON_DATAGUIDE` computes the data guide of a set of
JSON data. The data guide is returned as a `CLOB` which can be in either flat
or hierarchical format depending on the passing format parameter.

expr

`expr` is a SQL expression that evaluates to a JSON object or a JSON array. It
can also be a JSON column in a table.

format options

Use the format options to specify the format of the data guide that will be
returned. It must be one of the following values:

  * `dbms_json.format_flat` for a flat format. 

  * `dbms_json.format_hierarchical` for a hierarchical format. 

If the parameter is the absent, the default is `dbms_json.format_flat`.

flag options

`flag` can have the following values:

  * Specify `DBMS_JSON.PRETTY` to improve readability of the returned data guide with appropriate indentation. 

  * Specify `DBMS_JSON.GEOJSON` for the data guide to auto detect the `GeoJSON` type. The corresponding view column created by the data guide will be of `sdo_geometry` type. 

  * Specify `DBMS_JSON.GATHER_STATS` for the data guide to collect statistical information. The data guide report generated with `DBMS_JSON.GATHER_STATS` has a new field `o:sample_size`, in addition to all of the other statistical fields that you get with `DBMS_JSON.get_index_dataguide` . 

  * Specify `DBMS_JSON.DETECT_DATETIME` for the data guide to detect temporal types. The data guide reports a JSON field value that conforms to the ISO 8601 format as a timestamp type, not a string type. 

  * All values `DBMS_JSON.PRETTY`, `DBMS_JSON.GEOJSON`, and `DBMS_JSON.GATHER_STATS`, and `DBMS_JSON.DETECT_DATETIME` can be combined with a plus sign. For example, `DBMS_JSON.GEOJSON+DBMS_JSON.PRETTY`, or `DBMS_JSON.GEOJSON+DBMS_JSON.PRETTY+DBMS_JSON.GATHER_STATS`. 

See Also:

[JSON Data Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADJSN-GUID-219FC30E-89A7-4189-BC36-7B961A24067C)

Examples

The following example uses the `j_purchaseorder` table, which is created in
"[Creating a Table That Contains a JSON Document:
Example](JSON_TABLE.md#GUID-3C8E63B5-0B94-4E86-A2D3-3D4831B67C62__CJAHAAJE)".
This table contains a column of JSON data called `po_document`. This example
returns a flat data guide for each year group.

    
    
    SELECT EXTRACT(YEAR FROM date_loaded) YEAR,
           JSON_DATAGUIDE(po_document) "DATA GUIDE"
      FROM j_purchaseorder
      GROUP BY extract(YEAR FROM date_loaded)
      ORDER BY extract(YEAR FROM date_loaded) DESC;
    
    
    YEAR DATA GUIDE
    ---- ------------------------------------------
    2016 [
           {
             "o:path" : "$.PO_ID",
             "type" : "number",
             "o:length" : 4
           },
           {
             "o:path" : "$.PO_Ref",
             "type" : "string",
             "o:length" : 16
           },
           {
             "o:path" : "$.PO_Items",
             "type" : "array",
             "o:length" : 64
           },
           {
             "o:path" : "$.PO_Items.Part_No",
             "type" : "number",
             "o:length" : 16
           },
           {
             "o:path" : "$.PO_Items.Item_Quantity",
             "type" : "number",
             "o:length" : 2
           }
         ]
    . . .


[← Previous](JSON_ARRAYAGG.md)

[Next →](JSON_MERGEPATCH.md)
