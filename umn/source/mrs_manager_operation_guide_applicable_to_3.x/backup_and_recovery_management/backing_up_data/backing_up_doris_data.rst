:original_name: admin_guide_000423.html

.. _admin_guide_000423:

Backing Up Doris Data
=====================

Scenario
--------

To ensure Doris service data security, you need to back up Doris service data especially before you perform a major operation on Doris (such as upgrade or migration). The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

You can create automatic or manual tasks on Manager to back up Doris data.

.. note::

   This topic is available for clusters of MRS 3.5.0 and later only.

Prerequisites
-------------

-  To back up data to a remote HDFS, the following conditions must be met:

   -  A standby cluster for backing up data has been created. The authentication mode must be the same as that of the active cluster.
   -  At least one DBroker instance of the Doris service has been deployed in the active cluster.
   -  If the active and standby clusters are deployed in security mode and they are not managed by the same MRS Manager, mutual trust must be configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active and standby clusters are deployed in normal mode, no mutual trust is required.
   -  The time on the active and standby clusters must be the same, and the NTP service on the active and standby clusters uses the same time source.
   -  The HDFS in the standby cluster has sufficient space. You are advised to save backup files in a custom directory.
   -  The value of **hadoop.rpc.protection** of Doris must be the same as that of **hadoop.rpc.protection** of HDFS in both active and standby clusters.

-  You have planned the backup type, period, object, and directory based on service requirements.
-  If you want to back up data to OBS, you have connected the current cluster to OBS and have the permission to access OBS.


Backing Up Doris Data
---------------------

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. Click **Create**.

#. Set **Name** to the name of the backup task.

#. Select the desired cluster from **Backup Object**.

#. Set **Mode** to the type of the backup task.

   -  **Periodic**: indicates that the backup task is periodically executed. If you select this mode, you need to set other parameters by referring to :ref:`Table 1 <admin_guide_000423__en-us_topic_0000001819415328_table16898399515>`.
   -  **Manual**: indicates that the backup task is manually executed.

   .. _admin_guide_000423__en-us_topic_0000001819415328_table16898399515:

   .. table:: **Table 1** Periodic backup parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                       |
      +===================================+===================================================================================================+
      | Started                           | Time when the task is started for the first time                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | Period                            | The task execution interval. The options include **Hours** and **Days**.                          |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | Backup Policy                     | -  **Full backup at the first time and incremental backup subsequently**                          |
      |                                   | -  **Full backup every time**                                                                     |
      |                                   | -  **Full backup once every n times**                                                             |
      |                                   |                                                                                                   |
      |                                   | .. note::                                                                                         |
      |                                   |                                                                                                   |
      |                                   |    Currently, Doris supports only **full backup each time**. Incremental backup is not supported. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+

#. In **Configuration**, select **Doris** under **Metadata and other data**.

#. Set **Path Type** of **Doris** to a backup directory type.

   .. table:: **Table 2** Path of backup data

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Directory Type                    | Description                                                                                                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================================================================================================+
      | RemoteHDFS                        | Indicates that backup files are stored in the HDFS directory of the standby cluster. If you select this option, configure the following parameters:                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                          |
      |                                   | -  **Destination NameService Name**: indicates the NameService name of the standby cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS on the standby cluster.                                                       |
      |                                   |                                                                                                                                                                                                                                                                          |
      |                                   | -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects an IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.                                                                                   |
      |                                   | -  **Destination NameNode IP Address**: indicates the service plane IP address of the active NameNode in the standby cluster.                                                                                                                                            |
      |                                   | -  **Destination NameNode RPC Port**: indicates the value of **dfs.namenode.rpc.port** in the HDFS configuration of the destination cluster.                                                                                                                             |
      |                                   | -  **DBroker IP**: indicates the IP address of a service plane where the DBroker role in the cluster is deployed. The DBroker is used to transmit data during backup.                                                                                                    |
      |                                   | -  **Target Path**: indicates the HDFS directory for storing standby cluster backup data. The storage path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory, such as **/hbase** or **/user/hbase/backup**. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | OBS                               | Indicates that backup files are stored in an OBS directory. You need to set the **Target Path** to the OBS directory for storing backup data.                                                                                                                            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Set **Maximum Number of Recovery Points** to the number of snapshots that can be retained in the cluster.

#. Set **Backup Content** to one or multiple Doris tables to be backed up.

   You can select backup data using either of the following methods:

   -  Adding a backup data file

      Click the name of a database in the navigation pane to show all the tables in the database, and select specified tables.

   -  Using regular expressions

      a. Click **Query Regular Expression**.
      b. Enter the database where the Doris tables are located in the first text box as prompted. The database must be the same as the existing database, for example, **/example_db**.
      c. Enter a regular expression in the second box. Standard regular expressions are supported. For example, to search for all tables that contain the keyword **test** in the database, enter **test.\***.
      d. Click **Refresh** to view the displayed tables in **Directory Name**.
      e. Click **Synchronize** to save the result.

      .. note::

         -  When entering regular expressions, click |image1| or |image2| to add or delete an expression.
         -  If the selected table or directory is incorrect, click **Clear Selected Node** to deselect it.

#. Click **Verify** to check whether the backup task is configured correctly.

   The possible causes of the verification failure are as follows:

   -  The target NameNode IP address is incorrect.
   -  The name of the NameService is incorrect.
   -  The table to be backed up does not exist.
   -  The format of the table to be backed up is incorrect.
   -  The tables to be backed up must come from the same database.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name_Data source_Task creation time*, and the subdirectory is used to save latest data source backup files. All the backup file sets are stored in the related snapshot directories.

.. |image1| image:: /_static/images/en-us_image_0000002380008412.png
.. |image2| image:: /_static/images/en-us_image_0000002413647801.png
