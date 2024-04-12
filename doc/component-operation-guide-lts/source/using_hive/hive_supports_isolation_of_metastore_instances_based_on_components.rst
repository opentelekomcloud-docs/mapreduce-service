:original_name: mrs_01_24467.html

.. _mrs_01_24467:

Hive Supports Isolation of Metastore instances Based on Components
==================================================================

Scenario
--------

This function restricts components in a cluster to connect to specified Hive Metastore instances. By default, components can connect to all Metastore instances. This function applies only to clusters whose version is MRS 3.2.0 or later.

Currently, only HetuEngine, Hive, Loader, Metadata, Spark2x and Flink can connect to Metastore in a cluster. The Metastore instances can be allocated in a unified manner.

.. note::

   -  This function only limits the Metastore instances accessed by component servers. Metadata is not isolated.
   -  Currently, Flink tasks can only connect to Metastore instances through the client.
   -  When spark-sql is used to execute tasks, the client is directly connected to Metastore. The client needs to be updated for the isolation to take effect.
   -  This function supports only isolation in the same cluster. If HetuEngine is deployed in different clusters, unified isolation configuration is not supported. You need to modify the HetuEngine configuration to connect to the specified Metastore instance.
   -  You are advised to configure at least two Metastore instances for each component to ensure availability during isolation configuration.

Prerequisites
-------------

The Hive service has been installed in the cluster and is running properly.

Procedure
---------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Hive**. On the displayed page, click the **Configurations** tab and then **All Configurations**, and search for the **HIVE_METASTORE_URI** parameter.

#. .. _mrs_01_24467__li31543502585:

   Set the value of **HIVE_METASTORE_URI_DEFAULT** to the URI connection string of all Metastore instances.

   |image1|

#. Connect a component to a specified Metastore instance. Copy the value in :ref:`2 <mrs_01_24467__li31543502585>`, modify the configuration items based on the component name, save the modification, and restart the component.

   The following example shows how Spark2x connects to only two Metastore instances of Hive.

   a. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Hive**. On the displayed page, click the **Configurations** tab and then **All Configurations**, and search for the **HIVE_METASTORE_URI** parameter.

   b. Copy the default configuration of **HIVE_METASTORE_URI_DEFAULT** to the URI configuration item of Spark2x. If Spark2x needs to connect to only two Metastore instances, retain two nodes as required. Click **Save**.

      |image2|

   c. Choose **Cluster** > **Services** > **Spark2x**. On the displayed page, click the **Instance** tab, select the instances whose configuration has expired, and choose **More** > **Restart Instance**. In the dialog box that is displayed, enter the password and click **OK** to restart the instances.

.. |image1| image:: /_static/images/en-us_image_0000001533544798.png
.. |image2| image:: /_static/images/en-us_image_0000001583504773.png
