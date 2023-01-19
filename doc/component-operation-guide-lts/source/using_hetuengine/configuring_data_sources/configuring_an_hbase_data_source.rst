:original_name: mrs_01_2349.html

.. _mrs_01_2349:

Configuring an HBase Data Source
================================

Scenario
--------

This section describes how to add an HBase data source on HSConsole.

Prerequisites
-------------

-  The domain name of the cluster where the data source is located must be different from the HetuEngine cluster domain name.
-  The cluster where the data source is located and the HetuEngine cluster nodes can communicate with each other.
-  A HetuEngine compute instance has been created.

-  The SSL communication encryption configuration of ZooKeeper in the cluster where the data source is located must be the same as that of ZooKeeper in the cluster where HetuEngine is located.

   .. note::

      To check whether SSL communication encryption is enabled, log in to FusionInsight Manager, choose **Cluster** > **Services** > **ZooKeeper** > **Configurations** > **All Configurations**, and enter **ssl.enabled** in the search box. If the value of **ssl.enabled** is **true**, SSL communication encryption is enabled. If the value is **false**, SSL communication encryption is disabled.

Procedure
---------

#. .. _mrs_01_2349__en-us_topic_0000001173949888_li1823132412324:

   Obtain the **hbase-site.xml**, **hdfs-site.xml**, and **core-site.xml** configuration files of the HBase data source.

   a. Log in to FusionInsight Manager of the cluster where the HBase data source is located.

   b. Choose **Cluster** > **Dashboard**.

   c. Choose **More** > **Download Client** and download the client file as prompted.

   d. Decompress the downloaded client file package and obtain the **hbase-site.xml**, **core-site.xml**, and **hdfs-site.xml** files in the **FusionInsight_Cluster_1_Services_ClientConfig/HBase/config** directory.

   e. If **hbase.rpc.client.impl** exists in the **hbase-site.xml** file, change the value of **hbase.rpc.client.impl** to **org.apache.hadoop.hbase.ipc.RpcClientImpl**.

      .. code-block::

         <property>
         <name>hbase.rpc.client.impl</name>
         <value>org.apache.hadoop.hbase.ipc.RpcClientImpl</value>
         </property>

      .. note::

         In addition, if the **hdfs-site.xml** and **hbase-site.xml** files reference the host name of a non-HetuEngine cluster node, you need to add the mapping between the referenced host name and the corresponding IP address to the **/etc/hosts** file of each node in the HetuEngine cluster. Otherwise, HetuEngine cannot connect to the node that is not in this cluster based on the host name.

#. .. _mrs_01_2349__en-us_topic_0000001173949888_li1823134583712:

   Obtain the **user.keytab** and **krb5.conf** files of the proxy user of the HBase data source.

   a. Log in to FusionInsight Manager of the cluster where the HBase data source is located.
   b. Choose **System** > **Permission** > **User**.
   c. Locate the row that contains the target data source user, click **More** in the **Operation** column, and select **Download Authentication Credential**.
   d. Decompress the downloaded package to obtain the **user.keytab** and **krb5.conf** files.

   .. note::

      The proxy user of the data source must have the permission to perform HBase operations.

#. Log in to FusionInsight Manager as a HetuEngine administrator and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.

#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.

#. Choose **Data Source**.

