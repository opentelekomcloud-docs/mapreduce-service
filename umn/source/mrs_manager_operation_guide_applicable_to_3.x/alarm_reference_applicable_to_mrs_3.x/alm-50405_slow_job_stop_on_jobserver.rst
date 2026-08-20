:original_name: ALM-50405.html

.. _ALM-50405:

ALM-50405 Slow Job Stop on JobServer
====================================

.. note::

   This section applies only to MRS 3.5.1 and later versions.

Alarm Description
-----------------

The system checks the latency for stopping jobs every 30 seconds on the JobServer. This alarm is generated when the latency exceeds the threshold (10 seconds by default).

This alarm is cleared when the latency is lower than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50405    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

It takes a long time to stop a job, for example, through the REST API.

Possible Causes
---------------

The number of concurrent requests to JobServer on a node surges, or underlying services like YARN and HDFS take a long time to respond.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, search for the alarm "ALM-50405 Slow Job Stop on JobServer", locate the abnormal JobServer instance node according to alarm information, and obtain the alarm value from additional information.

#. On the alarm page, check whether there is a JobServer, YARN, or HDFS fault alarm.

   -  If yes, go to :ref:`3 <alm-50405__en-us_topic_0000002481675140_en-us_topic_0000002164351389_li9333108144418>`.
   -  If no, go to :ref:`4 <alm-50405__en-us_topic_0000002481675140_en-us_topic_0000002164351389_li1263992516714>`.

#. .. _alm-50405__en-us_topic_0000002481675140_en-us_topic_0000002164351389_li9333108144418:

   Rectify the fault by referring to the alarm help. Then, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-50405__en-us_topic_0000002481675140_en-us_topic_0000002164351389_li1263992516714>`.

#. .. _alm-50405__en-us_topic_0000002481675140_en-us_topic_0000002164351389_li1263992516714:

   Ignore the alarm. Check whether the alarm is cleared when service load goes down.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50405__en-us_topic_0000002481675140_en-us_topic_0000002164351389_li10879143910158>`.

**Collect fault information.**

5. .. _alm-50405__en-us_topic_0000002481675140_en-us_topic_0000002164351389_li10879143910158:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **JobGateway** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
