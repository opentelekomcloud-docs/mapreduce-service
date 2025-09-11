:original_name: ALM-45481.html

.. _ALM-45481:

ALM-45481 KuduTserver Has Full Disks
====================================

The system checks Kudu disk metrics every 60 seconds. This alarm is generated when the number of fully occupied disks for a Tserver is not 0.

This alarm is automatically cleared when the number of fully occupied disks for the Tserver becomes 0.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45481    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the threshold for triggering the alarm.        |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

Users cannot use the Kudu service properly.

Possible Causes
---------------

The disk configuration cannot meet service requirements, and the disk space used by the Kudu service is insufficient.

Handling Procedure
------------------

**Check the disk capacity and delete unnecessary files and data tables.**

#. Log in to MRS Manager. In the alarm list, click the drop-down arrow in the row that contains the alarm, and view the role name and the IP address of the hostname in **Location**.

#. .. _alm-45481__li64021312132010:

   Log in to the node for which the alarm is generated as user **root** and run the **df -h** command to check the mount directory where the disk usage is 100%.

#. Run the **find / -xdev -size +500M;** command to view files larger than 500 MB in the directory obtained in :ref:`2 <alm-45481__li64021312132010>`. Check whether such files are mistakenly written to the directory.

   -  If yes, go to :ref:`4 <alm-45481__li1777644333119>`.
   -  If no, go to :ref:`5 <alm-45481__li204144633410>`.

#. .. _alm-45481__li1777644333119:

   Delete the mistakenly written files and check whether the alarm is cleared 2 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45481__li204144633410>`.

#. .. _alm-45481__li204144633410:

   Check whether Kudu contains unnecessary data tables.

   -  If yes, go to :ref:`6 <alm-45481__li4525202919363>`.
   -  If no, go to :ref:`8 <alm-45481__li10695421193913>`.

#. .. _alm-45481__li4525202919363:

   Use **kudu table delete <master_addresses> <table_name> [-nomodify_external_catalogs]** to delete unnecessary tables.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45481__li10695421193913>`.

#. .. _alm-45481__li10695421193913:

   Contact the disk administrator to expand the disk capacity.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-45481__li4749473185459>`.

**Collect fault information.**

10. .. _alm-45481__li4749473185459:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, select **Kudu** for the target cluster, and click **OK**.

12. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
