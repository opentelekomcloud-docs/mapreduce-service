:original_name: mrs_01_1651.html

.. _mrs_01_1651:

What Should I Do If I Fail to Create Tables Due to the FAILED_OPEN State of Regions?
====================================================================================

Question
--------

What should I do if I fail to create tables due to the FAILED_OPEN state of Regions?

Answer
------

If a network, HDFS, or Active HMaster fault occurs during the creation of tables, some Regions may fail to go online and therefore enter the FAILED_OPEN state. In this case, tables fail to be created.

The tables that fail to be created due to the preceding mentioned issue cannot be repaired. To solve this problem, perform the following operations to delete and re-create the tables:

#. Run the following command on the cluster client to repair the state of the tables:

   **hbase hbck -fixTableStates**

#. Enter the HBase shell and run the following commands to delete the tables that fail to be created:

   **truncate** *'<table_name>'*

   **disable** *'<table_name>'*

   **drop** *'<table_name>'*

#. Create the tables using the recreation command.
