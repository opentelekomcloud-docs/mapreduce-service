:original_name: mrs_01_1416.html

.. _mrs_01_1416:

CarbonData Data Migration
=========================

Scenario
--------

If you want to rapidly migrate CarbonData data from a cluster to another one, you can use the CarbonData backup and restoration commands. This method does not require data import in the target cluster, reducing required migration time.

Prerequisites
-------------

The Spark2x client has been installed in a directory, for example, **/opt/client**, in two clusters. The source cluster is cluster A, and the target cluster is cluster B.

Procedure
---------

#. Log in to the node where the client is installed in cluster A as a client installation user.

#. Run the following commands to configure environment variables:

   **source /opt/ficlient/bigdata_env**

   **source /opt/ficlient/Spark2x/component_env**

#. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, skip user authentication.

   **kinit** *carbondatauser*

   *carbondatauser* indicates the user of the original data. That is, the user has the read and write permissions for the tables.

#. Run the following command to connect to the database and check the location for storing table data on HDFS:

   **spark-beeline**

   **desc formatted** *Name of the table containing the original data*\ **;**

   **Location** in the displayed information indicates the directory where the data file resides.

#. Log in to the node where the client is installed in cluster B as a client installation user and configure the environment variables:

   **source /opt/ficlient/bigdata_env**

   **source /opt/ficlient/Spark2x/component_env**

#. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, skip user authentication.

   **kinit** *carbondatauser2*

   *carbondatauser2* indicates the user that uploads data.

#. Run the **spark-beeline** command to connect to the database.

#. Does the database that maps to the original data exist?

   -  If yes, go to :ref:`9 <mrs_01_1416__en-us_topic_0000001219230605_lb95e9d29c6fc469a8375f190f4136467>`.
   -  If no, create a database with the same name and go to :ref:`9 <mrs_01_1416__en-us_topic_0000001219230605_lb95e9d29c6fc469a8375f190f4136467>`.

#. .. _mrs_01_1416__en-us_topic_0000001219230605_lb95e9d29c6fc469a8375f190f4136467:

   Copy the original data from the HDFS directory in cluster A to the HDFS directory in cluster B.

   When uploading data in cluster B, ensure that the upload directory has the directories with the same names as the database and table in the original directory and the upload user has the permission to write data to the upload directory. After the data is uploaded, the user has the permission to read and write the data.

   For example, if the original data is stored in **/user/carboncadauser/warehouse/db1/tb1**, the data can be stored in **/user/carbondatauser2/warehouse/db1/tb1** in the new cluster.

#. .. _mrs_01_1416__en-us_topic_0000001219230605_laf7ce95fc3cc4ab2a96640541690ed30:

   In the client environment of cluster B, run the following command to generate the metadata associated with the table corresponding to the original data in Hive:

   **REFRESH TABLE** *$dbName.$tbName*\ **;**

   *$dbName* indicates the database name, and *$tbName* indicates the table name.

#. If the original table contains an index table, perform :ref:`9 <mrs_01_1416__en-us_topic_0000001219230605_lb95e9d29c6fc469a8375f190f4136467>` and :ref:`10 <mrs_01_1416__en-us_topic_0000001219230605_laf7ce95fc3cc4ab2a96640541690ed30>` to migrate the index table directory from cluster A to cluster B.

#. Run the following command to register an index table for the CarbonData table (skip this step if no index table is created for the original table):

   **REGISTER INDEX TABLE** *$tableName* ON *$maintable*;

   *$tableName* indicates the index table name, and *$maintable* indicates the table name.
