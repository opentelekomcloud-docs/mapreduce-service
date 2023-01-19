:original_name: mrs_01_0953.html

.. _mrs_01_0953:

Using HDFS Colocation to Store Hive Tables
==========================================

Scenario
--------

HDFS Colocation is the data location control function provided by HDFS. The HDFS Colocation API stores associated data or data on which associated operations are performed on the same storage node. Hive supports the HDFS Colocation function. When Hive tables are created, after the locator information is set for table files, data files of related tables are stored on the same storage node when data is inserted into tables using the insert statement (other data import modes are not supported). This ensures convenient and efficient data computing among associated tables. The supported table formats are only TextFile and RCFile.

Procedure
---------

#. Log in to the node where the client is installed as a client installation user.

#. Run the following command to switch to the client installation directory, for example, **opt/client**:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user:

   **kinit** *MRS username*

#. Create the *groupid* through the HDFS API.

   **hdfs colocationadmin -createGroup -groupId <groupid> -locatorIds <locatorid1>,\ <locatorid2>,\ <locatorid3>**

   .. note::

      In the preceding command, *<groupid>* indicates the name of the created group. The group created in this example contains three locators. You can define the number of locators as required.

      For details about group ID creation and HDFS Colocation, see HDFS description.

#. Run the following command to log in to the Hive client:

   **beeline**

#. Enable Hive to use colocation.

   Assume that **table_name1** and **table_name2** are associated with each other. Run the following statements to create them:

   **CREATE TABLE <[db_name.]table_name1>[(col_name data_type , ...)] [ROW FORMAT <row_format>] [STORED AS <file_format>] TBLPROPERTIES("groupId"=" <group> ","locatorId"="<locator1>");**

   **CREATE TABLE <[db_name.]table_name2> [(col_name data_type , ...)] [ROW FORMAT <row_format>] [STORED AS <file_format>] TBLPROPERTIES("groupId"=" <group> ","locatorId"="<locator1>");**

   After data is inserted into **table_name1** and **table_name2** using the insert statement, data files of **table_name1** and **table_name2** are distributed to the same storage position in the HDFS, facilitating associated operations among the two tables.
