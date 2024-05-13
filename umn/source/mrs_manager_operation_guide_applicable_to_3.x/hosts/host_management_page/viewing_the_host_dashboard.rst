:original_name: admin_guide_000052.html

.. _admin_guide_000052:

Viewing the Host Dashboard
==========================

Overview
--------

Log in to MRS Manager, click **Hosts**, and click a host name in the host list. The host details page contains the basic information area, disk status area, role list area, and monitoring chart.

Basic Information Area
----------------------

The basic information area contains the key information about the host, such as the management IP address, service IP address, host type, rack, firewall, number of CPU cores, and OS.

Disk Status Area
----------------

The disk status area contains all disk partitions configured for the cluster on the host and the usage of each disk partition.

Instance List Area
------------------

The instance list area displays all role instances installed on the host and the status of each role instance. You can click the log file next to a role instance name to view the log file content of the instance online.

Alarm and Event History
-----------------------

The alarm and event history area displays the key alarms and events reported by the current host. The system can display a maximum of 20 historical records.

Chart
-----

The monitoring chart area is displayed on the right of the host details page, and contains the key monitoring metrics of the host.

You can choose |image1| > **Customize** in the upper right corner to customize the monitoring reports to be displayed in the chart area. Select a time range and choose |image2| > **Export** to export detailed monitoring metric data within the specified time range.

You can click |image3| next to the title of a monitoring indicator to open the description of the monitoring indicator.

Click the **Chart** tab of the host to view the full monitoring chart information about the host.

GPU Card Status Area
--------------------

If the host is configured with GPU cards, the GPU card status area displays the model, location, and status of the GPU card installed on the host.

.. |image1| image:: /_static/images/en-us_image_0000001392414478.png
.. |image2| image:: /_static/images/en-us_image_0000001392254950.png
.. |image3| image:: /_static/images/en-us_image_0000001442773705.png
