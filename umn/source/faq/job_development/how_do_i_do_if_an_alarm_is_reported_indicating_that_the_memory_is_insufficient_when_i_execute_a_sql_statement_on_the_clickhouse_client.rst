:original_name: mrs_03_1201.html

.. _mrs_03_1201:

How Do I Do If an Alarm Is Reported Indicating that the Memory Is Insufficient When I Execute a SQL Statement on the ClickHouse Client?
=======================================================================================================================================

Symptom
-------

The ClickHouse client restricts the memory used by GROUP BY statements. When a SQL statement is executed on the ClickHouse client, the following error information is displayed:

.. code-block::

   Progress: 1.83 billion rows, 85.31 GB (68.80 million rows/s., 3.21 GB/s.)        6%Received exception from server:
   Code: 241. DB::Exception: Received from localhost:9000, 127.0.0.1.
   DB::Exception: Memory limit (for query) exceeded: would use 9.31 GiB (attempt to allocate chunk of 1048576 bytes), maximum: 9.31 GiB:
   (while reading column hits):

Solution
--------

-  Run the following command before executing an SQL statement on condition that the cluster has sufficient memory:

   .. code-block::

      SET max_memory_usage = 128000000000; #128G

-  If no sufficient memory is available, ClickHouse enables you to overflow data to disk to free up the memory: You are advised to set the value of **max_memory_usage** to twice the size of **max_bytes_before_external_group_by**.

   .. code-block::

      set max_bytes_before_external_group_by=20000000000; #20G
      set max_memory_usage=40000000000; #40G
