:original_name: mrs_01_24283.html

.. _mrs_01_24283:

Configuring the Timeout Interval of DBService Backup Tasks
==========================================================

Scenario
--------

The default timeout interval of DBService backup tasks is 2 hours. When the data volume in DBService is too large, the backup task may fail to be executed because the timeout interval is reached.

This section describes how to customize the timeout interval of a DBService backup task.

Prerequisites
-------------

-  Clusters have been properly installed.
-  DBService is running properly.

Procedure
---------

#. .. _mrs_01_24283__en-us_topic_0000001219029805_li140316245439:

   Log in to the active OMS node as user **omm** using PuTTY. In the **${CONTROLLER_HOME}/etc/om/controller.properties** configuration file, change the value of **controller.backup.conf.script.execute.timeout** to **10000000s** (Set the timeout interval based on the data volume of DBService).

#. Log in to the active OMS node as user **omm** using PuTTY and repeat step :ref:`1 <mrs_01_24283__en-us_topic_0000001219029805_li140316245439>`.

#. Log in to the active OMS node as user **omm** using PuTTY, run the following command to query the ID of **BackupRecoveryPluginProcess** process, and stop the process.

   **jps|grep -i BackupRecoveryPluginProcess**

   **kill -9** *Queried process ID*

#. Log in to FusionInsight Manager and perform the DBService backup task again.

#. Run the following command to check whether the **BackupRecoveryPluginProcess** process is started:

   **jps|grep -i BackupRecoveryPluginProcess**
