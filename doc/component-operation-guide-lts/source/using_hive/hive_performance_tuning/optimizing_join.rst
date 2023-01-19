:original_name: mrs_01_0979.html

.. _mrs_01_0979:

Optimizing Join
===============

Scenario
--------

When the Join statement is used, the command execution speed and query speed may be slow in case of large data volume. To resolve this problem, you can optimize Join.

Join optimization can be classified into the following modes:

-  Map Join
-  Sort Merge Bucket Map Join
-  Optimizing Join Sequences

Map Join
--------

Hive Map Join applies to small tables (the table size is less than 25 MB) that can be stored in the memory. The table size can be defined using **hive.mapjoin.smalltable.filesize**, and the default table size is 25 MB.

Map Join has two methods:

-  Use ``/*+ MAPJOIN(join_table) */``.

-  Set the following parameter before running the statement. The default value is true in the current version.

   **set hive.auto.convert.join=true;**

There is no Reduce task when Map Join is used. Instead, a MapReduce Local Task is created before the Map job. The task uses TableScan to read small table data to the local computer, saves and writes the data in HashTable mode to a hard disk on the local computer, upload the data to DFS, and saves the data in distributed cache. The small table data that the map task reads from the local disk or distributed cache is the output together with the large table join result.

When using Map Join, make sure that the size of small tables cannot be too large. If small tables use up memory, the system performance will deteriorate and even memory leakage occurs.

Sort Merge Bucket Map Join
--------------------------

The following conditions must be met before using Sort Merge Bucket Map Join:

-  The two Join tables are large and cannot be stored in the memory.
-  The two tables are bucketed (clustered by (column)) and sorted (sorted by(column)) according to the join key, and the buckets counts of the two tables are in integral multiple relationship.

Set the following parameters to enable Sort Merge Bucket Map Join:

**set hive.optimize.bucketmapjoin=true;**

**set hive.optimize.bucketmapjoin.sortedmerge=true;**

This type of Map Join does not have Reduce tasks too. A MapReduce Local Task is started before the Map job to read small table data by bucket to the local computer. The local computer saves the HashTable backup of multiple buckets and writes the backup into HDFS. The backup is also saved in the distributed cache. The small table data that the map task reads from the local disk or distributed cache by bucket is the output after mapping with the large table.

Optimizing Join Sequences
-------------------------

If the Join operation is to be performed on three or more tables and different Join sequences are used, the execution time will be greatly different. Using an appropriate Join sequence can shorten the time for task execution.

Rules of a Join sequence:

-  A table with small data volume or a combination with fewer results generated after a Join operation is executed first.
-  A table with large data volume or a combination with more results generated after a Join operation is executed later.

For example, the **customer** table has the largest data volume, and fewer results will be generated if a Join operation is performed on the **orders** and **lineitem** tables first.

The original Join statement is as follows.

.. code-block::

   select
     l_orderkey,
     sum(l_extendedprice * (1 - l_discount)) as revenue,
     o_orderdate,
     o_shippriority
   from
     customer,
     orders,
     lineitem
   where
     c_mktsegment = 'BUILDING'
     and c_custkey = o_custkey
     and l_orderkey = o_orderkey
     and o_orderdate < '1995-03-22'
     and l_shipdate > '1995-03-22'
   limit 10;

After the sequence is optimized, the Join statements are as follows:

.. code-block::

   select
     l_orderkey,
     sum(l_extendedprice * (1 - l_discount)) as revenue,
     o_orderdate,
     o_shippriority
   from
     orders,
     lineitem,
     customer
   where
     c_mktsegment = 'BUILDING'
     and c_custkey = o_custkey
     and l_orderkey = o_orderkey
     and o_orderdate < '1995-03-22'
     and l_shipdate > '1995-03-22'
   limit 10;

Precautions
-----------

**Join Data Skew Problem**

Data skew refers to the symptom that the task progress is 99% for a long time.

Data skew often exists because the data volume of a few Reduce tasks is much larger than that of others. Most Reduce tasks are complete while a few Reduce tasks are not complete.

To resolve the data skew problem, set **hive.optimize.skewjoin=true** and adjust the value of **hive.skewjoin.key**. **hive.skewjoin.key** specifies the maximum number of keys received by a Reduce task. If the number reaches the maximum, the keys are atomically distributed to other Reduce tasks.
