:original_name: mrs_01_0248.html

.. _mrs_01_0248:

Synchronizing Service Configurations
====================================

Scenario
--------

If **Configuration Status** of a service is **Expired** or **Failed**, synchronize configurations for the cluster or service to restore its configuration status. If all services in the cluster are in the **Failed** state, synchronize the cluster configuration with the background configuration.

Impact on the System
--------------------

After synchronizing service configurations, you need to restart the services whose configurations have expired. These services are unavailable during restart.

Procedure
---------

#. On MRS Manager page, click **Services**.

#. Select the target service from the service list.

#. In the upper part of the service status and metric information, choose **More** > **Synchronize Configuration**.

#. In the displayed dialog box, select **Restart services and instances whose configuration have expired.** and click **OK** to restart the service whose configuration has expired.

   When **Operation successful** is displayed, click **Finish**. The service is started successfully.
