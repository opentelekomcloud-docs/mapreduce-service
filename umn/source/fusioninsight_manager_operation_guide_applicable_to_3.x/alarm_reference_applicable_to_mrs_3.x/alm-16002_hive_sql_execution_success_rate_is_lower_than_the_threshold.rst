:original_name: ALM-16002.html

.. _ALM-16002:

ALM-16002 Hive SQL Execution Success Rate Is Lower Than the Threshold
=====================================================================

Description
-----------

The system checks the percentage of the HQL statements that are executed successfully in every 30 seconds. The formula is: Percentage of HQL statements that are executed successfully = Number of HQL statements that are executed successfully by Hive in a specified period/Total number of HQL statements that are executed by Hive. This indicator can be viewed on the **Cluster >** *Name of the desired cluster* **> Services** > **Hive > Instance** > *HiveServer instance* **.** The default threshold of the percentage of HQL statements that are executed successfully is **90%**. An alarm is reported when the percentage is lower than the **90%**. Users can view the name of the host where an alarm is generated in the location information about the alarm. The IP address of the host is the IP address of the HiveServer node.

Users can modify the threshold by choosing **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **Hive** > **Percentage of HQL Statements That Are Executed Successfully by Hive**.

This alarm is cleared when the execution success rate is higher than 110% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
16002    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The system configuration and performance cannot meet service processing requirements.

Possible Causes
---------------

-  A syntax error occurs in HQL statements.
-  The HBase service is abnormal when a Hive on HBase task is performed.
-  The Spark service is abnormal when a Hive on Spark task is performed.
-  The dependent basic services, such as HDFS, Yarn, and ZooKeeper, are abnormal.

Procedure
---------

**Check whether the HQL statements comply with syntax.**

#. On the FusionInsight Manager page, choose **O&M** > **Alarm** to view the alarm details and obtain the node where the alarm is generated.

#. Use the Hive client to log in to the HiveServer node where an alarm is reported. Query the HQL syntax provided by Apache, and check whether the HQL commands are correct.

   -  If yes, go to :ref:`4 <alm-16002__li2677546914456>`.
   -  If no, go to :ref:`3 <alm-16002__li3343432914456>`.

   .. note::

      To view the user who runs an incorrect statement, you can download the hiveserver audit log file of the HiveServer node where this alarm is generated. **Start Data** and **End Data** are 10 minutes before and after the alarm generation time respectively. Open the log file and search for the **Result=FAIL** keyword to filter the log information about the incorrect statement, and then view the user who runs the incorrect statement according to **UserName** in the log information.

#. .. _alm-16002__li3343432914456:

   Enter the correct HQL statements, and check whether the command can be properly executed.

   -  If yes, go to :ref:`12 <alm-16002__li5821800114456>`.
   -  If no, go to :ref:`4 <alm-16002__li2677546914456>`.

**Check whether the HBase service is abnormal.**

4. .. _alm-16002__li2677546914456:

   Check whether an Hive on HBase task is performed with the user who runs the HQL command.

   -  If yes, go to :ref:`5 <alm-16002__li1989232914456>`.
   -  If no, go to :ref:`8 <alm-16002__li4623094014456>`.

5. .. _alm-16002__li1989232914456:

   On the FusionInsight Manager page, click **Cluster** > *Name of the desired cluster* > **Services**, check whether the HBase service is normal in the service list.

   -  If yes, go to :ref:`8 <alm-16002__li4623094014456>`.
   -  If no, go to :ref:`6 <alm-16002__li4481323314456>`.

6. .. _alm-16002__li4481323314456:

   Choose **O&M** > **Alarm**, check the related alarms displayed on the alarm page and clear them according to related alarm help.

7. Enter the correct HQL statements, and check whether the command can be properly executed.

   -  If yes, go to :ref:`12 <alm-16002__li5821800114456>`.
   -  If no, go to :ref:`8 <alm-16002__li4623094014456>`.

**Check whether the HDFS, Yarn, and ZooKeeper are normal.**

8.  .. _alm-16002__li4623094014456:

    On the FusionInsight Manager portal, click **Cluster** > *Name of the desired cluster* > **Services**.

9.  In the service list, check whether the services, such as HDFS, Yarn, and ZooKeeper are normal.

    -  If yes, go to :ref:`12 <alm-16002__li5821800114456>`.
    -  If no, go to :ref:`10 <alm-16002__li6532844614456>`.

10. .. _alm-16002__li6532844614456:

    Check the related alarms displayed on the alarm page and clear them according to related alarm help.

11. Enter the correct HQL statements, and check whether the command can be properly executed.

    -  If yes, go to :ref:`12 <alm-16002__li5821800114456>`.
    -  If no, go to :ref:`13 <alm-16002__li2812112614456>`.

12. .. _alm-16002__li5821800114456:

    After 1 minute, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-16002__li2812112614456>`.

**Collect fault information.**

13. .. _alm-16002__li2812112614456:

    On the FusionInsight Manager home page, choose **O&M** > **Log > Download**.

14. Select the following nodes in the required cluster from the **Service**:

    -  MapReduce
    -  Hive

15. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607850.png
