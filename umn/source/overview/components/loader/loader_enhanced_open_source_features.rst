:original_name: mrs_08_00173.html

.. _mrs_08_00173:

Loader Enhanced Open Source Features
====================================

Loader Enhanced Open-Source Feature: Data Import and Export
-----------------------------------------------------------

Loader is developed based on Sqoop. In addition to the Sqoop functions, Loader has the following enhanced features:

-  Provides data conversion functions.
-  Supports GUI-based configuration conversion.
-  Imports data from an SFTP/FTP server to HDFS/OBS.
-  Imports data from an SFTP/FTP server to an HBase table.
-  Imports data from an SFTP/FTP server to a Phoenix table.
-  Imports data from an SFTP/FTP server to a Hive table.
-  Exports data from HDFS/OBS to an SFTP/FTP server.
-  Exports data from an HBase table to an SFTP/FTP server.
-  Exports data from a Phoenix table to an SFTP/FTP server.
-  Imports data from a relational database to an HBase table.
-  Imports data from a relational database to a Phoenix table.
-  Imports data from a relational database to a Hive table.
-  Exports data from an HBase table to a relational database.
-  Exports data from a Phoenix table to a relational database.
-  Imports data from an Oracle partitioned table to HDFS/OBS.
-  Imports data from an Oracle partitioned table to an HBase table.
-  Imports data from an Oracle partitioned table to a Phoenix table.
-  Imports data from an Oracle partitioned table to a Hive table.
-  Exports data from HDFS/OBS to an Oracle partitioned table.
-  Exports data from HBase to an Oracle partitioned table.
-  Exports data from a Phoenix table to an Oracle partitioned table.
-  Imports data from HDFS to an HBase table, a Phoenix table, and a Hive table in the same cluster.
-  Exports data from an HBase table and a Phoenix table to HDFS/OBS in the same cluster.
-  Imports data to an HBase table and a Phoenix table by using **bulkload** or **put list**.
-  Imports all types of files from an SFTP/FTP server to HDFS. The open source component Sqoop can import only text files.
-  Exports all types of files from HDFS/OBS to an SFTP server. The open source component Sqoop can export only text files and SequenceFile files.
-  Supports file coding format conversion during file import and export. The supported coding formats include all formats supported by Java Development Kit (JDK).
-  Retains the original directory structure and file names during file import and export.
-  Supports file combination during file import and export. For example, if a large number of files are to be imported, these files can be combined into *n* files (*n* can be configured).
-  Supports file filtering during file import and export. The filtering rules support wildcards and regular expressions.
-  Supports batch import and export of ETL tasks.
-  Supports query by page and key word and group management of ETL tasks.
-  Provides floating IP addresses for external components.
