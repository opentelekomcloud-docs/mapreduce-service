:original_name: mrs_01_1105.html

.. _mrs_01_1105:

Typical Scenario: Exporting Data from Hive to an SFTP Server
============================================================

Scenario
--------

Use Loader to export data from Hive to an SFTP server.

Prerequisites
-------------

-  You have obtained the service username and password for creating a Loader job.
-  You have had the permission to access the Hive table specified in the job.
-  You have obtained the username and password of the SFTP server and the user has the write permission of the data export directory on the SFTP server.
-  No disk space alarm is reported, and the available disk space is sufficient for importing and exporting data.
-  If a configured task requires the Yarn queue function, the user must be authorized with related Yarn queue permission.
-  The user who configures a task must obtain execution permission on the task and obtain usage permission on the related connection of the task.

Procedure
---------

**Setting Basic Job Information**

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.


      .. figure:: /_static/images/en-us_image_0000001438241209.png
         :alt: **Figure 1** Loader web UI

         **Figure 1** Loader web UI

#. Click **New Job** to go to the **Basic Information** page and set basic job information.


   .. figure:: /_static/images/en-us_image_0000001349139405.png
      :alt: **Figure 2** **Basic Information**

      **Figure 2** **Basic Information**

   a. Set **Name** to the name of the job.
   b. Set **Type** to **Export**.
   c. Set **Group** to the group to which the job belongs. No group is created by default. You need to click **Add** to create a group and click **OK** to save the created group.
   d. Set **Queue** to the Yarn queue that executes the job. The default value is **root.default**.
   e. Set **Priority** to the priority of the Yarn queue that executes the job. The default value is **NORMAL**. The options are **VERY_LOW**, **LOW**, **NORMAL**, **HIGH**, and **VERY_HIGH**.

#. In the **Connection** area, click **Add** to create a connection, set **Connector** to **sftp-connector**, click **Add**, set connection parameters, and click **Test** to verify whether the connection is available. When "**Test Success**" is displayed, click **OK**. Loader allows multiple SFTP servers to be configured. Click **Add** to add the configuration information of multiple SFTP servers.

   .. table:: **Table 1** Connection parameters

      +------------------+--------------------------------------------------------+---------------+
      | Parameter        | Description                                            | Example Value |
      +==================+========================================================+===============+
      | **Name**         | Specifies the name of the SFTP server connection.      | sftpName      |
      +------------------+--------------------------------------------------------+---------------+
      | SFTP server IP   | Specifies the IP address of the SFTP server.           | 10.16.0.1     |
      +------------------+--------------------------------------------------------+---------------+
      | SFTP server port | Specifies the port number of the SFTP server.          | 22            |
      +------------------+--------------------------------------------------------+---------------+
      | SFTP username    | Specifies the user name for accessing the SFTP server. | root          |
      +------------------+--------------------------------------------------------+---------------+
      | SFTP password    | Specifies the password for accessing the SFTP server.  | xxxx          |
      +------------------+--------------------------------------------------------+---------------+
      | SFTP public key  | Specifies public key of the SFTP server.               | OdDt/yn...etM |
      +------------------+--------------------------------------------------------+---------------+

   .. note::

      When multiple SFTP servers are configured, the data of Hive tables will be divided into multiple parts and saved to the SFTP servers randomly.

   **Setting Data Source Information**

#. Click **Next**. On the displayed **From** page, set **Source type** to **HIVE**.

   .. table:: **Table 2** Data source parameters

      +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter     | Description                                                                                                                                                                                                                                                      | Example Value |
      +===============+==================================================================================================================================================================================================================================================================+===============+
      | Hive instance | Specifies the Hive service instance that Loader selects from all available Hive service instances in the cluster. If the selected Hive service instance is not added to the cluster, the Hive job cannot run properly.                                           | hive          |
      +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Quantity      | Specifies the number of maps that are started at the same time in a MapReduce job of a data configuration operation. The value must be less than or equal to 3000. You are advised to set the parameter to the maximum number of connections on the SFTP server. | 20            |
      +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   **Setting Data Transformation**

