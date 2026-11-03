:original_name: ALM-27009.html

.. _ALM-27009:

ALM-27009 Average SQL Execution Duration Exceeds the Threshold
==============================================================

Alarm Description
-----------------

The system checks the average SQL execution duration in the DBServer database every 30 seconds. By default, the threshold is exceeded if the average SQL execution duration is greater than 10 seconds. This alarm is generated when the threshold (10s by default) is exceeded for *N* consecutive times. N indicates the value of **Trigger Count**, which is **3** by default.

When **Trigger Count** is set to **1**, this alarm is cleared if the average SQL execution duration in the DBServer database is less than or equal to the threshold. When **Trigger Count** is set to a value greater than 1, this alarm is cleared if the average SQL execution duration in the DBServer database is less than 90% of the threshold for *N* consecutive times.

This section applies to MRS 3.6.0-LTS.1 and later versions.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
27009    Major          Yes
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

-  Long-running SQL queries consume excessive system resources, affecting other tasks to obtain resources.
-  Services are running slowly, affecting user experience.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The average execution duration of the running SQL queries is long.

   -  The system resource usage is too high, causing slow task running.
   -  The SQL service logic is complex or the data volume is too large, causing slow task execution.

Handling Procedure
------------------

**Check whether the threshold is set properly.**

#. On Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **DBService** > **Database** > **Average Duration of the Running SQL Statements in DBService**, and check whether the alarm threshold is proper (the default value is **10**).

   -  If yes, go to :ref:`3 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li696213241773>`.
   -  If no, go to :ref:`2 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li76152032183613>`.

#. .. _alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li76152032183613:

   Click **Modify** in the **Operation** column and change the alarm threshold as required.

#. .. _alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li696213241773:

   Choose **Cluster** > **Services** > **DBService**. On the **Dashboard** page, check whether the average SQL execution time in DBService is less than the threshold in the **Average Duration of the Running SQL Statements in DBService** chart.

   -  If yes, go to :ref:`4 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li461543273618>`.
   -  If no, go to :ref:`5 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li149831549185912>`.

#. .. _alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li461543273618:

   Check whether the alarm is cleared 2 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li149831549185912>`.

**Check the average SQL execution duration.**

5. .. _alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li149831549185912:

   Log in to the active DBService management node as user **omm** and log in to the DBService database.

   **gsql -p 20015 -U omm -W** *${Database password}*

6. Check whether the average SQL execution duration of the database exceeds the threshold.

   a. Obtain the total SQL execution duration.

      **select sum(EXTRACT(EPOCH FROM (now() - QUERY_START::timestamptz))) AS totalSeconds from pg_stat_activity where STATE = 'active' and pid <> pg_backend_pid();**

   b. Obtain the number of the running SQL queries.

      **select count(1) from pg_stat_activity where STATE = 'active' and pid <> pg_backend_pid();**

   c. Calculate the average SQL execution duration and check whether it exceeds the threshold.

      Average duration = ${*Total task duration*} / ${*Total number of tasks*}

   -  If yes, go to :ref:`7 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li11270141513437>`.
   -  If no, go to :ref:`8 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li366932304312>`.

7. .. _alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li11270141513437:

   Handle the time-consuming SQL tasks or change the alarm threshold based on the site requirements. Wait for 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li366932304312>`.

**Collect fault information.**

8.  .. _alm-27009__en-us_topic_0000002554598595_en-us_topic_0000002522689160_li366932304312:

    On Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

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
