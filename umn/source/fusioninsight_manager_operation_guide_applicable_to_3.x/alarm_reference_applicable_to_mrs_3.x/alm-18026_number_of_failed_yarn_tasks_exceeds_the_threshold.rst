:original_name: ALM-18026.html

.. _ALM-18026:

ALM-18026 Number of Failed Yarn Tasks Exceeds the Threshold
===========================================================

Description
-----------

The alarm module checks the number of failed applications in the Yarn root queue every 60 seconds. The alarm is generated when the number exceeds 50 for three consecutive times.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18026    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Cluster Name      | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Service Name      | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Role Name         | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

-  A large number of application tasks fail to be executed.
-  Failed tasks need to be submitted again.

Possible Causes
---------------

The task fails to be executed due to some error.

Procedure
---------

**Check the alarm details.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms** to go to the alarm page.

#. View **Additional Information** in the alarm details to check whether the alarm threshold is too small.

   -  If yes, go to :ref:`3 <alm-18026__li7914580481>`.
   -  If no, go to :ref:`4 <alm-18026__li691418874816>`.

#. .. _alm-18026__li7914580481:

   Choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Yarn** > **Other** > **Failed Applications of root queue** to modify the threshold. Go to :ref:`6 <alm-18026__li291712812484>`.

#. .. _alm-18026__li691418874816:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **ResourceManager(Active)** to access the ResourceManager web UI.

#. Click **FAILED** in **Applications** and click the task on the top. View the description of **Diagnostics** and rectify the fault based on the task failure causes.

#. .. _alm-18026__li291712812484:

   Wait for 3 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18026__li189131680485>`.

**Collect the fault information.**

7.  .. _alm-18026__li189131680485:

    On the FusionInsight Manager, choose O&M > Log > Download.

8.  Expand the **Service** drop-down list, and select **Yarn** for the target cluster.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417414.png
