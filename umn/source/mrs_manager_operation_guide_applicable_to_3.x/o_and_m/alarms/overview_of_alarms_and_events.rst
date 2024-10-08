:original_name: admin_guide_000070.html

.. _admin_guide_000070:

Overview of Alarms and Events
=============================

Alarms
------

Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. You can view information about alarms reported by all clusters, including the alarm name, ID, severity, and generation time. By default, the latest 10 alarms are displayed on each page.

You can click |image1| on the left of an alarm to view detailed alarm parameters. :ref:`Table 1 <admin_guide_000070__table19183175495311>` describes the parameters.

.. _admin_guide_000070__table19183175495311:

.. table:: **Table 1** Alarm parameters

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                     |
   +===================================+=================================================================================================================================================================+
   | Alarm ID                          | Alarm ID                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Alam Name                         | Alarm name                                                                                                                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Severity                          | Alarm severity. Value options are **Critical**, **Major**, **Minor**, and **Suggestion**.                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Generated                         | Time when an alarm is generated                                                                                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Cleared                           | Time when an alarm is cleared. If the alarm is not cleared, **--** is displayed.                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Source                            | Cluster name                                                                                                                                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Object                            | Service, process, or module that triggers the alarm                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Automatically Cleared             | Whether the alarm can be automatically cleared after the fault is rectified                                                                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Alarm Status                      | Current status of the alarm. Value options are **Auto**, **Manual**, and **Uncleared**.                                                                         |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Alarm Cause                       | Indicates the possible cause of an alarm.                                                                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Serial Number                     | Indicates the number of alarms generated by the system.                                                                                                         |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Additional Information            | Indicates the error information.                                                                                                                                |
   |                                   |                                                                                                                                                                 |
   |                                   | MRS 3.3.0 and later versions: You can view the monitoring metric values in **Additional Information** if thresholds are set for the metrics to generate alarms. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Location                          | Detailed information for locating the alarm, which includes the following:                                                                                      |
   |                                   |                                                                                                                                                                 |
   |                                   | -  **Source**: cluster for which the alarm is generated                                                                                                         |
   |                                   | -  **ServiceName**: service for which the alarm is generated                                                                                                    |
   |                                   | -  **RoleName**: role for which the alarm is generated                                                                                                          |
   |                                   | -  **HostName**: host for which the alarm is generated                                                                                                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Manage alarms.**

-  Click **Export All** to export all alarm details.
-  If multiple alarms have been handled, you can select one or more alarms to be cleared and click **Clear Alarm** to clear the alarms in batches. A maximum of 300 alarms can be cleared in each batch.
-  You can click |image2| to manually refresh the current page and click |image3| to filter columns to display.
-  You can filter alarms by object or cluster.
-  You can click **Advanced Search** to search for alarms by alarm ID, name, type, severity, start time, or end time. Click **Search** to filter alarms that meet the search criteria. Click **Advanced Search** again to view the number of search criteria that you have configured.
-  You can click **Clear**, **Mask**, or **View Help** to perform corresponding operations on an alarm.
-  If there are a large number of alarms, you can click **View by Category** to sort uncleared alarms by alarm ID. After alarms are classified, click the number of uncleared alarms to view alarm details.

Events
------

Log in to MRS Manager and choose **O&M** > **Alarm** > **Events**. On the **Events** page that is displayed, you can view information about all events in the cluster, including the event name, ID, severity, generation time, object, and location. By default, the latest 10 events are displayed on each page.


.. figure:: /_static/images/en-us_image_0000001392254906.png
   :alt: **Figure 1** Events page

   **Figure 1** Events page

You can click |image4| on the left of an event to view detailed event parameters. :ref:`Table 2 <admin_guide_000070__table13671201172912>` describes the parameters.

.. _admin_guide_000070__table13671201172912:

.. table:: **Table 2** Event parameters

   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                               |
   +===================================+===========================================================================================+
   | Event ID                          | Event ID                                                                                  |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Event Name                        | Event name                                                                                |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Severity                          | Event severity. Value options are **Critical**, **Major**, **Minor**, and **Suggestion**. |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Generated                         | Time when an event is generated                                                           |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Object                            | Object for which the event may be generated                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Serial Number                     | Number of the event generated by the system                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Location                          | Detailed information for locating the event, which includes the following:                |
   |                                   |                                                                                           |
   |                                   | -  **Source**: cluster for which the event is generated                                   |
   |                                   | -  **ServiceName**: service for which the event is generated                              |
   |                                   | -  **RoleName**: role for which the event is generated                                    |
   |                                   | -  **HostName**: host for which the event is generated                                    |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Additional Information            | Indicates the error information.                                                          |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Event Cause                       | Indicates the possible cause of an event.                                                 |
   +-----------------------------------+-------------------------------------------------------------------------------------------+
   | Source                            | Cluster name                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------+

**Manage events.**

-  Click **Export All** to export all event details.
-  You can click |image5| to manually refresh the current page and click |image6| to filter columns to display.
-  You can filter events by object or cluster.
-  You can click **Advanced Search** to search for events by event ID, name, severity, start time, or end time.

.. |image1| image:: /_static/images/en-us_image_0000001392574038.png
.. |image2| image:: /_static/images/en-us_image_0000001392574030.png
.. |image3| image:: /_static/images/en-us_image_0000001392414438.png
.. |image4| image:: /_static/images/en-us_image_0000001392414442.png
.. |image5| image:: /_static/images/en-us_image_0000001392574030.png
.. |image6| image:: /_static/images/en-us_image_0000001392733994.png
