:original_name: mrs_01_24743.html

.. _mrs_01_24743:

Configuring an IoTDB Data Source
================================

This section applies to MRS 3.2.0 or later.

Scenario
--------

Add an IoTDB JDBC data source on HSConsole of a cluster in security mode.

Prerequisites
-------------

-  The domain name of the cluster where the data source is located must be different from that of the HetuEngine cluster.
-  The cluster where the data source is located and the HetuEngine cluster nodes can communicate with each other.
-  A HetuEngine compute instance has been created.
-  By default, SSL is enabled for the IoTDB service in a security cluster. After SSL is enabled, you need to upload the **truststore.jks** file. For details about how to obtain the file, see :ref:`Using the IoTDB Client <mrs_01_24158>`.

Procedure
---------

#. Log in to FusionInsight Manager as a HetuEngine administrator and choose **Cluster** > **Services** > **HetuEngine**.

#. On the **Dashboard** tab page that is displayed, find the **Basic Information** area, and click the link next to **HSConsole WebUI**.

#. Choose **Data Source** and click **Add Data Source**. Configure parameters on the **Add Data Source** page.

   a. In the **Basic Configuration** area, configure **Name** and choose **JDBC** > **IoTDB** for **Data Source Type**.

   b. Configure parameters in the **IoTDB Configuration** area by referring to :ref:`Table 1 <mrs_01_24743__en-us_topic_0000001521279689_table102190549122>`.

      .. _mrs_01_24743__en-us_topic_0000001521279689_table102190549122:

      .. table:: **Table 1** IoTDB configuration parameters

         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter             | Description                                                                                                                                                | Example Value                                                                                                                                                |
         +=======================+============================================================================================================================================================+==============================================================================================================================================================+
         | Driver                | The default value is **iotdb**.                                                                                                                            | iotdb                                                                                                                                                        |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | JDBC URL              | JDBC URL for connecting to IoTDB.                                                                                                                          | jdbc:iotdb://10.10.10.11:22260,10.10.10.12:22260                                                                                                             |
         |                       |                                                                                                                                                            |                                                                                                                                                              |
         |                       | Format: **jdbc:iotdb://**\ *Service IP address 1 of IoTDBServer*\ **:**\ *Port number*\ **,**\ *Service IP address 2 of IoTDBServer*\ **:**\ *Port number* |                                                                                                                                                              |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Username              | IoTDB username for connecting to the IoTDB data source                                                                                                     | .. note::                                                                                                                                                    |
         |                       |                                                                                                                                                            |                                                                                                                                                              |
         |                       |                                                                                                                                                            |    If the cluster where IoTDB resides is in non-security mode, set this parameter to the default IoTDB user **root**.                                        |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Password              | Password of the IoTDB username for connecting to the IoTDB data source                                                                                     | .. note::                                                                                                                                                    |
         |                       |                                                                                                                                                            |                                                                                                                                                              |
         |                       |                                                                                                                                                            |    If the cluster where the IoTDB service is installed is in non-security mode, obtain the password of user **root** from the administrator of this cluster. |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Enable SSL            | Whether SSL is enabled for the IoTDB service. SSL is enabled by default in a security cluster.                                                             | Yes                                                                                                                                                          |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | truststore File       | After SSL is enabled for IoTDB, upload the **truststore.jks** file.                                                                                        | ``-``                                                                                                                                                        |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+

      .. note::

         -  Service IP addresses of IoTDBServer:

            Log in to FusionInsight Manager, choose **Cluster** > **Services** > **IoTDB**. On the page that is displayed, click the **Instance** tab. On this tab page, check **Service IP Address** of IoTDBServer.

         -  Port number:

            Log in to FusionInsight Manager, choose **Cluster** > **Services** > **IoTDB**. On the page that is displayed, click the **Configurations** tab. On this tab page, search for and check the value of **IOTDB_SERVER_RPC_PORT**. The default value is **22260**.

   c. (Optional) Add custom configurations as needed.

   d. Click **OK**.

#. Log in to the node where the cluster client is located and run the following commands to switch to the client installation directory and authenticate the user:

   **cd /opt/client**

   **source bigdata_env**

   **kinit** *User performing HetuEngine operations* (If the cluster is in normal mode, skip this step.)

#. Run the following command to log in to the catalog of the data source:

   **hetu-cli --catalog** *Data source name* **--schema** *Database name*

   For example, run the following command:

   **hetu-cli --catalog** **iotdb_1** **--schema root.ln**

#. Run the following command. If the database table information can be viewed or no error is reported, the connection is successful.

   **show tables;**

Data Type Mapping
-----------------

=============== ====================
IoTDB Data Type HetuEngine Data Type
=============== ====================
BOOLEAN         BOOLEAN
INT32           BIGINT
INT64           BIGINT
FLOAT           DOUBLE
DOUBLE          DOUBLE
TEXT            VARCHAR
=============== ====================

Function Enhancement
--------------------

-  IoTDB can confgiure any label fields for time series. These IoTDB label fields and other data sources can be jointly queried through HetuEngine.
-  Any nodes that are stored by IoTDB to the time series can be used as tables for data query on HetuEngine.

Constraints
-----------

-  IoTDB data cannot be created but can be queried.
-  The IoTDB user who uses HetuEngine for query must at least be configured with the read permission on the root directory.
