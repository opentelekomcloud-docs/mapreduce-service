:original_name: ALM-26052.html

.. _ALM-26052:

ALM-26052 Number of Available Supervisors of the Storm Service Is Less Than the Threshold
=========================================================================================

Description
-----------

The system periodically checks the number of available Supervisors every 60 seconds and compares the number of available Supervisors with the threshold. This alarm is generated when the number of available Supervisors is less than the threshold.

You can change the threshold in **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster*.

This alarm is cleared when the number of available Supervisors is greater than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
26052    Major          Yes
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

Existing tasks in the cluster cannot be performed. The cluster can receive new Storm tasks, but cannot perform these tasks.

Possible Causes
---------------

The status of some Supervisors in the cluster is abnormal.

Procedure
---------

**Check the Supervisor status.**

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Storm** > **Supervisor** to go to the Storm service management page.

#. In **Roles**, check whether any instance whose status is **Faulty** or **Restoring** exists.

   -  If yes, go to :ref:`3 <alm-26052__li14723901201046>`.
   -  If no, go to :ref:`5 <alm-26052__li59911910201046>`.

#. .. _alm-26052__li14723901201046:

   Select Supervisor role instances whose status is **Faulty** or **Restoring**, choose **More** > **Restart Instance**, and check whether the instances restart successfully.

   -  If yes, go to :ref:`4 <alm-26052__li58537778201046>`.
   -  If no, go to :ref:`5 <alm-26052__li59911910201046>`.

#. .. _alm-26052__li58537778201046:

   Wait for 30 seconds, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-26052__li59911910201046>`.

      .. note::

         Services are interrupted when the Supervisor is being restarted. Then, services are restored after the restarting.

**Collect fault information.**

5. .. _alm-26052__li59911910201046:

   On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

6. Select **Storm** and **ZooKeeper** in the required cluster from the **Service** drop-down list box.

7. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127329.png
