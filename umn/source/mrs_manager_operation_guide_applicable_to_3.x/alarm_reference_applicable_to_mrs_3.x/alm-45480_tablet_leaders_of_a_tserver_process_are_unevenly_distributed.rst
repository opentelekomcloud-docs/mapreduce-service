:original_name: ALM-45480.html

.. _ALM-45480:

ALM-45480 Tablet Leaders of a Tserver Process Are Unevenly Distributed
======================================================================

Alarm Description
-----------------

The system checks the Kudu service status every 60 seconds. This alarm is generated when the ratio of tablet leaders of a Tserver process to total tablet leaders in the cluster exceeds the threshold.

This alarm is cleared when the ratio of tablet leaders of a Tserver process to total tablet leaders in the cluster becomes normal.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45480    Minor          Yes
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

If Tserver tablet leaders are unevenly distributed, the query performance of the Kudu engine deteriorates.

Possible Causes
---------------

-  Tserver instances are added or restarted.
-  The threshold is not properly set.

Handling Procedure
------------------

**Handle the uneven distribution of tablet leaders.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarm **ALM-45480 Tablet Leaders of a Tserver Process Are Unevenly Distributed** exists.

   -  If yes, go to :ref:`2 <alm-45480__li9323830151>`.
   -  If no, go to :ref:`8 <alm-45480__li04411042959>`.

#. .. _alm-45480__li9323830151:

   Log in to the Kudu node where the number of tablet leaders exceeds the threshold.

#. Run the following commands to manually adjust the number of tablet leaders:

   **su omm**

   **cd /opt/Bigdata/FusionInsight_Kudu\_**\ *xxx*\ **/install/FusionInsight-Kudu-xxx/kudu/bin**

   **./kudu tablet leader_step_down** *<master_addresses> <tablet_id>* **[-new_leader_uuid=**\ *<new_tablet_server_uuid>*\ **]**

   .. note::

      -  **master_addresses**: The value is in the format of **KuduMaster service IP address 1:7051,KuduMaster service IP address 2:7051,KuduMaster service IP address 3:7051**.

         **KuduMaster service IP address**: You can log in to MRS Manager and choose **Cluster** > **Services** > **Kudu** > **Instances** to view the service IP address of the KuduMaster instance.

      -  **tablet_id**: tablet ID to be adjusted.

         You can log in to Manager, choose **Cluster** > **Services** > **Kudu**, and click **KuduMaster(KuduMaster)** next to **KuduMaster WebUI** to access the KuduMaster web UI. Choose **Tables** on the menu bar, click the ID in the **Table Id** column, and obtain the target tablet ID in **Detail**.

      -  **new_tablet_server_uuid**: ID of the target tablet servers.

         You can log in to the KuduMaster web UI, choose **Tablet Servers** on the menu bar, and view the UUID.

      -  **new_leader_uuid**: You are advised to set the UUID of the node with a small number of tablet leaders.

#. Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45480__li1926420379516>`.

**Change the threshold.**

5. .. _alm-45480__li1926420379516:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarm **ALM-45480 Tablet Leaders of a Tserver Process Are Unevenly Distributed** exists.

   -  If yes, go to :ref:`6 <alm-45480__li426413371515>`.
   -  If no, go to :ref:`8 <alm-45480__li04411042959>`.

6. .. _alm-45480__li426413371515:

   Choose **Cluster** > **Kudu** > **Configurations** > **All Configurations** > **KuduMaster**, locate the alarm threshold parameter **TABLET_LEADER_UNBALANCE_SCALE**, change the value, and rolling-restart all Kudu Masters to make the configuration take effect.

7. Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45480__li04411042959>`.

**Collect fault information.**

8.  .. _alm-45480__li04411042959:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **Kudu** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
