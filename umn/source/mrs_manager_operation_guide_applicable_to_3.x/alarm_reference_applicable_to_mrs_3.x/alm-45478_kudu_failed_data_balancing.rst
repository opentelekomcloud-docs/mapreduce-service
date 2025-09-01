:original_name: ALM-45478.html

.. _ALM-45478:

ALM-45478 Kudu Failed Data Balancing
====================================

Alarm Description
-----------------

The system periodically balances data among Kudu data tables. This alarm is generated when the system detects that the data balancing API returns a failure response.

This alarm is cleared when the Kudu data balancing API is successfully called.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45478    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+----------------------------------------------------------+
| Type                 | Parameter   | Description                                              |
+======================+=============+==========================================================+
| Location Information | Source      | Specifies the cluster for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

Failed to call the data balancing API. The Kudu component may be abnormal.

Possible Causes
---------------

The segment or replica in the Kudu data table is lost.

Handling Procedure
------------------

**Handle the Kudu instance exception.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the displayed page, locate alarm **ALM-45478 Kudu Failed Data Balancing**.

#. .. _alm-45478__li12115911627:

   In the **Location** field, record the host name and role name.

#. Choose **Cluster** > **Services** > **Kudu** > **Instances**. Click the role name for the host name obtained in :ref:`2 <alm-45478__li12115911627>` and restore the instance. Then, check whether the alarm is cleared.

   -  If yes, go to :ref:`4 <alm-45478__li101155118218>`.
   -  If no, go to :ref:`5 <alm-45478__li411513113216>`.

#. .. _alm-45478__li101155118218:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45478__li411513113216>`.

#. .. _alm-45478__li411513113216:

   On the Kudu web UI, check whether any segment or replica is missing.

**Collect fault information.**

6. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Kudu** for the target cluster.
8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.
9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
