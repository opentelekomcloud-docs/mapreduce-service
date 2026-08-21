:original_name: ALM-27008.html

.. _ALM-27008:

ALM-27008 Total Number of Long Transactions in DBService Exceeds the Threshold
==============================================================================

Alarm Description
-----------------

The system checks the total number of long transactions in the DBServer database every 30 seconds. By default, a transaction whose running time is greater than 30 minutes is considered as a long transaction. This alarm is generated when the system detects that the total number of long transactions exceeds the threshold (the default threshold is **1**) for *N* consecutive times. *N* indicates the value of **Trigger Count**, which is **3** by default.

When **Trigger Count** is set to **1**, this alarm is cleared if the total number of long transactions in the DBServer database is no more than the threshold. When **Trigger Count** is set to a value greater than 1, this alarm is cleared if the total number of long transactions in the DBServer database is less than 90% of the threshold for *N* consecutive times.

This section applies to MRS 3.6.0-LTS.1 and later versions.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
27008    Major          Yes
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

-  Long transactions block garbage collection, causing tables and indexes to continuously expand and consume a large amount of storage space. In addition, performance deteriorates (for example, the I/O overhead increases sharply), lock resource competition occurs, and replication and O&M operations fail.
-  Long transactions slow down their own execution and block other SQL tasks, causing severe service delays and connection pool exhaustion. If a transaction is interrupted unexpectedly, the rollback takes a long time, increasing the risk of data inconsistency.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The database has long transactions.

   -  Large transactions process data in batches, which may cause long execution time or low SQL efficiency (due to missing indexes, poor joins, and complex calculation), and inefficient execution of a single statement.
   -  Transactions are blocked and retried repeatedly due to lock contentions or deadlocks.
   -  Transactions are in the orphaned state because applications are not submitted or rolled back, or the client is interrupted unexpectedly.

Handling Procedure
------------------

**Check whether the threshold is set properly.**

#. On Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **DBService** > **Database** > **Total Number of Long DBService Transactions**, and check whether the alarm threshold is proper (the default value is **1**).

   -  If yes, go to :ref:`3 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li696213241773>`.
   -  If no, go to :ref:`2 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li76152032183613>`.

#. .. _alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li76152032183613:

   Click **Modify** in the **Operation** column and change the alarm threshold as required.

#. .. _alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li696213241773:

   Choose **Cluster** > **Services** > **DBService**. On the **Dashboard** page, check whether the total number of long DBService transactions is less than the threshold in the **Total Number of Long DBService Transactions** chart.

   -  If yes, go to :ref:`4 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li461543273618>`.
   -  If no, go to :ref:`5 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li149831549185912>`.

#. .. _alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li461543273618:

   Check whether the alarm is cleared 2 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li149831549185912>`.

**Check whether the database has long transactions.**

5. .. _alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li149831549185912:

   Log in to the active DBService management node as user **omm** and log in to the DBService database.

   **gsql -p 20015 -U omm -W** *${Database password}*

6. Run the following statements to check whether the database has long transactions:

   **SELECT COUNT(1) FROM PG_STAT_ACTIVITY WHERE STATE IN ('active','idle in transaction', 'fastpath function call', 'idle in transaction (aborted)') AND PID <> PG_BACKEND_PID() AND EXTRACT(EPOCH FROM (now() - QUERY_START::timestamptz)) >= 1800;**

   If the query result is greater than **0**, the database has long transactions. If the query result is **0**, the database does not have long transactions.

   -  If yes, go to :ref:`7 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li11270141513437>`.
   -  If no, go to :ref:`8 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li366932304312>`.

7. .. _alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li11270141513437:

   Resolve the long transactions based on the site requirements and check whether the alarm is cleared 2 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li366932304312>`.

**Collect fault information.**

8.  .. _alm-27008__en-us_topic_0000002523518646_en-us_topic_0000002522849160_li366932304312:

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
