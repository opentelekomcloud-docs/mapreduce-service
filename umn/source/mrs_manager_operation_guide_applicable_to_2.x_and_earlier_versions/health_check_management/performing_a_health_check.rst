:original_name: mrs_01_0274.html

.. _mrs_01_0274:

Performing a Health Check
=========================

Scenario
--------

To ensure that cluster parameters, configurations, and monitoring are correct and that the cluster can run stably for a long time, you can perform a health check during routine maintenance.

.. note::

   A system health check includes MRS Manager, service-level, and host-level health checks:

   -  MRS Manager health checks focus on whether the unified management platform can provide management functions.
   -  Service-level health checks focus on whether components can provide services properly.
   -  Host-level health checks focus on whether host indicators are normal.

   The system health check includes three types of check items: health status, related alarms, and customized monitoring indicators for each check object. The health check results are not always the same as the **Health Status** on the portal.

Procedure
---------

-  Manually perform the health check for all services.

   #. Click **Services** and select the target service.
   #. Choose **More** > **Start Service Health Check** to start the health check for the service.

   .. note::

      -  The cluster health check includes Manager, service, and host status checks.
      -  To perform cluster health checks, you can also choose **System** > **Check Health Check** > **Start Cluster Health Check** on MRS Manager.
      -  To export the health check result, click **Export Report** in the upper left corner.

-  Manually perform the health check for a service.

   #. Click **Services**. In the services list, click the desired service name.
   #. Choose **More** > **Start Service Health Check** to start the health check for the service.

-  Manually perform the health check for a host.

   #. Click **Hosts**.
   #. Select the check box of the host for which you want to check the health status.
   #. Choose **More** > **Start Host Health Check** to start the health check for the host.

-  Automatically performing a health check

   #. Click **System**.

   #. Click **Check Health Status** under **Maintenance**.

   #. Click **Configure Health Check** to configure automatic health check items.

      **Periodic Health Check**: specifies whether to enable automatic health check. The **Periodic Health Check** function is disabled by default. You can click to enable the function and select **Daily**, **Weekly**, or **Monthly** based on management requirements.

   #. Click **OK** to save the settings. The **Health check configuration saved successfully** is displayed in the upper right corner.
