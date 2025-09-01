:original_name: ALM-47001.html

.. _ALM-47001:

ALM-47001 MemArtsCC Service Unavailable
=======================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

The system checks the status of the ZooKeeper service on which the MemArtsCC depends every 60 seconds. This alarm is generated when the ZooKeeper service is unavailable.

This alarm is automatically cleared when the ZooKeeper service is normal.

Alarm Attributes
----------------

======== ============== ============== ============ ============
Alarm ID Alarm Severity Alarm Type     Service Type Auto Cleared
======== ============== ============== ============ ============
47001    Critical       Error handling MemArtsCC    Yes
======== ============== ============== ============ ============

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

The service will be unavailable.

Possible Causes
---------------

The ZooKeeper service on which the MemArtCC service depends is unavailable.

Handling Procedure
------------------

**Handling ZooKeeper exceptions**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. On the ZooKeeper dashboard page, check whether the ZooKeeper service is faulty.

   -  If yes, go to :ref:`2 <alm-47001__li1511344114716>`.
   -  If no, go to :ref:`4 <alm-47001__li10917181517316>`.

#. .. _alm-47001__li1511344114716:

   Rectify the ZooKeeper fault based on the error information and alarm information and the ZooKeeper help document.

3. After the ZooKeeper service becomes normal, wait for 60 seconds and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-47001__li10917181517316>`.

**Collect fault information.**

4. .. _alm-47001__li10917181517316:

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
