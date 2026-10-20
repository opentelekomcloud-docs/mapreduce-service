:original_name: ALM-27011.html

.. _ALM-27011:

ALM-27011 Number of DBService Database Deadlocks Exceeds the Threshold
======================================================================

Alarm Description
-----------------

The system checks the number of deadlocks in the DBService database every 30 seconds. This alarm is generated when the number of deadlocks exceeds the threshold (**1** by default) for *N* consecutive times. *N* indicates the value of **Trigger Count**, which is **3** by default.

When **Trigger Count** is set to **1**, this alarm is cleared if the number of deadlocks in the DBService database is less than or equal to the threshold. When **Trigger Count** is set to a value greater than 1, this alarm is cleared if the number of deadlocks in the DBService database is less than 90% of the threshold for *N* consecutive times.

This section applies to MRS 3.6.0-LTS.1 and later versions.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
27011    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+----------------+----------------------------------------------------------+
| Type                   | Parameter      | Description                                              |
+========================+================+==========================================================+
| Location Information   | Source         | Specifies the cluster for which the alarm was generated. |
+------------------------+----------------+----------------------------------------------------------+
|                        | ServiceName    | Specifies the service for which the alarm was generated. |
+------------------------+----------------+----------------------------------------------------------+
|                        | RoleName       | Specifies the role for which the alarm was generated.    |
+------------------------+----------------+----------------------------------------------------------+
|                        | HostName       | Specifies the host for which the alarm was generated.    |
+------------------------+----------------+----------------------------------------------------------+
| Additional Information | ThresholdValue | Specifies the threshold for triggering the alarm.        |
+------------------------+----------------+----------------------------------------------------------+
|                        | CurrentValue   | Specifies the metric value that is collected recently.   |
+------------------------+----------------+----------------------------------------------------------+

Impact on the System
--------------------

-  Long-standing database deadlocks may cause a large number of transactions to wait for each other to release resources and not to work. As a result, the system throughput and concurrency deteriorate significantly.
-  Deadlocks result in excessive transaction blocking or retries, leading to slow service response, interface timeout, and front-end response failure.

Possible Causes
---------------

-  The alarm threshold is improperly configured.

-  The number of database deadlocks exceeds the threshold.

   If system resources are insufficient or different transactions apply for multiple lock resources in reverse order, a global lock-waiting loop occurs in distributed multi-node scenarios.

Handling Procedure
------------------

**Check whether the threshold is set properly.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **DBService** > **Database** > **DBService Database Deadlocks**, and check whether the alarm threshold is proper (the default value is **1**).

   -  If yes, go to :ref:`3 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li696213241773>`.
   -  If no, go to :ref:`2 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li76152032183613>`.

#. .. _alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li76152032183613:

   Click **Modify** in the **Operation** column and change the alarm threshold as required.

#. .. _alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li696213241773:

   Choose **Cluster** > **Services** > **DBService**. On the **Dashboard** page, check whether the number of database deadlocks is less than the threshold in the **DBService Database Deadlocks** chart.

   -  If yes, go to :ref:`4 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li461543273618>`.
   -  If no, go to :ref:`5 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li149831549185912>`.

#. .. _alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li461543273618:

   Check whether the alarm is cleared 2 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li149831549185912>`.

**Check the number of database deadlocks.**

5. .. _alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li149831549185912:

   Log in to the active DBService management node as user **omm** and log in to the DBService database.

   **gsql -p 20015 -U omm -W** *${Database password}*

6. Check whether there is a deadlock in the database.

   **SELECT SUM(deadlocks) AS total_deadlocks FROM pg_stat_database;**

   If the query result is greater than **0**, a deadlock exists. If the query result is **0**, no deadlock exists.

   -  If yes, go to :ref:`7 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li11270141513437>`.
   -  If no, go to :ref:`8 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li366932304312>`.

7. .. _alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li11270141513437:

   Handle the deadlocks or change the alarm threshold based on the site requirements. Wait for 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li366932304312>`.

**Collect fault information.**

8.  .. _alm-27011__en-us_topic_0000002523478672_en-us_topic_0000002553889071_li366932304312:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **DBService** and **OMS** for the target cluster.

10. Specify **Hosts** for collecting logs, which is optional. By default, all hosts are selected.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Send the collected fault logs to O&M personnel for help.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
