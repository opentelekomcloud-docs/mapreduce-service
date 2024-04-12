:original_name: mrs_01_24576.html

.. _mrs_01_24576:

Configuring Intranet and Extranet Access for Kafka
==================================================

This section applies to MRS 3.2.0 or later.

Scenario
--------

To access Kafka Broker deployed on a private network from the Kafka client via the Internet, enable the Kafka private and public network traffic distribution function.

Prerequisites
-------------

-  The node where Broker resides has both private and public IP addresses. Broker is bound to the private IP address and cannot be accessed via the Internet. Alternatively, the node where Broker resides has only private IP addresses, and external services access the private network through gateway mapping.
-  The ZooKeeper service is running properly.
-  The Kafka instance status and disk status are normal.

Procedure
---------

#. Log in to FusionInsight Manager.

#. .. _mrs_01_24576__li718292175116:

   Choose **Cluster** > **Services** > **Kafka**. On the page that is displayed, click the **Instance** tab. On this tab page, select the target broker instance in the instance list. On the displayed page, click the **Instance Configurations** tab and then the **All Configurations** sub-tab. Enter **broker.id** in the search box to view and record the broker ID of the current broker instance.

#. Repeat :ref:`2 <mrs_01_24576__li718292175116>` to view and record the broker ID of each broker instance.

#. Choose **Cluster** > **Services** > **Kafka**. On the page that is displayed, click the **Configurations** tab then the **All Configurations** sub-tab. On this sub-tab page, click **Broker(Role)** and select **Server**. Enter **advertised** and **actual** in the search box. The five configuration items shown in the following figure are displayed. Configure the parameters according to :ref:`Table 1 <mrs_01_24576__table25971414778>`.

   |image1|

   |image2|

   .. _mrs_01_24576__table25971414778:

   .. table:: **Table 1** Parameter description

      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                     | Description                                                                                                                                                                                | Remarks                                                                                                                                                                                                                                                                    |
      +===============================+============================================================================================================================================================================================+============================================================================================================================================================================================================================================================================+
      | enable.advertised.listener    | Whether to enable the advertised.listeners configuration. The default value is **false**.                                                                                                  | Set **enable.advertised.listener** to **true**.                                                                                                                                                                                                                            |
      |                               |                                                                                                                                                                                            |                                                                                                                                                                                                                                                                            |
      |                               |                                                                                                                                                                                            | .. note::                                                                                                                                                                                                                                                                  |
      |                               |                                                                                                                                                                                            |                                                                                                                                                                                                                                                                            |
      |                               |                                                                                                                                                                                            |    When you install the Kafka service, do not set this parameter to **true**. You can set this parameter to **true** only after broker instances and ZooKeeper are running properly.                                                                                       |
      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | advertised.broker.id.ip.map   | IP address released by Kafka. This parameter is left blank by default.                                                                                                                     | Map the broker ID of each broker instance recorded in :ref:`2 <mrs_01_24576__li718292175116>` to the IP address to which the broker instance to bound.                                                                                                                     |
      |                               |                                                                                                                                                                                            |                                                                                                                                                                                                                                                                            |
      |                               | Format: *Broker ID:IP*. Multiple brokers can use the same IP address. If multiple mappings are configured, use commas (,) to separate them.                                                | For example, if there are three broker instances and one IP address, the broker IDs are **1**, **2**, and **3**, and the IP address is **10.**\ *xxx.xxx.xxx*, the configuration format is **1:10.**\ *xxx.xxx.xxx*\ **,2:10.**\ *xxx.xxx.xxx*\ **,3:10.**\ *xxx.xxx.xxx*. |
      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | advertised.broker.id.port.map | Port released by Kafka. This parameter is left blank by default.                                                                                                                           | Map the broker ID of each broker instance recorded in :ref:`2 <mrs_01_24576__li718292175116>` to the port to which the broker instance to bound.                                                                                                                           |
      |                               |                                                                                                                                                                                            |                                                                                                                                                                                                                                                                            |
      |                               | Format: *Broker ID:Port*. **Port** indicates the port to be bound. This port is a custom port and must be available. If multiple mappings are configured, use commas (,) to separate them. | For example, if there are three broker instances and three ports, the broker IDs are **1**, **2**, and **3**, and the ports are **3307**, **3308**, and **3309**, the configuration format is **1:3307,2:3308,3:3309**.                                                    |
      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | actual.broker.id.ip.map       | IP address bound to Kafka. This parameter is left blank by default.                                                                                                                        | Map the broker ID of each broker instance recorded in :ref:`2 <mrs_01_24576__li718292175116>` to the IP address to which the broker instance to bound.                                                                                                                     |
      |                               |                                                                                                                                                                                            |                                                                                                                                                                                                                                                                            |
      |                               | Format: *Broker ID:IP*. If multiple mappings are configured, use commas (,) to separate them.                                                                                              | For example, if there are three broker instances and one IP address, the broker IDs are **1**, **2**, and **3**, and the IP address is **10.**\ *xxx.xxx.xxx*, the configuration format is **1:10.**\ *xxx.xxx.xxx*\ **,2:10.**\ *xxx.xxx.xxx*\ **,3:10.**\ *xxx.xxx.xxx*. |
      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | actual.broker.id.port.map     | Port bound to Kafka. This parameter is left blank by default.                                                                                                                              | Map the broker ID of each broker instance recorded in :ref:`2 <mrs_01_24576__li718292175116>` to the port to which the broker instance to bound.                                                                                                                           |
      |                               |                                                                                                                                                                                            |                                                                                                                                                                                                                                                                            |
      |                               | Format: *Broker ID:Port*. **Port** indicates the port to be bound. This port is a custom port and must be available. If multiple mappings are configured, use commas (,) to separate them. | For example, if there are three broker instances and three ports, the broker IDs are **1**, **2**, and **3**, and the ports are **3307**, **3308**, and **3309**, the configuration format is **1:3307,2:3308,3:3309**.                                                    |
      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. After the configuration is complete, click **Save** in the upper left corner. On the **Instance** tab, select the target broker instances and choose **More** > **Instance Rolling Restart**. Wait until the rolling restart is complete.

#. (Optional) To disable this configuration, set **enable.advertised.listener** to **false** and click **Save**. On the **Instance** page of Kafka, select Kafka instances, choose **More** > **Instance Rolling Restart**, and wait until the rolling restart is complete.

.. note::

   In a cluster with Kerberos authentication enabled, after **enable.advertised.listener** is configured, the client supports only Kerberos authentication, but not PLAIN authentication.

.. |image1| image:: /_static/images/en-us_image_0000001583349121.png
.. |image2| image:: /_static/images/en-us_image_0000001532709204.png
