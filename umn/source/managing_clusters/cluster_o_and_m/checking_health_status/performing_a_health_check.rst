:original_name: mrs_01_0224.html

.. _mrs_01_0224:

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

   On the MRS details page, choose **Management Operations** > **Start Cluster Health Check**.

   .. note::

      For the operations on MRS Manager of MRS 1.7.2 or earlier, see :ref:`Performing a Health Check <mrs_01_0274>`; for the operations on MRS Manager of MRS 3.\ *x* or later, see :ref:`Overview <admin_guide_000011>`.

      -  The cluster health check includes Manager, service, and host status checks.
      -  To perform cluster health checks, you can also choose **System** > **Check Health Status** > **Start Cluster Health Check** on MRS Manager.
      -  To export the health check result, click **Export Report** in the upper left corner.

-  Manually perform the health check for a service.

   #. On the MRS cluster details page, click **Components**.

      .. note::

         For versions earlier than MRS 1.7.2, see :ref:`Performing a Health Check <mrs_01_0274>`.

   #. Select the target service from the service list.
   #. Choose **More** > **Start Service Health Check** to start the health check for the service.

-  Manually perform the health check for a host.

   #. On the MRS details page, click **Nodes**.

      .. note::

         For MRS 1.7.2 or earlier, see :ref:`Performing a Health Check <mrs_01_0274>`. For MRS 3.\ *x* or later, see :ref:`Perform a Health Check <admin_guide_000076>`.

   #. Expand the node group information and select the check box of the host to be checked.
   #. Choose **Node** > **Start Host Health Check** to start the health check for the host.
