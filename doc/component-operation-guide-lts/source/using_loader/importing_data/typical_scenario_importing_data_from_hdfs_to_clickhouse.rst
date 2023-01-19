:original_name: mrs_01_24173.html

.. _mrs_01_24173:

Typical Scenario: Importing Data from HDFS to ClickHouse
========================================================

Scenario
--------

Use Loader to import data from HDFS to ClickHouse.

Prerequisites
-------------

-  You have obtained the service username and password for creating a Loader job.
-  You have had the permission to access the HDFS directories and data involved in job execution.
-  You have created a ClickHouse table, and you have operation permissions on the table during job execution.
-  No disk space alarm is reported, and the available disk space is sufficient for importing and exporting data.
-  When using Loader to import data from HDFS, the input paths and input path subdirectories of HDFS and the name of the files in these directories do not contain any of the special characters **/"':;**.
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


   .. figure:: /_static/images/en-us_image_0000001349139741.png
      :alt: **Figure 2** Basic Information

      **Figure 2** Basic Information

   a. Set **Name** to the name of the job.
   b. Set **Type** to **Import**.
   c. Set **Group** to the group to which the job belongs. No group is created by default. You need to click **Add** to create a group and click **OK** to save the created group.
   d. Set **Queue** to the Yarn queue that executes the job. The default value is **root.default**.
   e. Set **Priority** to the priority of the Yarn queue that executes the job. The default value is **NORMAL**. The options are **VERY_LOW**, **LOW**, **NORMAL**, **HIGH**, and **VERY_HIGH**.

#. In the **Connection** area, click **Add** to create a connection, set **Connector** to **hdfs-connector**, set connection parameters, and click **Test** to verify whether the connection is available. When "Test Success" is displayed, click **OK**.

**Setting Data Source Information**

4. Click **Next**. On the displayed **From** page, set the data source information.

   .. table:: **Table 1** Parameter description

      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter             | Description                                                                                                                                                                                                                                                                                                            | Example               |
      +=======================+========================================================================================================================================================================================================================================================================================================================+=======================+
      | Input Path            | Input path of source files in HDFS                                                                                                                                                                                                                                                                                     | /user/test            |
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

5. Click **Next**. On the displayed **Transform** page, set the transformation operations in the data transformation process. For details about how to select operators and set parameters, see :ref:`Operator Help <mrs_01_1119>` and :ref:`Table 2 <mrs_01_24173__en-us_topic_0000001173471260_table4607134162717>`.

   .. _mrs_01_24173__en-us_topic_0000001173471260_table4607134162717:

   .. table:: **Table 2** Input and output parameters of the operator

      ============== =================
      Input Type     Output Type
      ============== =================
      CSV File Input ClickHouse Output
      ============== =================


   .. figure:: /_static/images/en-us_image_0000001388071772.png
      :alt: **Figure 3** Operator operation procedure

      **Figure 3** Operator operation procedure

**Setting Data Storage Information and Executing the Job**

6. Click **Next**. On the displayed **To** page, set **Storage type** to **CLICKHOUSE** based on the actual situation.

   .. table:: **Table 3** Parameter description

      +-----------------+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
      | Storage Type    | Parameter                | Description                                                                                                                                                                                                                         | Example         |
      +=================+==========================+=====================================================================================================================================================================================================================================+=================+
      | CLICKHOUSE      | ClickHouse instance      | ClickHouse service instance that Loader selects from all available ClickHouse service instances in the cluster. If the selected ClickHouse service instance is not added to the cluster, the ClickHouse job cannot be run properly. | ClickHouse      |
      +-----------------+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
      |                 | Clear data before import | Whether to clear data in the original table before importing data **true** indicates clearing data and **false** indicates not to clear data. If you do not set this parameter, the original table is not cleared by default.       | false           |
      |                 |                          |                                                                                                                                                                                                                                     |                 |
      |                 |                          | .. note::                                                                                                                                                                                                                           |                 |
      |                 |                          |                                                                                                                                                                                                                                     |                 |
      |                 |                          |    ClickHouse distributed tables do not support clearing data before import. You need to manually clear the table.                                                                                                                  |                 |
      +-----------------+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
      |                 | Extractors               | Number of Maps that are started at the same time in a MapReduce task of a data configuration operation. The value must be less than or equal to 3000.                                                                               | 20              |
      +-----------------+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
      |                 | Extractor size           | ClickHouse does not support this parameter. Please set **Extractors**.                                                                                                                                                              | ``-``           |
      +-----------------+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
      |                 | Number                   | Number of Map tasks.                                                                                                                                                                                                                | ``-``           |
      +-----------------+--------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+

7. Click **Save and Run** to save and run the job.

**Checking the Job Execution Result**

8. Go to the Loader web UI. When **Status** is **Succeeded**, the job is complete.


   .. figure:: /_static/images/en-us_image_0000001296219656.png
      :alt: **Figure 4** Viewing job details

      **Figure 4** Viewing job details

9. On the ClickHouse client, check whether the data in the ClickHouse table is the same as that imported from HDFS.
