:original_name: ALM-18025.html

.. _ALM-18025:

ALM-18025 Number of Terminated Yarn Tasks Exceeds the Threshold
===============================================================

Description
-----------

The alarm module checks the number of terminated applications in the Yarn root queue every 60 seconds. The alarm is generated when the number exceeds 50 for three consecutive times.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18025    Major          Yes
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

A large number of application tasks are forcibly terminated.

Possible Causes
---------------

-  The user forcibly terminates a large number of tasks.
-  The system terminates tasks due to some error.

Procedure
---------

**Check the alarm details.**

#. On the MRS Manager portal, choose **O&M > Alarm > Alarms** to go to the alarm page.

#. View **Additional Information** in the alarm details to check whether the alarm threshold is too small.

   -  If yes, go to :ref:`3 <alm-18025__li20880184714436>`.
   -  If no, go to :ref:`4 <alm-18025__li2088019471430>`.

#. .. _alm-18025__li20880184714436:

   Choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Yarn** > **Other** > **Terminated Applications of root queue** to modify the threshold. Go to :ref:`6 <alm-18025__li4883154713439>`.

#. .. _alm-18025__li2088019471430:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **ResourceManager(Active)** to access the ResourceManager web UI.

#. Click **KILLED** in **Applications** and click the task on the top. View the description of **Diagnostics** and rectify the fault based on the task termination details (for example, the task is terminated by a user).

#. .. _alm-18025__li4883154713439:

   Wait for 3 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18025__li4879124718434>`.

**Collect the fault information.**

7.  .. _alm-18025__li4879124718434:

    On the MRS Manager, choose **O&M > Log > Download**.

8.  Expand the **Service** drop-down list, and select **Yarn** for the target cluster.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087357.png
