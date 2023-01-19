:original_name: mrs_01_24172.html

.. _mrs_01_24172:

Typical Scenario: Importing Data from a Relational Database to ClickHouse
=========================================================================

Scenario
--------

This section describes how to use Loader to import data from a relational database to ClickHouse using MySQL as an example.

Prerequisites
-------------

-  You have obtained the service username and password for creating a Loader job.
-  You have created a ClickHouse table, and you have operation permissions on the table during job execution.
-  You have obtained the user name and password of the MySQL database.
-  No disk space alarm is reported, and the available disk space is sufficient for importing and exporting data.
-  If a configured task requires the Yarn queue function, the user must be authorized with related Yarn queue permission.
-  The user who configures a task must obtain execution permission on the task and obtain usage permission on the related connection of the task.
-  Before the operation, perform the following steps:

   #. Obtain the MySQL client JAR file (for example, **mysqlclient-5.8.1.jar**) from the MySQL database installation path and save it to the following directory on the active and standby Loader nodes: **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib**.

   #. Obtain the **clickhouse-jdbc-*.jar** file from the ClickHouse installation directory and save it in the **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib** directory on the active and standby Loader nodes.

   #. Run the following command on the active and standby nodes as user **root** to modify the permission:

      **cd** **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib**

      **chown omm:wheel** *JAR* *file name*

      **chmod 600** *JAR* *file name*

   #. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Loader** > **More** > **Restart Service** and enter the system administrator password to restart the Loader service.

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


   .. figure:: /_static/images/en-us_image_0000001296219364.png
      :alt: **Figure 2** Basic Information

      **Figure 2** Basic Information

   a. Set **Name** to the name of the job.
   b. Set **Type** to **Import**.
   c. Set **Group** to the group to which the job belongs. No group is created by default. You need to click **Add** to create a group and click **OK** to save the created group.
   d. Set **Queue** to the Yarn queue that executes the job. The default value is **root.default**.
   e. Set **Priority** to the priority of the Yarn queue that executes the job. The default value is **NORMAL**. The options are **VERY_LOW**, **LOW**, **NORMAL**, **HIGH**, and **VERY_HIGH**.

#. In the **Connection** area, click **Add** to create a connection, set **Connector** to **generic-jdbc-connector** or a dedicated database connector (oracle-connector, oracle-partition-connector, or mysql-fastpath-connector), set connection parameters, and click **Test** to verify whether the connection is available. When "Test Success" is displayed, click **OK**.

   .. note::

      -  For connection to relational databases, general database connectors (generic-jdbc-connector) or dedicated database connectors (oracle-connector, oracle-partition-connector, and mysql-fastpath-connector) are available. However, compared with general database connectors, dedicated database connectors perform better in data import and export because they are optimized for specific database types.
      -  When mysql-fastpath-connector is used, the **mysqldump** and **mysqlimport** commands of MySQL must be available on NodeManager nodes, and the MySQL client version to which the two commands belong must be compatible with the MySQL server version. If the two commands are unavailable or the versions are incompatible, install the MySQL client applications and tools following the instructions at http://dev.mysql.com/doc/refman/5.7/en/linux-installation-rpm.html.

   .. table:: **Table 1** generic-jdbc-connector connection parameters

      +------------------------+------------------------------------------+-------------------------------------------------------------------------------+
      | Parameter              | Description                              | Example                                                                       |
      +========================+==========================================+===============================================================================+
      | Name                   | Name of a relational database connection | mysql_test                                                                    |
      +------------------------+------------------------------------------+-------------------------------------------------------------------------------+
      | JDBC Driver Class      | Name of a JDBC driver class              | com.mysql.jdbc.Driver                                                         |
      +------------------------+------------------------------------------+-------------------------------------------------------------------------------+
      | JDBC Connection String | JDBC connection string                   | jdbc:mysql://10.254.144.102:3306/test?useUnicode=true&characterEncoding=UTF-8 |
      +------------------------+------------------------------------------+-------------------------------------------------------------------------------+
      | Username               | Username for connecting to the database  | root                                                                          |
      +------------------------+------------------------------------------+-------------------------------------------------------------------------------+
      | Password               | Password for connecting to the database  | xxxx                                                                          |
      +------------------------+------------------------------------------+-------------------------------------------------------------------------------+