#. Click **Next**. On the displayed **Transform** page, set the transformation operations in the data transformation process. For details about how to select operators and set parameters, see :ref:`Operator Help <mrs_01_1119>` and :ref:`Table 3 <mrs_01_1105__en-us_topic_0000001219230969_table895989011525>`.

   .. _mrs_01_1105__en-us_topic_0000001219230969_table895989011525:

   .. table:: **Table 3** Setting the input and output parameters of the operator

      ========== ===========
      Input Type Export Type
      ========== ===========
      Hive input File output
      ========== ===========


   .. figure:: /_static/images/en-us_image_0000001349258993.png
      :alt: **Figure 3** Operator operation procedure

      **Figure 3** Operator operation procedure

   **Setting Data Storage Information and Executing the Job**

#. Click **Next**. On the displayed **To** page, set the data storage mode.

   .. table:: **Table 4** Parameter description

      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter             | Description                                                                                                                                                                                                                                                                                                                                                                                                                        | Example Value         |
      +=======================+====================================================================================================================================================================================================================================================================================================================================================================================================================================+=======================+
      | Output path           | Specifies the path or file name of the exported file on an SFTP server. If multiple SFTP server IP addresses are configured for the connector, you can set this parameter to multiple paths or file names separated with semicolons (**;**). Ensure that the number of paths or file names is the same as the number of SFTP servers configured for the connector.                                                                 | /opt/tempfile         |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                    |                       |
      |                       | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                          |                       |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                    |                       |
      |                       |    You can use macros to define path parameters. For details, see :ref:`Using Macro Definitions in Configuration Items <mrs_01_1153>`.                                                                                                                                                                                                                                                                                             |                       |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Operation             | Specifies the action during data import. When all data is to be imported from the input path to the destination path, the data is stored in a temporary directory and then copied from the temporary directory to the destination path. After the data is imported successfully, the data is deleted from the temporary directory. One of the following actions can be taken when duplicate file names exist during data transfer: | OVERRIDE              |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                    |                       |
      |                       | -  **OVERRIDE**: overrides the old file.                                                                                                                                                                                                                                                                                                                                                                                           |                       |
      |                       | -  **RENAME**: renames as new file. For a file without an extension, a string is added to the file name as the extension; for a file with an extension, a string is added to the extension. The string is unique.                                                                                                                                                                                                                  |                       |
      |                       | -  **APPEND**: adds the content of the new file to the end of the old file. This action only adds content regardless of whether the file can be used. For example, a text file can be used after this operation, while a compressed file cannot.                                                                                                                                                                                   |                       |
      |                       | -  **IGNORE**: reserves the old file and does not copy the new file.                                                                                                                                                                                                                                                                                                                                                               |                       |
      |                       | -  **ERROR**: stops the task and reports an error if duplicate file names exist. Transferred files are imported successfully, while files that have duplicate names and files that are not transferred fail to be imported.                                                                                                                                                                                                        |                       |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Encode type           | Specifies the exported file encoding format, for example, UTF-8. This parameter can be set only in text file export.                                                                                                                                                                                                                                                                                                               | UTF-8                 |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Compression           | Indicates whether to enable the compressed transmission function when SFTP is used to export data.                                                                                                                                                                                                                                                                                                                                 | true                  |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                    |                       |
      |                       | -  The value **true** indicates that compression is enabled.                                                                                                                                                                                                                                                                                                                                                                       |                       |
      |                       | -  The value **false** indicates that compression is disabled.                                                                                                                                                                                                                                                                                                                                                                     |                       |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

#. Click **Save and run** to save and run the job.

   **Checking the Job Execution Result**

#. Go to the **Loader WebUI**. When **Status** is **Succeeded**, the job is complete.


   .. figure:: /_static/images/en-us_image_0000001439347017.png
      :alt: **Figure 4** Viewing job

      **Figure 4** Viewing job
