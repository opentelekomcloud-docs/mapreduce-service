:original_name: admin_guide_000043.html

.. _admin_guide_000043:

Managing Instance Configurations
================================

Scenario
--------

Configuration parameters of each role instance can be modified. In the scenario where instances are migrated to a new cluster or the service is redeployed, the cluster administrator can import or export all configuration data of a service on MRS Manager to quickly copy configuration results.

MRS Manager can manage configuration parameters of a single role instance. Modifying configuration parameters and importing or exporting instance configurations do not affect other instances.

Impact on the System
--------------------

After modifying the configuration of a role instance, you need to restart the instance if the instance status is **Expired**. The role instance is unavailable during restart.

Modifying Instance Configuration
--------------------------------

#. Log in to MRS Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. On the page that is displayed, click the **Instance** tab.

#. Click the specified instance and select **Instance Configuration**.

   By default, **Basic Configuration** is displayed. To modify more parameters, click **All Configurations**. All parameter categories supported by the instance are displayed on the **All Configurations** tab page.

#. In the navigation tree, select the specified parameter category and change the parameter values on the right.

   If you are not sure about the location of a parameter, you can enter the parameter name in search box in the upper right corner. The system searches for the parameter in real time and displays the result.

#. Click **Save**. In the confirmation dialog box, click **OK**.

   Wait until the message "Operation succeeded." is displayed. Click **Finish**.

   The configuration is modified.

   .. note::

      After the configuration parameters of a role instance are modified, you need to restart the instance if the instance status is **Expired**. You can select the expired instance on the **Instances** page and choose **More** > **Restart Instance**.

Exporting/Importing Instance Configuration
------------------------------------------

#. Log in to MRS Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services**.
#. Click the specified service name on the service management page. On the displayed page, click the **Instance** tab.
#. Click the specified instance and select **Instance Configurations**.
#. Click **Export** to export the configuration parameter file to the local host.
#. On the **Instance Configurations** page, click **Import**, select the configuration parameter file of the instance, and import the file.
