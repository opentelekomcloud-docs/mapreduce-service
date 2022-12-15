:original_name: admin_guide_000349.html

.. _admin_guide_000349:

Backing Up ClickHouse Service Data
==================================

Scenario
--------

To ensure ClickHouse service data security routinely or before a major operation on ClickHouse (such as upgrade or migration), you need to back up ClickHouse service data. The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

You can create a backup task on FusionInsight Manager to back up ClickHouse service data. Both automatic and manual backup tasks are supported.

.. important::

   This function is supported only by MRS 3.1.0 or later.

Prerequisites
-------------

-  If data needs to be backed up to the remote HDFS, you have prepared a standby cluster for data backup. The authentication mode of the standby cluster is the same as that of the active cluster. For other backup modes, you do not need to prepare the standby cluster.
-  If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same FusionInsight Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.
-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.

-  You have planned the backup type, period, object, and directory based on service requirements.
-  The HDFS in the standby cluster has sufficient space. You are advised to save backup files in a custom directory.

Procedure
---------

#. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. Click **Create**.

#. Set **Name** to the name of the backup task.

#. Select the cluster to be operated from **Backup Object**.

#. Set **Mode** to the type of the backup task.

   **Periodic** indicates that the backup task is executed by the system periodically. **Manual** indicates that the backup task is executed manually.

   .. table:: **Table 1** Periodic backup parameters

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                     |
      +===================================+=================================================================================================================================================+
      | Started                           | Indicates the time when the task is started for the first time.                                                                                 |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Period                            | Indicates the task execution interval. The options include **Hours** and **Days**.                                                              |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Backup Policy                     | -  **Full backup at the first time and incremental backup subsequently**                                                                        |
      |                                   | -  **Full backup every time**                                                                                                                   |
      |                                   | -  **Full backup once every n times**                                                                                                           |
      |                                   |                                                                                                                                                 |
      |                                   | .. note::                                                                                                                                       |
      |                                   |                                                                                                                                                 |
      |                                   |    -  Incremental backup is not supported when Manager data and component metadata are backed up. Only **Full backup every time** is supported. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

#. In **Configuration**, select **ClickHouse** under **Service Data**.

#. Set **Path Type** of **ClickHouse** to a backup directory type.

   Currently, only the **RemoteHDFS** type is available.

   **RemoteHDFS**: indicates that backup files are stored in HDFS of the standby cluster.

   This value option is available only after you configure the environment by referring to :ref:`How Do I Configure the Environment When I Create a ClickHouse Backup Task on FusionInsight Manager and Set the Path Type to RemoteHDFS? <admin_guide_000357>`.

   You also need to configure the following parameters:

   -  **Destination NameService Name**: indicates the NameService name of the standby cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.

   -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
   -  **Target NameNode IP Address**: indicates the IP address of the NameNode service plane in the standby cluster. It can be of an active or standby node.
   -  **Target Path**: indicates the HDFS directory for storing standby cluster backup data. The storage path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory, such as **/hbase** or **/user/hbase/backup**.
   -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.
   -  **Maximum Number of Maps**: indicates the maximum number of maps in a MapReduce task. The default value is **20**.
   -  **Maximum Bandwidth of a Map (MB/s)**: indicates the maximum bandwidth of a map. The default value is **100**.

#. Set **Maximum Number of Recovery Points** to the number of snapshots that can be retained in the cluster.

#. Set **Backup Content** to one or multiple ClickHouse tables to be backed up.

   You can select backup data using either of the following methods:

   -  Adding a backup data file

      Click the name of a database in the navigation tree to show all the tables in the database, and select specified tables.

   -  Selecting using regular expressions

      a. Click **Query Regular Expression**.
      b. Enter the database where the ClickHouse tables are located in the first text box as prompted. The database must be the same as the existing database, for example, **default**.
      c. Enter a regular expression in the second text box. Standard regular expressions are supported. For example, to get all tables in the database, enter **([\\s\\S]*?)**. To get tables named in the format of letters and digits, for example, **tb1**, enter **tb\\d\***.
      d. Click **Refresh** to view the displayed tables in **Directory Name**.
      e. Click **Synchronize** to save the result.

      .. note::

         -  When entering regular expressions, click |image1| or |image2| to add or delete an expression.
         -  If the selected table or directory is incorrect, click **Clear Selected Node** to deselect it.

#. Click **Verify** to check whether the backup task is configured correctly.

   The possible causes of the verification failure are as follows:

   -  The target NameNode IP address is incorrect.
   -  The directory or table to be backed up does not exist.
   -  The name of the NameService is incorrect.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Data source_Task creation time*, and the subdirectory is used to save latest data source backup files.

.. |image1| image:: /_static/images/en-us_image_0000001197336255.png
.. |image2| image:: /_static/images/en-us_image_0000001151336594.png
