:original_name: ALM-38014.html

.. _ALM-38014:

ALM-38014 Total Produce Request Latency Exceeds the Threshold
=============================================================

Alarm Description
-----------------

The system checks the total latency of Produce requests on Broker instances every 30 seconds. This alarm is generated when the total latency of Produce requests on a Broker instance has exceeded the threshold for 10 consecutive times.

This alarm is cleared when the total latency of Produce requests is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.5.0 or later.

Alarm Attributes
----------------

+-----------------------+--------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                       | Auto Cleared          |
+=======================+======================================+=======================+
| 38014                 | Critical (default threshold: 120000) | Yes                   |
|                       |                                      |                       |
|                       | Major (default threshold: 60000)     |                       |
+-----------------------+--------------------------------------+-----------------------+

Alarm Parameters
----------------

+----------------------+-------------+----------------------------------------------------------+
| Type                 | Parameter   | Description                                              |
+======================+=============+==========================================================+
| Location Information | Source      | Specifies the cluster for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

The total latency of Produce requests on the Broker instance exceeds the threshold. For latency-sensitive services, a large number of service query requests may time out.

Possible Causes
---------------

-  The number of threads used by the Broker instance to process requests is incorrectly configured.
-  A slow disk fault has occurred.
-  The Broker disk I/O is busy.
-  Broker partitions are unevenly distributed, and hotspotting has occurred.

Handling Procedure
------------------

**Check whether the number of threads used by the Broker instance to process requests is appropriate.**

#. Log in to MRS Manager and choose **Cluster** > **Services** > **Kafka**. On the page that is displayed, click **Configurations** and then **All Configurations**.
#. Search for and check the value of **num.io.threads**. If the value is too small, increase it. You are advised to change the value to twice the number of CPU cores. The maximum value is **64**. Save the configuration.
#. Click the **Instances** tab, select all Broker instances, click **More**, and select **Instance Rolling Restart**.

   .. note::

      **Services may be affected or interrupted during the restart. Restart the instances during off-peak hours.**

#. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-38014__en-us_topic_0000001960602962_li87691941020>`.

**Check whether a slow disk fault has occurred.**

5. .. _alm-38014__en-us_topic_0000001960602962_li87691941020:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, view the host name for which this alarm is generated.

6. Check whether alarm **Slow Disk Fault** or **Disk Unavailable** is generated for the same node in :ref:`5 <alm-38014__en-us_topic_0000001960602962_li87691941020>`.

   -  If yes, rectify the fault by following the handling procedure of **ALM-12033 Slow Disk Fault** or **ALM-12063 Disk Unavailable**.
   -  If no, go to :ref:`8 <alm-38014__en-us_topic_0000001960602962_li101192197102>`.

7. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-38014__en-us_topic_0000001960602962_li101192197102>`.

**Check whether the Broker disk I/O is busy.**

8. .. _alm-38014__en-us_topic_0000001960602962_li101192197102:

   Check whether alarm **Busy Broker Disk I/Os** exists on the node for which this alarm is generated in :ref:`5 <alm-38014__en-us_topic_0000001960602962_li87691941020>`.

   -  If yes, rectify the fault by following the handling procedure of **ALM-38009 Busy Broker Disk I/Os** and then go to :ref:`9 <alm-38014__en-us_topic_0000001960602962_li511916193102>`.
   -  If no, go to :ref:`10 <alm-38014__en-us_topic_0000001960602962_li3896194118387>`.

9. .. _alm-38014__en-us_topic_0000001960602962_li511916193102:

   Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-38014__en-us_topic_0000001960602962_li3896194118387>`.

**Check whether Broker partitions are evenly distributed and hotspotting has occurred.**

10. .. _alm-38014__en-us_topic_0000001960602962_li3896194118387:

    Choose **Cluster** > **Services** > **Kafka** > **Chart**, select **Partition** from the **Chart Category** area, zoom in **Number of Partitions-All Instances** in the upper right corner, and click **Distribution** to check whether partitions are evenly distributed on Broker.


    .. figure:: /_static/images/en-us_image_0000002447402305.png
       :alt: **Figure 1** Example of uneven partition distribution on Broker

       **Figure 1** Example of uneven partition distribution on Broker

    -  If yes, go to :ref:`13 <alm-38014__en-us_topic_0000001960602962_li1473912318017>`.
    -  If no, go to :ref:`11 <alm-38014__en-us_topic_0000001960602962_li17855621113716>`.

11. .. _alm-38014__en-us_topic_0000001960602962_li17855621113716:

    Click the uneven distribution bar on the rightmost, and check whether the node obtained in :ref:`5 <alm-38014__en-us_topic_0000001960602962_li87691941020>` is included in the unevenly distributed instances. If it is, perform data balancing.

12. Wait 5 minutes and check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-38014__en-us_topic_0000001960602962_li1473912318017>`.

**Collect fault information.**

13. .. _alm-38014__en-us_topic_0000001960602962_li1473912318017:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

14. Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

15. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact O&M engineers and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
