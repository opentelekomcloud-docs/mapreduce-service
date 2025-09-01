:original_name: ALM-16052.html

.. _ALM-16052:

ALM-16052 Latency for MetaStore to Access the Meta Database During Table Creation Exceeds the Threshold
=======================================================================================================

Alarm Description
-----------------

The system periodically checks the latency for MetaStore to access the meta database during table creation. This alarm is generated when the average latency in the last 5 minutes exceeds the threshold.

This alarm is cleared when the average latency falls below the threshold.

This alarm applies to MRS 3.5.0 or later.

Alarm Attributes
----------------

+-----------------------+------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                           | Auto Cleared          |
+=======================+==========================================+=======================+
| 16052                 | Critical (default threshold: 60 seconds) | Yes                   |
|                       |                                          |                       |
|                       | Major (default threshold: 10 seconds)    |                       |
+-----------------------+------------------------------------------+-----------------------+

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
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

If this alarm is generated, the latency for inserting related table information to the meta database is high during table creation in MetaStore. As a result, calling to MetaStore APIs becomes slow or an error occurs.

Possible Causes
---------------

The MetaStore GC takes a long time or the meta database is abnormal (for example, the disk I/O usage is too high or there are too many long transactions).

Handling Procedure
------------------

**Check whether the GC time of MetaStore is too long.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarm **Heap Memory Usage of the Hive Process Exceeds the Threshold** exists in the alarm list.

   -  If yes, go to :ref:`2 <alm-16052__en-us_topic_0000002019514985_li032518153407>`.
   -  If no, go to :ref:`4 <alm-16052__en-us_topic_0000002019514985_li64031235409>`.

#. .. _alm-16052__en-us_topic_0000002019514985_li032518153407:

   Rectify the fault by following the handling procedure of **ALM-16005 Heap Memory Usage of the Hive Process Exceeds the Threshold**.

#. Check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-16052__en-us_topic_0000002019514985_li64031235409>`.

**Check whether the meta database is normal.**

4. .. _alm-16052__en-us_topic_0000002019514985_li64031235409:

   Contact the administrator of the cluster meta database to check whether the database is normal.

   -  If yes, go to :ref:`5 <alm-16052__en-us_topic_0000002019514985_li032541514407>`.
   -  If no, go to :ref:`6 <alm-16052__en-us_topic_0000002019514985_li19517422154756>`.

5. .. _alm-16052__en-us_topic_0000002019514985_li032541514407:

   Contact the meta database O&M personnel to rectify the fault. After the meta database is restored, check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-16052__en-us_topic_0000002019514985_li19517422154756>`.

**Collect fault information.**

6.  .. _alm-16052__en-us_topic_0000002019514985_li19517422154756:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7.  Expand the **Service** drop-down list, and select **Hive** for the target cluster.

8.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9.  On MRS Manager, choose **Cluster** > **Services** > **Hive**. On the displayed **Dashboard** page, click **More** and select **Collect Stack Information**. On the displayed page, set the following parameters:

    -  Select **MetaStore** for the role where you want to collect data.
    -  Select **jstack** and **Enable continuous collection of jstack and jmap -histo information**.
    -  Set the collection interval to 10 seconds and the duration to 2 minutes.

10. Click **OK**. After the collection is complete, click **Download**.

11. Contact O&M personnel and provide the collected logs and stack information.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
