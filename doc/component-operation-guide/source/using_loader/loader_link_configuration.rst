:original_name: mrs_01_0402.html

.. _mrs_01_0402:

Loader Link Configuration
=========================

This section applies to versions earlier than MRS 3.x.

Overview
--------

Loader supports the following links. This section describes configurations of each link.

-  obs-connector
-  generic-jdbc-connector
-  ftp-connector or sftp-connector
-  hbase-connector, hdfs-connector, or hive-connector

OBS Link
--------

An OBS link is a data exchange channel between Loader and OBS. :ref:`Table 1 <mrs_01_0402__t6fd2dae9f81e4309906aec5754a1bf77>` describes the configuration parameters.

.. _mrs_01_0402__t6fd2dae9f81e4309906aec5754a1bf77:

.. table:: **Table 1** **obs-connector** configuration

   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                |
   +===================================+============================================================================================+
   | Name                              | Name of a Loader connection                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | OBS Server                        | Enter an OBS endpoint. The common format is **OBS.\ Region.\ DomainName**.                 |
   |                                   |                                                                                            |
   |                                   | Run the following command to query the endpoints of OBS:                                   |
   |                                   |                                                                                            |
   |                                   | **cat /opt/Bigdata/apache-tomcat-7.0.78/webapps/web/WEB-INF/classes/cloud-obs.properties** |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | Port                              | Specifies the port for accessing OBS data. The default value is **443**.                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | Access Key                        | AK for a user to access OBS                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | Security Key                      | SK corresponding to AK                                                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------+

Relational Database Link
------------------------

A relational database link is a data exchange channel between Loader and a relational database. :ref:`Table 2 <mrs_01_0402__t938c9f27e7004e4dbcca6c3c0ba5d8a2>` describes the configuration parameters.

.. note::

   Some parameters are hidden by default. They appear only after you click **Show Senior Parameter**.

.. _mrs_01_0402__t938c9f27e7004e4dbcca6c3c0ba5d8a2:

.. table:: **Table 2** **generic-jdbc-connector** configuration

   +---------------+----------------------------------------------------------------------------+
   | Parameter     | Description                                                                |
   +===============+============================================================================+
   | Name          | Name of a Loader link                                                      |
   +---------------+----------------------------------------------------------------------------+
   | Database Type | Data types supported by Loader links: **ORACLE**, **MYSQL**, and **MPPDB** |
   +---------------+----------------------------------------------------------------------------+
   | Host          | Database access address, which can be an IP address or domain name.        |
   +---------------+----------------------------------------------------------------------------+
   | Port          | Port for accessing the database                                            |
   +---------------+----------------------------------------------------------------------------+
   | Database      | Name of the database saving data                                           |
   +---------------+----------------------------------------------------------------------------+
   | Username      | Username for accessing the database                                        |
   +---------------+----------------------------------------------------------------------------+
   | Password      | Password of the user Use the actual password.                              |
   +---------------+----------------------------------------------------------------------------+

.. table:: **Table 3** Senior parameter configuration

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Description                                                                                                                                                                                    |
   +=======================+================================================================================================================================================================================================+
   | Fetch Size            | A maximum volume of data obtained during each database access                                                                                                                                  |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Connection Properties | Drive properties exclusive to the database link supported by databases of different types, for example, **autoReconnect** of MYSQL. If you want to define the drive properties, click **Add**. |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Identifier Enclose    | Delimiter for reserving keywords in the database SQL. Delimiters defined in different databases vary.                                                                                          |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_01_0402__s73ada4f9d7e94890a00a2c7a90856ba6:

File Server Link
----------------

File server links include FTP and SFTP links and serve as a data exchange channel between Loader and a file server. :ref:`Table 4 <mrs_01_0402__t15d36a6a4bda4efe8b7dd5d4abb70019>` describes the configuration parameters.

.. _mrs_01_0402__t15d36a6a4bda4efe8b7dd5d4abb70019:

.. table:: **Table 4** **ftp-connector** or **sftp-connector** configuration

   +-----------------------------------+-------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                   |
   +===================================+===============================================================================+
   | Name                              | Name of a Loader link                                                         |
   +-----------------------------------+-------------------------------------------------------------------------------+
   | Hostname/IP                       | Enter the file server access address, which can be a host name or IP address. |
   +-----------------------------------+-------------------------------------------------------------------------------+
   | Port                              | Port for accessing the file server.                                           |
   |                                   |                                                                               |
   |                                   | -  Use port **21** for FTP.                                                   |
   |                                   | -  Use port **22** for SFTP.                                                  |
   +-----------------------------------+-------------------------------------------------------------------------------+
   | Username                          | Username for logging in to the file server                                    |
   +-----------------------------------+-------------------------------------------------------------------------------+
   | Password                          | Password of the user                                                          |
   +-----------------------------------+-------------------------------------------------------------------------------+

MRS Cluster Link
----------------

MRS cluster links include HBase, HDFS, and Hive links and serve as a data exchange channel between Loader and HBase, HDFS, or Hive.

When configuring an MRS cluster link, set the name, select a connector, for example, **hbase-connector**, **hdfs-connector**, or **hive-connector**, and save the settings.
