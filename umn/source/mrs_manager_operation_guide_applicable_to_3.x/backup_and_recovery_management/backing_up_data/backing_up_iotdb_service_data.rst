:original_name: admin_guide_000360.html

.. _admin_guide_000360:

Backing Up IoTDB Service Data
=============================

Scenario
--------

To ensure IoTDB service data security routinely or before a major operation on IoTDB (such as upgrade or migration), you need to back up IoTDB service data. The backup data can be used to recover the system if an exception occurs or the operation has not achieved the expected result, minimizing the adverse impacts on services.

You can create a backup task on MRS Manager to back up IoTDB service data. Both automatic and manual backup tasks are supported.

Prerequisites
-------------

-  If data needs to be backed up to the remote HDFS, you have prepared a standby cluster for data backup. The authentication mode of the standby cluster is the same as that of the active cluster. For other backup modes, you do not need to prepare the standby cluster. Currently, IoTDB data can be backed up only to HDFS.
-  For the IoTDB cluster in normal mode, service data cannot be backed up to HDFS in a cluster in security mode.

-  If the active cluster is deployed in security mode and the active and standby clusters are not managed by the same MRS Manager, mutual trust has been configured. For details, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`. If the active cluster is deployed in normal mode, no mutual trust is required.

-  Time is consistent between the active and standby clusters and the NTP services on the active and standby clusters use the same time source.
-  The HDFS in the standby cluster has sufficient space. You are advised to save backup files in a custom directory.

Procedure
---------

#. On MRS Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

#. Click **Create**.

#. Set **Name** to the name of the backup task.

#. Select the cluster to be operated from **Backup Object**.

#. Set **Mode** to the type of the backup task.

   **Periodic** indicates that the backup task is executed by the system periodically. **Manual** indicates that the backup task is executed manually.

   .. table:: **Table 1** Periodic backup parameters

      +-----------------------------------+----------------------------------------------------------------------------+
      | Parameter                         | Description                                                                |
      +===================================+============================================================================+
      | Started                           | Indicates the time when the task is started for the first time.            |
      +-----------------------------------+----------------------------------------------------------------------------+
      | Period                            | The task execution interval. Value options include **Hours** and **Days**. |
      +-----------------------------------+----------------------------------------------------------------------------+
      | Backup Policy                     | Indicates a periodic backup policy.                                        |
      |                                   |                                                                            |
      |                                   | -  **Full backup at the first time and incremental backup subsequently**   |
      |                                   | -  **Full backup every time**                                              |
      |                                   | -  **Full backup once every n times**                                      |
      +-----------------------------------+----------------------------------------------------------------------------+

#. In **Configuration**, choose **IoTDB** > **IoTDB** under **Service data**.

#. Set **Path Type** of **IoTDB** to a backup directory type.

   The following backup directory types are supported:

   **RemoteHDFS**: indicates that the backup files are stored in the HDFS directory of the standby cluster.

   If you select this option, set the following parameters:

   -  **Destination NameService Name**: indicates the NameService name of the standby cluster, for example, **hacluster**. You can obtain it from the **NameService Management** page of HDFS of the standby cluster.

   -  **IP Mode**: indicates the mode of the target IP address. The system automatically selects the IP address mode based on the cluster network type, for example, **IPv4** or **IPv6**.
   -  **Destination Active NameNode IP Address**: indicates the service plane IP address of the active NameNode in the standby cluster.
   -  **Destination Standby NameNode IP Address**: indicates the service plane IP address of the standby NameNode in the standby cluster.
   -  **Destination NameNode RPC Port**: indicates the value of **dfs.namenode.rpc.port** in the HDFS basic configuration of the standby cluster.
   -  **Target Path**: indicates the HDFS directory for storing standby cluster backup data. The storage path cannot be an HDFS hidden directory, such as a snapshot or recycle bin directory, or a default system directory, such as **/hbase** or **/user/hbase/backup**.
   -  **Maximum Number of Backup Copies**: indicates the number of backup file sets that can be retained in the backup directory.

#. Set **Backup Content** to one or multiple service data records to be backed up.

   You can select backup data using either of the following methods:

   -  Adding a backup data file

      Click the name of a database in the navigation tree to show all the tables in the database, and select specified tables.

      MRS 3.2.0 or later:

      a. Click **Add**.
      b. Select the table to be backed up under **File Directory**, and click **Add** to add the table to **Backup Content**.
      c. Click **OK**.

   -  Selecting using regular expressions

      a. Click **Query Regular Expression**.
      b. Enter the parent directory full path of the directory in the first text box as prompted. The directory must be the same as the existing directory, for example, **/root**.
      c. Enter a regular expression in the second text box. Standard regular expressions are supported. For example, to get all files or subdirectories in the parent directory, enter **([\\s\\S]*?)**. To get files whose names consist of letters and digits, for example, **file\ 1**, enter **file\\d\***.
      d. Enter a regular expression in the second text box. Standard regular expressions are supported. For example, to get objects containing **test**, enter **.*test.\***. To get objects starting with **test**, enter **test.\***. To get objects ending with **test**, enter **.*test**.
      e. Click **Refresh** to view the displayed directories in **Directory Name**.
      f. Click **Synchronize** to save the result.

      .. note::

         -  When entering regular expressions, click |image1| or |image2| to add or delete an expression.
         -  If the selected table or directory is incorrect, click **Clear Selected Node** to deselect it.
         -  The backup directory cannot contain files that have been written for a long time. Otherwise, the backup task will fail. Therefore, you are not advised to perform operations on the top-level directory, such as **/user**, **/tmp**, and **/mr-history**.

#. Click **Verify** to check whether the backup task is configured correctly.

   The possible causes of the verification failure are as follows:

   -  The target NameNode IP address is incorrect.
   -  The data to be backed up does not exist.

#. Click **OK**.

#. In the **Operation** column of the created task in the backup task list, click **More** and select **Back Up Now** to execute the backup task.

   After the backup task is executed, the system automatically creates a subdirectory for each backup task in the backup directory. The format of the subdirectory name is *Backup task name_Data source_Task creation time*, and the subdirectory is used to save latest data source backup files. All the backup file sets are stored in the related snapshot directories.

.. |image1| image:: /_static/images/en-us_image_0000001584751969.png
.. |image2| image:: /_static/images/en-us_image_0000001534512058.png
