:original_name: mrs_01_1109.html

.. _mrs_01_1109:

Typical Scenario: Exporting Data from Hive to a Relational Database
===================================================================

Scenario
--------

Use Loader to export data from Hive to a relational database.

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

   #. Run the following command on the active and standby nodes as user root to modify the permission:

      **cd ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.2.2/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib**

      **chown omm:wheel** *JAR package name*

      **chmod 600** *JAR package name*

   #. Log in to FusionInsight Manager. Choose **Cluster** > *Name of the desired cluster* > **Service** > **Loader** > **More** > **Restart**. Enter the password of the system administrator to restart the Loader service.

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


   .. figure:: /_static/images/en-us_image_0000001348739761.png
      :alt: **Figure 2** **Basic Information**

      **Figure 2** **Basic Information**

   a. Set **Name** to the name of the job.
   b. Set **Type** to **Export**.
   c. Set **Group** to the group to which the job belongs. No group is created by default. You need to click **Add** to create a group and click **OK** to save the created group.
   d. Set **Queue** to the Yarn queue that executes the job. The default value is **root.default**.
   e. Set **Priority** to the priority of the Yarn queue that executes the job. The default value is **NORMAL**. The options are **VERY_LOW**, **LOW**, **NORMAL**, **HIGH**, and **VERY_HIGH**.

#. In the **Connection** area, click **Add** to create a connection, set **Connector** to **generic-jdbc-connector** or dedicated database connector (oracle-connector, oracle-partition-connector or mysql-fastpath-connector), set connection parameters, and click **Test** to verify whether the connection is available. When "**Test Success**" is displayed, click **OK**.

   .. note::

      -  For connection to relational databases, general database connectors (generic-jdbc-connector) or dedicated database connectors (oracle-connector, oracle-partition-connector, and mysql-fastpath-connector) are available. However, compared with general database connectors, dedicated database connectors perform better in data import and export because they are optimized for specific database types.
      -  When **mysql-fastpath-connector** is used, the **mysqldump** and **mysqlimport** commands of MySQL must be available on NodeManagers, and the MySQL client version to which the two commands belong must be compatible with the MySQL server version. If the two commands are unavailable or the versions are incompatible, see http://dev.mysql.com/doc/refman/5.7/en/linux-installation-rpm.html. Install the MySQL client applications and tools.

   .. table:: **Table 1** **generic-jdbc-connector** connection parameters

      +----------------------------+-------------------------------------------------------------------------+------------------------------------------+
      | Parameter                  | Description                                                             | Example Value                            |
      +============================+=========================================================================+==========================================+
      | Name                       | Specifies the name of a relational database connection.                 | dbName                                   |
      +----------------------------+-------------------------------------------------------------------------+------------------------------------------+
      | JDBC Driver Class          | Specifies the name of a Java database connectivity (JDBC) driver class. | oracle.jdbc.driver.OracleDriver          |
      +----------------------------+-------------------------------------------------------------------------+------------------------------------------+
      | JDBC Connection String     | Specifies the JDBC connection string.                                   | jdbc:oracle:thin:@//10.16.0.1:1521/oradb |
      +----------------------------+-------------------------------------------------------------------------+------------------------------------------+
      | Username                   | Specifies the username for connecting to the database.                  | omm                                      |
      +----------------------------+-------------------------------------------------------------------------+------------------------------------------+
      | Password                   | Specifies the password for connecting to the database.                  | xxxx                                     |
      +----------------------------+-------------------------------------------------------------------------+------------------------------------------+
      | JDBC Connection Properties | JDBC connection attribute. Click **Add** to manually add the attribute. | -  Name: socketTimeout                   |
      |                            |                                                                         | -  Value: 20                             |
      |                            | -  Name: connection attribute name                                      |                                          |
      |                            | -  Value: connection attribute value                                    |                                          |
      +----------------------------+-------------------------------------------------------------------------+------------------------------------------+

   **Setting Data Source Information**

#. Click **Next**. On the displayed **From** page, set **Source type** to **HIVE**.

   .. table:: **Table 2** Data source parameters

      +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter     | Description                                                                                                                                                                                                            | Example Value |
      +===============+========================================================================================================================================================================================================================+===============+
      | Hive instance | Specifies the Hive service instance that Loader selects from all available Hive service instances in the cluster. If the selected Hive service instance is not added to the cluster, the Hive job cannot run properly. | hive          |
      +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Quantity      | Specifies the number of maps that are started at the same time in a MapReduce job of a data configuration operation. The value must be less than or equal to 3000.                                                     | 20            |
      +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   **Setting Data Transformation**

#. Click **Next**. On the displayed **Transform** page, set the transformation operations in the data transformation process. For details about how to select operators and set parameters, see :ref:`Operator Help <mrs_01_1119>` and :ref:`Table 3 <mrs_01_1109__en-us_topic_0000001219350451_table895989011525>`.

   .. _mrs_01_1109__en-us_topic_0000001219350451_table895989011525:

   .. table:: **Table 3** Setting the input and output parameters of the operator

      ========== ============
      Input Type Export Type
      ========== ============
      Hive input Table output
      ========== ============


   .. figure:: /_static/images/en-us_image_0000001349259041.png
      :alt: **Figure 3** Operator operation procedure

      **Figure 3** Operator operation procedure

   **Setting Data Storage Information and Executing the Job**

#. Click **Next**. On the displayed **To** page, set the data storage mode.

   .. table:: **Table 4** Parameter description

      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter             | Description                                                                                                                                                                                                                                                                                                                             | Example Value         |
      +=======================+=========================================================================================================================================================================================================================================================================================================================================+=======================+
      | Schema name           | Specifies the database schema name.                                                                                                                                                                                                                                                                                                     | dbo                   |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Table name            | Specifies the name of a database table that is used to save the final data of the transmission.                                                                                                                                                                                                                                         | test                  |
      |                       |                                                                                                                                                                                                                                                                                                                                         |                       |
      |                       | .. note::                                                                                                                                                                                                                                                                                                                               |                       |
      |                       |                                                                                                                                                                                                                                                                                                                                         |                       |
      |                       |    Table names can be defined using macros. For details, see :ref:`Using Macro Definitions in Configuration Items <mrs_01_1153>`.                                                                                                                                                                                                       |                       |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Temporary table       | Specifies the name of a temporary database table that is used to save temporary data during the transmission. The fields in the table must be the same as those in the database specified by **Table name**.                                                                                                                            | tmp_test              |
      |                       |                                                                                                                                                                                                                                                                                                                                         |                       |
      |                       | .. note::                                                                                                                                                                                                                                                                                                                               |                       |
      |                       |                                                                                                                                                                                                                                                                                                                                         |                       |
      |                       |    A temporary table is used to prevent dirty data from being generated in the destination table when data is exported to the database. Data is migrated from the temporary table to the destination table only after all data is successfully written to the temporary table. Using temporary tables increases the job execution time. |                       |
      +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

#. Click **Save and run** to save and run the job.

   **Checking the Job Execution Result**

#. Go to the **Loader WebUI**. When **Status** is **Succeeded**, the job is complete.


   .. figure:: /_static/images/en-us_image_0000001389307342.png
      :alt: **Figure 4** Viewing job

      **Figure 4** Viewing job
