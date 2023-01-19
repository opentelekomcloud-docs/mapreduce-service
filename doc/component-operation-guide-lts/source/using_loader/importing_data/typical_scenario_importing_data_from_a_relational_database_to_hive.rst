:original_name: mrs_01_1096.html

.. _mrs_01_1096:

Typical Scenario: Importing Data from a Relational Database to Hive
===================================================================

Scenario
--------

Use Loader to import data from a relational database to Hive.

Prerequisites
-------------

-  You have obtained the service username and password for creating a Loader job.
-  You have had the permission to access the Hive tables that are used during job execution.
-  You have obtained the username and password of the relational database.
-  No disk space alarm is reported, and the available disk space is sufficient for importing and exporting data.
-  If a configured task requires the Yarn queue function, the user must be authorized with related Yarn queue permission.
-  The user who configures a task must obtain execution permission on the task and obtain usage permission on the related connection of the task.
-  Before the operation, perform the following steps:

   #. Obtain the JAR package of the relational database driver and save it to the following directory on the active and standby Loader nodes: **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib**.

   #. Run the following command on the active and standby nodes as user **root** to modify the permission:

      **cd** **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib**

      **chown omm:wheel** *JAR package name*

      **chmod 600** *JAR package name*

   #. Log in to FusionInsight Manager. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader** > **More** > **Restart Service**. Enter the password of the system administrator to restart the Loader service.

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


   .. figure:: /_static/images/en-us_image_0000001296059896.png
      :alt: **Figure 2** **Basic Information**

      **Figure 2** **Basic Information**

   a. Set **Name** to the name of the job.
   b. Set **Type** to **Import**.
   c. Set **Group** to the group to which the job belongs. No group is created by default. You need to click **Add** to create a group and click **OK** to save the created group.
   d. Set **Queue** to the Yarn queue that executes the job. The default value is **root.default**.
   e. Set **Priority** to the priority of the Yarn queue that executes the job. The default value is **NORMAL**. The options are **VERY_LOW**, **LOW**, **NORMAL**, **HIGH**, and **VERY_HIGH**.

#. In the **Connection** area, click **Add** to create a connection, set **Connector** to **generic-jdbc-connector** or a dedicated database connector (oracle-connector, oracle-partition-connector, or mysql-fastpath-connector), set connection parameters, and click **Test** to verify whether the connection is available. When "Test Success" is displayed, click **OK**.

   .. note::

      -  For connection to relational databases, general database connectors (generic-jdbc-connector) or dedicated database connectors (oracle-connector, oracle-partition-connector, and mysql-fastpath-connector) are available. However, compared with general database connectors, dedicated database connectors perform better in data import and export because they are optimized for specific database types.
      -  When mysql-fastpath-connector is used, the **mysqldump** and **mysqlimport** commands of MySQL must be available on NodeManager nodes, and the MySQL client version to which the two commands belong must be compatible with the MySQL server version. If the two commands are unavailable or the versions are incompatible, install the MySQL client applications and tools following the instructions at http://dev.mysql.com/doc/refman/5.7/en/linux-installation-rpm.html.

   .. table:: **Table 1** **generic-jdbc-connector** connection parameters

      +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
      | Parameter                  | Description                                                                                                                                                                    | Example Value                            |
      +============================+================================================================================================================================================================================+==========================================+
      | Name                       | Name of a relational database connection                                                                                                                                       | dbName                                   |
      +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
      | JDBC Driver Class          | Name of a JDBC driver class                                                                                                                                                    | oracle.jdbc.driver.OracleDriver          |
      +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
      | JDBC Connection String     | JDBC connection string                                                                                                                                                         | jdbc:oracle:thin:@//10.16.0.1:1521/oradb |
      +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
      | Username                   | Username for connecting to the database                                                                                                                                        | omm                                      |
      +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
      | Password                   | Password for connecting to the database                                                                                                                                        | xxxx                                     |
      +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
      | JDBC Connection Properties | JDBC connection attribute. Click **Add** to manually add the attribute.                                                                                                        | -  Name: **socketTimeout**               |
      |                            |                                                                                                                                                                                | -  Value: **20**                         |
      |                            | -  Name: connection attribute name                                                                                                                                             |                                          |
      |                            | -  Value: connection attribute value                                                                                                                                           |                                          |
      |                            |                                                                                                                                                                                |                                          |
      |                            |    .. important::                                                                                                                                                              |                                          |
      |                            |                                                                                                                                                                                |                                          |
      |                            |       NOTICE:                                                                                                                                                                  |                                          |
      |                            |       If a general connector is used to connect to the MySQL database and there a large amount of data, you need to set **useCursorFetch=true** in the JDBC connection string. |                                          |
      +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+

   **Setting Data Source Information**

