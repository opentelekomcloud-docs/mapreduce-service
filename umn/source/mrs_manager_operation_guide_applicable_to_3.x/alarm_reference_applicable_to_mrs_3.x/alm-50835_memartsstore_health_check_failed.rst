:original_name: ALM-50835.html

.. _ALM-50835:

ALM-50835 MemArtsStore Health Check Failed
==========================================

Alarm Description
-----------------

The system checks the process status, port status, and gRPC communication status between sidecar and Worker instances every 30 seconds. This alarm is generated when the system detects that the status is abnormal and the health check fails.

This alarm is cleared when the abnormal status is cleared and the health check is successful.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50835    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+--------------------------------------------------------------------+
| Parameter   | Description                                                        |
+=============+====================================================================+
| Source      | Specifies the cluster or system for which the alarm was generated. |
+-------------+--------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm was generated.           |
+-------------+--------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The service cannot be accessed.

Possible Causes
---------------

-  The process does not exist.
-  The process status is abnormal.
-  The port check is abnormal.
-  The gRPC communication between sidecar and Worker instances fails.

Handling Procedure
------------------

**Check the MemArtsStore process status.**

#. On MRS Manager, choose **Cluster** > **Services** > **MemArtsStore** > **Instances**.

#. Select the instances whose status is not **Normal**, click **More**, and select **Restart Instance**.

#. Check whether the instance status becomes normal after the restart.

   -  If yes, go to :ref:`4 <alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li11229134385114>`.
   -  If no, go to :ref:`5 <alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li122275434515>`.

#. .. _alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li11229134385114:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li122275434515>`.

**Check the port status or the communication status between sidecar and Worker instances.**

5.  .. _alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li122275434515:

    Log in to the node where the MemArtsStore service is abnormal.

6.  Go to the directory of the MemArtsStore configuration file.

    **cd** **/opt/Bigdata/FusionInsight_MemArtsStore_8.1.2.1/1_25_StoreWorker/etc**

7.  Open the **worker.json** configuration file and find the port number in the additional information.

8.  Check the port usage.

    **lsof -i:Port number**

    Resolve the port occupation problem.

9.  On MRS Manager, choose **Cluster** > **Services** > **MemArtsStore** > **Instances**.

10. Select the instances whose status is not **Normal**, click **More**, and select **Restart Instance**.

11. Check whether the instance status becomes normal after the restart.

    -  If yes, go to :ref:`12 <alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li12228184320518>`.
    -  If no, go to :ref:`13 <alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li10360155511379>`.

12. .. _alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li12228184320518:

    Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li10360155511379>`.

**Collect fault information.**

13. .. _alm-50835__en-us_topic_0000002520267257_en-us_topic_0000002157418392_li10360155511379:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

14. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

15. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
