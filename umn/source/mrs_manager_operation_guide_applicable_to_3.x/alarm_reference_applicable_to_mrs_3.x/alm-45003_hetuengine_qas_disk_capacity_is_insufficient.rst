:original_name: ALM-45003.html

.. _ALM-45003:

ALM-45003 HetuEngine QAS Disk Capacity Is Insufficient
======================================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the HetuEngine QAS disk usage every 60 seconds and compares the actual disk usage with the threshold. The disk usage has a default threshold. This alarm is generated if the disk usage exceeds the threshold.

To change the threshold, choose **O&M** > **Alarm** > **Thresholds**. In the service list, choose **HetuEngine** > **Disk** > **QAS Disk Usage (QAS)**.

If the **Trigger Count** is **1**, this alarm is cleared when the usage of the HetuEngine QAS disk is less than or equal to the threshold. If the **Trigger Count** is greater than **1**, this alarm is cleared when the disk usage is less than or equal to 80% of the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45003    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------------+----------------------------------------------------------------+
| Parameter         | Description                                                    |
+===================+================================================================+
| Source            | Specifies the cluster for which the alarm is generated.        |
+-------------------+----------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.        |
+-------------------+----------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.           |
+-------------------+----------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.           |
+-------------------+----------------------------------------------------------------+
| PartitionName     | Specifies the disk partition for which the alarm is generated. |
+-------------------+----------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.              |
+-------------------+----------------------------------------------------------------+

Impact on the System
--------------------

If the disk capacity is insufficient, QAS fails to write data, affecting SQL diagnosis and automatic recommendation of materialized views.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The configuration of the HetuEngine QAS disk cannot meet service requirements. The disk usage reaches the upper limit.

Handling Procedure
------------------

**Check whether the threshold is set properly.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Thresholds**. In the service list, choose **HetuEngine** > **Disk** > **QAS Disk Usage (QAS)**. Check whether the alarm threshold is set properly. The default threshold is 80% of the disk capacity. You can change the threshold as required.

   -  If the threshold is set properly, go to :ref:`4 <alm-45003__li1561212104442>`.
   -  If the threshold is not set properly, go to :ref:`2 <alm-45003__li1673781151015>`.

#. .. _alm-45003__li1673781151015:

   Click **Modify** in the **Operation** column to modify and save the alarm threshold as required.

#. Wait 2 minutes and check whether the alarm is cleared.

   -  If the alarm is cleared, no further action is required.
   -  If the alarm is not cleared, go to :ref:`4 <alm-45003__li1561212104442>`.

**Check whether the disk usage reaches the upper limit.**

4. .. _alm-45003__li1561212104442:

   Expand the alarm information, view the information in the **Location** area, and check the role name and host name of the QAS disk where the alarm is generated.

5. Choose **Cluster** > **Services** > **HetuEngine** and click **Instance**. On the displayed page, click the QAS role name in the alarm information. On the instance page that is displayed, click **Chart** and check whether the QAS disk usage in the **QAS Disk Usage** chart exceeds the threshold (80% of the disk capacity by default).

   -  If the disk usage reaches the upper limit, go to :ref:`6 <alm-45003__li1266819163911>`.
   -  If the disk usage does not reaches the upper limit, go to :ref:`9 <alm-45003__li1573581113104>`.

6. .. _alm-45003__li1266819163911:

   Log in to the host of the node where the QAS instance reporting the alarm is located as the **root** user.

7. Run the following command to go to the QAS data directory and delete temporary files as required:

   **cd ${BIGDATA_DATA_HOME}/hetuengine/qas**

   .. important::

      Deleting temporary files affects the latest QAS execution result but does not affect subsequent results.

8. Wait 2 minutes and check whether the alarm is cleared.

   -  If the alarm is cleared, no further action is required.
   -  If the alarm fails to be cleared, go to :ref:`9 <alm-45003__li1573581113104>`.

**Collect fault information.**

9.  .. _alm-45003__li1573581113104:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, select **HetuEngine** for the target cluster, and click **OK**.

11. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

12. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
