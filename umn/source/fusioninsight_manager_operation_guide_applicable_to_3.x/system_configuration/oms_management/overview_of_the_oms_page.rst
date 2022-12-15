:original_name: admin_guide_000160.html

.. _admin_guide_000160:

Overview of the OMS Page
========================

Overview
--------

Log in to FusionInsight Manager and choose **System** > **OMS**. You can perform maintenance operations on the OMS page, including viewing basic information, viewing the service status of OMS service modules, and manually triggering health checks.

.. note::

   OMS is the management node of the O&M system. Generally, there are two OMS nodes that work in active/standby mode.

Basic Information
-----------------

OMS-associated information is displayed on FusionInsight Manager, as listed in :ref:`Table 1 <admin_guide_000160__table14579151510169>`.

.. _admin_guide_000160__table14579151510169:

.. table:: **Table 1** OMS information

   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item            | Description                                                                                                                                               |
   +=================+===========================================================================================================================================================+
   | Version         | Indicates the OMS version, which is consistent with the FusionInsight Manager version.                                                                    |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IP Mode         | Indicates the IP address mode of the current cluster network.                                                                                             |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HA Mode         | Indicates the OMS working mode, which is specified by the configuration file during FusionInsight Manager installation.                                   |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Current Active  | Indicates the host name of the active OMS node, that is, the host name of the active management node. Click a host name to go to the host details page.   |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Current Standby | Indicates the host name of the standby OMS node, that is, the host name of the standby management node. Click a host name to go to the host details page. |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Duration        | Indicates the duration for starting the OMS process.                                                                                                      |
   +-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

OMS Service Status
------------------

FusionInsight Manager displays the running status of all OMS service modules. If the status of each service module is displayed as |image1|, the OMS is running properly.

Health Check
------------

You can click **Health Check** on the OMS page to check the OMS status. If some check items are faulty, you can view the check description for troubleshooting.

Entering or Exiting Maintenance Mode
------------------------------------

Configure OMS to enter or exit the maintenance mode.

System Parameters
-----------------

Connect to the DMPS cluster in large-scale cluster scenarios.

.. |image1| image:: /_static/images/en-us_image_0263899675.png
