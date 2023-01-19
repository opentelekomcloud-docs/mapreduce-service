:original_name: mrs_01_1092.html

.. _mrs_01_1092:

Typical Scenario: Importing Data from an SFTP Server to Spark
=============================================================

Scenario
--------

Use Loader to import data from an SFTP server to Spark.

Prerequisites
-------------

-  You have obtained the service username and password for creating a Loader job.
-  You have had the permission to access the Spark table specified in the job.
-  You have obtained the username and password of the SFTP server as well as the read permission for the source files on the SFTP server. If file name extension needs to be added after a source file is imported, the user must have the write permission of the source file.
-  No disk space alarm is reported, and the available disk space is sufficient for importing and exporting data.
-  When using Loader to import data from the SFTP server, the input paths and input path subdirectories of the SFTP server and the name of the files in these directories do not contain any of the special characters /"':;.
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


   .. figure:: /_static/images/en-us_image_0000001296219728.png
      :alt: **Figure 2** **Basic Information**

      **Figure 2** **Basic Information**

   a. Set **Name** to the name of the job.
   b. Set **Type** to **Import**.
   c. Set **Group** to the group to which the job belongs. No group is created by default. You need to click **Add** to create a group and click **OK** to save the created group.
   d. Set **Queue** to the Yarn queue that executes the job. The default value is **root.default**.
   e. Set **Priority** to the priority of the Yarn queue that executes the job. The default value is **NORMAL**. The options are **VERY_LOW**, **LOW**, **NORMAL**, **HIGH**, and **VERY_HIGH**.

#. In the **Connection** area, click **Add** to create a connection, set **Connector** to **sftp-connector**, click **Add**, set connection parameters, and click **Test** to verify whether the connection is available. When "Test Success" is displayed, click **OK**. Loader allows multiple SFTP servers to be configured. Click **Add** to add the configuration information of multiple SFTP servers.

   .. table:: **Table 1** Connection parameters

      +------------------------+----------------------------------------+---------------+
      | Parameter              | Description                            | Example Value |
      +========================+========================================+===============+
      | Name                   | Name of the SFTP server connection     | sftpName      |
      +------------------------+----------------------------------------+---------------+
      | SFTP Server IP Address | IP address of the SFTP server          | 10.16.0.1     |
      +------------------------+----------------------------------------+---------------+
      | SFTP Server Port       | Port number of the SFTP server         | 22            |
      +------------------------+----------------------------------------+---------------+
      | SFTP Username          | Username for accessing the SFTP server | root          |
      +------------------------+----------------------------------------+---------------+
      | SFTP Password          | Password for accessing the SFTP server | xxxx          |
      +------------------------+----------------------------------------+---------------+
      | SFTP Public Key        | Public key of the SFTP server          | OdDt/yn...etM |
      +------------------------+----------------------------------------+---------------+

   .. note::

      When multiple SFTP servers are configured, the data in the specified directories of the servers is imported to Spark.

   **Setting Data Source Information**

