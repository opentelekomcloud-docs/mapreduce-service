:original_name: mrs_01_2348.html

.. _mrs_01_2348:

Configuring a Traditional Data Source
=====================================

Scenario
--------

This section describes how to add a Hive data source on HSConsole.

Currently, HetuEngine supports data sources of the following traditional data formats: AVRO, TEXT, RCTEXT, Binary, ORC, Parquet, and SequenceFile.

Prerequisites
-------------

-  The domain name of the cluster where the data source is located must be different from the HetuEngine cluster domain name.
-  The cluster where the data source is located and the HetuEngine cluster nodes can communicate with each other.
-  A HetuEngine compute instance has been created.

Procedure
---------

#. .. _mrs_01_2348__en-us_topic_0000001219351171_li4515762384:

   Obtain the **hdfs-site.xml** and **core-site.xml** configuration files of the Hive data source cluster.

   a. Log in to FusionInsight Manager of the cluster where the Hive data source is located.

   b. Choose **Cluster** > **Dashboard**.

   c. Choose **More** > **Download Client** and download the client file to the local computer.

   d. Decompress the downloaded client file package and obtain the **core-site.xml** and **hdfs-site.xml** files in the **FusionInsight_Cluster_1_Services_ClientConfig/HDFS/config** directory.

   e. Check whether the **core-site.xml** file contains the **fs.trash.interval** configuration item. If not, add the following configuration items:

      .. code-block::

         <property>
         <name>fs.trash.interval</name>
         <value>2880</value>
         </property>

   f. Change the value of **dfs.client.failover.proxy.provider.hacluster** in the **hdfs-site.xml** file to **org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider**.

      .. code-block::

         <property>
         <name>dfs.client.failover.proxy.provider.hacluster</name>
         <value>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</value>
         </property>

      -  If HDFS has multiple NameServices, change the values of **dfs.client.failover.proxy.provider.**\ *NameService name* for multiple NameServices in the **hdfs-site.xml** file to **org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider**.
      -  In addition, if the **hdfs-site.xml** file references the host name of a non-HetuEngine cluster node, you need to add the mapping between the referenced host name and the corresponding IP address to the **/etc/hosts** file of each HetuEngine cluster node. Otherwise, HetuEngine cannot connect to the node that is not in this cluster based on the host name.

      .. important::

         If the Hive data source to be interconnected is in the same Hadoop cluster with HetuEngine, you can log in to the HDFS client and run the following commands to obtain the **hdfs-site.xml** and **core-site.xml** configuration files. For details, see :ref:`Using the HDFS Client <mrs_01_1663>`.

         **hdfs dfs -get /user/hetuserver/fiber/restcatalog/hive/core-site.xml**

         **hdfs dfs -get /user/hetuserver/fiber/restcatalog/hive/hdfs-site.xml**

#. .. _mrs_01_2348__en-us_topic_0000001219351171_li051517619384:

   Obtain the **user.keytab** and **krb5.conf** files of the proxy user of the Hive data source.

   a. Log in to FusionInsight Manager of the cluster where the Hive data source is located.
   b. Choose **System** > **Permission** > **User**.
   c. Locate the row that contains the target data source user, click **More** in the **Operation** column, and select **Download Authentication Credential**.
   d. Decompress the downloaded package to obtain the **user.keytab** and **krb5.conf** files.

      .. note::

         The proxy user of the Hive data source must be associated with at least the **hive** user group.

#. .. _mrs_01_2348__en-us_topic_0000001219351171_li05151668382:

   Obtain the MetaStore URL and the Principal of the server.

   a. Decompress the client package of the cluster where the Hive data source is located and obtain the **hive-site.xml** file from the **FusionInsight_Cluster_1_Services_ClientConfig/Hive/config** directory.
   b. Open the **hive-site.xml** file and search for **hive.metastore.uris**. The value of **hive.metastore.uris** is the value of MetaStore URL. Search for **hive.server2.authentication.kerberos.principal**. The value of **hive.server2.authentication.kerberos.principal** is the value of Principal on the server.

#. Log in to FusionInsight Manager as a HetuEngine administrator and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.

#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.

