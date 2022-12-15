:original_name: mrs_01_1652.html

.. _mrs_01_1652:

How Do I Delete Residual Table Names in the /hbase/table-lock Directory of ZooKeeper?
=====================================================================================

Question
--------

In security mode, names of tables that failed to be created are unnecessarily retained in the table-lock node (default directory is /hbase/table-lock) of ZooKeeper. How do I delete these residual table names?

Answer
------

Perform the following steps:

#. On the client, run the kinit command as the hbase user to obtain a security certificate.
#. Run the **hbase zkcli** command to launch the ZooKeeper Command Line Interface (zkCLI).
#. Run the **ls /hbase/table** command on the zkCLI to check whether the table name of the table that fails to be created exists.

   -  If the table name exists, no further operation is required.
   -  If the table name does not exist, run **ls /hbase/table-lock** to check whether the table name of the table fail to be created exist. If the table name exists, run the **delete /hbase/table-lock/<table>** command to delete the table name. In the **delete /hbase/table-lock/<table>** command, **<table>** indicates the residual table name.
