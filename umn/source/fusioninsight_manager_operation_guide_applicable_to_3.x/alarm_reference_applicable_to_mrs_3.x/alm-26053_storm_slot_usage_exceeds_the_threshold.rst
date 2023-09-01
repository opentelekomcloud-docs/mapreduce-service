:original_name: ALM-26053.html

.. _ALM-26053:

ALM-26053 Storm Slot Usage Exceeds the Threshold
================================================

Description
-----------

The system checks the slot usage every 60 seconds and compares the actual slot usage with the threshold. This alarm is generated when the slot usage is greater than the threshold.

You can change the threshold in **O&M** > **Alarm** > **Thresholds**.

This alarm is cleared when the slot usage is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
26053    Major          Yes
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
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

New Storm tasks cannot be performed.

Possible Causes
---------------

-  The status of some Supervisors in the cluster is abnormal.
-  The status of all Supervisors is normal, but the processing capability is insufficient.

Procedure
---------

**Check the Supervisor status.**

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Storm** > **Instance** to go to the Storm instance management page.

#. Check whether any instance whose status is **Faulty** or **Restoring** exists.

   -  If yes, go to :ref:`3 <alm-26053__li3410841620655>`.
   -  If no, go to :ref:`5 <alm-26053__li4446687120655>`.

#. .. _alm-26053__li3410841620655:

   Select Supervisor role instances whose status is **Faulty** or **Restoring**, choose **More** > **Restart Instance**, and check whether the instances restart successfully.

   -  If yes, go to :ref:`4 <alm-26053__li6572378120655>`.
   -  If no, go to :ref:`10 <alm-26053__li1692048320655>`.

#. .. _alm-26053__li6572378120655:

   Wait several minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-26053__li4446687120655>`.

**Increase the number of slots in each Supervisor.**

5. .. _alm-26053__li4446687120655:

   Log in to the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Storm** > **Configurations** > **All** **Configurations**.

6. Increase the number of ports in the **supervisor.slots.ports** parameter of each Supervisor role and restart the instance.

7. Wait several minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-26053__li517745320655>`.

8. .. _alm-26053__li517745320655:

   Perform capacity expansion for Supervisor.

9. Wait several minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-26053__li1692048320655>`.

      .. note::

         Services are interrupted when the Supervisor is being restarted. Then, services are restored after the restarting.

**Collect fault information.**

10. .. _alm-26053__li1692048320655:

    On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

11. Select **Storm** and **ZooKeeper** in the required cluster from the **Service** drop-down list box.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127341.png
