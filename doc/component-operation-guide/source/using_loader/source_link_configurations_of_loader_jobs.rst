:original_name: mrs_01_0404.html

.. _mrs_01_0404:

Source Link Configurations of Loader Jobs
=========================================

Overview
--------

When Loader jobs obtain data from different data sources, a link corresponding to a data source type needs to be selected and the link properties need to be configured.

This section applies to versions earlier than MRS 3.x.

.. _mrs_01_0404__sdd455438f59c455d868736ad52d1097c:

obs-connector
-------------

.. table:: **Table 1** Data source link properties of **obs-connector**

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                               |
   +===================================+===========================================================================================================================================================+
   | Bucket Name                       | OBS file system for storing source data.                                                                                                                  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Source Directory/File             | Actual storage form of source data. It can be either all data files in a directory or a single data file contained in the file system.                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Format                       | Loader supports the following file formats of data stored in OBS:                                                                                         |
   |                                   |                                                                                                                                                           |
   |                                   | -  **CSV_FILE**: Specifies a text file. When the destination link is a database link, only the text file is supported.                                    |
   |                                   | -  **BINARY_FILE**: Specifies binary files excluding text files.                                                                                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Line Separator                    | Identifier of each line end of source data                                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Field Separator                   | Identifier of each field end of source data                                                                                                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Encoding Type                     | Text encoding type of source data. It takes effect on text files only.                                                                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Split Type                   | The following types are supported:                                                                                                                        |
   |                                   |                                                                                                                                                           |
   |                                   | -  **File**: The number of files is assigned to a map task by the total number of files. The calculation formula is **Total number of files/Extractors**. |
   |                                   | -  **Size**: A file size is assigned to a map task by the total file size. The calculation formula is **Total file size/Extractors**.                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

generic-jdbc-connector
----------------------

.. table:: **Table 2** Data source link properties of **generic-jdbc-connector**

   +-------------------+-------------------------------------------------------------------------------------------+
   | Parameter         | Description                                                                               |
   +===================+===========================================================================================+
   | Schema/Tablespace | Name of the database storing source data. You can query and select it on the interface.   |
   +-------------------+-------------------------------------------------------------------------------------------+
   | Table Name        | Data table storing the source data. You can query and select it on the interface.         |
   +-------------------+-------------------------------------------------------------------------------------------+
   | Partition Column  | If multiple columns need to be read, use this column to split the result and obtain data. |
   +-------------------+-------------------------------------------------------------------------------------------+
   | Where Clause      | Query statement used when accessing the database                                          |
   +-------------------+-------------------------------------------------------------------------------------------+

.. _mrs_01_0404__s033d5edc10164032b9ea23d01081beae:

ftp-connector or sftp-connector
-------------------------------

.. table:: **Table 3** Data source link properties of **ftp-connector** or **sftp-connector**

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                      |
   +===================================+==================================================================================================================================================================+
   | Source Directory/File             | Actual storage form of source data. It can be either all data files in a directory or single data file contained in the file server.                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Format                       | Loader supports the following file formats of data stored in the file server:                                                                                    |
   |                                   |                                                                                                                                                                  |
   |                                   | -  **CSV_FILE**: Specifies a text file. When the destination link is a database link, only the text file is supported.                                           |
   |                                   | -  **BINARY_FILE**: Specifies binary files excluding text files.                                                                                                 |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Line Separator                    | Identifier of each line end of source data                                                                                                                       |
   |                                   |                                                                                                                                                                  |
   |                                   | .. note::                                                                                                                                                        |
   |                                   |                                                                                                                                                                  |
   |                                   |    If FTP or SFTP serves as a source link and **File Format** is set to **BINARY_FILE**, the value of **Line Separator** in the advanced properties is invalid.  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Field Separator                   | Identifier of each field end of source data                                                                                                                      |
   |                                   |                                                                                                                                                                  |
   |                                   | .. note::                                                                                                                                                        |
   |                                   |                                                                                                                                                                  |
   |                                   |    If FTP or SFTP serves as a source link and **File Format** is set to **BINARY_FILE**, the value of **Field Separator** in the advanced properties is invalid. |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Encoding Type                     | Text encoding type of source data. It takes effect on text files only.                                                                                           |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Split Type                   | The following types are supported:                                                                                                                               |
   |                                   |                                                                                                                                                                  |
   |                                   | -  **File**: The number of files is assigned to a map task by the total number of files. The calculation formula is **Total number of files/Extractors**.        |
   |                                   | -  **Size**: A file size is assigned to a map task by the total file size. The calculation formula is **Total file size/Extractors**.                            |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

hbase-connector
---------------

.. table:: **Table 4** Data source link properties of **hbase-connector**

   ========== ===============================
   Parameter  Description
   ========== ===============================
   Table Name HBase table storing source data
   ========== ===============================

hdfs-connector
--------------

.. table:: **Table 5** Data source link properties of **hdfs-connector**

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                               |
   +===================================+===========================================================================================================================================================+
   | Source Directory/File             | Actual storage form of source data. It can be either all data files in a directory or single data file contained in HDFS.                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Format                       | Loader supports the following file formats of data stored in HDFS:                                                                                        |
   |                                   |                                                                                                                                                           |
   |                                   | -  **CSV_FILE**: Specifies a text file. When the destination link is a database link, only the text file is supported.                                    |
   |                                   | -  **BINARY_FILE**: Specifies binary files excluding text files.                                                                                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Line Separator                    | Identifier of each line end of source data                                                                                                                |
   |                                   |                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                 |
   |                                   |                                                                                                                                                           |
   |                                   |    If HDFS serves as a source link and **File Format** is set to **BINARY_FILE**, the value of **Line Separator** in the advanced properties is invalid.  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Field Separator                   | Identifier of each field end of source data                                                                                                               |
   |                                   |                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                 |
   |                                   |                                                                                                                                                           |
   |                                   |    If HDFS serves as a source link and **File Format** is set to **BINARY_FILE**, the value of **Field Separator** in the advanced properties is invalid. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Split Type                   | The following types are supported:                                                                                                                        |
   |                                   |                                                                                                                                                           |
   |                                   | -  **File**: The number of files is assigned to a map task by the total number of files. The calculation formula is **Total number of files/Extractors**. |
   |                                   | -  **Size**: A file size is assigned to a map task by the total file size. The calculation formula is **Total file size/Extractors**.                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

hive-connector
--------------

.. table:: **Table 6** Data source link properties of **hive-connector**

   +---------------+--------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                      |
   +===============+==================================================================================================+
   | Database Name | Name of the Hive database storing the data source. You can query and select it on the interface. |
   +---------------+--------------------------------------------------------------------------------------------------+
   | Table         | Name of the Hive table storing the data source. You can query and select it on the interface.    |
   +---------------+--------------------------------------------------------------------------------------------------+
