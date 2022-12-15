:original_name: admin_guide_000035.html

.. _admin_guide_000035:

Modifying Service Configuration Parameters
==========================================

Scenario
--------

To meet actual service requirements, cluster administrators can quickly view and modify default service configurations on FusionInsight Manager. Configure parameters based on the information provided in the configuration description.

.. note::

   The parameters of DBService cannot be modified when only one DBService role instance exists in the cluster.

Impact on the System
--------------------

-  After configuring properties of a service, you need to restart the service if the service status is **Expired**. The service is unavailable during the restart.
-  After the service configuration parameters are modified and then take effect after restart, you need to download and install the client again or download the configuration file to update the client. For example, you can modify configuration parameters of the following services: HBase, HDFS, Hive, Spark, YARN, and MapReduce.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Click the specified service name on the service management page.

#. Click **Configuration**.

   The **Basic Configuration** page is displayed by default. To modify more parameters, click the **All Configurations** tab. The navigation tree displays all configuration parameters of the service. The level-1 nodes in the navigation tree are service names or role names. The parameter category is displayed after the level-1 node is expanded.

#. In the navigation tree, select the specified parameter category and change the parameter values on the right.

   .. note::

      Select a port parameter value from the value range on the right. Ensure that all parameter values in the same service are within the value range and are unique. Otherwise, the service fails to be started.

   If you are not sure about the location of a parameter, you can enter the parameter name in search box in the upper right corner. The system searches for the parameter in real time and displays the result.

#. Click **Save**. In the confirmation dialog box, click **OK**.

   Wait until the message "Operation succeeded." is displayed. Click **Finish**.

   The configuration is modified.

   .. note::

      -  To update the queue configuration of the YARN service without restarting service, choose **More** > **Refresh Queue** to update the queue for the configuration to take effect.
      -  During configuration of the **flume.config.file** parameter, you can upload and download files. After a configuration file is uploaded, the old file will be overwritten. If the configuration is not saved and the service is restarted, the configuration does not take effect. Save the configuration in time.
      -  If you need to restart the service for the configuration to take effect after modifying service configuration parameters, choose **More** > **Restart Service** in the upper right corner of the service page.
