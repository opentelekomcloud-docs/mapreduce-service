:original_name: mrs_01_0504.html

.. _mrs_01_0504:

List of Open Source Component Ports
===================================

Common HBase Ports
------------------

The protocol type of all ports in the table is TCP (for MRS 1.6.3 or later).

+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Parameter                      | Default Port           | Default Port                    | Port Description                                                                                                           |
|                                |                        |                                 |                                                                                                                            |
|                                | (MRS 1.6.3 or Earlier) | (Versions Later than MRS 1.6.3) |                                                                                                                            |
+================================+========================+=================================+============================================================================================================================+
| hbase.master.port              | 21300                  | 16000                           | HMaster RPC port. This port is used to connect the HBase client to HMaster.                                                |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | .. note::                                                                                                                  |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | -  Is the port enabled by default during the installation: Yes                                                             |
|                                |                        |                                 | -  Is the port enabled after security hardening: Yes                                                                       |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| hbase.master.info.port         | 21301                  | 16010                           | HMaster HTTPS port. This port is used by the remote web client to connect to the HMaster UI.                               |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | .. note::                                                                                                                  |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | -  Is the port enabled by default during the installation: Yes                                                             |
|                                |                        |                                 | -  Is the port enabled after security hardening: Yes                                                                       |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| hbase.regionserver.port        | 21302                  | 16020                           | RegoinServer (RS) RPC port. This port is used to connect the HBase client to RegionServer.                                 |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | .. note::                                                                                                                  |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | -  Is the port enabled by default during the installation: Yes                                                             |
|                                |                        |                                 | -  Is the port enabled after security hardening: Yes                                                                       |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| hbase.regionserver.info.port   | 21303                  | 16030                           | HTTPS port of the Region server. This port is used by the remote web client to connect to the RegionServer UI.             |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | .. note::                                                                                                                  |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | -  Is the port enabled by default during the installation: Yes                                                             |
|                                |                        |                                 | -  Is the port enabled after security hardening: Yes                                                                       |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| hbase.thrift.info.port         | 21304                  | 9095                            | Thrift Server listening port of Thrift Server                                                                              |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | This port is used for:                                                                                                     |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | Listening when the client is connected                                                                                     |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | .. note::                                                                                                                  |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | -  Is the port enabled by default during the installation: Yes                                                             |
|                                |                        |                                 | -  Is the port enabled after security hardening: Yes                                                                       |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| hbase.regionserver.thrift.port | 21305                  | 9090                            | Thrift Server listening port of RegionServer                                                                               |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | This port is used for:                                                                                                     |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | Listening when the client is connected to the RegionServer                                                                 |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | .. note::                                                                                                                  |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                |                        |                                 |                                                                                                                            |
|                                |                        |                                 | -  Is the port enabled by default during the installation: Yes                                                             |
|                                |                        |                                 | -  Is the port enabled after security hardening: Yes                                                                       |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| hbase.rest.info.port           | 21308                  | 8085                            | Port of the RegionServer RESTServer native web page                                                                        |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| ``-``                          | 21309                  | 21309                           | REST port of RegionServer RESTServer                                                                                       |
+--------------------------------+------------------------+---------------------------------+----------------------------------------------------------------------------------------------------------------------------+