#. Click **Next**. On the displayed **From** page, set the data source information.

   .. table:: **Table 2** Parameter description

      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter             | Description                                                                                                                                                                                                                                                                                                                                                                                                       | Example Value         |
      +=======================+===================================================================================================================================================================================================================================================================================================================================================================================================================+=======================+
      | Input Path            | Input path or name of the source file on an SFTP server. If multiple SFTP server IP addresses are configured for the connector, you can set this parameter to multiple input paths separated with semicolons (;). Ensure that the number of input paths is the same as that of SFTP servers configured for the connector.                                                                                         | /opt/tempfile;/opt    |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | .. note::                                                                                                                                                                                                                                                                                                                                                                                                         |                       |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       |    You can use macros to define path parameters. For details, see :ref:`Using Macro Definitions in Configuration Items <mrs_01_1153>`.                                                                                                                                                                                                                                                                            |                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | File Split Type       | Indicates whether to split source files by file name or size. The files obtained after the splitting are used as the input files of each Map in the MapReduce task for data import.                                                                                                                                                                                                                               | FILE                  |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | -  **FILE**: indicates that the source file is split by file. That is, each Map processes one or multiple complete files, the same source file cannot be allocated to different Maps, and the source file directory structure is retained after data import.                                                                                                                                                      |                       |
      |                       | -  **SIZE**: indicates that the source file is split by size. That is, each Map processes input files of a certain size, and a source file can be divided and processed by multiple Maps. After data is stored in the output directory, the number of saved files is the same as that of Maps. The file name format is **import_part\_**\ *xxxx*, where *xxxx* is a unique random number generated by the system. |                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Filter Type           | File filter condition. This parameter is used when **Path Filter** or **File Filter** is set.                                                                                                                                                                                                                                                                                                                     | WILDCARD              |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | -  **WILDCARD**: indicates using a wildcard.                                                                                                                                                                                                                                                                                                                                                                      |                       |
      |                       | -  **REGEX**: indicates using a regular expression.                                                                                                                                                                                                                                                                                                                                                               |                       |
      |                       | -  If the parameter is not set, a wildcard is used by default.                                                                                                                                                                                                                                                                                                                                                    |                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Path Filter           | Wildcard or regular expression for filtering the directories in the input path of the source files. This parameter is used when **Filter Type** is set. **Input Path** is not used for filtering. Use semicolons (;) to separate the path filters on multiple servers and use commas (,) to separate the filter conditions of each server. If this parameter is left empty, directories are not filtered.         | 1*,2*;1\*             |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | -  **?** matches a single character.                                                                                                                                                                                                                                                                                                                                                                              |                       |
      |                       | -  **\*** indicates multiple characters.                                                                                                                                                                                                                                                                                                                                                                          |                       |
      |                       | -  Adding **^** before the condition indicates negated filtering, that is, file filtering.                                                                                                                                                                                                                                                                                                                        |                       |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | For example, when **Filter type** is set to **WILDCARD**, set the parameter to **\***; when **Filter type** is set to **REGEX**, set the parameter to **\\\\.\***.                                                                                                                                                                                                                                                |                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | File Filter           | Wildcard or regular expression for filtering the file names of the source files. This parameter is used when **Filter Type** is set. Use semicolons (;) to separate the path filters on multiple servers and use commas (,) to separate the filter conditions of each server. This parameter cannot be left blank.                                                                                                | \*.txt,*.csv;*.txt    |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | -  **?** matches a single character.                                                                                                                                                                                                                                                                                                                                                                              |                       |
      |                       | -  **\*** indicates multiple characters.                                                                                                                                                                                                                                                                                                                                                                          |                       |
      |                       | -  Adding **^** before the condition indicates negated filtering, that is, file filtering.                                                                                                                                                                                                                                                                                                                        |                       |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | For example, when **Filter type** is set to **WILDCARD**, set the parameter to **\***; when **Filter type** is set to **REGEX**, set the parameter to **\\\\.\***.                                                                                                                                                                                                                                                |                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Encoding Type         | Source file encoding format, for example, UTF-8 and GBK. This parameter can be set only in text file import.                                                                                                                                                                                                                                                                                                      | UTF-8                 |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Suffix                | File name extension added to a source file after the source file is imported. If this parameter is empty, no file name extension is added to the source file. This parameter is valid only when the data source is a file system. You are advised to set this parameter in incremental data import.                                                                                                               | .log                  |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | For example, if the parameter is set to **.txt** and the source file is **test-loader.csv**, the source file name is **test-loader.csv.txt** after export.                                                                                                                                                                                                                                                        |                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Compression           | Indicates whether to enable compressed transmission when SFTP is used to export data.                                                                                                                                                                                                                                                                                                                             | true                  |
      |                       |                                                                                                                                                                                                                                                                                                                                                                                                                   |                       |
      |                       | -  The value **true** indicates that compression is enabled.                                                                                                                                                                                                                                                                                                                                                      |                       |
      |                       | -  The value **false** indicates that compression is disabled.                                                                                                                                                                                                                                                                                                                                                    |                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

   **Setting Data Transformation**

#. Click **Next**. On the displayed **Transform** page, set the transformation operations in the data transformation process. For details about how to select operators and set parameters, see :ref:`Operator Help <mrs_01_1119>` and :ref:`Table 3 <mrs_01_1092__en-us_topic_0000001173949520_table895989011525>`.

   .. _mrs_01_1092__en-us_topic_0000001173949520_table895989011525:

   .. table:: **Table 3** Input and output parameters of the operator

      ================ ============
      Input Type       Output Type
      ================ ============
      CSV File Input   Spark Output
      HTML Input       Spark Output
      Fixed File Input Spark Output
      ================ ============


   .. figure:: /_static/images/en-us_image_0000001295740296.png
      :alt: **Figure 3** Operator operation procedure

      **Figure 3** Operator operation procedure

   **Setting Data Storage Information and Executing the Job**

#. Click **Next**. On the displayed **To** page, set **Storage type** to **SPARK**.

   .. table:: **Table 4** Parameter description

      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter             | Description                                                                                                                                                                                                                                         | Example Value         |
      +=======================+=====================================================================================================================================================================================================================================================+=======================+
      | Output Directory      | Specifies the directory for storing data imported into Spark.                                                                                                                                                                                       | /opt/tempfile         |
      |                       |                                                                                                                                                                                                                                                     |                       |
      |                       | .. note::                                                                                                                                                                                                                                           |                       |
      |                       |                                                                                                                                                                                                                                                     |                       |
      |                       |    You can use macros to define path parameters. For details, see :ref:`Using Macro Definitions in Configuration Items <mrs_01_1153>`.                                                                                                              |                       |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Extractors            | Number of Maps that are started at the same time in a MapReduce task of a data configuration operation. The value must be less than or equal to 3000. You are advised to set the parameter to the maximum number of connections on the SFTP server. | 20                    |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Extractor Size        | Spark does not support this parameter. Please set **Extractors**.                                                                                                                                                                                   | ``-``                 |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

#. Click **Save and run** to save and run the job.

   **Checking the Job Execution Result**

#. Go to the Loader web UI. When **Status** is **Succeeded**, the job is complete.


   .. figure:: /_static/images/en-us_image_0000001349139813.png
      :alt: **Figure 4** Viewing job details

      **Figure 4** Viewing job details
