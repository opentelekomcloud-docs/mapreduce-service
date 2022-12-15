:original_name: mrs_01_0113.html

.. _mrs_01_0113:

Viewing and Manually Clearing an Alarm
======================================

Scenario
--------

You can view and clear alarms on MRS.

Generally, the system automatically clears an alarm when the fault is rectified. If the fault has been rectified and the alarm cannot be automatically cleared, you can manually clear the alarm.

You can view the latest 100,000 alarms (including uncleared, manually cleared, and automatically cleared alarms) on MRS. If the number of cleared alarms exceeds 100,000 and is about to reach 110,000, the system automatically dumps the earliest 10,000 cleared alarms to the dump path.

3. In versions earlier than x, the value is the same as that of ${BIGDATA_HOME}/OMSV100R001C00x8664/workspace/data for the active management node.

(For 3.x and later versions) The path is **${BIGDATA_HOME}/om-server/OMS/workspace/data** of the active management node.

A directory is automatically generated when alarms are dumped for the first time.

.. note::

   Set an automatic refresh interval or click |image1| for an immediate refresh.

   The following refresh interval options are supported:

   -  Refresh every 30 seconds
   -  Refresh every 60 seconds
   -  Stop refreshing

Procedure
---------

#. Choose **Clusters > Active Clusters** and click a cluster name to go to the cluster details page.
#. Click **Alarms** and view the alarm information in the alarm list.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Viewing and Manually Clearing an Alarm <mrs_01_0237>`.

   -  By default, the alarm list page displays the latest 10 alarms.
   -  By default, data is sorted in descending order based on the generation time. For MRS 3.x or earlier, you can click the alarm ID, severity, and generation time to modify the sorting mode. For clusters of MRS 3.x or later, you can click the severity and generation time to modify the sorting mode.
   -  You can filter all alarms of the same severity. The results include cleared and uncleared alarms.
   -  For clusters of MRS 3.x and earlier versions, you can click |image2|, |image3|, |image4| or |image5| in the upper right corner of the page to quickly filter **Critical**, **Major**, **Minor**, or **Suggestion** alarms that are uncleared.
   -  For clusters of MRS 3.x or later: You can click |image6|, |image7|, |image8| or |image9| in the upper right corner of the page to quickly filter uncleared **Critical**, **Major**, **Minor** or **Warning** alarms.

3. Click **Advanced Search**. In the displayed alarm search area, set search criteria and click **Search** to view the information about specified alarms. You can click **Reset** to clear the search criteria.

   .. note::

      The start time and end time are specified in **Time Range**. You can search for alarms generated within the time range.

   Handle the alarm by referring to **Alarm Reference**. If the alarms in some scenarios are generated due to other cloud services that MRS depends on, you need to contact maintenance personnel of the corresponding cloud services.

4. If the alarm needs to be manually cleared after errors are rectified, click **Clear Alarm**.

   .. note::

      If multiple alarms have been handled, you can select one or more alarms to be cleared and click **Clear Alarm** to clear the alarms in batches. A maximum of 300 alarms can be cleared in each batch.

Exporting Alarms
----------------

#. Choose **Clusters > Active Clusters** and click a cluster name to go to the cluster details page.
#. Click **Alarm Management** > **Alarms**.
#. Click **Export All**.
#. In the displayed dialog box, select the type and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001348737925.png
.. |image2| image:: /_static/images/en-us_image_0000001296058164.jpg
.. |image3| image:: /_static/images/en-us_image_0000001295898324.jpg
.. |image4| image:: /_static/images/en-us_image_0000001296058168.jpg
.. |image5| image:: /_static/images/en-us_image_0000001295738372.jpg
.. |image6| image:: /_static/images/en-us_image_0000001348738185.jpg
.. |image7| image:: /_static/images/en-us_image_0000001296217800.jpg
.. |image8| image:: /_static/images/en-us_image_0000001349257461.jpg
.. |image9| image:: /_static/images/en-us_image_0000001349057985.jpg
