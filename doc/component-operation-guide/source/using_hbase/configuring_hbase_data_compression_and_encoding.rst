:original_name: mrs_01_24112.html

.. _mrs_01_24112:

Configuring HBase Data Compression and Encoding
===============================================

Scenario
--------

HBase encodes data blocks in HFiles to reduce duplicate keys in KeyValues, reducing used space. Currently, the following data block encoding modes are supported: NONE, PREFIX, DIFF, FAST_DIFF, and ROW_INDEX_V1. NONE indicates that data blocks are not encoded. HBase also supports compression algorithms for HFile compression. The following algorithms are supported by default: NONE, GZ, SNAPPY, and ZSTD. NONE indicates that HFiles are not compressed.

The two methods are used on the HBase column family. They can be used together or separately.

Prerequisites
-------------

-  You have installed an HBase client. For example, the client is installed in **opt/client**.
-  If authentication has been enabled for HBase, you must have the corresponding operation permissions. For example, you must have the creation (C) or administration (A) permission on the corresponding namespace or higher-level items to create a table, and the creation (C) or administration (A) permission on the created table or higher-level items to modify a table. For details about how to grant permissions, see :ref:`Creating HBase Roles <mrs_01_1608>`.

Procedure
---------

**Setting data block encoding and compression algorithms during creation**

-  **Method 1: Using hbase shell**

   #. Log in to the node where the client is installed as the client installation user.

   #. Run the following command to go to the client directory:

      **cd /opt/client**

   #. Run the following command to configure environment variables:

      **source bigdata_env**

   #. If the Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step:

      **kinit** *Component service user*

      For example, **kinit hbaseuser**.

   #. Run the following HBase client command:

      **hbase shell**

   #. Create a table.

      **create '**\ *t1*\ **', {NAME => '**\ *f1*\ **', COMPRESSION => '**\ *SNAPPY*\ **', DATA_BLOCK_ENCODING => '**\ *FAST_DIFF*\ **'}**

      .. note::

         -  *t1*: indicates the table name.
         -  *f1*: indicates the column family name.
         -  *SNAPPY*: indicates the column family uses the SNAPPY compression algorithm.
         -  *FAST_DIFF*: indicates FAST_DIFF is used for encoding.
         -  The parameter in the braces specifies the column family. You can specify multiple column families using multiple braces and separate them by commas (,). For details about table creation statements, run the **help 'create'** statement in the HBase shell.

-  **Method 2: Using Java APIs**

   The following code snippet shows only how to set the encoding and compression modes of a column family when creating a table. For complete code for creating a table and how to use the code to create a table, see "HBase Development Guide" > "Modifying a Table" in .

   .. code-block::

      TableDescriptorBuilder htd = TableDescriptorBuilder.newBuilder(TableName.valueOf("t1"));// Create a descriptor for table t1.
      ColumnFamilyDescriptorBuilder hcd = ColumnFamilyDescriptorBuilder.newBuilder(Bytes.toBytes("f1"));// Create a builder for column family f1.
      hcd.setDataBlockEncoding(DataBlockEncoding.FAST_DIFF);// Set the encoding mode of column family f1 to FAST_DIFF.
      hcd.setCompressionType(Compression.Algorithm.SNAPPY);// Set the compression algorithm of column family f1 to SNAPPY.
      htd.setColumnFamily(hcd.build())// Add the column family f1 to the descriptor of table t1.

**Setting or modifying the data block encoding mode and compression algorithm for an existing table**

-  **Method 1: Using hbase shell**

   #. Log in to the node where the client is installed as the client installation user.

   #. Run the following command to go to the client directory:

      **cd /opt/client**

   #. Run the following command to configure environment variables:

      **source bigdata_env**

   #. If the Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step:

      **kinit** *Component service user*

      For example, **kinit hbaseuser**.

   #. Run the following HBase client command:

      **hbase shell**

   #. Run the following command to modify the table:

      **alter '**\ *t1*\ **', {NAME => '**\ *f1*\ **', COMPRESSION => '**\ *SNAPPY*\ **', DATA_BLOCK_ENCODING => '**\ *FAST_DIFF*\ **'}**

-  **Method 2: Using Java APIs**

   The following code snippet shows only how to modify the encoding and compression modes of a column family in an existing table. For complete code for modifying a table and how to use the code to modify a table, see "HBase Development Guide".

   .. code-block::

      TableDescriptor htd = admin.getDescriptor(TableName.valueOf("t1"));// Obtain the descriptor of table t1.
      ColumnFamilyDescriptor originCF = htd.getColumnFamily(Bytes.toBytes("f1"));// Obtain the descriptor of column family f1.
      builder.ColumnFamilyDescriptorBuilder hcd = ColumnFamilyDescriptorBuilder.newBuilder(originCF);// Create a builder based on the existing column family attributes.
      hcd.setDataBlockEncoding(DataBlockEncoding.FAST_DIFF);// Change the encoding mode of the column family to FAST_DIFF.
      hcd.setCompressionType(Compression.Algorithm.SNAPPY);// Change the compression algorithm of the column family to SNAPPY.
      admin.modifyColumnFamily(TableName.valueOf("t1"), hcd.build());// Submit to the server to modify the attributes of column family f1.

   After the modification, the encoding and compression modes of the existing HFile will take effect after the next compaction.
