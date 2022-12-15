:original_name: mrs_01_0237.html

.. _mrs_01_0237:

Viewing and Manually Clearing an Alarm
======================================

Scenario
--------

You can view and clear alarms on MRS Manager.

Generally, the system automatically clears an alarm when the fault is rectified. If the fault has been rectified and the alarm cannot be automatically cleared, you can manually clear the alarm.

You can view the latest 100,000 alarms (including uncleared, manually cleared, and automatically cleared alarms) on MRS Manager. If the number of cleared alarms exceeds 100,000 and is about to reach 110,000, the system automatically dumps the earliest 10,000 cleared alarms to **${BIGDATA_HOME}/OMSV100R001C00x8664/workspace/data** on the active management node. A directory is automatically generated when alarms are dumped for the first time.

.. note::

   Set an automatic refresh interval or click |image1| for an immediate refresh.

   The following refresh interval options are supported:

   -  Refresh every 30 seconds
   -  Refresh every 60 seconds
   -  Stop refreshing

Procedure
---------

#. On MRS Manager, click **Alarms** to view the alarm information in the alarm list.

   -  By default, the alarm list page displays the latest 10 alarms.
   -  By default, alarms are displayed in descending order by **Generated**. You can click **Alarm ID**, **Alarm Name**, **Severity**, **Generated**, **Location**, **Operation** to change the display mode.
   -  You can filter all alarms of the same severity in **Severity**, including cleared and uncleared alarms.
   -  You can click |image2|, |image3|, |image4|, or |image5| to filter out **Critical**, **Major**, **Minor**, or **Warning** alarms.

2. Click **Advanced Search**. In the displayed alarm search area, set search criteria and click **Search** to view the information about specified alarms. Click **Reset** to clear the search criteria.

   .. note::

      You can set the **Start Time** and **End Time** to specify the time range. You can search for alarms generated within the time range.

   Handle the alarm by referring to **Alarm Reference**. If the alarms in some scenarios are generated due to other cloud services that MRS depends on, you need to contact maintenance personnel of the corresponding cloud services.

3. If the alarm needs to be manually cleared after errors are rectified, click **Clear Alarm**.

   .. note::

      If multiple alarms have been handled, you can select one or more alarms to be cleared and click **Clear Alarm** to clear the alarms in batches. A maximum of 300 alarms can be cleared in each batch.

.. |image1| image:: /_static/images/en-us_image_0000001348737925.png
.. |image2| image:: /_static/images/en-us_image_0000001348738141.jpg
.. |image3| image:: /_static/images/en-us_image_0000001295898280.jpg
.. |image4| image:: /_static/images/en-us_image_0000001349137829.jpg
.. |image5| image:: /_static/images/en-us_image_0000001349257417.jpg
