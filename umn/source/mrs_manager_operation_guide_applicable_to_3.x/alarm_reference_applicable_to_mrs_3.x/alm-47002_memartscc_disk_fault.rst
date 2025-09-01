:original_name: ALM-47002.html

.. _ALM-47002:

ALM-47002 MemArtsCC Disk Fault
==============================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

The alarm module checks the status of the local disk used by MemArtsCC every 60 seconds. This alarm is generated when the alarm module detects that the disk status is abnormal. This alarm is cleared when the disk becomes normal.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
47002    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+-------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                       |
+======================+=============+===================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm is generated. |
+----------------------+-------------+-------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm is generated.           |
+----------------------+-------------+-------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm is generated.              |
+----------------------+-------------+-------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm is generated.              |
+----------------------+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

MemArtsCC becomes abnormal or its performance deteriorates.

Possible Causes
---------------

The disk used by MemArtsCC is damaged or the permission is read-only.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, search for "ALM-47002 MemArtsCC Disk Fault", and locate the abnormal disk directory based on the alarm information.

#. Contact O&M engineers to check whether the disk is faulty.

   -  If yes, replace the disk, restart the CCSideCar and CCWorker roles of the faulty node, and go to :ref:`3 <alm-47002__li41441647115312>`.
   -  If no, go to :ref:`4 <alm-47002__li10917181517316>`.

#. .. _alm-47002__li41441647115312:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-47002__li10917181517316>`.

**Collect fault information.**

4. .. _alm-47002__li10917181517316:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **MemArtsCC** for the target cluster.

6. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