Common HDFS Ports
-----------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| Parameter                  | Default Port           | Default Port                                | Port Description                                                                                                           |
|                            |                        |                                             |                                                                                                                            |
|                            | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later)                        |                                                                                                                            |
+============================+========================+=============================================+============================================================================================================================+
| dfs.namenode.rpc.port      | 25000                  | -  9820 (versions earlier than MRS 3.\ *x*) | NameNode RPC port                                                                                                          |
|                            |                        | -  8020 (MRS 3.\ *x* and later)             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 1. Communication between the HDFS client and NameNode                                                                      |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 2. Connection between the DataNode and NameNode                                                                            |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.namenode.http.port     | 25002                  | 9870                                        | HDFS HTTP port (NameNode)                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 1. Point-to-point NameNode checkpoint operations.                                                                          |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 2. Connecting the remote web client to the NameNode UI                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.namenode.https.port    | 25003                  | 9871                                        | HDFS HTTPS port (NameNode)                                                                                                 |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 1. Point-to-point NameNode checkpoint operations                                                                           |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 2. Connecting the remote web client to the NameNode UI                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.datanode.ipc.port      | 25008                  | 9867                                        | IPC server port of DataNode                                                                                                |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | Connection between the client and DataNode to perform RPC operations.                                                      |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.datanode.port          | 25009                  | 9866                                        | DataNode data transmission port                                                                                            |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 1. Transmitting data from HDFS client from or to the DataNode                                                              |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | 2. Point-to-point DataNode data transmission                                                                               |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.datanode.http.port     | 25010                  | 9864                                        | DataNode HTTP port                                                                                                         |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | Connecting to the DataNode from the remote web client in security mode                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.datanode.https.port    | 25011                  | 9865                                        | HTTPS port of DataNode                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | Connecting to the DataNode from the remote web client in security mode                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.JournalNode.rpc.port   | 25012                  | 8485                                        | RPC port of JournalNode                                                                                                    |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | Client communication to access multiple types of information                                                               |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.journalnode.http.port  | 25013                  | 8480                                        | JournalNode HTTP port                                                                                                      |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | Connecting to the JournalNode from the remote web client in security mode                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| dfs.journalnode.https.port | 25014                  | 8481                                        | HTTPS port of JournalNode                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | Connecting to the JournalNode from the remote web client in security mode                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
| httpfs.http.port           | 25018                  | 14000                                       | Listening port of the HttpFS HTTP server                                                                                   |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | This port is used for:                                                                                                     |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | Connecting to the HttpFS from the remote REST API                                                                          |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | .. note::                                                                                                                  |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                            |                        |                                             |                                                                                                                            |
|                            |                        |                                             | -  Is the port enabled by default during the installation: Yes                                                             |
|                            |                        |                                             | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------+------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+

Common Hive Ports
-----------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+--------------------------+------------------------+----------------------+--------------------------------------------------------------------------------------------------------------------+
| Parameter                | Default Port           | Default Port         | Port Description                                                                                                   |
|                          |                        |                      |                                                                                                                    |
|                          | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                                                    |
+==========================+========================+======================+====================================================================================================================+
| templeton.port           | 21055                  | 9111                 | Port used for WebHCat to provide the REST service                                                                  |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | This port is used for:                                                                                             |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | Communication between the WebHCat client and WebHCat server                                                        |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | -  Is the port enabled by default during the installation: Yes                                                     |
|                          |                        |                      | -  Is the port enabled after security hardening: Yes                                                               |
+--------------------------+------------------------+----------------------+--------------------------------------------------------------------------------------------------------------------+
| hive.server2.thrift.port | 21066                  | 10000                | Port for HiveServer to provide Thrift services                                                                     |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | This port is used for:                                                                                             |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | Communication between the HiveServer and HiveServer client                                                         |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | -  Is the port enabled by default during the installation: Yes                                                     |
|                          |                        |                      | -  Is the port enabled after security hardening: Yes                                                               |
+--------------------------+------------------------+----------------------+--------------------------------------------------------------------------------------------------------------------+
| hive.metastore.port      | 21088                  | 9083                 | Port for MetaStore to provide Thrift services                                                                      |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | This port is used for:                                                                                             |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | Communication between the MetaStore client and MetaStore, that is, communication between HiveServer and MetaStore. |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | -  Is the port enabled by default during the installation: Yes                                                     |
|                          |                        |                      | -  Is the port enabled after security hardening: Yes                                                               |
+--------------------------+------------------------+----------------------+--------------------------------------------------------------------------------------------------------------------+
| hive.server2.webui.port  | ``-``                  | 10002                | Web UI port of Hive                                                                                                |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | This port is used for: HTTPS/HTTP communication between Web requests and the Hive UI server                        |
|                          |                        |                      |                                                                                                                    |
|                          |                        |                      | This port is supported in MRS 1.9.x or later.                                                                      |
+--------------------------+------------------------+----------------------+--------------------------------------------------------------------------------------------------------------------+

