:original_name: mrs_01_1636.html

.. _mrs_01_1636:

Improving the BulkLoad Efficiency
=================================

Scenario
--------

BulkLoad uses MapReduce jobs to directly generate files that comply with the internal data format of HBase, and then loads the generated StoreFiles to a running cluster. Compared with HBase APIs, BulkLoad saves more CPU and network resources.

ImportTSV is an HBase table data loading tool.

Prerequisites
-------------

When using BulkLoad, the output path of the file has been specified using the **Dimporttsv.bulk.output** parameter.

Procedure
---------

Add the following parameter to the BulkLoad command when performing a batch loading task:

.. table:: **Table 1** Parameter for improving BulkLoad efficiency

   +--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------+
   | Parameter                | Description                                                                                                                                                                                                                                                                                                                     | Value                                                   |
   +==========================+=================================================================================================================================================================================================================================================================================================================================+=========================================================+
   | -Dimporttsv.mapper.class | The construction of key-value pairs is moved from the user-defined mapper to reducer to improve performance. The mapper only needs to send the original text in each row to the reducer. The reducer parses the record in each row and creates a key-value) pair.                                                               | org.apache.hadoop.hbase.mapreduce.TsvImporterByteMapper |
   |                          |                                                                                                                                                                                                                                                                                                                                 |                                                         |
   |                          | .. note::                                                                                                                                                                                                                                                                                                                       | and                                                     |
   |                          |                                                                                                                                                                                                                                                                                                                                 |                                                         |
   |                          |    When this parameter is set to **org.apache.hadoop.hbase.mapreduce.TsvImporterByteMapper**, this parameter is used only when the batch loading command without the *HBASE_CELL_VISIBILITY OR HBASE_CELL_TTL* option is executed. The **org.apache.hadoop.hbase.mapreduce.TsvImporterByteMapper** provides better performance. | org.apache.hadoop.hbase.mapreduce.TsvImporterTextMapper |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------+
