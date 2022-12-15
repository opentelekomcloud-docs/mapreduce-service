:original_name: mrs_01_2211.html

.. _mrs_01_2211:

How Do I Deal with the Restrictions of the Phoenix BulkLoad Tool?
=================================================================

Question
--------

When the indexed field data is updated, if a batch of data exists in the user table, the BulkLoad tool cannot update the global and partial mutable indexes.

Answer
------

**Problem Analysis**

#. Create a table.

   .. code-block::

      CREATE TABLE TEST_TABLE(
      DATE varchar not null,
      NUM integer not null,
      SEQ_NUM integer not null,
      ACCOUNT1 varchar not null,
      ACCOUNTDES varchar,
      FLAG varchar,
      SALL double,
      CONSTRAINT PK PRIMARY KEY (DATE,NUM,SEQ_NUM,ACCOUNT1)
      );

#. Create a global index.

   **CREATE INDEX TEST_TABLE_INDEX ON TEST_TABLE(ACCOUNT1,DATE,NUM,ACCOUNTDES,SEQ_NUM)**;

#. Insert data.

   **UPSERT INTO TEST_TABLE (DATE,NUM,SEQ_NUM,ACCOUNT1,ACCOUNTDES,FLAG,SALL) values ('20201001',30201001,13,'367392332','sffa1','','');**

#. Execute the BulkLoad task to update data.

   **hbase org.apache.phoenix.mapreduce.CsvBulkLoadTool -t TEST_TABLE -i /tmp/test.csv**, where the content of **test.csv** is as follows:

   ======== ======== == ========= ======= ======= ==
   20201001 30201001 13 367392332 sffa888 1231243 23
   ======== ======== == ========= ======= ======= ==

#. Symptom: The existing index data cannot be directly updated. As a result, two pieces of index data exist.

   .. code-block::

      +------------+-----------+-----------+---------------+----------------+
      | :ACCOUNT1  |   :DATE   |   :NUM    | 0:ACCOUNTDES  | :SEQ_NUM  |
      +------------+-----------+-----------+---------------+----------------+
      | 367392332  | 20201001  | 30201001  | sffa1          |  13                    |
      | 367392332  | 20201001  | 30201001  | sffa888       | 13                    |
      +------------+-----------+-----------+---------------+----------------+

**Solution**

#. Delete the old index table.

   **DROP INDEX TEST_TABLE_INDEX ON TEST_TABLE;**

#. Create an index table in asynchronous mode.

   **CREATE INDEX TEST_TABLE_INDEX ON TEST_TABLE(ACCOUNT1,DATE,NUM,ACCOUNTDES,SEQ_NUM) ASYNC;**

#. Recreate a index.

   **hbase org.apache.phoenix.mapreduce.index.IndexTool --data-table TEST_TABLE --index-table TEST_TABLE_INDEX --output-path /user/test_table**
