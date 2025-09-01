:original_name: ALM-45449.html

.. _ALM-45449:

ALM-45449 The Counter Number of zxid Used by ClickHouse Exceeds the Threshold
=============================================================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

ClickHouse uses ZooKeeper Transaction ID (**zxid**) to manage transactions. The **zxid** is a 64-bit number used to keep consistency of the distributed system. The **zxid** has two parts: the high order 32-bits for the epoch and the low order 32-bits for the counter. The epoch number represents the lifecycle of the leader, and the counter number indicates the location of a transaction in the request. Each time a new transaction is generated, the counter number is automatically increased by 1. When the value of **zxid** reaches the maximum value, that is, the counter number reaches **0xffffffff**, the cluster forcibly elects the leader and ZooKeeper is unavailable in a short period. The system checks the counter number every two hours. This alarm is generated when the the counter number of **zxid** exceeds the threshold.

This alarm is cleared when the counter number is smaller than the threshold.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45449    Major          Quality of service ClickHouse   Yes
======== ============== ================== ============ ============

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

ZooKeeper leader election is forcibly triggered at an uncertain time, which may interrupt the ClickHouse service.

Possible Causes
---------------

The counter number of ZooKeeper zxid exceeds the threshold.

Handling Procedure
------------------

#. Log in to MRS Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the **Dashboard** page of the ZooKeeper service, click **More** and select **Service Rolling Restart** in the upper right corner. In the displayed dialog box, enter the password and click **OK**. On the **Service Rolling Restart** page, click **OK** and wait until the rolling restart of the ZooKeeper service is complete.

   .. note::

      Restart the ZooKeeper service during off-peak hours of ClickHouse.

#. Wait for 2 hours and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-45449__li1461914620531>`.

**Collect fault information.**

3. .. _alm-45449__li1461914620531:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

4. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

5. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

6. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
