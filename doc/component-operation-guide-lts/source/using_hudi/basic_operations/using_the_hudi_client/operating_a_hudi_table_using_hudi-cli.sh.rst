:original_name: mrs_01_24063.html

.. _mrs_01_24063:

Operating a Hudi Table Using hudi-cli.sh
========================================

Prerequisites
-------------

-  You have created a user and added the user to user groups **hadoop** and **hive** on Manager.
-  The Hudi client has been downloaded and installed.

Basic Operations
----------------

#. Log in to the client node as user **root** and run the following commands:

   **cd** *Client installation directory*

   **source bigdata_env**

   **cd** *Client installation directory*\ **Hudi**

   **source component_env**

   **kinit** *Created user*

#. Run the **hudi-cli.sh** command to access the Hudi client.

   **cd** *Client installation directory*\ **Hudi**

   **hudi-cli.sh**

   |image1|

#. Run the following example commands as required. For details about all commands, visit the `Hudi official website <https://hudi.apache.org/docs/quick-start-guide/>`__.

   -  Viewing help information

      **help** // View all Hudi CLI commands.

      **help 'command'** // View the help information and parameter list of a certain command.

   -  Connecting to a table

      **connect --path '**\ */tmp/huditest/test_table*'

   -  Viewing table information

      **desc**

   -  Viewing compaction plans

      **compactions show all**

   -  Viewing cleaning plans

      **cleans show**

   -  Performing the cleaning operation

      **cleans run**

   -  Viewing commit information

      **commits show**

   -  Viewing the partition where the commit is written to

      **commit showpartitions --commit** *20210127153356*

      .. note::

         *20210127153356* indicates the commit timestamp.

   -  Viewing the file where the commit is written to

      **commit showfiles --commit** *20210127153356*

   -  Comparing the commit information of two tables

      **commits compare --path** */tmp/hudimor/mytest100*

   -  Rolling back a commit (Only the last commit can be rolled back.)

      **commit rollback --commit** *20210127164905*

   -  Scheduling a compaction

      **compaction schedule --**\ *hoodieConfigs 'hoodie.compaction.strategy=org.apache.hudi.table.action.compact.strategy.BoundedIOCompactionStrategy,hoodie.compaction.target.io=1,hoodie.compact.inline.max.delta.commits=1'*

   -  Performing a compaction

      **compaction run --**\ *parallelism 100 --sparkMemory 1g --retry 1 --compactionInstant 20210602101315 --hoodieConfigs 'hoodie.compaction.strategy=org.apache.hudi.table.action.compact.strategy.BoundedIOCompactionStrategy,hoodie.compaction.target.io=1,hoodie.compact.inline.max.delta.commits=1' --propsFilePath hdfs://hacluster/tmp/default/tb_test_mor/.hoodie/hoodie.properties --schemaFilePath /tmp/default/tb_test_mor/.hoodie/compact_tb_base.json*

   -  Creating a savepoint

      **savepoint create** **--commit** *20210318155750*

   -  Rolling back a specified savepoint

      **savepoint rollback** **--savepoint** *20210318155750*

      .. caution::

         a. If the commit operation causes metadata conflicts, you can run the **commit rollback** and **savepoint rollback** commands to roll back data, but the Hive metadata cannot be rolled back. In this case, you can delete the Hive table and manually synchronize data.
         b. The **commit rollback** command rolls back only the latest commit, and the **savepoint rollback** command rolls back only the latest savepoint. You cannot specify a commit or savepoint to roll back.

.. |image1| image:: /_static/images/en-us_image_0000001348739865.png
