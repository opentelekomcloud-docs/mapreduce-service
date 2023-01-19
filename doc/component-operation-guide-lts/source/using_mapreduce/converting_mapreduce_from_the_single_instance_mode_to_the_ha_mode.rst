:original_name: mrs_01_0835.html

.. _mrs_01_0835:

Converting MapReduce from the Single Instance Mode to the HA Mode
=================================================================

Scenario
--------

The JobHistoryServer service of MapReduce is a single instance, or the single instance is used to install the MapReduce service during cluster installation. To avoid the MapReduce single point of failure (SPOF) problem, you can enable JobHistoryServer HA to ensure high availability of the MapReduce service.

Impact on the System
--------------------

-  Before the conversion, change the MapReduce server parameter **JHS_FLOAT_IP** to an available floating IP address. (The service IP address of the node is used by default in the single instance mode.)
-  During the conversion, component services that depend on MapReduce will expire. In this case, restart the expired component services, such as Yarn, Hive, and HBase.
-  After the conversion, update the configuration file of the Yarn client. If the configuration file is not updated, application task logs on the native Yarn page may fail to be queried.

Procedure
---------

#. Log in to Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **MapReduce** > **Configurations** to go to the configuration page of the MapReduce service.
#. Change the value of **JHS_FLOAT_IP** to an available floating IP address and click **Save**. On the displayed dialog box, click **OK**.
#. Choose **Instance** > **Add Instance**, select a node, and choose **Next** > **Next** > **Submit**. The instance is successfully added.
#. On the Manager home page, click |image1| next to the name of the target cluster and select **Restart Configuration-Expired Instances**. The instance is restarted successfully.
#. View the restarted instances. For example, the active and standby instances of MapReduce are normally displayed and run properly.

.. |image1| image:: /_static/images/en-us_image_0000001295899868.jpg
