:original_name: mrs_01_0628.html

.. _mrs_01_0628:

Performing Rolling Restart
==========================

After modifying the configuration items of a big data component, you need to restart the corresponding service to make new configurations take effect. If you use a normal restart mode, all services or instances are restarted concurrently, which may cause service interruption. To ensure that services are not affected during service restart, you can restart services or instances in batches by rolling restart. For instances in active/standby mode, a standby instance is restarted first and then an active instance is restarted. Rolling restart takes longer than normal restart.

:ref:`Table 1 <mrs_01_0628__en-us_topic_0173397702_table054720341161>` provides services and instances that support or do not support rolling restart in the MRS cluster.

.. _mrs_01_0628__en-us_topic_0173397702_table054720341161:

.. table:: **Table 1** Services and instances that support or do not support rolling restart

   ========= ================ ==================================
   Service   Instance         Whether to Support Rolling Restart
   ========= ================ ==================================
   HDFS      NameNode         Yes
   \         Zkfc
   \         JournalNode
   \         HttpFS
   \         DataNode
   Yarn      ResourceManager  Yes
   \         NodeManager
   Hive      MetaStore        Yes
   \         WebHCat
   \         HiveServer
   Mapreduce JobHistoryServer Yes
   HBase     HMaster          Yes
   \         RegionServer
   \         ThriftServer
   \         RESTServer
   Spark     JobHistory       Yes
   \         JDBCServer
   \         SparkResource    No
   Hue       Hue              No
   Tez       TezUI            No
   Loader    Sqoop            No
   Zookeeper Quorumpeer       Yes
   Kafka     Broker           Yes
   \         MirrorMaker      No
   Flume     Flume            Yes
   \         MonitorServer
   Storm     Nimbus           Yes
   \         UI
   \         Supervisor
   \         Logviewer
   ========= ================ ==================================

Restrictions
------------

-  Perform a rolling restart during off-peak hours.

   -  Otherwise, a rolling restart failure may occur. For example, if the throughput of Kafka is high (over 100 MB/s) during the Kafka rolling restart, the Kafka rolling restart may fail.
   -  For example, if the requests per second of each RegionServer on the native interface exceed 10,000 during the HBase rolling restart, you need to increase the number of handles to prevent a RegionServer restart failure caused by heavy loads during the restart.

-  Before the restart, check the number of current requests of HBase. If the number of requests of each RegionServer on the native interface exceeds 10,000, increase the number of handles to prevent a failure.
-  If the number of Core nodes in a cluster is less than six, services may be affected for a short period of time.
-  Preferentially perform a rolling instance or service restart and select **Only restart instances whose configurations have expired**.

Performing a Rolling Service Restart
------------------------------------

#. Choose **Clusters** > **Active Clusters** and click a cluster name to go to the cluster details page.
#. Click **Components** and select a service for which you want to perform a rolling restart.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Performing a Rolling Service Restart <mrs_01_0579__en-us_topic_0138965094_section1115494813176>`.

#. On the **Service Status** tab page, click **More** and select **Rolling-restart Service**.
#. The **Rolling-restart Service** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart for the service.
#. After the rolling restart task is complete, click **Finish**.

Performing a Rolling Instance Restart
-------------------------------------

#. Choose **Clusters** > **Active Clusters** and click a cluster name to go to the cluster details page.
#. Click **Components** and select a service for which you want to perform a rolling restart.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Performing a Rolling Instance Restart <mrs_01_0579__en-us_topic_0138965094_section938837152120>`.

#. On the **Instance** tab page, select the instance to be restarted. Click **More** and select **Rolling-restart Instance**.
#. After you enter the administrator password, the **Rolling-restart Instance** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart for the instance.
#. After the rolling restart task is complete, click **Finish**.

Perform a Rolling Cluster Restart
---------------------------------

#. Choose **Clusters** > **Active Clusters** and click a cluster name to go to the cluster details page.
#. In the upper right corner of the page, choose **Management Operations** > **Perform Rolling Cluster Restart**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Perform a Rolling Cluster Restart <mrs_01_0579__en-us_topic_0138965094_section1787148152416>`.

#. The **Rolling-restart Cluster** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart for the cluster.
#. After the rolling restart task is complete, click **Finish**.

Rolling Restart Parameter Description
-------------------------------------

:ref:`Table 2 <mrs_01_0628__table817615121520>` describes rolling restart parameters.

.. _mrs_01_0628__table817615121520:

.. table:: **Table 2** Rolling restart parameter description

   +----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                                                | Description                                                                                                                                                                                                                                                                    |
   +==========================================================+================================================================================================================================================================================================================================================================================+
   | Only restart instances whose configurations have expired | Specifies whether to restart only the modified instances in a cluster.                                                                                                                                                                                                         |
   +----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Data Node Instances to Be Batch Restarted                | Specifies the number of instances that are restarted in each batch when the batch rolling restart strategy is used. The default value is **1**. The value ranges from 1 to 20. This parameter is valid only for data nodes.                                                    |
   +----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Batch Interval                                           | Specifies the interval between two batches of instances for rolling restart. The default value is **0**. The value ranges from 0 to 2147483647. The unit is second.                                                                                                            |
   |                                                          |                                                                                                                                                                                                                                                                                |
   |                                                          | Note: Setting the batch interval parameter can increase the stability of the big data component process during the rolling restart. You are advised to set this parameter to a non-default value, for example, 10.                                                             |
   +----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Batch Fault Tolerance Threshold                          | Specifies the tolerance times when the rolling restart of instances fails to be executed in batches. The default value is **0**, which indicates that the rolling restart task ends after any batch of instances fails to be restarted. The value ranges from 0 to 2147483647. |
   +----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure in a Typical Scenario
-------------------------------

#. Choose **Clusters** > **Active Clusters** and click a cluster name to go to the cluster details page.
#. Click **Components** and select **HBase**. The **HBase** service page is displayed.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Procedure in a Typical Scenario <mrs_01_0579__en-us_topic_0138965094_section830817219322>`.

#. Click the **Service Configuration** tab, and modify an HBase parameter. After the following dialog box is displayed, click **OK** to save the configurations.

   .. note::

      Do not select **Restart the affected services or instances**. This option indicates a normal restart. If you select this option, all services or instances will be restarted, which may cause service interruption.

#. After saving the configurations, click **Finish**.
#. Click the **Service Status** tab.
#. On the **Service Status** tab page, click **More** and select **Rolling-restart Service**.
#. After you enter the administrator password, the **Rolling-restart Service** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart.
#. After the rolling restart task is complete, click **Finish**.
