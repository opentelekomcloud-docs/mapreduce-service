:original_name: mrs_01_0961.html

.. _mrs_01_0961:

Using Hive to Read Data in a Relational Database
================================================

Scenario
--------

Hive allows users to create external tables to associate with other relational databases. External tables read data from associated relational databases and support Join operations with other tables in Hive.

Currently, the following relational databases can use Hive to read data:

-  DB2
-  Oracle

.. note::

   This section applies to MRS 3.\ *x* or later clusters.

Prerequisites
-------------

The Hive client has been installed.

Procedure
---------

#. Log in to the node where the Hive client is installed as the Hive client installation user .

#. Run the following command to go to the client installation directory:

   **cd** *Client installation directory*

   For example, if the client installation directory is **/opt/client**, run the following command:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Check whether the cluster authentication mode is Security.

   -  If yes, run the following command to authenticate the user:

      **kinit** *Hive service user*

   -  If no, go to :ref:`5 <mrs_01_0961__lad1ae23de6bb407cb136beb10cc94ad2>`.

#. .. _mrs_01_0961__lad1ae23de6bb407cb136beb10cc94ad2:

   Run the following command to upload the driver JAR package of the relational database to be associated to an HDFS directory.

   **hdfs dfs -put** *directory where the JAR package is located* *HDFS directory to which the JAR is uploaded*

   For example, to upload the Oracle driver JAR package in **/opt** to the **/tmp** directory in HDFS, run the following command:

   **hdfs dfs -put /opt/ojdbc6.jar /tmp**

#. Create an external table on the Hive client to associate with the relational database, as shown in the following example.

   .. note::

      If the security mode is used, the user who creates the table must have the **ADMIN** permission. The **ADD JAR** path is subject to the actual path.

      .. code-block::

         -- Example of associating with an Oracle Linux 6 database
         -- In security mode, set the admin permission.
         set role admin;
         -- Upload the driver JAR package of the relational database to be associated. The driver JAR packages vary according to databases.
         ADD JAR hdfs:///tmp/ojdbc6.jar;

         CREATE EXTERNAL TABLE ora_test
         -- The Hive table must have one more column than the database return result. This column is used for paging query.
         (id STRING,rownum string)
         STORED BY 'com.qubitproducts.hive.storage.jdbc.JdbcStorageHandler'
         TBLPROPERTIES (
         -- Relational database table type
         "qubit.sql.database.type" = "ORACLE",
         -- Connect to the URL of the relational database through JDBC. (The URL formats vary according to databases.)
         "qubit.sql.jdbc.url" = "jdbc:oracle:thin:@//10.163.0.1:1521/mydb",
         -- Relational database driver class type
         "qubit.sql.jdbc.driver" = "oracle.jdbc.OracleDriver",
         -- SQL statement queried in the relational database. The result is returned to the Hive table.
         "qubit.sql.query" = "select name from aaa",
         -- (Optional) Match the Hive table columns to the relational database table columns.
         "qubit.sql.column.mapping" = "id=name",
         -- Relational database user
         "qubit.sql.dbcp.username" = "test",
         -- Relational database password
         "qubit.sql.dbcp.password" = "xxx");