#. Click **Next**. On the displayed **From** page, set the data source information.

   .. table:: **Table 2** Parameter description

      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+
      | Parameter                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Example Value                           |
      +=======================================+===================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=========================================+
      | Schema Name                           | Database schema name. This parameter exists in the **Table name** schema.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | dbo                                     |
      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+
      | Table Name                            | Database table name. This parameter exists in the **Table name** schema.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | test                                    |
      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+
      | SQL Statement                         | SQL statement for Loader to query data to be imported in **Table SQL statement** mode. The SQL statement requires the query condition **WHERE ${CONDITIONS}**. Without this condition, the SQL statement cannot be run properly. An example SQL statement is as follows: **select \* from TABLE WHERE A>B and ${CONDITIONS}**. If **Table column names** is set, the column specified by **Table column names** will replace the column queried in the SQL statement. This parameter cannot be set when **Schema name** or **Table name** is set. | select \* from test where ${CONDITIONS} |
      |                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                         |
      |                                       | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                         |
      |                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                         |
      |                                       |    You can use macros to define SQL Where statements. For details, see :ref:`Using Macro Definitions in Configuration Items <mrs_01_1153>`.                                                                                                                                                                                                                                                                                                                                                                                                       |                                         |
      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+
      | Table Column Names                    | Table columns whose content is to be imported by Loader. Use commas (**,**) to separate multiple fields.                                                                                                                                                                                                                                                                                                                                                                                                                                          | ``-``                                   |
      |                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                         |
      |                                       | If the parameter is not set, all the columns are imported and the **Select \*** order is used as the column location.                                                                                                                                                                                                                                                                                                                                                                                                                             |                                         |
      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+
      | Partition Column Name                 | Database table column based on which to-be-imported data is determined. This parameter is used for partitioning in a Map job. You are advised to configure the primary key field.                                                                                                                                                                                                                                                                                                                                                                 | id                                      |
      |                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                         |
      |                                       | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                         |
      |                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                         |
      |                                       |    -  A partition column must have an index. If no index exists, do not specify a partition column. If a partition column without an index is specified, the database server disk I/O will be busy, the access of other services to the database will be affected, and the import will take a long period.                                                                                                                                                                                                                                        |                                         |
      |                                       |    -  In multiple fields with indexes, select the field that has the most discrete value as the partition column. A partition column that is not discrete may result in load imbalance when multiple MapReduce jobs are imported.                                                                                                                                                                                                                                                                                                                 |                                         |
      |                                       |    -  The sorting rules of partition columns must be case-sensitive. Otherwise, data may be lost during data import.                                                                                                                                                                                                                                                                                                                                                                                                                              |                                         |
      |                                       |    -  You are not advised to select fields of the float or double type for the partition column. Otherwise, the records containing the minimum and maximum values of the partition column may fail to be imported due to precision issues.                                                                                                                                                                                                                                                                                                        |                                         |
      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+
      | Nulls in Partition Column             | Indicates whether to process records whose values are null in database table columns.                                                                                                                                                                                                                                                                                                                                                                                                                                                             | true                                    |
      |                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                         |
      |                                       | -  **true**: Records whose values are null are processed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                         |
      |                                       | -  **false**: Records whose values are not null are processed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                         |
      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+
      | Whether to Specify a Partition Column | Indicates whether to specify a partition column.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | true                                    |
      +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+

   **Setting Data Transformation**

#. Click **Next**. On the displayed **Transform** page, set the transformation operations in the data transformation process. For details about how to select operators and set parameters, see :ref:`Operator Help <mrs_01_1119>` and :ref:`Table 3 <mrs_01_1096__en-us_topic_0000001219350435_table895989011525>`.

   .. _mrs_01_1096__en-us_topic_0000001219350435_table895989011525:

   .. table:: **Table 3** Input and output parameters of the operator

      =========== ===========
      Input Type  Output Type
      =========== ===========
      Table input Hive output
      =========== ===========


   .. figure:: /_static/images/en-us_image_0000001349059741.png
      :alt: **Figure 3** Operator operation procedure

      **Figure 3** Operator operation procedure

   **Setting Data Storage Information and Executing the Job**

#. Click **Next**. On the displayed **To** page, set **Storage type** to **HIVE**.

   .. table:: **Table 4** Parameter description

      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter             | Description                                                                                                                                                                                                                                         | Example Value         |
      +=======================+=====================================================================================================================================================================================================================================================+=======================+
      | Output Directory      | Directory for storing data imported into Hive.                                                                                                                                                                                                      | /opt/tempfile         |
      |                       |                                                                                                                                                                                                                                                     |                       |
      |                       | .. note::                                                                                                                                                                                                                                           |                       |
      |                       |                                                                                                                                                                                                                                                     |                       |
      |                       |    You can use macros to define path parameters. For details, see :ref:`Using Macro Definitions in Configuration Items <mrs_01_1153>`.                                                                                                              |                       |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Extractors            | Number of Maps that are started at the same time in a MapReduce task of a data configuration operation. The value must be less than or equal to 3000. You are advised to set the parameter to the maximum number of connections on the SFTP server. | 20                    |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Extractor Size        | Hive does not support this parameter. Please set **Extractors**.                                                                                                                                                                                    | ``-``                 |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

#. Click **Save and run** to save and run the job.

   **Checking the Job Execution Result**

#. Go to the Loader web UI. When **Status** is **Succeeded**, the job is complete.


   .. figure:: /_static/images/en-us_image_0000001349259197.png
      :alt: **Figure 4** Viewing job details

      **Figure 4** Viewing job details
