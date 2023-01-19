:original_name: mrs_01_24233.html

.. _mrs_01_24233:

Enabling Oozie High Availability (HA)
=====================================

Scenario
--------

When multiple Oozie nodes provide services at the same time, you can use ZooKeeper to provide high availability (HA), which helps avoid single points of failure (SPOFs) and prevent multiple nodes from concurrently processing the same task.

Impact on the System
--------------------

Enabling Oozie HA requires an Oozie restart, and Oozie cannot provide services during the restart.

Prerequisites
-------------

-  Oozie and ZooKeeper have been installed and are running properly.
-  No task is running.
-  The current cluster is of the latest version. If it is not, copy the **curator-x-discovery-4.2.0.jar** package from the **$BIGDATA_HOME/FusionInsight_Porter\_\ X.X.X/install/FusionInsight-Oozie-X.X.X/oozie-X.X.X/embedded-oozie-server/webapp/WEB-INF/lib** directory to the **$BIGDATA_HOME/FusionInsight_Porter\_\ X.X.X/install/FusionInsight-Oozie-X.X.X/oozie-X.X.X/lib** directory.

Procedure
---------

#. On **FusionInsight Manager**, choose **Cluster** > **Services** > **Oozie**. On the displayed page, click the **Configurations** tab, and then click **All Configurations**. In the navigation pane, choose **Customization** under **oozie(Role)**, and add the configuration items listed in the following table for **oozie.site.configs**. Click **Save** after the modification. In the displayed dialog box, click **OK**.

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | Parameter                         | Setting                                                                                                                                                                          | Description                              |
   +===================================+==================================================================================================================================================================================+==========================================+
   | oozie.services.ext                | org.apache.oozie.service.ZKLocksService,org.apache.oozie.service.ZKXLogStreamingService,org.apache.oozie.service.ZKJobsConcurrencyService,org.apache.oozie.service.ZKUUIDService | Services providing enhanced HA           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | oozie.zookeeper.connection.string | *ZooKeeper instance service IP address:Port number*. Use commas (,) to separate multiple IP address:port pairs.                                                                  | ZooKeeper connection information         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | oozie.zookeeper.namespace         | oozie                                                                                                                                                                            | Oozie path on ZooKeeper                  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | oozie.zookeeper.secure            | Security cluster: true                                                                                                                                                           | Whether to enable Kerberos on ZooKeeper. |
   |                                   |                                                                                                                                                                                  |                                          |
   |                                   | Normal cluster: not required                                                                                                                                                     |                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+

#. On the **Dashboard** page of Oozie, click **Stop Service** in the upper-right corner, and select **Restart Service** to restart Oozie.
