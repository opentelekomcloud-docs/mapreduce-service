:original_name: admin_guide_000008.html

.. _admin_guide_000008:

Managing Monitoring Metric Reports
==================================

Scenario
--------

On MRS Manager, you can customize monitoring items to display on the homepage and export monitoring data.

.. note::

   The interval on the horizontal axis of the chart varies depending on the time period you specify. Data monitoring rules are as follows:

   -  If the disk usage of the partition where GaussDB resides exceeds 80%, real-time monitoring data and monitoring data whose interval is 5 minutes will be deleted.
   -  **Storage resources (HDFS) in Tenant Resources (0 to 300 hours)**: The interval is 1 hour. The cluster must have been installed for at least 1 hour, and monitoring data of a maximum of 3 months is saved.

   **For clusters of versions earlier than MRS 3.3.0**:

   -  **0 to 25 hours**: The interval is 5 minutes. The cluster must have been installed for at least 10 minutes, and monitoring data of a maximum of 15 days is saved.
   -  **25 to 150 hours**: The interval is 30 minutes. The cluster must have been installed for at least 30 minutes, and monitoring data of a maximum of 3 months is saved.
   -  **150 to 300 hours**: The interval is 1 hour. The cluster must have been installed for at least 1 hour, and monitoring data of a maximum of 3 months is saved.
   -  **300 hours to 300 days**: The interval is 1 day. The cluster must have been installed for at least 1 day, and monitoring data of a maximum of 6 months is saved.
   -  **Over 300 days**: The interval is 7 days. The cluster must have been installed for more than 7 days, and monitoring data of a maximum of 1 year is saved.

   **For clusters of MRS 3.3.0 or later versions**:

   -  **0 to 21 hours and 20 minutes**: The interval is 5 minutes. The cluster must have been installed for at least 10 minutes, and monitoring data of a maximum of 90 days is saved.
   -  **21 hours and 20 minutes to 128 hours**: The interval is 30 minutes. The cluster must have been installed for at least 30 minutes, and monitoring data of a maximum of 90 days is saved.
   -  **128 to 256 hours**: The interval is 1 hour. The cluster must have been installed for at least 1 hour, and monitoring data of a maximum of 90 days is saved.
   -  **256 hours to 256 days**: The interval is 1 day. The cluster must have been installed for at least 1 day, and monitoring data of a maximum of 90 days is saved.

Customizing a Monitoring Metric Report
--------------------------------------

#. Log in to MRS Manager.
#. Choose **Homepage**.
#. In the upper right corner of the chart area, click |image1| and choose **Customize** from the displayed menu.

   .. note::

      Monitoring data of the past 1 hour is displayed at an interval of 5 minutes. After you enter the **Real-time Monitoring** page, you can view that real-time monitoring data is displayed on the right of the monitoring chart at an interval of 5 minutes.

#. In the left pane of the **Customize Statistics** dialog box, select a resource to monitor.
#. Select one or multiple monitoring metrics in the right pane.
#. Click **OK**.

Exporting All Monitoring Data
-----------------------------

#. Log in to MRS Manager.

#. Choose **Homepage**.

#. In the upper right corner of the chart area, select a time range to obtain monitoring data, for example, **1w**.

   Real-time data is displayed by default, which cannot be exported. You can click |image2| to customize a time range.

#. In the upper right corner of the chart area, click |image3| and choose **Export** from the displayed menu.

Exporting Monitoring Data of a Specified Monitoring Item
--------------------------------------------------------

#. Log in to MRS Manager.

#. Choose **Homepage**.

#. Click |image4| in the upper right corner of any monitoring report pane in the chart area of the target cluster.

#. Select a time range to obtain monitoring data, for example, **1w**.

   Real-time data is displayed by default, which cannot be exported. You can click |image5| to customize a time range.

#. Click **Export**.

.. |image1| image:: /_static/images/en-us_image_0000001442653701.png
.. |image2| image:: /_static/images/en-us_image_0000001392414434.png
.. |image3| image:: /_static/images/en-us_image_0000001442494085.png
.. |image4| image:: /_static/images/en-us_image_0000001392254902.png
.. |image5| image:: /_static/images/en-us_image_0000001442773665.png
