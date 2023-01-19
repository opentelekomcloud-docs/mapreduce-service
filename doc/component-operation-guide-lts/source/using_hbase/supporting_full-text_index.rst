:original_name: mrs_01_0493.html

.. _mrs_01_0493:

Supporting Full-Text Index
==========================

You can create tables and indexes using **createTable** of **org.apache.luna.client.LunaAdmin** and specify table names, column family names, requests for creating indexes, as well as the directory path for storing mapping files. You can also add indexes to existing tables using **addCollection** and obtain tables to perform a scan operation by using **getTable** of **org.apache.luna.client.LunaAdmin**.

The column name and column family name of a table consist of letters, digits, and underscores (_) but cannot contain any special characters.

HBase tables with a full-text index have the following limitations:

-  Disaster recovery, backup, and restoration are not supported.
-  Rows and column families cannot be deleted.
-  Tight consistency is not supported by the query on Solr.

Code Snippet Example
--------------------

The following code snippet belongs to the **testFullTextScan** method in the **LunaSample** class of the **hbase.examples** package.

.. code-block::

    public static void testFullTextScan() throws Exception {
       /**
        * Create create request of Solr. Specify collection name, confset name,
        * number of shards, and number of replication factor.
        */
       Create create = new Create();
       create.setCollectionName(COLLECTION_NAME);
       create.setConfigName(CONFSET_NAME);
       create.setNumShards(NUM_OF_SHARDS);
       create.setReplicationFactor(NUM_OF_REPLICATIONFACTOR);
       /**
        * Create mapping. Specify index fields(mandatory) and non-index
        * fields(optional).
        */
       List<ColumnField> indexedFields = new ArrayList<ColumnField>();
       indexedFields.add(new ColumnField("name", "f:n"));
       indexedFields.add(new ColumnField("cat", "f:t"));
       indexedFields.add(new ColumnField("features", "f:d"));
       Mapping mapping = new Mapping(indexedFields);
       /**
        * Create table descriptor of HBase.
        */
       HTableDescriptor desc = new HTableDescriptor(HBASE_TABLE);
       desc.addFamily(new HColumnDescriptor(TABLE_FAMILY));
       /**
        * Create table and collection at the same time.
        */
       LunaAdmin admin = null;
       try {
         admin = new AdminSingleton().getAdmin();
         admin.deleteTable(HBASE_TABLE);
         if (!admin.tableExists(HBASE_TABLE)) {
           admin.createTable(desc, Bytes.toByteArrays(new String[] { "0", "1", "2", "3", "4" }),
               create, mapping);
         }
         /**
          * Put data.
          */
         Table table = admin.getTable(HBASE_TABLE);
         int i = 0;
         while (i < 5) {
           byte[] row = Bytes.toBytes(i + "+sohrowkey");
           Put put = new Put(row);
           put.addColumn(TABLE_FAMILY, Bytes.toBytes("n"), Bytes.toBytes("ZhangSan" + i));
           put.addColumn(TABLE_FAMILY, Bytes.toBytes("t"), Bytes.toBytes("CO" + i));
           put.addColumn(TABLE_FAMILY, Bytes.toBytes("d"), Bytes.toBytes("Male, Leader of M.O" + i));
           table.put(put);
           i++;
         }

         /**
          * Scan table.
          */
         Scan scan = new Scan();
         SolrQuery query = new SolrQuery();
         query.setQuery("name:ZhangSan1 AND cat:CO1");
         Filter filter = new FullTextFilter(query, COLLECTION_NAME);
         scan.setFilter(filter);
         ResultScanner scanner = table.getScanner(scan);
         LOG.info("-----------------records----------------");
         for (Result r = scanner.next(); r != null; r = scanner.next()) {
           for (Cell cell : r.rawCells()) {
             LOG.info(Bytes.toString(CellUtil.cloneRow(cell)) + ":"
                 + Bytes.toString(CellUtil.cloneFamily(cell)) + ","
                 + Bytes.toString(CellUtil.cloneQualifier(cell)) + ","
                 + Bytes.toString(CellUtil.cloneValue(cell)));
           }
         }
         LOG.info("-------------------end------------------");
         /**
          * Delete collection.
          */
         admin.deleteCollection(HBASE_TABLE, COLLECTION_NAME);

         /**
          * Delete table.
          */
         admin.deleteTable(HBASE_TABLE);
       } catch (IOException e) {
         e.printStackTrace();
       } finally {
         /**
          * When everything done, close LunaAdmin.
          */
         admin.close();
       }
     }

Precautions
-----------

-  Tables and indexes to be created must be unique.
-  Use LunaAdmin only to obtain tables to perform a scan operation.
