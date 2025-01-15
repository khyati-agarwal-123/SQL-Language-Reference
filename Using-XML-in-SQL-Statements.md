##  Using XML in SQL Statements {#GUID-5FE21EC9-1F66-45F1-9FD8-ECA5336EDC14} 

This section describes some of the ways you can use ` XMLType ` data in the database. 

XMLType Tables 

The sample schema ` oe ` contains a table ` warehouses ` , which contains an ` XMLType ` column ` warehouse_spec ` . Suppose you want to create a separate table with the ` warehouse_spec ` information. The following example creates a very simple ` XMLType ` table with one ` CLOB ` column: 
    
    
    ```
    CREATE TABLE xwarehouses OF XMLTYPE
      XMLTYPE STORE AS CLOB;
    
    ```

You can insert into such a table using ` XMLType ` syntax, as shown in the next statement. (The data inserted in this example corresponds to the data in the ` warehouse_spec ` column of the sample table ` oe.warehouses ` where ` warehouse_id ` = 1.) 
    
    
    ```
    INSERT INTO xwarehouses VALUES 
      (xmltype('
      
        1
        Southlake, Texas
        Owned
        25000
        2
        Rear load
        true
        N
        Street
        10
      '));
    ```

> **note:** See Also: 

[ *Oracle XML DB Developer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDB0400) for information on ` XMLType ` and its member methods 

You can query this table with the following statement: 
    
    
    ```
    SELECT e.getClobVal() FROM xwarehouses e;
    
    ```

` CLOB ` columns are subject to all of the restrictions on LOB columns. To avoid these restrictions, create an XMLSchema-based table. The XMLSchema maps the XML elements to their object-relational equivalents. The following example registers an XMLSchema locally. The XMLSchema ( ` xwarhouses.xsd ` ) reflects the same structure as the ` xwarehouses ` table. (XMLSchema declarations use PL/SQL and the ` DBMS_XMLSCHEMA ` package, so the example is shown in italics.) 

> **note:** See Also: 

[ *Oracle XML DB Developer's Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADXDB0800) for information on creating XMLSchemas 
    
    
    ```
    begin
     dbms_xmlschema.registerSchema(
      'http://www.example.com/xwarehouses.xsd',  
      '
           targetNamespace="http://www.example.com/xwarehouses.xsd" 
           xmlns:who="http://www.example.com/xwarehouses.xsd"
           version="1.0">
     
      
       
        
        
       
      
     
      
       
        
        
       
      
      
      
        
         
          
          
          
          
          
          
          
          
          
          
         
        
      
    ',
       TRUE, TRUE, FALSE, FALSE);
    end;
    /
    ```

Now you can create an XMLSchema-based table, as shown in the following example: 
    
    
    ```
    CREATE TABLE xwarehouses OF XMLTYPE
       XMLSCHEMA "http://www.example.com/xwarehouses.xsd"
       ELEMENT "Warehouse";
    
    ```

By default, Oracle stores this as an object-relational table. Therefore, you can insert into it as shown in the example that follows. (The data inserted in this example corresponds to the data in the ` warehouse_spec ` column of the sample table ` oe.warehouses ` where ` warehouse_id ` = 1.) 
    
    
    ```
    INSERT INTO xwarehouses VALUES(   xmltype.createxml('
       
          1
          Southlake, Texas
          Owned
          25000
          2
          Rear load
          true
          false
          Street
          10
          '));
    ...
    ```

You can define constraints on an XMLSchema-based table. To do so, you use the ` XMLDATA ` pseudocolumn to refer to the appropriate attribute within the ` Warehouse ` XML element: 
    
    
    ```
    ALTER TABLE xwarehouses ADD (PRIMARY KEY(XMLDATA."WarehouseId"));
    
    ```

Because the data in ` xwarehouses ` is stored object relationally, Oracle rewrites queries to this ` XMLType ` table to go to the underlying storage when possible. Therefore the following queries would use the index created by the primary key constraint in the preceding example: 
    
    
    ```
    SELECT * FROM xwarehouses x 
       WHERE EXISTSNODE(VALUE(x), '/Warehouse[WarehouseId="1"]',
       'xmlns:who="http://www.example.com/xwarehouses.xsd"') = 1;
    
    SELECT * FROM xwarehouses x
       WHERE EXTRACTVALUE(VALUE(x), '/Warehouse/WarehouseId',
       'xmlns:who="http://www.example.com/xwarehouses.xsd"') = 1;
    
    ```

You can also explicitly create indexes on XMLSchema-based tables, which greatly enhance the performance of subsequent queries. You can create object-relational views on ` XMLType ` tables, and you can create ` XMLType ` views on object-relational tables. 

> **note:** See Also: 

  * [ XMLDATA Pseudocolumn ](XMLDATA-Pseudocolumn.md#GUID-EBB52EE8-57B4-4DCA-A17E-351DE5CFA934) for information on the ` XMLDATA ` pseudocolumn 

  * " [ Creating an XMLType View: Example ](CREATE-VIEW.md#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30__I2117764) " 

  * [ Creating an Index on an XMLType Table: Example ](CREATE-INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE__I2113966)




XMLType Columns 

The sample table ` oe.warehouses ` was created with a ` warehouse_spec ` column of type ` XMLType ` . The examples in this section create a shortened form of the ` oe.warehouses ` table, using two different types of storage. 

The first example creates a table with an ` XMLType ` table stored as a ` CLOB ` . This table does not require an XMLSchema, so the content structure is not predetermined: 
    
    
    ```
    CREATE TABLE xwarehouses (
       warehouse_id        NUMBER,
       warehouse_spec      XMLTYPE)
       XMLTYPE warehouse_spec STORE AS CLOB
       (TABLESPACE example
        STORAGE (INITIAL 6144)
        CHUNK 4000
        NOCACHE LOGGING);
    
    ```

The following example creates a similar table, but stores the ` XMLType ` data in an object-relational ` XMLType ` column whose structure is determined by the specified XMLSchema: 
    
    
    ```
    CREATE TABLE xwarehouses (
       warehouse_id    NUMBER,
       warehouse_spec  XMLTYPE)
       XMLTYPE warehouse_spec STORE AS OBJECT RELATIONAL
          XMLSCHEMA "http://www.example.com/xwarehouses.xsd"
          ELEMENT "Warehouse";
    ```
