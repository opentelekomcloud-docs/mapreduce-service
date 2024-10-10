:original_name: admin_guide_000007.html

.. _admin_guide_000007:

Overview
========

After you log in to MRS Manager, **Homepage** is displayed by default. On this page, the **Summary** tab displays the service statuses and monitoring status reports of each cluster, and the **Alarm Analysis** tab displays the statistics and analysis of top alarms.

-  On the right of the home page, you can view the number of alarms of different severities, number of running tasks, current user, and help information.

   -  Click |image1| to view the task name, cluster, status, progress, start time, and end time of the last 100 operation tasks in **Task Management Center**.

      .. note::

         For a start, stop, restart, or rolling restart task, you can abort it by clicking the task name in the task list, clicking **Abort**, and then entering the system administrator password in the dialog box that is displayed. An aborted task is no longer executed.

   -  Click |image2| to obtain help information.

      .. table:: **Table 1** Help information

         ===== =============================================
         Item  Description
         ===== =============================================
         About Provides the MRS Manager version information.
         ===== =============================================

-  The taskbar at the bottom of the home page displays the language options of MRS Manager and the current cluster time and time zone information. You can switch the system language as needed.

Service Status Preview Area
---------------------------

The number of hosts available in and the number of services installed in each cluster are displayed on the left of the homepage. You can click |image3| to expand all service information of the cluster and view the status and alarms of each service.

Click |image4| to perform basic O&M management operations on the current cluster. For details, see :ref:`Table 1 <admin_guide_000011__table17943743105914>`.

The |image5| icon on the left of each service name indicates that the service is running properly; the |image6| icon indicates that the current service fails to start; and the |image7| icon indicates that the current service is not started.

You can also check whether alarms have been generated for the service on the right of the service name. If alarms have been generated, the alarm severities and the number of alarms are displayed.

For components that support multiple services, if multiple services have been installed in the same cluster, the number of installed services is displayed on the right of each component.

The |image8| icon displayed on the right of the service name indicates that the service configuration has expired.

Monitoring Status Report Area
-----------------------------

The chart area is on the right of the homepage, which displays key monitoring metric reports, such as the status of all hosts in the cluster, host CPU usage, and host memory usage. You can customize monitoring reports to display in this area. For details about how to manage monitoring metrics, see :ref:`Managing Monitoring Metric Reports <admin_guide_000008>`.

You can view the data source of a monitoring chart in the lower left corner of the chart. You can zoom in on a monitoring report to view chart values more clearly or close the monitoring report.

Alarm Analysis
--------------

On the **Alarm Analysis** tab page, you can view the **Top 20 Alarms** table and **Analysis on Top 3 Alarms** chart. You can click an alarm name in the **Top 20 Alarms** table to view analysis information of this alarm only. Alarm analysis allows you to view top alarms and their occurrence time so you can handle alarms accordingly, improving system stability.

.. note::

   For MRS 3.3.0 and later versions, the alarm information page is different from that of other versions.

.. |image1| image:: /_static/images/en-us_image_0000001392734034.png
.. |image2| image:: /_static/images/en-us_image_0000001442494125.png
.. |image3| image:: /_static/images/en-us_image_0000001392254958.png
.. |image4| image:: /_static/images/en-us_image_0000001442653741.png
.. |image5| image:: /_static/images/en-us_image_0000001392574078.png
.. |image6| image:: /_static/images/en-us_image_0000001442653745.png
.. |image7| image:: /_static/images/en-us_image_0000001442653749.png
.. |image8| image:: /_static/images/en-us_image_0000001392414490.png
