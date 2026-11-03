:original_name: ALM-14045.html

.. _ALM-14045:

ALM-14045 Average ReadBlock Operation Time Exceeds the Threshold
================================================================

Alarm Description
-----------------

The system checks the average time of the ReadBlock operation on the DataNode every 30 seconds. This alarm is generated when the average time exceeds the threshold for a specified number of times (20 times by default) consecutively.

This alarm is cleared when the average time of the ReadBlock operation on the DataNode falls below the threshold.

This section applies to MRS 3.6.0-LTS.1 and later versions.

Alarm Attributes
----------------

+-----------------------+--------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                       | Auto Cleared          |
+=======================+======================================+=======================+
| 14045                 | Minor (default threshold: 5,000 ms)  | Yes                   |
|                       |                                      |                       |
|                       | Major (default threshold: 10,000 ms) |                       |
+-----------------------+--------------------------------------+-----------------------+

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

If block reading on the DataNode becomes slow, services that depend on HDFS for data reading become slow.

Possible Causes
---------------

-  The alarm threshold is improperly set.
-  The memory allocated to the DataNode is insufficient and frame freezing occurs on the JVM due to frequent Full GCs.
-  The disk of the node where the DataNode is located is slow in performance.
-  The disk write speed of the DataNode OS is slow.
-  The network between the client and the DataNode is faulty.

Handling Procedure
------------------

**Check whether the alarm threshold is proper.**

#. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li145751322404:

   Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, view the alarm details, and obtain the host name of the DataNode for which the alarm is generated.

#. Check whether the services that depend on HDFS are running normally and whether the services are running slowly or timed out.

   -  If yes, go to :ref:`6 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li1257510211407>`.
   -  If no, go to :ref:`3 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li18575152104020>`.

#. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li18575152104020:

   On Manager, choose **Cluster** > **Services** > **HDFS** > **Instances**, click the DataNode role name of the host name obtained in :ref:`1 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li145751322404>`, choose **Chart** > **Operation**, and check the indicator **DataNode Operation Time** to obtain its peak value within one day before and after the alarm is generated.

#. Choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **HDFS**, locate the **Average ReadBlock Operation Time**, click **Modify** in the **Operation** column of the **default** rule, change the threshold to 150% of the peak value of the indicator within one day before and after the alarm is generated, and click **OK**.

#. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li1257510211407>`.

**Check whether the memory configured for the DataNode is proper.**

6. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li1257510211407:

   On Manager, choose **O&M** > **Alarm** > **Alarms** to check whether the **ALM-14015 DataNode GC Time Exceeds the Threshold** alarm is generated and whether the host of the alarm is the same as that obtained in :ref:`1 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li145751322404>`.

   -  If yes, go to :ref:`7 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li75751622404>`.
   -  If no, go to :ref:`9 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li22658717445>`.

7. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li75751622404:

   Click **View Help** in the row where the alarm is located and handle the alarm by referring to the help document.

8. After the ALM-14015 alarm is cleared, wait for 10 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li22658717445>`.

**Check whether the disk on the node where the DataNode is located is slow in performance.**

9.  .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li22658717445:

    On Manager, choose **O&M** > **Alarm** > **Alarms** and check whether there is any of the following alarms: **ALM-12180 Suspended Disk I/O**, **ALM-12191 Disk I/O Usage Exceeds the Threshold**, **ALM-12204 Wait Duration of a Disk Read Exceeds the Threshold**, and **ALM-12205 Wait Duration of a Disk Write Exceeds the Threshold**, and whether the host of the alarm is the same as that obtained in :ref:`1 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li145751322404>`.

    -  If yes, go to :ref:`10 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li102651777447>`.
    -  If no, go to :ref:`12 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li7100111118442>`.

10. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li102651777447:

    Click **View Help** in the row where the alarm is located and handle the alarm by referring to the help document.

11. Wait for 10 minutes and check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li7100111118442>`.

**Check whether the disk write speed of the DataNode OS is slow.**

12. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li7100111118442:

    On Manager, choose **Cluster** > **Services** > **HDFS** > **Instances**, click the DataNode role name corresponding to the host name obtained in :ref:`1 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li145751322404>`, and choose **Chart** > **Performance**. Check whether the indicators **Number of Slow IOs Per Second**, **Slow WriteDataToDisk Occurrences Per Second**, and **Slow Flush or Sync Occurrences Per Second** are abnormal during the period when the alarm is generated.

    -  If yes, contact O&M engineers to check the disk performance.
    -  If no, go to :ref:`14 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li1012412147444>`.

13. Wait 5 minutes and check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li1012412147444>`.

**Check whether the network between DataNodes is slow.**

14. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li1012412147444:

    On Manager, choose **Cluster** > **Services** > **HDFS** > **Instances**, click the DataNode role name corresponding to the host name obtained in :ref:`1 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li145751322404>`, and choose **Chart** > **Performance**. Check the indicator **Slow WritePacketToDownStream Occurrences Per Second**. Check whether the indicator is abnormal when the alarm is generated.

    -  If yes, contact O&M engineers to rectify the network fault.
    -  If no, go to :ref:`16 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li12907101604418>`.

15. Wait 5 minutes and check whether the alarm is automatically cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li12907101604418>`.

**Collect fault information.**

16. .. _alm-14045__en-us_topic_0000002540781438_en-us_topic_0000002530603274_li12907101604418:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

17. Expand the **Service** drop-down list, select the HDFS services for the target cluster, and click **OK**.

18. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

19. Send the collected fault logs to O&M engineers for help.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
