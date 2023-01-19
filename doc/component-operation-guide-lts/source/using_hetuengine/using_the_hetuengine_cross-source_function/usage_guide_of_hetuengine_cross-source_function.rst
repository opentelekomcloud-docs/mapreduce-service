:original_name: mrs_01_2341.html

.. _mrs_01_2341:

Usage Guide of HetuEngine Cross-Source Function
===============================================

#. Register the data source by referring to :ref:`Configuring a HetuEngine Data Source <mrs_01_1719>`.

#. If the HBase data source is used, you need to create a structured mapping table.

   -  The format of the statement for creating a mapping table is as follows:

      .. code-block::

         CREATE TABLE schemaName.tableName (
           rowId VARCHAR,
           qualifier1 TINYINT,
           qualifier2 SMALLINT,
           qualifier3 INTEGER,
           qualifier4 BIGINT,
           qualifier5 DOUBLE,
           qualifier6 BOOLEAN,
           qualifier7 TIME,
           qualifier8 DATE,
           qualifier9 TIMESTAMP
         )
         WITH (
         column_mapping = 'qualifier1:f1:q1,qualifier2:f1:q2,qualifier3:f2:q3,qualifier4:f2:q4,qualifier5:f2:q5,qualifier6:f3:q1,qualifier7:f3:q2,qualifier8:f3:q3,qualifier9:f3:q4',
         row_id = 'rowId',
         hbase_table_name = 'hbaseNamespace:hbaseTable',
         external = true
         );
         -- Note: The value of schemaName must be the same as the value of hbaseNamespace in hbase_table_name. Otherwise, the table fails to be created.

   -  Supported mapping tables: Mapping tables can be directly associated with tables in the HBase data source or created and associated with new tables that do not exist in the HBase data source.

   -  Supported data types in a mapping table: VARCHAR, TINYINT, SMALLINT, INTEGER, BIGINT, DOUBLE, BOOLEAN, TIME, DATE, and TIMESTAMP

   -  The following table describes the keywords in the statements for creating mapping tables.

      .. table:: **Table 1** Keywords in the statements for creating mapping tables

         +------------------+---------+-----------+------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Keyword          | Type    | Mandatory | Default Value                                        | Remarks                                                                                                                                                                                                                                                                                                                                                                 |
         +==================+=========+===========+======================================================+=========================================================================================================================================================================================================================================================================================================================================================================+
         | column_mapping   | String  | No        | All columns belong to the same Family column family. | Specify the mapping between columns in the mapping table and column families in the HBase data source table. If a table in the HBase data source needs to be associated, the value of **column_mapping** must be the same as that in the HBase data source. If you create a table that does not exist in the HBase data source, you need to specify **column_mapping**. |
         +------------------+---------+-----------+------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | row_id           | String  | No        | First column in the mapping table                    | Column name corresponding to the rowkey table in the HBase data source                                                                                                                                                                                                                                                                                                  |
         +------------------+---------+-----------+------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | hbase_table_name | String  | No        | Null                                                 | Tablespace and table name of the HBase data source to be associated. Use a colon (:) to separate them. The default tablespace is **default**. If a new table that does not exist in the HBase data source is created, **hbase_table_name** does not need to be specified.                                                                                               |
         +------------------+---------+-----------+------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | external         | Boolean | No        | true                                                 | If **external** is set to **true**, the table is a mapping table in the HBase data source and the original table in the HBase data source cannot be deleted. If **external** is set to false, the table in the HBase data source is deleted when the **Hetu-HBase** table is deleted.                                                                                   |
         +------------------+---------+-----------+------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Use cross-source collaborative analysis.

   .. code-block::

      // 1. Register three types of data sources, including Hive, Elasticsearch, and GaussDB A.
      hetuengine> show catalogs;
        Catalog
      ----------
      dws
      es
      hive
      hive_dg
      system
      systemremote
      (6 rows)

      // 2. Compile SQL statements for cross-source collaborative analysis.
      select * from hive_dg.schema1.table1 t1 join es.schema3.table3 t2 join dws.schema02.table4 t3 on t1.name = t2.item and t2.id = t3.cardNo;
