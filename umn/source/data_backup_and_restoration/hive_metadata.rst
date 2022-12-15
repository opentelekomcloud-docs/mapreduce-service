:original_name: mrs_01_0446.html

.. _mrs_01_0446:

Hive Metadata
=============

Backing Up Hive Metadata
------------------------

Hive table data is stored in HDFS. Table data and the metadata of the table data is centrally migrated in directories by HDFS in a unified manner. Metadata of Hive tables can be stored in different types of relational databases (such as MySQL, PostgreSQL, and Oracle) based on cluster configurations. The exported metadata of the Hive tables in this document is the Hive table description stored in the relational database.

The mainstream big data release editions in the industry support Sqoop installation. For on-premises big data clusters of the community version, you can download the Sqoop of the community version for installation. Use Sqoop to decouple the strong dependency between the metadata to be exported and the relational database and export Hive metadata to HDFS and migrate it together with the table data for restoration. The procedure is as follows:

#. Download the Sqoop tool from the source cluster and install it. For details, see http://sqoop.apache.org/.

#. Download the JDBC driver of the relational database to the **$Sqoop_Home/lib** directory.

#. Run the following command to export all Hive metadata tables: All exported data is stored in the **/user/<user_name>/<table_name>** directory on HDFS.

   .. code-block::

      $Sqoop_Home/bin/sqoop import --connect jdbc:<driver_type>://<ip>:<port>/<database> --table <table_name> --username <user> -password <passwd> -m 1

   The following provides description about the parameters in the preceding command.

   -  **$Sqoop_Home**: Sqoop installation directory
   -  **<driver_type>**: Database type
   -  **<ip>**: IP address of the database in the source cluster
   -  **<port>**: Port number of the database in the source cluster
   -  **<table_name>**: Name of the table to be exported
   -  **<user>**: Username
   -  **<passwd>**: User password

Hive Metadata Restoration
-------------------------

Install Sqoop and run the Sqoop command in the destination cluster to import the exported Hive metadata to DBService in the MRS cluster.

.. code-block::

   $Sqoop_Home/bin/sqoop export --connect jdbc:postgresql://<ip>:20051/hivemeta --table <table_name> --username hive -password <passwd> --export-dir <export_from>

The following provides description about the parameters in the preceding command.

-  **$Sqoop_Home**: Sqoop installation directory in the destination cluster
-  **<ip>**: IP address of the database in the destination cluster
-  **<table_name>**: Name of the table to be restored
-  **<passwd>**: Password of user **hive**
-  *<*\ **export_from>**: HDFS address of the metadata in the destination cluster
