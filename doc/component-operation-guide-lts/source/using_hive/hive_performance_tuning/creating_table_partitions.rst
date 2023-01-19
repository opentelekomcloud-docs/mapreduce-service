:original_name: mrs_01_0978.html

.. _mrs_01_0978:

Creating Table Partitions
=========================

Scenario
--------

During the Select query, Hive generally scans the entire table, which is time-consuming. To improve query efficiency, create table partitions based on service requirements and query dimensions.

Procedure
---------

#. Log in to the node where the Hive client has been installed as user **root**.

#. Run the following command to go to the client installation directory, for example, **/opt/client**.

   **cd /opt/client**

#. Run the **source bigdata_env** command to configure environment variables for the client.

#. Run the following command on the client for login:

   **kinit** *Username*

#. Run the following command to log in to the client tool:

   **beeline**

#. Select the static or dynamic partition.

   -  Static partition:

      Manually enter a partition name, and use the keyword **PARTITIONED BY** to specify partition column name and data type when creating a table. During application development, use the **ALTER TABLE ADD PARTITION** statement to add a partition and use the **LOAD DATA INTO PARTITION** statement to load data to the partition, which supports only static partitions.

   -  Dynamic partition: Use a query command to insert results to a partition of a table. The partition can be a dynamic partition.

      The dynamic partition can be enabled on the client tool by running the following command:

      **set hive.exec.dynamic.partition=true;**

      The default mode of the dynamic partition is strict. That is, at least a column must be specified as a static partition, under which dynamic sub-partitions can be created. You can run the following command to enable a completely dynamic partition:

      **set hive.exec.dynamic.partition.mode=nonstrict;**

   .. note::

      -  The dynamic partition may cause a DML statement to create a large number of partitions and new mapping folders, which deteriorates system performance.
      -  If there are a large number of files, it takes a long time to run a SQL statement. You can run the **set mapreduce.input.fileinputformat.list-status.num-threads = 100;** statement before running a SQL statement to shorten the time. The parameter **mapreduce.input.fileinputformat.list-status.num-threads** can be set only after being added to the Hive whitelist.
