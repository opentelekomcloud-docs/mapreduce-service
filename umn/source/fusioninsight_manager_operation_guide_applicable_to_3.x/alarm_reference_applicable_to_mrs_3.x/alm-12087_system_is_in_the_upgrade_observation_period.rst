:original_name: ALM-12087.html

.. _ALM-12087:

ALM-12087 System Is in the Upgrade Observation Period
=====================================================

Description
-----------

The system checks whether it is in the upgrade observation period at 00:00 every day and checks whether the duration that it has been in the upgrade observation state exceeds the preset upgrade observation period, 10 days by default. This alarm is generated when the system is in the upgrade observation period and the duration that the system has been in the upgrade observation state exceeds the preset period (10 days by default). This alarm is automatically cleared if the system exits the upgrade observation period after the user performs a rollback or submission.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12087    Major          Yes
======== ============== ==========

Parameters
----------

+-----------------------------------+--------------------------------------------------------------------------+
| Name                              | Meaning                                                                  |
+===================================+==========================================================================+
| Source                            | Specifies the cluster or system for which the alarm is generated.        |
+-----------------------------------+--------------------------------------------------------------------------+
| ServiceName                       | Specifies the service for which the alarm is generated.                  |
+-----------------------------------+--------------------------------------------------------------------------+
| RoleName                          | Specifies the role for which the alarm is generated.                     |
+-----------------------------------+--------------------------------------------------------------------------+
| HostName                          | Specifies the host for which the alarm is generated.                     |
+-----------------------------------+--------------------------------------------------------------------------+
| Upgrade Observation Period (Days) | Specifies the days that the system is in the upgrade observation period. |
+-----------------------------------+--------------------------------------------------------------------------+

Impact on the System
--------------------

The next upgrade or patch installation will fail.

Possible Causes
---------------

The upgrade task is not submitted a specified period of time (10 days by default) after the system upgrade.

Procedure
---------

**Check whether the system is in the upgrade observation period.**

#. Log in to the active management node as user **root**.

#. Run the following commands to switch to user **omm** and log in to the **omm** database:

   **su - omm**

   **gsql -U omm -W** *omm database password* **-p 20015**

#. Run the **select \* from OM_CLUSTERS** command to view cluster information.

#. Check whether the value of **upgradObservationPeriod isON** is **true**, as shown in :ref:`Figure 1 <alm-12087__fig1299312444469>`.

   -  If it is, the system is in the upgrade observation period. Use the UpdateTool to submit the upgrade task. For details, see the upgrade guide of the corresponding version.

   -  If it is not, go to :ref:`6 <alm-12087__li5925153912518>`.

      .. _alm-12087__fig1299312444469:

      .. figure:: /_static/images/en-us_image_0000001532767554.png
         :alt: **Figure 1** Cluster information

         **Figure 1** Cluster information

5. In the early morning of the next day, check whether this alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`6 <alm-12087__li5925153912518>`.

**Collect fault information.**

6. .. _alm-12087__li5925153912518:

   On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

7. Select **Controller** from the **Service** and click **OK**.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927490.png
