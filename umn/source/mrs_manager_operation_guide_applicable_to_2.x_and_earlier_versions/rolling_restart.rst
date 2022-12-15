:original_name: mrs_01_0579.html

.. _mrs_01_0579:

Rolling Restart
===============

After modifying the configuration items of a big data component, you need to restart the corresponding service to make new configurations take effect. If you use a normal restart mode, all services or instances are restarted concurrently, which may cause service interruption. To ensure that services are not affected during service restart, you can restart services or instances in batches by rolling restart. For instances in active/standby mode, a standby instance is restarted first and then an active instance is restarted. Rolling restart takes longer than normal restart.

:ref:`Table 1 <mrs_01_0579__en-us_topic_0138965094_en-us_topic_0143479582_table054720341161>` provides services and instances that support or do not support rolling restart in the MRS cluster.

.. _mrs_01_0579__en-us_topic_0138965094_en-us_topic_0143479582_table054720341161:

.. table:: **Table 1** Services and instances that support or do not support rolling restart

   ========= ================ ==================================
   Service   Instance         Whether to Support Rolling Restart
   ========= ================ ==================================
   HDFS      NameNode         Yes
   \         ZKFC
   \         JournalNode
   \         HttpFS
   \         DataNode
   Yarn      ResourceManager  Yes
   \         NodeManager
   Hive      MetaStore        Yes
   \         WebHCat
   \         HiveServer
   MapReduce JobHistoryServer Yes
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
   ZooKeeper Quorumpeer       Yes
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

-  Before the restart, check the number of current requests of HBase. If requests of each RegionServer on the native interface exceed 10,000, increase the number of handles to prevent a failure.
-  If the number of Core nodes in a cluster is less than six, services may be affected for a short period of time.
-  Preferentially perform a rolling instance or service restart and select **Only restart instances whose configurations have expired**.

.. _mrs_01_0579__en-us_topic_0138965094_section1115494813176:

Performing a Rolling Service Restart
------------------------------------

#. On MRS Manager, click **Services** and select a service for which you want to perform a rolling restart.
#. On the **Service Status** tab page, click **More** and select **Perform Rolling Service Restart**.
#. After you enter the administrator password, the **Perform Rolling Service Restart** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart for the service.
#. After the rolling restart task is complete, click **Finish**.

.. _mrs_01_0579__en-us_topic_0138965094_section938837152120:

Performing a Rolling Instance Restart
-------------------------------------

#. On MRS Manager, click **Services** and select a service for which you want to perform a rolling restart.
#. On the **Instance** tab page, select the instance to be restarted. Click **More** and select **Perform Rolling Instance Restart**.
#. After you enter the administrator password, the **Perform Rolling Instance Restart** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart for the instance.
#. After the rolling restart task is complete, click **Finish**.

.. _mrs_01_0579__en-us_topic_0138965094_section1787148152416:

Perform a Rolling Cluster Restart
---------------------------------

#. On MRS Manager, click **Services**. The **Services** page is displayed.
#. Click **More** and select **Perform Rolling Cluster Restart**.
#. After you enter the administrator password, the **Perform Rolling Cluster Restart** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart for the cluster.
#. After the rolling restart task is complete, click **Finish**.

Rolling Restart Parameter Description
-------------------------------------

:ref:`Table 2 <mrs_01_0579__en-us_topic_0138965094_table817615121520>` describes rolling restart parameters.

.. _mrs_01_0579__en-us_topic_0138965094_table817615121520:

.. table:: **Table 2** Rolling restart parameter description

   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                                                | Description                                                                                                                                                                                                                                                                   |
   +==========================================================+===============================================================================================================================================================================================================================================================================+
   | Only restart instances whose configurations have expired | Specifies whether to restart only the modified instances in a cluster.                                                                                                                                                                                                        |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Data Node Instances to Be Batch Restarted                | Specifies the number of instances that are restarted in each batch when the batch rolling restart strategy is used. The default value is **1**. The value ranges from 1 to 20. This parameter is valid only for data nodes.                                                   |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Batch Interval                                           | Specifies the interval between two batches of instances for rolling restart. The default value is **0**. The value ranges from 0 to 2147483647. The unit is second.                                                                                                           |
   |                                                          |                                                                                                                                                                                                                                                                               |
   |                                                          | Note: Setting the batch interval parameter can increase the stability of the big data component process during the rolling restart. You are advised to set this parameter to a non-default value, for example, 10.                                                            |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Batch Fault Tolerance Threshold                          | Specifies the tolerance times when the rolling restart of instances fails to be executed in batches. The default value is **0**, which indicates that the rolling restart task ends after any batch of instances fails to be restarted. The value ranges from 0 to 214748364. |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_01_0579__en-us_topic_0138965094_section830817219322:

Procedure in a Typical Scenario
-------------------------------

#. On MRS Manager, click **Services** and select HBase. The HBase service page is displayed.
#. Click the **Service Configuration** tab, and modify an HBase parameter. After the following dialog box is displayed, click **OK** to save the configurations.

   .. note::

      Do not select **Restart the affected services or instances**. This option indicates a normal restart. If you select this option, all services or instances will be restarted, which may cause service interruption.

#. After saving the configurations, click **Finish**.
#. Click the **Service Status** tab.
#. On the **Service Status** tab page, click **More** and select **Perform Rolling Service Restart**.
#. After you enter the administrator password, the **Perform Rolling Service Restart** page is displayed. Select **Only restart instances whose configurations have expired** and click **OK** to perform rolling restart for the service.
#. After the rolling restart task is complete, click **Finish**.
