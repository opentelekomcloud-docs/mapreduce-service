:original_name: mrs_01_0405.html

.. _mrs_01_0405:

Destination Link Configurations of Loader Jobs
==============================================

Overview
--------

When Loader jobs save data to different storage locations, a destination link needs to be selected and the link properties need to be configured.

obs-connector
-------------

.. table:: **Table 1** Destination link properties of **obs-connector**

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                            |
   +===================================+========================================================================================================================+
   | Bucket Name                       | OBS file system for storing final data.                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Output Directory                  | Directory for storing final data in the file system. A directory must be specified.                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | File Format                       | Loader supports the following file formats of data stored in OBS:                                                      |
   |                                   |                                                                                                                        |
   |                                   | -  **CSV_FILE**: Specifies a text file. When the destination link is a database link, only the text file is supported. |
   |                                   | -  **BINARY_FILE**: Specifies binary files excluding text files.                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Line Separator                    | Identifier of each line end of final data                                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Field Separator                   | Identifier of each field end of final data                                                                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Encoding Type                     | Text encoding type of final data. It takes effect on text files only.                                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+

generic-jdbc-connector
----------------------

.. table:: **Table 2** Destination link properties of **generic-jdbc-connector**

   =========== =======================================
   Parameter   Description
   =========== =======================================
   Schema Name Name of the database storing final data
   Table       Name of the table saving final data
   =========== =======================================

ftp-connector or sftp-connector
-------------------------------

.. table:: **Table 3** Destination link properties of **ftp-connector** or **sftp-connector**

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                           |
   +===================================+=======================================================================================================================================================================+
   | Output Directory                  | Directory for storing final data in the file server. A directory must be specified.                                                                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Format                       | Loader supports the following file formats of data stored in the file server:                                                                                         |
   |                                   |                                                                                                                                                                       |
   |                                   | -  **CSV_FILE**: Specifies a text file. When the destination link is a database link, only the text file is supported.                                                |
   |                                   | -  **BINARY_FILE**: Specifies binary files excluding text files.                                                                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Line Separator                    | Identifier of each line end of final data                                                                                                                             |
   |                                   |                                                                                                                                                                       |
   |                                   | .. note::                                                                                                                                                             |
   |                                   |                                                                                                                                                                       |
   |                                   |    If FTP or SFTP serves as a destination link and **File Format** is set to **BINARY_FILE**, the value of **Line Separator** in the advanced properties is invalid.  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Field Separator                   | Identifier of each field end of final data                                                                                                                            |
   |                                   |                                                                                                                                                                       |
   |                                   | .. note::                                                                                                                                                             |
   |                                   |                                                                                                                                                                       |
   |                                   |    If FTP or SFTP serves as a destination link and **File Format** is set to **BINARY_FILE**, the value of **Field Separator** in the advanced properties is invalid. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Encoding Type                     | Text encoding type of final data. It takes effect on text files only.                                                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

hbase-connector
---------------

.. table:: **Table 4** Destination link properties of **hbase-connector**

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                    |
   +===================================+================================================================================================================================================+
   | Table Name                        | Name of the HBase table saving final data. You can query and select it on the interface.                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Method                            | Data can be imported to an HBase table using either **BULKLOAD** or **PUTLIST**.                                                               |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Clear Data Before Import          | Whether to clear data in the destination HBase table. Options are as follows:                                                                  |
   |                                   |                                                                                                                                                |
   |                                   | -  **True**: Clean up data in the table.                                                                                                       |
   |                                   | -  **False**: Do not clean up data in the table. If you select **False**, an error is reported during job running if data exists in the table. |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_01_0405__s0e7a49c2520c498aa9e3d9fa84325e2e:

hdfs-connector
--------------

.. table:: **Table 5** Destination link properties of **hdfs-connector**

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                    |
   +===================================+================================================================================================================================================================+
   | Output Directory                  | Directory for storing final data in HDFS. A directory must be specified.                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Format                       | Loader supports the following file formats of data stored in HDFS:                                                                                             |
   |                                   |                                                                                                                                                                |
   |                                   | -  **CSV_FILE**: Specifies a text file. When the destination link is a database link, only the text file is supported.                                         |
   |                                   | -  **BINARY_FILE**: Specifies binary files excluding text files.                                                                                               |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Compression Codec                 | Compression mode used when a file is saved to HDFS. The following modes are supported: **NONE**, **DEFLATE**, **GZIP**, **BZIP2**, **LZ4**, and **SNAPPY**.    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Overwrite                         | How to process files in the output directory when files are imported to HDFS. Options are as follows:                                                          |
   |                                   |                                                                                                                                                                |
   |                                   | -  **True**: Clean up files in the directory and import new files by default.                                                                                  |
   |                                   | -  **False**: Do not clean up files. If files exist in the output directory, job running fails.                                                                |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Line Separator                    | Identifier of each line end of final data                                                                                                                      |
   |                                   |                                                                                                                                                                |
   |                                   | .. note::                                                                                                                                                      |
   |                                   |                                                                                                                                                                |
   |                                   |    If HDFS serves as a destination link and **File Format** is set to **BINARY_FILE**, the value of **Line Separator** in the advanced properties is invalid.  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Field Separator                   | Identifier of each field end of final data                                                                                                                     |
   |                                   |                                                                                                                                                                |
   |                                   | .. note::                                                                                                                                                      |
   |                                   |                                                                                                                                                                |
   |                                   |    If HDFS serves as a destination link and **File Format** is set to **BINARY_FILE**, the value of **Field Separator** in the advanced properties is invalid. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+

hive-connector
--------------

.. table:: **Table 6** Destination link properties of **hive-connector**

   +-----------+---------------------------------------------------------------------------------------------+
   | Parameter | Description                                                                                 |
   +===========+=============================================================================================+
   | Database  | Name of the Hive database storing final data. You can query and select it on the interface. |
   +-----------+---------------------------------------------------------------------------------------------+
   | Table     | Name of the Hive table saving final data. You can query and select it on the interface.     |
   +-----------+---------------------------------------------------------------------------------------------+
