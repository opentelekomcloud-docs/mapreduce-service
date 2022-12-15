:original_name: mrs_01_1703.html

.. _mrs_01_1703:

Can I Delete or Modify the Data Storage Directory in DataNode?
==============================================================

Question
--------

-  In DataNode, the storage directory of data blocks is specified by **dfs.datanode.data.dir**\ **.** Can I modify **dfs.datanode.data.dir** to modify the data storage directory?
-  Can I modify files under the data storage directory?

Answer
------

During the system installation, you need to configure the **dfs.datanode.data.dir** parameter to specify one or more root directories.

-  During the system installation, you need to configure the dfs.datanode.data.dir parameter to specify one or more root directories.

-  Exercise caution when modifying dfs.datanode.data.dir. You can configure this parameter to add a new data root directory.
-  Do not modify or delete data blocks in the storage directory. Otherwise, the data blocks will lose.

.. note::

   Similarly, do not delete the storage directory, or modify or delete data blocks under the directory using the following parameters:

   -  dfs.namenode.edits.dir
   -  dfs.namenode.name.dir
   -  dfs.journalnode.edits.dir