Common Hue Ports
----------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+-----------------+------------------------+----------------------+--------------------------------------------------------------------------------+
| Parameter       | Default Port           | Default Port         | Port Description                                                               |
|                 |                        |                      |                                                                                |
|                 | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                |
+=================+========================+======================+================================================================================+
| HTTP_PORT       | 21200                  | 8888                 | Port for Hue to provide HTTPS services                                         |
|                 |                        |                      |                                                                                |
|                 |                        |                      | This port is used to provide web services in HTTPS mode, which can be changed. |
|                 |                        |                      |                                                                                |
|                 |                        |                      | -  Is the port enabled by default during the installation: Yes                 |
|                 |                        |                      | -  Is the port enabled after security hardening: Yes                           |
+-----------------+------------------------+----------------------+--------------------------------------------------------------------------------+

Common Kafka Ports
------------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+-----------------+------------------------+----------------------+-------------------------------------------------------------------------------------------------+
| Parameter       | Default Port           | Default Port         | Port Description                                                                                |
|                 |                        |                      |                                                                                                 |
|                 | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                                 |
+=================+========================+======================+=================================================================================================+
| port            | 21005                  | 9092                 | Port for a broker to receive data and obtain services                                           |
+-----------------+------------------------+----------------------+-------------------------------------------------------------------------------------------------+
| ssl.port        | 21008                  | 9093                 | SSL port used by a broker to receive data and obtain services                                   |
+-----------------+------------------------+----------------------+-------------------------------------------------------------------------------------------------+
| sasl.port       | 21007                  | 21007                | SASL security authentication port provided by a broker, which provides the secure Kafka service |
+-----------------+------------------------+----------------------+-------------------------------------------------------------------------------------------------+
| sasl-ssl.port   | 21009                  | 21009                | Port used by a broker to provide encrypted service based on the SASL and SSL protocols          |
+-----------------+------------------------+----------------------+-------------------------------------------------------------------------------------------------+

Common Loader Ports
-------------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+-------------------+------------------------+----------------------+--------------------------------------------------------------------------------------+
| Parameter         | Default Port           | Default Port         | Port Description                                                                     |
|                   |                        |                      |                                                                                      |
|                   | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                      |
+===================+========================+======================+======================================================================================+
| LOADER_HTTPS_PORT | 21351                  | 21351                | This port is used to provide REST APIs for configuration and running of Loader jobs. |
|                   |                        |                      |                                                                                      |
|                   |                        |                      | -  Is the port enabled by default during the installation: Yes                       |
|                   |                        |                      | -  Is the port enabled after security hardening: Yes                                 |
+-------------------+------------------------+----------------------+--------------------------------------------------------------------------------------+

Common Manager Ports
--------------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+-----------------+------------------------+----------------------------------------------------+----------------------------------------------------------------+
| Parameter       | Default Port           | Default Port                                       | Port Description                                               |
|                 |                        |                                                    |                                                                |
|                 | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or later/Versions Earlier Than MRS 3.x) |                                                                |
+=================+========================+====================================================+================================================================+
| ``-``           | 8080                   | 8080                                               | Port provided by WebService for user access                    |
|                 |                        |                                                    |                                                                |
|                 |                        |                                                    | This port is used to access the web UI over HTTP.              |
|                 |                        |                                                    |                                                                |
|                 |                        |                                                    | -  Is the port enabled by default during the installation: Yes |
|                 |                        |                                                    | -  Is the port enabled after security hardening: Yes           |
+-----------------+------------------------+----------------------------------------------------+----------------------------------------------------------------+
| ``-``           | 28443                  | 28443                                              | Port provided by WebService for user access                    |
|                 |                        |                                                    |                                                                |
|                 |                        |                                                    | This port is used to access the web UI over HTTPS.             |
|                 |                        |                                                    |                                                                |
|                 |                        |                                                    | -  Is the port enabled by default during the installation: Yes |
|                 |                        |                                                    | -  Is the port enabled after security hardening: Yes           |
+-----------------+------------------------+----------------------------------------------------+----------------------------------------------------------------+

