:original_name: ALM-14023.html

.. _ALM-14023:

ALM-14023 Percentage of Total Reserved Disk Space for Replicas Exceeds the Threshold
====================================================================================

Description
-----------

The system checks the percentage of total reserved disk space for replicas (Total reserved disk space for replicas/(Total reserved disk space for replicas + Total remaining disk space)) every 30 seconds and compares the actual percentage with the threshold (**90%** by default). This alarm is generated when the percentage of total reserved disk space for replicas exceeds the threshold for multiple consecutive times (**Trigger Count**).

The alarm is cleared in the following two scenarios: The value of **Trigger Count** is **1** and the percentage of total reserved disk space for replicas is less than or equal to the threshold; the value of **Trigger Count** is greater than **1** and the percentage of total reserved disk space for replicas is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14023    Minor          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| NameServiceName   | Specifies the NameService service for which the alarm is generated.                                                          |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The performance of writing data to HDFS is affected. If all remaining DataNode space is reserved for replicas, writing HDFS data fails.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The disk space configured for the HDFS cluster is insufficient.
-  The volume of services that access HDFS is too large and therefore DataNode is overloaded.

Procedure
---------

**Check whether the alarm threshold is appropriate.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **HDFS** > **Disk** > **Percentage of Reserved Space for Replicas of Unused Space** to check whether the alarm threshold is appropriate. (The default threshold is **90%**. Users can change it as required.)

   -  If yes, go to :ref:`4 <alm-14023__li13034211102848>`.
   -  If no, go to :ref:`2 <alm-14023__li44798865102848>`.

#. .. _alm-14023__li44798865102848:

   Choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **HDFS** > **Disk** > **Percentage of Reserved Space for Replicas of Unused Space** and Click **Modify,** change the threshold based on the actual usage.

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14023__li13034211102848>`.

**Check whether an alarm indicating insufficient disk space is generated.**

4. .. _alm-14023__li13034211102848:

   On the FusionInsight Manager portal, check whether **ALM-14001 HDFS Disk Usage Exceeds the Threshold** or **ALM-14002 DataNode Disk Usage Exceeds the Threshold** exists on the **O&M > Alarm > Alarms** page.

   -  If yes, go to :ref:`5 <alm-14023__li31013859102848>`.
   -  If no, go to :ref:`7 <alm-14023__li16883378102848>`.

5. .. _alm-14023__li31013859102848:

   Handle the alarm by referring to instructions in **ALM-14001 HDFS Disk Usage Exceeds the Threshold** or **ALM-14002 DataNode Disk Usage Exceeds the Threshold** and check whether the alarm is cleared.

   -  If yes, go to :ref:`6 <alm-14023__li20775880102848>`.
   -  If no, go to :ref:`7 <alm-14023__li16883378102848>`.

6. .. _alm-14023__li20775880102848:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-14023__li16883378102848>`.

**Expand the DataNode capacity.**

7. .. _alm-14023__li16883378102848:

   Expand the DataNode capacity.

8. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14023__li35167437102848>`.

**Collect fault information.**

9.  .. _alm-14023__li35167437102848:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

10. Select **HDFS** in the required cluster from the **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 20 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448202.png
