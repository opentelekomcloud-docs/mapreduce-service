:original_name: ALM-27010.html

.. _ALM-27010:

ALM-27010 DBService Database File Handle Usage Exceeds the Threshold
====================================================================

Alarm Description
-----------------

The system checks the number of database file handles used by DBService every 30 seconds. This alarm is generated when the number of used database file handles exceeds the threshold for *N* consecutive times. *N* indicates the value of **Trigger Count**, which is **3** by default.

When **Trigger Count** is set to **1**, this alarm is cleared if the number of database file handles used by the DBServer is less than or equal to the threshold. When **Trigger Count** is set to a value greater than 1, this alarm is cleared if the number of database file handles used by the DBServer is less than 90% of the threshold for *N* consecutive times.

This section applies to MRS 3.6.0-LTS.1 and later versions.

Alarm Attributes
----------------

+-----------------------+----------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                   | Auto Cleared          |
+=======================+==================================+=======================+
| 27010                 | Major (default threshold: 10000) | Yes                   |
|                       |                                  |                       |
|                       | Minor (default threshold: 8000)  |                       |
+-----------------------+----------------------------------+-----------------------+

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

-  If the file handles usage is high for a long time, the system cannot open new files. As a result, the database fails to read and write files, or the database performance deteriorates sharply.
-  New service connections cannot be established because the handles are used up. When an existing SQL statement is executed, the error message "Too many open files" or "Temporary resources are unavailable" is displayed. As a result, the service tasks fail to be executed.

Possible Causes
---------------

-  The alarm threshold is improperly configured.

-  The database file handle usage exceeds the threshold.

   A process opens a file, and the file is physically deleted by the **rm** or **mv** command. However, the process is not restarted or does not close the handles, causing continuous resource occupation.

Handling Procedure
------------------

**Check whether the threshold is set properly.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **DBService** > **Database** > **DBService Database File Handle Usage**, and check whether the alarm threshold is proper.

   -  If yes, go to :ref:`3 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li696213241773>`.
   -  If no, go to :ref:`2 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li76152032183613>`.

#. .. _alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li76152032183613:

   Click **Modify** in the **Operation** column and change the alarm threshold as required.

#. .. _alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li696213241773:

   Choose **Cluster** > **Services** > **DBService**. On the **Dashboard** page, check whether the number of the file handles used by the DBService database is less than the threshold in the **DBService Database File Handle Usage** chart.

   -  If yes, go to :ref:`4 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li461543273618>`.
   -  If no, go to :ref:`5 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li149831549185912>`.

#. .. _alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li461543273618:

   Check whether the alarm is cleared 2 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li149831549185912>`.

**Check the database file handle usage.**

5. .. _alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li149831549185912:

   Log in to the active DBService management node as user **omm**.

6. Check whether the database file handle usage of DBService exceeds the threshold.

   **pgrep -u omm gaussdb \| xargs -I{} sh -c 'ls /proc/{}/fd 2>/dev/null' \| wc -l**

   -  If yes, go to :ref:`7 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li11270141513437>`.
   -  If no, go to :ref:`8 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li366932304312>`.

7. .. _alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li11270141513437:

   Handle the used file handles or change the alarm threshold based on the site requirements. Wait for 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li366932304312>`.

**Collect fault information.**

8.  .. _alm-27010__en-us_topic_0000002554518561_en-us_topic_0000002553769089_li366932304312:

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