Common MapReduce Ports
----------------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| Parameter                              | Default Port           | Default Port         | Port Description                                                                                                           |
|                                        |                        |                      |                                                                                                                            |
|                                        | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                                                            |
+========================================+========================+======================+============================================================================================================================+
| mapreduce.jobhistory.webapp.port       | 26012                  | 19888                | Web HTTP port of the JobHistory server                                                                                     |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | This port is used for: viewing the web page of the JobHistory server                                                       |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | .. note::                                                                                                                  |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | -  Is the port enabled by default during the installation: Yes                                                             |
|                                        |                        |                      | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| mapreduce.jobhistory.port              | 26013                  | 10020                | Port of the JobHistory server                                                                                              |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | This port is used for:                                                                                                     |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | 1. Task data restoration in the MapReduce client                                                                           |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | 2. Obtaining task report in the Job client                                                                                 |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | .. note::                                                                                                                  |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | -  Is the port enabled by default during the installation: Yes                                                             |
|                                        |                        |                      | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| mapreduce.jobhistory.webapp.https.port | 26014                  | 19890                | Web HTTPS port of the JobHistory server                                                                                    |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | This port is used to view the web page of the JobHistory server.                                                           |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | .. note::                                                                                                                  |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | -  Is the port enabled by default during the installation: Yes                                                             |
|                                        |                        |                      | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+

Common Spark Ports
------------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+--------------------------+------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter                | Default Port           | Default Port         | Port Description                                                                                                                                                                                                                                                 |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                                                                                                                                                                                                  |
+==========================+========================+======================+==================================================================================================================================================================================================================================================================+
| hive.server2.thrift.port | 22550                  | 22550                | JDBC thrift port                                                                                                                                                                                                                                                 |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | This port is used for:                                                                                                                                                                                                                                           |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | Socket communication between Spark2.1.0 CLI/JDBC client and server                                                                                                                                                                                               |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | .. note::                                                                                                                                                                                                                                                        |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      |    If **hive.server2.thrift.port** is occupied, an exception indicating that the port is occupied is reported.                                                                                                                                                   |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | -  Is the port enabled by default during the installation: Yes                                                                                                                                                                                                   |
|                          |                        |                      | -  Is the port enabled after security hardening: Yes                                                                                                                                                                                                             |
+--------------------------+------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| spark.ui.port            | 22950                  | 4040                 | Web UI port of JDBC                                                                                                                                                                                                                                              |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | This port is used for: HTTPS/HTTP communication between Web requests and the JDBC Server Web UI server                                                                                                                                                           |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | .. note::                                                                                                                                                                                                                                                        |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      |    The system verifies the port configuration. If the port is invalid, the value of the port plus 1 is used till the calculated value is valid. (A maximum number of 16 attempts are allowed. The number of attempts is specified by **spark.port.maxRetries**.) |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | -  Is the port enabled by default during the installation: Yes                                                                                                                                                                                                   |
|                          |                        |                      | -  Is the port enabled after security hardening: Yes                                                                                                                                                                                                             |
+--------------------------+------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| spark.history.ui.port    | 22500                  | 18080                | JobHistory Web UI port                                                                                                                                                                                                                                           |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | This port is used for: HTTPS/HTTP communication between Web requests and Spark2.1.0 History Server                                                                                                                                                               |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | .. note::                                                                                                                                                                                                                                                        |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      |    The system verifies the port configuration. If the port is invalid, the value of the port plus 1 is used till the calculated value is valid. (A maximum number of 16 attempts are allowed. The number of attempts is specified by **spark.port.maxRetries**.) |
|                          |                        |                      |                                                                                                                                                                                                                                                                  |
|                          |                        |                      | -  Is the port enabled by default during the installation: Yes                                                                                                                                                                                                   |
|                          |                        |                      | -  Is the port enabled after security hardening: Yes                                                                                                                                                                                                             |
+--------------------------+------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Common Storm Ports
------------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+------------------------+------------------------+----------------------+---------------------------------------------------------------------------+
| Parameter              | Default Port           | Default Port         | Port Description                                                          |
|                        |                        |                      |                                                                           |
|                        | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                           |
+========================+========================+======================+===========================================================================+
| nimbus.thrift.port     | 29200                  | 6627                 | Port for Nimbus to provide thrift services                                |
+------------------------+------------------------+----------------------+---------------------------------------------------------------------------+
| supervisor.slots.ports | 29200-29499            | 6700,6701,6702,6703  | Port for receiving service requests that are forwarded from other servers |
+------------------------+------------------------+----------------------+---------------------------------------------------------------------------+
| logviewer.https.port   | 29248                  | 29248                | Port for LogViewer to provide HTTPS services                              |
+------------------------+------------------------+----------------------+---------------------------------------------------------------------------+
| ui.https.port          | 29243                  | 29243                | Port for Storm UI to provide HTTPS services (ui.https.port)               |
+------------------------+------------------------+----------------------+---------------------------------------------------------------------------+

