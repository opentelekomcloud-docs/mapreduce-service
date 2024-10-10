:original_name: ALM-25008.html

.. _ALM-25008:

ALM-25008 SlapdServer CPU Usage Exceeds the Threshold
=====================================================

Alarm Description
-----------------

The system checks the CPU usage of the SlapdServer node every 30 seconds and compares the actual usage with the threshold. This alarm is generated when the SlapdServer CPU usage exceeds the threshold for multiple times (**5** by default).

Its **Trigger Count** is configurable. If **Trigger Count** is set to **1**, this alarm is cleared when the SlapdServer CPU usage is less than or equal to the threshold. If **Trigger Count** is greater than **1**, this alarm is cleared when the SlapdServer CPU usage is less than or equal to 90% of the threshold.

Alarm Attributes
----------------

+-----------------------+-----------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                    | Auto Cleared          |
+=======================+===================================+=======================+
| 25008                 | Critical (default threshold: 85%) | Yes                   |
|                       |                                   |                       |
|                       | Major (default threshold: 75%)    |                       |
+-----------------------+-----------------------------------+-----------------------+

Alarm Parameters
----------------

+-------------------+-------------------------------------------------------------------+
| Parameter         | Description                                                       |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Processes respond slowly or do not work.

Possible Causes
---------------

-  The alarm threshold or alarm trigger count is improperly configured.
-  The CPU configuration cannot meet service requirements, and the CPU usage reaches the upper limit.

Handling Procedure
------------------

**Check whether the alarm threshold or alarm trigger count is properly configured.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds**, click the name of the desired cluster, choose **LdapServer** > **Other** > **SlapdServer Service Total CPU Percentage**, and check whether the alarm trigger count and alarm threshold are set properly.

   -  If yes, go to :ref:`4 <alm-25008__li848412361466>`.
   -  If no, go to :ref:`2 <alm-25008__li174859361464>`.

#. .. _alm-25008__li174859361464:

   Change the trigger count and alarm threshold based on the actual CPU usage, and apply the changes.

#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-25008__li848412361466>`.

**Check whether the CPU usage reaches the upper limit.**

4. .. _alm-25008__li848412361466:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. In the right pane, click this alarm and obtain the host name in **Location**.

5. .. _alm-25008__li1248417366465:

   Choose **Cluster** > **Services** > **LdapServer**, click the **Instance** tab, and click the SlapdServer instance corresponding to the host name in :ref:`4 <alm-25008__li848412361466>`.

6. .. _alm-25008__li133258517208:

   On the dashboard of the instance, observe the real-time data of the **CPU Usage of a Single SlapdServer Instance** chart for about 5 minutes and check whether the CPU usage exceeds the threshold (**75%** by default) for multiple times.

   -  If yes, go to :ref:`7 <alm-25008__li14826210161714>`.
   -  If no, go to :ref:`9 <alm-25008__li89991152124618>`.

7. .. _alm-25008__li14826210161714:

   Check whether the status of other SlapdServer instances is normal. For details, see :ref:`5 <alm-25008__li1248417366465>` to :ref:`6 <alm-25008__li133258517208>`.

   -  If yes, contact the MRS cluster administrator to evaluate whether to expand the capacity of SlapdServer instances. Then, go to :ref:`8 <alm-25008__li12485203614616>`.
   -  If no, repair the faulty SlapdServer instance and go to :ref:`8 <alm-25008__li12485203614616>`.

8. .. _alm-25008__li12485203614616:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-25008__li89991152124618>`.

**Collect fault information.**

9.  .. _alm-25008__li89991152124618:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **LdapServer** for the target cluster.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002008258989.png
