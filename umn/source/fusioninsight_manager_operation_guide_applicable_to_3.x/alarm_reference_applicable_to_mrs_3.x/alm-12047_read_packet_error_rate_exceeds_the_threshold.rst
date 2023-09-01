:original_name: ALM-12047.html

.. _ALM-12047:

ALM-12047 Read Packet Error Rate Exceeds the Threshold
======================================================

Description
-----------

The system checks the read packet error rate every 30 seconds. This alarm is generated when the read packet error rate exceeds the threshold (the default threshold is **0.5%**) for multiple times (the default value is **5**).

To change the threshold, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Packet Error Rate**.

If **Trigger Count** is **1**, this alarm is cleared when the read packet error rate is less than or equal to the threshold. If **Trigger Count** is greater than **1**, this alarm is cleared when the read packet error rate is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12047    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------+
| Name              | Meaning                                                           |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| Port Name         | Specifies the network port for which the alarm is generated.      |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The communication is intermittently interrupted, and services time out.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The network quality is poor.

Procedure
---------

**Check whether the threshold is set properly.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Packet Error Rate**, and check whether the alarm threshold is configured properly. The default value is **0.5%**. You can adjust the threshold as needed.

   -  If yes, go to :ref:`4 <alm-12047__li47122569144325>`.
   -  If no, go to :ref:`2 <alm-12047__li18938060144325>`.

#. .. _alm-12047__li18938060144325:

   Choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Packet Error Rate**. Click **Modify** in the **Operation** column to change the threshold.

   See :ref:`Figure 1 <alm-12047__fig35859496144325>`.

   .. _alm-12047__fig35859496144325:

   .. figure:: /_static/images/en-us_image_0000001532767698.png
      :alt: **Figure 1** Configuring the alarm threshold

      **Figure 1** Configuring the alarm threshold

#. After 5 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-12047__li47122569144325>`.

**Check whether the network connection is normal.**

4. .. _alm-12047__li47122569144325:

   Contact the network administrator to check whether the network is normal.

   -  If yes, rectify the fault and go to :ref:`5 <alm-12047__li52164171144325>`.
   -  If no, go to :ref:`6 <alm-12047__li66824355144325>`.

5. .. _alm-12047__li52164171144325:

   After 5 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12047__li66824355144325>`.

**Collect the fault information.**

6.  .. _alm-12047__li66824355144325:

    On FusionInsight Manager of the active cluster, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7.  Select **OMS** for **Service** and click **OK**.

8.  Expand the **Hosts** dialog box and select the alarm node and the active OMS node.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927350.png