Common Yarn Ports
-----------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| Parameter                              | Default Port           | Default Port         | Port Description                                                                                                           |
|                                        |                        |                      |                                                                                                                            |
|                                        | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                                                            |
+========================================+========================+======================+============================================================================================================================+
| yarn.resourcemanager.webapp.port       | 26000                  | 8088                 | Web HTTP port of the ResourceManager service                                                                               |
+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| yarn.resourcemanager.webapp.https.port | 26001                  | 8090                 | Web HTTPS port of the ResourceManager service                                                                              |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | This port is used to access the Resource Manager web applications in security mode.                                        |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | .. note::                                                                                                                  |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | -  Is the port enabled by default during the installation: Yes                                                             |
|                                        |                        |                      | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| yarn.nodemanager.webapp.port           | 26006                  | 8042                 | NodeManager Web HTTP port                                                                                                  |
+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| yarn.nodemanager.webapp.https.port     | 26010                  | 8044                 | NodeManager Web HTTPS port                                                                                                 |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | This port is used for:                                                                                                     |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | Accessing the NodeManager web application in security mode                                                                 |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | .. note::                                                                                                                  |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                                        |                        |                      |                                                                                                                            |
|                                        |                        |                      | -  Is the port enabled by default during the installation: Yes                                                             |
|                                        |                        |                      | -  Is the port enabled after security hardening: Yes                                                                       |
+----------------------------------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+

Common ZooKeeper Ports
----------------------

The protocol type of all ports in the table is TCP (for MRS 1.7.0 or later).

+-----------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+
| Parameter       | Default Port           | Default Port         | Port Description                                                                                                           |
|                 |                        |                      |                                                                                                                            |
|                 | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                                                            |
+=================+========================+======================+============================================================================================================================+
| clientPort      | 24002                  | 2181                 | ZooKeeper client port                                                                                                      |
|                 |                        |                      |                                                                                                                            |
|                 |                        |                      | This port is used for:                                                                                                     |
|                 |                        |                      |                                                                                                                            |
|                 |                        |                      | Connection between the ZooKeeper client and server.                                                                        |
|                 |                        |                      |                                                                                                                            |
|                 |                        |                      | .. note::                                                                                                                  |
|                 |                        |                      |                                                                                                                            |
|                 |                        |                      |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code. |
|                 |                        |                      |                                                                                                                            |
|                 |                        |                      | -  Is the port enabled by default during the installation: Yes                                                             |
|                 |                        |                      | -  Is the port enabled after security hardening: Yes                                                                       |
+-----------------+------------------------+----------------------+----------------------------------------------------------------------------------------------------------------------------+

Common Kerberos Ports
---------------------

The protocol type of all ports in the table is UDP (for MRS 1.7.0 or later).

+-----------------+------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter       | Default Port           | Default Port         | Port Description                                                                                                                         |
|                 |                        |                      |                                                                                                                                          |
|                 | (MRS 1.6.3 or Earlier) | (MRS 1.7.0 or Later) |                                                                                                                                          |
+=================+========================+======================+==========================================================================================================================================+
| kdc_ports       | 21732                  | 21732                | Kerberos server port                                                                                                                     |
|                 |                        |                      |                                                                                                                                          |
|                 |                        |                      | This port is used for:                                                                                                                   |
|                 |                        |                      |                                                                                                                                          |
|                 |                        |                      | Performing Kerberos authentication for components. This parameter may be used during the configuration of mutual trust between clusters. |
|                 |                        |                      |                                                                                                                                          |
|                 |                        |                      | .. note::                                                                                                                                |
|                 |                        |                      |                                                                                                                                          |
|                 |                        |                      |    The port ID is a recommended value and is specified based on the product. The port range is not restricted in the code.               |
|                 |                        |                      |                                                                                                                                          |
|                 |                        |                      | -  Is the port enabled by default during the installation: Yes                                                                           |
|                 |                        |                      | -  Is the port enabled after security hardening: Yes                                                                                     |
+-----------------+------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------+

