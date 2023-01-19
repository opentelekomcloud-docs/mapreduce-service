:original_name: mrs_01_1087.html

.. _mrs_01_1087:

Overview
========

Description
-----------

Loader is an ETL tool that enables MRS to exchange data and files with external data sources, such as relational databases, SFTP servers, and FTP servers. It allows data or files to be imported from relational databases or file systems to MRS.

Loader supports the following data import modes:

-  Importing data from a relational database to HDFS or OBS
-  Importing data from a relational database to HBase
-  Importing data from a relational database to Phoenix tables
-  Importing data from a relational database to Hive tables
-  Importing data from an SFTP server to HDFS or OBS
-  Importing data from an SFTP server to HBase
-  Importing data from an SFTP server to Phoenix tables
-  Importing data from an SFTP server to Hive tables
-  Importing data from an FTP server to HDFS or OBS
-  Importing data from an FTP server to HBase
-  Importing data from an FTP server to Phoenix tables
-  Importing data from an FTP server to Hive tables
-  Importing data from HDFS or OBS to HBase in the same cluster

MRS needs to connect to an external data source to exchange data and files with the data source. The following connectors are used to configure connection parameters for different types of data sources:

-  generic-jdbc-connector: relational database connector
-  ftp-connector: FTP data source connector
-  hdfs-connector: HDFS data source connector
-  oracle-connector: dedicated connector for Oracle databases. **row_id** serves as partition columns. Compared with generic-jdbc-connector, Map jobs are more evenly distributed on oracle-connector, and whether indexes have been created for the partition columns does not matter.
-  mysql-fastpath-connector: dedicated connector for MySQL databases. Data is imported and exported by using the mysqldump and mysqlimport tools of MySQL. Compared with generic-jdbc-connector, mysql-fastpath-connector delivers a faster data import and export speed.
-  sftp-connector: SFTP data source connector
-  oracle-partition-connector: connector that supports the Oracle partition feature, which is used to optimize the import and export of Oracle partition tables.

.. note::

   -  When an FTP data source connector is used, data is not encrypted. This may result in security risks. You are advised to use an SFTP data source connector.

   -  You are advised to deploy the SFTP server, FTP server, database server, and Loader into separate subnets to ensure secure data import.

   -  For connection to relational databases, general database connectors (generic-jdbc-connector) or dedicated database connectors (oracle-connector, oracle-partition-connector, and mysql-fastpath-connector) are available. However, compared with general database connectors, dedicated database connectors perform better in data import and export because they are optimized for specific database types.

   -  When mysql-fastpath-connector is used, the **mysqldump** and **mysqlimport** commands of MySQL must be available on NodeManager nodes, and the MySQL client version to which the two commands belong must be compatible with the MySQL server version. If the two commands are unavailable or the versions are incompatible, install the MySQL client applications and tools following the instructions at http://dev.mysql.com/doc/refman/5.7/en/linux-installation-rpm.html.

   -  When oracle-connector is used, the connection user must be granted the select permission on the following system catalogs or views:

      dba_tab_partitions, dba_constraints, dba_tables, dba_segments, v$version, dba_objects, v$instance, SYS_CONTEXT, dba_extents, and dba_tab_subpartitions

   -  When oracle-partition-connector is used, the connection user must be granted the select permission on the following system catalogs: dba_objects and dba_extents.

Import Process
--------------

You can import data on the Loader web UI. :ref:`Figure 1 <mrs_01_1087__en-us_topic_0000001219029709_f7d1e5fcc8b5e46729bfc5fdfb897c502>` shows the data import process.

.. _mrs_01_1087__en-us_topic_0000001219029709_f7d1e5fcc8b5e46729bfc5fdfb897c502:

.. figure:: /_static/images/en-us_image_0000001296059864.png
   :alt: **Figure 1** Import process

   **Figure 1** Import process

You can also use shell scripts to update and run Loader jobs. To use this method, you need to configure the installed Loader client.
