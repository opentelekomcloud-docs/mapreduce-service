:original_name: mrs_01_24837.html

.. _mrs_01_24837:

An Error Is Reported in Logs When the Auxiliary ZooKeeper or Replica Data Is Used to Synchronize Table Data
===========================================================================================================

Question
--------

An error is reported in logs when the auxiliary ZooKeeper or replica data is used to synchronize table data.

.. code-block::

   DB::Exception: Cannot parse input: expected 'quorum:' before: 'merge_type: 2'…" and "Too many parts (315). Merges are processing significantly slower than inserts…

Answer
------

The versions of replication table replicas are inconsistent, causing compatibility issues. The table schema contains TTL statements. TTL_DELETE is added in versions later than ClickHouse 20.9, which cannot be identified in earlier versions. This issue occurs when the replication table replica of a later version is elected as the leader.

You can modify the **config.xml** file of ClickHouse of a later version to avoid such an issue. Ensure that the replication table replicas are the same as those of ClickHouse.