Common OpenTSDB Ports
---------------------

The protocol type of the port in the table is TCP.

+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------+
| Parameter             | Default Port          | Port Description                                                                                |
+=======================+=======================+=================================================================================================+
| tsd.network.port      | 4242                  | Web UI port of OpenTSDB                                                                         |
|                       |                       |                                                                                                 |
|                       |                       | This port is used for: HTTPS/HTTP communication between web requests and the OpenTSDB UI server |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------+

Common Tez Ports
----------------

The protocol type of the port in the table is TCP.

=========== ============ ==================
Parameter   Default Port Port Description
=========== ============ ==================
tez.ui.port 28888        Web UI port of Tez
=========== ============ ==================

Common KafkaManager Ports
-------------------------

The protocol type of the port in the table is TCP.

================== ============ ===========================
Parameter          Default Port Port Description
================== ============ ===========================
kafka_manager_port 9099         Web UI port of KafkaManager
================== ============ ===========================

Common Presto Ports
-------------------

The protocol type of the port in the table is TCP.

+------------------------+--------------+---------------------------------------------------------------------------+
| Parameter              | Default Port | Port Description                                                          |
+========================+==============+===========================================================================+
| http-server.http.port  | 7520         | HTTP port for Presto coordinator to provide services to external systems  |
+------------------------+--------------+---------------------------------------------------------------------------+
| http-server.https.port | 7521         | HTTPS port for Presto coordinator to provide services to external systems |
+------------------------+--------------+---------------------------------------------------------------------------+
| http-server.http.port  | 7530         | HTTP port for Presto worker to provide services to external systems       |
+------------------------+--------------+---------------------------------------------------------------------------+
| http-server.https.port | 7531         | HTTPS port for Presto worker to provide services to external systems      |
+------------------------+--------------+---------------------------------------------------------------------------+

Common Flink Ports
------------------

The protocol type of the port in the table is TCP.

+-----------------------+-----------------------+--------------------------------------------------------------------------------------------------+
| Parameter             | Default Port          | Port Description                                                                                 |
+=======================+=======================+==================================================================================================+
| jobmanager.web.port   | 32261-32325           | Web UI port of Flink                                                                             |
|                       |                       |                                                                                                  |
|                       |                       | This port is used for: HTTP/HTTPS communication between the client web requests and Flink server |
+-----------------------+-----------------------+--------------------------------------------------------------------------------------------------+

Common ClickHouse Ports
-----------------------

The protocol type of the port in the table is TCP.

+-----------------+--------------+------------------------------------------------------------------------------------------------------------+
| Parameter       | Default Port | Port Description                                                                                           |
+=================+==============+============================================================================================================+
| tcp_port        | 9000         | TCP port for accessing the service client                                                                  |
+-----------------+--------------+------------------------------------------------------------------------------------------------------------+
| http_port       | 8123         | HTTP port for accessing the service client                                                                 |
+-----------------+--------------+------------------------------------------------------------------------------------------------------------+
| https_port      | 8443         | HTTPS port for accessing the service client                                                                |
+-----------------+--------------+------------------------------------------------------------------------------------------------------------+
| tcp_port_secure | 9440         | TCP With SSL port for accessing the service client. This port is enabled only in security mode by default. |
+-----------------+--------------+------------------------------------------------------------------------------------------------------------+

Common Impala Ports
-------------------

The protocol type of the port in the table is TCP.

+-----------------+--------------+------------------------------------------------------------------------------+
| Parameter       | Default Port | Port Description                                                             |
+=================+==============+==============================================================================+
| --beeswax_port  | 21000        | Port for impala-shell communication                                          |
+-----------------+--------------+------------------------------------------------------------------------------+
| --hs2_port      | 21050        | Port for Impala application communication                                    |
+-----------------+--------------+------------------------------------------------------------------------------+
| --hs2_http_port | 28000        | Port used by Impala to provide the HiveServer2 protocol for external systems |
+-----------------+--------------+------------------------------------------------------------------------------+
