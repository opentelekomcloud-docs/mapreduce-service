:original_name: mrs_01_1101.html

.. _mrs_01_1101:

Loader Exporting Data Overview
==============================

Description
-----------

Loader is an extract, transform, and load (ETL) tool for exchanging data and files between MRS and relational databases and file systems. You can use the Loader to export data or files from MRS to the relational databases or file systems.

Loader supports the following data export modes:

-  Exporting data from HDFS/OBS to an SFTP server
-  Exporting data from HDFS/OBS to a relational database
-  Exporting data from HBase to an SFTP server
-  Exporting data from HBase to a relational database
-  Exporting data from Phoenix tables to an SFTP server
-  Exporting data from Phoenix tables to a relational database
-  Exporting data from Hive to an SFTP server
-  Exporting Data from Hive to a Relational Database
-  Exporting data from HBase to HDFS/OBS in the same cluster

The MRS needs to connect to the data source to exchange data and files with the external data source. The following connectors are used to configure connection parameters for different types of data sources:

-  generic-jdbc-connector: relational database connector
-  hdfs-connector: HDFS data source connector
-  oracle-connector: specifies a dedicated connector for Oracle databases. **row_id** serves as partition columns. Compared with generic-jdbc-connector, Map tasks are more evenly distributed on oracle-connector, and whether the partition columns have created indexes does not affect oracle-connector.
-  mysql-fastpath-connector: specifies a dedicated connector for MySQL databases. Data is imported and exported by using the mysqldump and mysqlimport tools of MySQL. Compared with generic-jdbc-connector, the data import and export speed is faster.
-  sftp-connector: SFTP data source connector
-  oracle-partition-connector: connector that supports the Oracle partition feature, which is used to optimize the import and export of Oracle partition tables.

.. note::

   -  You are advised to deploy the SFTP server, database server, and Loader into separate subnets to ensure secure data export.

   -  For connection to relational databases, general database connectors (generic-jdbc-connector) or dedicated database connectors (oracle-connector, oracle-partition-connector, and mysql-fastpath-connector) are available. However, compared with general database connectors, dedicated database connectors performs better in data import and export because it is optimized for specific database types.

   -  When **mysql-fastpath-connector** is used, the **mysqldump** and **mysqlimport** commands of MySQL must be available on NodeManagers, and the MySQL client version to which the two commands belong must be compatible with the MySQL server version. If the two commands are unavailable or the versions are incompatible, see http://dev.mysql.com/doc/refman/5.7/en/linux-installation-rpm.html. Install the MySQL client applications and tools.

   -  When oracle-connector is used, the connection user must be granted the select permission on the following system catalogs or views:

      dba_tab_partitions, dba_constraints, dba_tables, dba_segments, v$version, dba_objects, v$instance, dba_extents, dba_tab_partitions and dba_tab_subpartitions.

   -  When oracle-partition-connector is used, the connection user must be granted the select permission on the following system catalogs: dba_objects and dba_extents.

Export Process
--------------

A data export job can be executed in the Loader WebUI. :ref:`Figure 1 <mrs_01_1101__en-us_topic_0000001173949254_f60328404ddcf4db8953cedb2adec89d6>` shows the export process.

.. _mrs_01_1101__en-us_topic_0000001173949254_f60328404ddcf4db8953cedb2adec89d6:

.. figure:: /_static/images/en-us_image_0000001296059720.png
   :alt: **Figure 1** Export process

   **Figure 1** Export process

Loader jobs can also be updated and executed using shell scripts. In this mode, the Loader client that has been installed needs to be configured.