**Setting Data Source Information**

4. Click **Next**. On the displayed **From** page, configure the data source information. Currently, only **Table name** is supported.

   .. table:: **Table 2** Parameter description

      +-----------------------+--------------------------------------------------------------+---------+
      | Parameter             | Description                                                  | Example |
      +=======================+==============================================================+=========+
      | Schema name           | Schema name of the specified database                        | public  |
      +-----------------------+--------------------------------------------------------------+---------+
      | Table name            | Table name                                                   | test    |
      +-----------------------+--------------------------------------------------------------+---------+
      | Table column names    | Names of the columns to be imported                          | id,name |
      +-----------------------+--------------------------------------------------------------+---------+
      | Need partition column | Currently, only the unspecified partition mode is supported. | false   |
      +-----------------------+--------------------------------------------------------------+---------+

**Setting Data Transformation**

5. Click **Next**. On the displayed **Transform** page, set the transformation operations in the data transformation process. For details about how to select operators and set parameters, see :ref:`Operator Help <mrs_01_1119>` and :ref:`Table 3 <mrs_01_24172__en-us_topic_0000001173471080_table92181845553>`.

   .. _mrs_01_24172__en-us_topic_0000001173471080_table92181845553:

   .. table:: **Table 3** Input and output parameters of the operator

      =========== =================
      Input Type  Output Type
      =========== =================
      MySQL Input ClickHouse Output
      =========== =================

   Drag **Table Input** to the grid, double-click **Table Input**, and select **autoRecognition**, as shown in :ref:`Figure 3 <mrs_01_24172__en-us_topic_0000001173471080_fig1621911456515>`.

   .. _mrs_01_24172__en-us_topic_0000001173471080_fig1621911456515:

   .. figure:: /_static/images/en-us_image_0000001391556190.png
      :alt: **Figure 3** Operator input

      **Figure 3** Operator input

   Drag **ClickHouse Output** to the grid, double-click **Table Output**, and select **associate** or manually edit the table to correspond to the input table, as shown in :ref:`Figure 4 <mrs_01_24172__en-us_topic_0000001173471080_fig721910459510>`.

   .. _mrs_01_24172__en-us_topic_0000001173471080_fig721910459510:

   .. figure:: /_static/images/en-us_image_0000001349259037.png
      :alt: **Figure 4** Operator output

      **Figure 4** Operator output

**Setting Data Storage Information and Executing the Job**

6. Click **Next**. On the displayed **To** page, set **Storage type** to **CLICKHOUSE**.

   .. table:: **Table 4** Parameter description

      +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter                | Description                                                                                                        | Example               |
      +==========================+====================================================================================================================+=======================+
      | Storage type             | Select **CLICKHOUSE**.                                                                                             | ``-``                 |
      +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
      | ClickHouse instance      | Select **ClickHouse**.                                                                                             | ``-``                 |
      +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Clear data before import | Select **true** or **false**.                                                                                      | true                  |
      |                          |                                                                                                                    |                       |
      |                          | .. note::                                                                                                          |                       |
      |                          |                                                                                                                    |                       |
      |                          |    ClickHouse distributed tables do not support clearing data before import. You need to manually clear the table. |                       |
      +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+

7. Click **Save and Run** to save and run the job.

**Checking the Job Execution Result**

8. Go to the Loader web UI. When **Status** is **Succeeded**, the job is complete.


   .. figure:: /_static/images/en-us_image_0000001349139449.png
      :alt: **Figure 5** Viewing job details

      **Figure 5** Viewing job details

9. On the ClickHouse client, check whether the data in the ClickHouse table is the same as that in the MySql table.