#. Choose **Data Source** and click **Add Data Source**. Configure parameters on the **Add Data Source** page.

   a. Configure parameters in the **Basic Information** area. For details, see :ref:`Table 1 <mrs_01_2348__en-us_topic_0000001219351171_table14381114211546>`.

      .. _mrs_01_2348__en-us_topic_0000001219351171_table14381114211546:

      .. table:: **Table 1** Basic Information

         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Parameter             | Description                                                                                                    | Example Value         |
         +=======================+================================================================================================================+=======================+
         | Name                  | Name of the data source to be connected.                                                                       | hive_1                |
         |                       |                                                                                                                |                       |
         |                       | The value can contain only letters, digits, and underscores (_) and must start with a letter.                  |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Data Source Type      | Type of the data source to be connected. Select **Hive**.                                                      | Hive                  |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Mode                  | Mode of the current cluster. The default value is **Security Mode**.                                           | ``-``                 |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Description           | Description of the data source.                                                                                | ``-``                 |
         |                       |                                                                                                                |                       |
         |                       | The value can contain only letters, digits, commas (,), periods (.), underscores (_), spaces, and line breaks. |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+

   b. Configure parameters in the **Hive Configuration** area. For details, see :ref:`Table 2 <mrs_01_2348__en-us_topic_0000001219351171_table738124295411>`.

      .. _mrs_01_2348__en-us_topic_0000001219351171_table738124295411:

      .. table:: **Table 2** Hive Configuration

         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Parameter                         | Description                                                                                                                                                                   | Example Value         |
         +===================================+===============================================================================================================================================================================+=======================+
         | Driver                            | The default value is **fi-hive-hadoop**.                                                                                                                                      | fi-hive-hadoop        |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | hdfs-site File                    | Select the **hdfs-site.xml** configuration file obtained in :ref:`1 <mrs_01_2348__en-us_topic_0000001219351171_li4515762384>`. The file name is fixed.                        | ``-``                 |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | core-site File                    | Select the **core-site.xml** configuration file obtained in :ref:`1 <mrs_01_2348__en-us_topic_0000001219351171_li4515762384>`. The file name is fixed.                        | ``-``                 |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | krb5 File                         | Configure this parameter when the security mode is enabled.                                                                                                                   | krb5.conf             |
         |                                   |                                                                                                                                                                               |                       |
         |                                   | It is the configuration file used for Kerberos authentication. Select the **krb5.conf** file obtained in :ref:`2 <mrs_01_2348__en-us_topic_0000001219351171_li051517619384>`. |                       |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
         | Enable Data Source Authentication | Whether to use the permission policy of the Hive data source for authentication.                                                                                              | No                    |
         |                                   |                                                                                                                                                                               |                       |
         |                                   | If Ranger is disabled for the HetuEngine service, select **Yes**. If Ranger is enabled, select **No**.                                                                        |                       |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

   c. Configure parameters in the **MetaStore Configuration** area. For details, see :ref:`Table 3 <mrs_01_2348__en-us_topic_0000001219351171_table18381204214544>`.

      .. _mrs_01_2348__en-us_topic_0000001219351171_table18381204214544:

      .. table:: **Table 3** MetaStore Configuration

         +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                                                  | Example Value                                                                 |
         +===================================+==============================================================================================================================================================================================================+===============================================================================+
         | Metastore URL                     | URL of the MetaStore of the data source. For details, see :ref:`3 <mrs_01_2348__en-us_topic_0000001219351171_li05151668382>`.                                                                                | thrift://10.92.8.42:21088,thrift://10.92.8.43:21088,thrift://10.92.8.44:21088 |
         +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
         | Security Authentication Mechanism | After the security mode is enabled, the default value is **KERBEROS**.                                                                                                                                       | KERBEROS                                                                      |
         +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
         | Server Principal                  | Configure this parameter when the security mode is enabled.                                                                                                                                                  | hive/hadoop.hadoop.com@HADOOP.COM                                             |
         |                                   |                                                                                                                                                                                                              |                                                                               |
         |                                   | It specifies the username with domain name used by meta to access MetaStore. For details, see :ref:`3 <mrs_01_2348__en-us_topic_0000001219351171_li05151668382>`.                                            |                                                                               |
         +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
         | Client Principal                  | Configure this parameter when the security mode is enabled.                                                                                                                                                  | admintest@HADOOP.COM                                                          |
         |                                   |                                                                                                                                                                                                              |                                                                               |
         |                                   | The parameter format is as follows: *Username for accessing MetaStore*\ **@**\ *domain name (uppercase)*\ **.COM**.                                                                                          |                                                                               |
         |                                   |                                                                                                                                                                                                              |                                                                               |
         |                                   | *Username for accessing MetaStore* is the user to which the **user.keytab** file obtained in :ref:`2 <mrs_01_2348__en-us_topic_0000001219351171_li051517619384>` belongs.                                    |                                                                               |
         +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
         | Keytab File                       | Configure this parameter when the security mode is enabled.                                                                                                                                                  | user.keytab                                                                   |
         |                                   |                                                                                                                                                                                                              |                                                                               |
         |                                   | It specifies the keytab credential file of the MetaStore user name. The file name is fixed. Select the **user.keytab** file obtained in :ref:`2 <mrs_01_2348__en-us_topic_0000001219351171_li051517619384>`. |                                                                               |
         +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+

   d. Configure parameters in the **Connection Pool Configuration** area. For details, see :ref:`Table 4 <mrs_01_2348__en-us_topic_0000001219351171_table3527185012913>`.

      .. _mrs_01_2348__en-us_topic_0000001219351171_table3527185012913:

      .. table:: **Table 4** Connection Pool Configuration

         +------------------------+-------------------------------------------------------------------------------------+---------------+
         | Parameter              | Description                                                                         | Example Value |
         +========================+=====================================================================================+===============+
         | Enable Connection Pool | Whether to enable the connection pool when accessing Hive MetaStore.                | Yes/No        |
         +------------------------+-------------------------------------------------------------------------------------+---------------+
         | Maximum Connections    | Maximum number of connections in the connection pool when accessing Hive MetaStore. | 50            |
         +------------------------+-------------------------------------------------------------------------------------+---------------+

   e. Configure parameters in **Hive User Information Configuration**. For details, see :ref:`Table 5 <mrs_01_2348__en-us_topic_0000001219351171_table17970173051814>`.

      **Hive User Information Configuration** and **HetuEngine-Hive User Mapping Configuration** must be used together. When HetuEngine is connected to the Hive data source, user mapping enables HetuEngine users to have the same permissions of the mapped Hive data source user. Multiple HetuEngine users can correspond to one Hive user.

      .. _mrs_01_2348__en-us_topic_0000001219351171_table17970173051814:

      .. table:: **Table 5** Hive User Information Configuration

         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter             | Description                                                                                                                                                                                                             | Example Value                                                                                                                                                         |
         +=======================+=========================================================================================================================================================================================================================+=======================================================================================================================================================================+
         | Data Source User      | Data source user information.                                                                                                                                                                                           | If the data source user is set to **hiveuser1**, a HetuEngine user mapped to **hiveuser1** must exist. For example, create **hetuuser1** and map it to **hiveuser1**. |
         |                       |                                                                                                                                                                                                                         |                                                                                                                                                                       |
         |                       | The value can contain only letters, digits, underscores (_), hyphens (-), and periods (.), and must start with a letter or underscore (_). The minimum length is 2 characters and the maximum length is 100 characters. |                                                                                                                                                                       |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Keytab File           | Obtain the authentication credential of the user corresponding to the data source.                                                                                                                                      | hiveuser1.keytab                                                                                                                                                      |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   f. Configure parameters in the **HetuEngine-Hive User Mapping Configuration** area. For details, see :ref:`Table 6 <mrs_01_2348__en-us_topic_0000001219351171_table363354362015>`.

      .. _mrs_01_2348__en-us_topic_0000001219351171_table363354362015:

      .. table:: **Table 6** HetuEngine-Hive User Mapping Configuration

         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
         | Parameter             | Description                                                                                                                                                                                                             | Example Value                                                                                                                 |
         +=======================+=========================================================================================================================================================================================================================+===============================================================================================================================+
         | HetuEngine User       | HetuEngine user information.                                                                                                                                                                                            | hetuuser1                                                                                                                     |
         |                       |                                                                                                                                                                                                                         |                                                                                                                               |
         |                       | The value can contain only letters, digits, underscores (_), hyphens (-), and periods (.), and must start with a letter or underscore (_). The minimum length is 2 characters and the maximum length is 100 characters. |                                                                                                                               |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
         | Data Source User      | Data source user information.                                                                                                                                                                                           | **hiveuser1** (data source user configured in :ref:`Table 5 <mrs_01_2348__en-us_topic_0000001219351171_table17970173051814>`) |
         |                       |                                                                                                                                                                                                                         |                                                                                                                               |
         |                       | The value can contain only letters, digits, underscores (_), hyphens (-), and periods (.), and must start with a letter or underscore (_). The minimum length is 2 characters and the maximum length is 100 characters. |                                                                                                                               |
         +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

   g. .. _mrs_01_2348__en-us_topic_0000001219351171_li1438274211549:

      Modify custom configurations.

      -  You can click **Add** to add custom configuration parameters by referring to :ref:`Table 7 <mrs_01_2348__en-us_topic_0000001219351171_table16627151232810>`.

         .. _mrs_01_2348__en-us_topic_0000001219351171_table16627151232810:

         .. table:: **Table 7** Custom parameters

            +-----------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+
            | Parameter                               | Description                                                                                                                                                     | Example Value                                                                                                  |
            +=========================================+=================================================================================================================================================================+================================================================================================================+
            | hive.metastore.connection.pool.maxTotal | Maximum number of connections in the connection pool.                                                                                                           | 50 (Value range: 0-200)                                                                                        |
            +-----------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+
            | hive.metastore.connection.pool.maxIdle  | Maximum number of idle threads in the connection pool. When the number of idle threads reaches the maximum number, new threads are not released.                | 10 (The value ranges from 0 to 200 and cannot exceed the maximum number of connections.)                       |
            |                                         |                                                                                                                                                                 |                                                                                                                |
            |                                         | Default value: **10**.                                                                                                                                          |                                                                                                                |
            +-----------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+
            | hive.metastore.connection.pool.minIdle  | Minimum number of idle threads in the connection pool. When the number of idle threads reaches the minimum number, the thread pool does not create new threads. | 10 (The value ranges from 0 to 200 and cannot exceed the value of **hive.metastore.connection.pool.maxIdle**.) |
            |                                         |                                                                                                                                                                 |                                                                                                                |
            |                                         | Default value: **10**.                                                                                                                                          |                                                                                                                |
            +-----------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+

      -  You can click **Delete** to delete custom configuration parameters.

         .. note::

            -  You can add prefixes **coordinator.** and **worker.** to the preceding custom configuration items to configure coordinators and workers, respectively. For example, if **worker.hive.metastore.connection.pool.maxTotal** is set to **50**, a maximum number of 50 connections are allowed for workers to access Hive MetaStore. If no prefix is added, the configuration item is valid for both coordinators and workers.
            -  By default, the maximum number of connections for coordinators to access Hive MetaStore is 5 and the maximum and minimum numbers of idle data source connections are both 10. The maximum number of connections for workers to access Hive MetaStore is 20, the maximum and minimum numbers of idle data source connections are both 0.

   h. Click **OK**.

#. Log in to the node where the cluster client is located and run the following commands to switch to the client installation directory and authenticate the user:

   **cd /opt/client**

   **source bigdata_env**

   **kinit** *User performing HetuEngine operations* (If the cluster is in normal mode, skip this step.)

#. Run the following command to log in to the catalog of the data source:

   **hetu-cli --catalog** *Data source name* **--schema default**

   For example, run the following command:

   **hetu-cli --catalog** **hive\_1** **--schema default**

#. Run the following command to view the database table:

   **show tables;**

   .. code-block::

        Table
      ---------
       hivetb
      (1 rows)

      Query 20210730_084524_00023_u3sri@default@HetuEngine, FINISHED, 3 nodes
      Splits: 36 total, 36 done (100.00%)
      0:00 [2 rows, 47B] [7 rows/s, 167B/s]