6. Click **Add Data Source**. Configure parameters on the **Add Data Source** page.

   a. Configure **Basic Information**. For details, see :ref:`Table 1 <mrs_01_2349__en-us_topic_0000001173949888_table1755613194216>`.

      .. _mrs_01_2349__en-us_topic_0000001173949888_table1755613194216:

      .. table:: **Table 1** Basic Information

         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Parameter             | Description                                                                                                    | Example Value         |
         +=======================+================================================================================================================+=======================+
         | Name                  | Name of the data source to be connected.                                                                       | hbase_1               |
         |                       |                                                                                                                |                       |
         |                       | The value can contain only letters, digits, and underscores (_) and must start with a letter.                  |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Data Source Type      | Type of the data source to be connected. Select **HBase**.                                                     | HBase                 |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Description           | Description of the data source.                                                                                | ``-``                 |
         |                       |                                                                                                                |                       |
         |                       | The value can contain only letters, digits, commas (,), periods (.), underscores (_), spaces, and line breaks. |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+

   b. Configure parameters in the **HBase Configuration** area. For details, see :ref:`Table 2 <mrs_01_2349__en-us_topic_0000001173949888_table1075911311429>`.

      .. _mrs_01_2349__en-us_topic_0000001173949888_table1075911311429:

      .. table:: **Table 2** HBase Configuration

         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | Parameter                          | Description                                                                                                                                                                                                                                    | Example Value                                   |
         +====================================+================================================================================================================================================================================================================================================+=================================================+
         | Driver                             | The default value is **hbase-connector**.                                                                                                                                                                                                      | hbase-connector                                 |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | ZooKeeper Quorum Address           | Service IP addresses of all quorumpeer instances of the ZooKeeper service for the data source. If the ZooKeeper service of the data source uses IPv6, you need to specify the client port number in the ZooKeeper Quorum address.              | -  IPv4: 10.0.136.132,10.0.136.133,10.0.136.134 |
         |                                    |                                                                                                                                                                                                                                                | -  IPv6: [0.0.0.0.0.0.0.0]:24002                |
         |                                    | Log in to FusionInsight Manager, choose **Cluster** > **Services** > **ZooKeeper** > **Instance**, and view the IP addresses of all the hosts housing the quorumpeer instances.                                                                |                                                 |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | ZooKeeper Client Port Number       | Port number of the ZooKeeper client.                                                                                                                                                                                                           | 2181                                            |
         |                                    |                                                                                                                                                                                                                                                |                                                 |
         |                                    | Log in to FusionInsight Manager and choose **Cluster** > **Service** > **ZooKeeper**. On the **Configurations** tab page, check the value of **clientPort**.                                                                                   |                                                 |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | HBase RPC Communication Protection | Set this parameter based on the value of **hbase.rpc.protection** in the **hbase-site.xml** file obtained in :ref:`1 <mrs_01_2349__en-us_topic_0000001173949888_li1823132412324>`.                                                             | No                                              |
         |                                    |                                                                                                                                                                                                                                                |                                                 |
         |                                    | -  If the value is **authentication**, set this parameter to **No**.                                                                                                                                                                           |                                                 |
         |                                    | -  If the value is **privacy**, set this parameter to **Yes**.                                                                                                                                                                                 |                                                 |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | Security Authentication Mechanism  | After the security mode is enabled, the default value is **KERBEROS**.                                                                                                                                                                         | KERBEROS                                        |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | Principal                          | Configure this parameter when the security authentication mechanism is enabled. Set the parameter to the user to whom the **user.keytab** file obtained in :ref:`2 <mrs_01_2349__en-us_topic_0000001173949888_li1823134583712>` belongs.       | user_hbase@HADOOP2.COM                          |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | Keytab File                        | Configure this parameter when the security mode is enabled. It specifies the security authentication key. Select the **user.keytab** file obtained in :ref:`2 <mrs_01_2349__en-us_topic_0000001173949888_li1823134583712>`.                    | user.keytab                                     |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | krb5 File                          | Configure this parameter when the security mode is enabled. It is the configuration file used for Kerberos authentication. Select the **krb5.conf** file obtained in :ref:`2 <mrs_01_2349__en-us_topic_0000001173949888_li1823134583712>`.     | krb5.conf                                       |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | hbase-site File                    | Configure this parameter when the security mode is enabled. It is the configuration file required for connecting to HDFS. Select the **hbase-site.xml** file obtained in :ref:`1 <mrs_01_2349__en-us_topic_0000001173949888_li1823132412324>`. | hbase-site.xml                                  |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | core-site File                     | Configure this parameter when the security mode is enabled. This file is required for connecting to HDFS. Select the **core-site.xml** file obtained in :ref:`1 <mrs_01_2349__en-us_topic_0000001173949888_li1823132412324>`.                  | core-site.xml                                   |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
         | hdfs-site File                     | Configure this parameter when the security mode is enabled. This file is required for connecting to HDFS. Select the **hdfs-site.xml** file obtained in :ref:`1 <mrs_01_2349__en-us_topic_0000001173949888_li1823132412324>`.                  | hdfs-site.xml                                   |
         +------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+

   c. Modify custom configurations.

      -  You can click **Add** to add custom configuration parameters.
      -  You can click **Delete** to delete custom configuration parameters.

   d. Click **OK**.

7. Log in to the node where the cluster client is located and run the following commands to switch to the client installation directory and authenticate the user:

   **cd /opt/client**

   **source bigdata_env**

   **kinit** *User performing HetuEngine operations* (If the cluster is in normal mode, skip this step.)

8. Run the following command to log in to the catalog of the data source:

   **hetu-cli --catalog** *Data source name* **--schema default**

   For example, run the following command:

   **hetu-cli --catalog** **hbase_1** **--schema default**
