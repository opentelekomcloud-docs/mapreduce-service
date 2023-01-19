:original_name: mrs_01_1098.html

.. _mrs_01_1098:

Typical Scenario: Importing Data from HDFS or OBS to HBase
==========================================================

Scenario
--------

Use Loader to import data from HDFS or OBS to HBase.

Prerequisites
-------------

-  You have obtained the service username and password for creating a Loader job.
-  You have had the permission to access the HDFS or OBS directories and data involved in job execution.
-  You have had the permission to access the HBase tables or phoenix tables that are used during job execution.
-  No disk space alarm is reported, and the available disk space is sufficient for importing and exporting data.
-  When using Loader to import data from HDFS or OBS, the input paths and input path subdirectories of HDFS and the name of the files in these directories do not contain any of the special characters /"':;.
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


   .. figure:: /_static/images/en-us_image_0000001296060072.png
      :alt: **Figure 2** **Basic Information**

      **Figure 2** **Basic Information**

   a. Set **Name** to the name of the job.
   b. Set **Type** to **Import**.
   c. Set **Group** to the group to which the job belongs. No group is created by default. You need to click **Add** to create a group and click **OK** to save the created group.
   d. Set **Queue** to the Yarn queue that executes the job. The default value is **root.default**.
   e. Set **Priority** to the priority of the Yarn queue that executes the job. The default value is **NORMAL**. The options are **VERY_LOW**, **LOW**, **NORMAL**, **HIGH**, and **VERY_HIGH**.

#. In the **Connection** area, click **Add** to create a connection, set **Connector** to **hdfs-connector**, set connection parameters, and click **Test** to verify whether the connection is available. When "Test Success" is displayed, click **OK**.

   **Setting Data Source Information**

#. Click **Next**. On the displayed **From** page, set the data source information.

   .. table:: **Table 1** Parameter description

      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter             | Description                                                                                                                                                                                                                                                                                                            | Example Value         |
      +=======================+========================================================================================================================================================================================================================================================================================================================+=======================+
      | Input Path            | Input path of source files in HDFS or OBS                                                                                                                                                                                                                                                                              | /user/test            |
      |                       |                                                                                                                                                                                                                                                                                                                        |                       |
      |                       | .. note::                                                                                                                                                                                                                                                                                                              |                       |
      |                       |                                                                                                                                                                                                                                                                                                                        |                       |
      |                       |    You can use macros to define path parameters. For details, see :ref:`Using Macro Definitions in Configuration Items <mrs_01_1153>`.                                                                                                                                                                                 |                       |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Path Filter           | Wildcard for filtering the directories in the input paths of the source files. **Input Path** is not used for filtering. If there are multiple filter conditions, use commas (**,**) to separate them. If the parameter is empty, the directories are not filtered. The regular expression filtering is not supported. | \*                    |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | File Filter           | Wildcard for filtering the file names of the source files. If there are multiple filter conditions, use commas (**,**) to separate them. The value cannot be left blank. The regular expression filtering is not supported.                                                                                            | \*                    |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Encoding Type         | Source file encoding format, for example, UTF-8. This parameter can be set only in text file import.                                                                                                                                                                                                                   | UTF-8                 |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Suffix                | File name extension added to a source file after the source file is imported. If this parameter is empty, no file name extension is added to the source file.                                                                                                                                                          | .log                  |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

   **Setting Data Transformation**

#. Click **Next**. On the displayed **Transform** page, set the transformation operations in the data transformation process. For details about how to select operators and set parameters, see :ref:`Operator Help <mrs_01_1119>` and :ref:`Table 2 <mrs_01_1098__en-us_topic_0000001173470656_table895989011525>`.

   .. _mrs_01_1098__en-us_topic_0000001173470656_table895989011525:

   .. table:: **Table 2** Input and output parameters of the operator

      ================ ============
      Input Type       Output Type
      ================ ============
      CSV File Input   HBase Output
      HTML Input       HBase Output
      Fixed File Input HBase Output
      ================ ============


   .. figure:: /_static/images/en-us_image_0000001349259365.png
      :alt: **Figure 3** Operator operation procedure

      **Figure 3** Operator operation procedure

   **Setting Data Storage Information and Executing the Job**

#. Click **Next**. On the displayed **To** page, set **Storage type** to **HBASE_BULKLOAD** or **HBASE_PUTLIST** based on the actual situation.

   .. table:: **Table 3** Parameter description

      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Storage Type   | Applicable Scenario | Parameter                | Description                                                                                                                                                                                                                              | Example Value |
      +================+=====================+==========================+==========================================================================================================================================================================================================================================+===============+
      | HBASE_BULKLOAD | Large data volume   | HBase Instance           | HBase service instance that Loader selects from all available HBase service instances in the cluster. If the selected HBase service instance is not added to the cluster, the HBase job cannot be run properly.                          | HBase         |
      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      |                |                     | Clear data before import | Indicates whether to clear data in the original table before importing data. **True** indicates clearing data and **False** indicates not to clear data. If you do not set this parameter, the original table is not cleared by default. | true          |
      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      |                |                     | Extractors               | Number of Maps that are started at the same time in a MapReduce task of a data configuration operation. The value must be less than or equal to 3000.                                                                                    | 20            |
      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      |                |                     | Extractor Size           | HBase does not support this parameter. Please set **Extractors**.                                                                                                                                                                        | ``-``         |
      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | HBASE_PUTLIST  | Small data volume   | HBase Instance           | HBase service instance that Loader selects from all available HBase service instances in the cluster. If the selected HBase service instance is not added to the cluster, the HBase job cannot be run properly.                          | HBase         |
      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      |                |                     | Extractors               | Number of Maps that are started at the same time in a MapReduce task of a data configuration operation. The value must be less than or equal to 3000.                                                                                    | 20            |
      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      |                |                     | Extractor Size           | HBase does not support this parameter. Please set **Extractors**.                                                                                                                                                                        | ``-``         |
      +----------------+---------------------+--------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

#. Click **Save and run** to save and run the job.

   **Checking the Job Execution Result**

#. Go to the Loader web UI. When **Status** is **Succeeded**, the job is complete.


   .. figure:: /_static/images/en-us_image_0000001348740097.png
      :alt: **Figure 4** Viewing job details

      **Figure 4** Viewing job details
