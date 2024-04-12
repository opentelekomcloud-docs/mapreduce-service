:original_name: mrs_01_24738.html

.. _mrs_01_24738:

Load Balancing for Hive MetaStore Client Connection
===================================================

Scenario
--------

The client connection of Hive MetaStore supports load balancing. That is, heavy load of a single MetaStore node during heavy service traffic can be avoided by connecting to the node with the least connections based on the connection number recorded in ZooKeeper. Enabling this function does not affect the original connection mode.

.. note::

   This section applies to MRS 3.2.0 or later.

Procedure
---------

#. Log in to FusionInsight Manager, click **Cluster**, choose **Services** > **Hive**, click **Configurations**, and then **All Configurations**.

#. Search for the **hive.metastore-ext.balance.connection.enable** parameter and set its value to **true**.

#. Click **Save**.

#. Click **Instance**, select all instances, choose **More** > **Restart Instance**, enter the password, and click **OK** to restart all Hive instances.

#. For other components that connect to MetaStore, add the **hive.metastore-ext.balance.connection.enable** parameter and set its value to **true**.

   The following example shows how to add this parameter if Spark2x needs to be connected to MetaStore:

   a. Log in to FusionInsight Manager, click **Cluster**, choose **Services** > **Spark2x**, and click **Configurations**.
   b. Click **Customization**, add a custom parameter **hive.metastore-ext.balance.connection.enable** to all **hive-site.xml** parameter files, set its value to **true**, and click **Save**.
   c. Click **Instance**, select all configuration-expired instances, choose **More** > **Restart Instance**, enter the password, and click **OK** to restart them.
