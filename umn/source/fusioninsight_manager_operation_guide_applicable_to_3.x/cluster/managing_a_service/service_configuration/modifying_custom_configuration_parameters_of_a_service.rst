:original_name: admin_guide_000036.html

.. _admin_guide_000036:

Modifying Custom Configuration Parameters of a Service
======================================================

Scenario
--------

All open source parameters can be configured for all MRS cluster components. Parameters used in some key application scenarios can be modified on FusionInsight Manager, and some parameters of open source features may not be configured for some component clients. To modify the component parameters that are not directly supported by Manager, cluster administrators can add new parameters for components using the configuration customization function on Manager. Newly added parameters are saved in component configuration files and take effect after restart.

Impact on the System
--------------------

-  After configuring properties of a service, you need to restart the service if the service status is **Expired**. The service is unavailable during the restart.
-  After the service configuration parameters are modified and then take effect after restart, you need to download and install the client again or download the configuration file to update the client.

Prerequisites
-------------

Cluster administrators have fully understood the meanings of the parameters to be added, configuration files to take effect, and the impact on components.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Click the specified service name on the service management page.

#. Click **Configuration** and click **All Configurations**.

#. In the navigation tree on the left, locate a level-1 node and select **Customization**. The system displays the customized parameters of the current component.

   The configuration files that save the newly added custom parameters are displayed in the **Parameter File** column. Different configuration files may have same open source parameters. After the parameters in different files are set to different values, the configuration takes effect depends on the loading sequence of the configuration files by components. You can customize parameters for services and roles as required. Adding customized parameters for a single role instance is not supported.

#. Locate the row where a specified parameter resides, enter the parameter name supported by the component in the **Name** column and enter the parameter value in the **Value** column.

   You can click **+** or **-** to add or delete a customized parameter.

#. Click **Save**. In the displayed **Save Configuration** dialog box, confirm the modification and click **OK**. After the system displays "Operation succeeded", click **Finish**. The configuration is saved successfully.

   Restart the expired service or instance for the configuration to take effect.

Task Example (Configuring Customized Hive Parameters)
-----------------------------------------------------

Hive depends on HDFS. By default, Hive accesses the HDFS client. The configuration parameters that have taken effect are controlled by HDFS. For example, the HDFS parameter **ipc.client.rpc.timeout** affects the RPC timeout interval for all clients to connect to the HDFS server. Cluster administrators can modify the timeout interval for Hive to connect to HDFS by configuring custom parameters. After this parameter is added to the **core-site.xml** file of Hive, this parameter can be identified by the Hive service and its configuration overwrites the parameter configuration in HDFS.

#. On FusionInsight Manager, click **Cluster**, click the name of the desired cluster, and click **Services**.

#. On the displayed page, click **Configuration** and click **All Configurations**.

#. In the navigation tree on the left, select **Customization** for the Hive service. The system displays the custom service parameters supported by Hive.

#. In **core-site.xml**, locate the row that contains the **core.site.customized.configs** parameter, enter **ipc.client.rpc.timeout** in the **Name** column, and enter a new value in the **Value** column, for example, 150000. The unit is ms.

#. Click **Save**. In the displayed **Save Configuration** dialog box, confirm the modification and click **OK**. Wait until the message "Operation succeeded" is displayed, and click **Finish**.

   The configuration is saved successfully.

   After the configuration is saved, restart the expired service or instance for the configuration to take effect.
