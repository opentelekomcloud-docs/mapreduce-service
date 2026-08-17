:original_name: ALM-12043.html

.. _ALM-12043:

ALM-12043 DNS Parsing Duration Exceeds the Threshold
====================================================

Alarm Description
-----------------

The system checks the DNS parsing duration every 30 seconds. This alarm is generated when the DNS parsing duration exceeds the threshold (the default threshold is 1,000 ms) for consecutive *X* times (**6** by default).

When **Trigger Count** is set to **1**, this alarm is cleared if the DNS parsing duration is less than or equal to the threshold. When **Trigger Count** is set to a value greater than 1, this alarm is cleared if the DNS parsing duration is less than or equal to 90% of the threshold.

This section applies only to MRS 3.6.0-LTS.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12043    Major          Yes
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
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

-  Kerberos-based secondary authentication is slow.
-  The ZooKeeper service is abnormal.
-  The node is faulty.

Possible Causes
---------------

-  The DNS server is faulty or the DNS configuration is incorrect.
-  The network is congested or the bandwidth is insufficient.

Handling Procedure
------------------

**Check whether the DNS server is faulty or the DNS configuration is incorrect.**

#. On the node for which the alarm is generated, check whether the IP address of the DNS server can be pinged.

   -  If yes, refresh the DNS cache.
   -  If no, the network cannot reach the DNS server. Change the IP address to an available one.

#. Wait for 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-12043__en-us_topic_0000002577507250_en-us_topic_0000002526179894_li148818535531>`.

**Check whether the network is congested or the bandwidth is insufficient.**

3. .. _alm-12043__en-us_topic_0000002577507250_en-us_topic_0000002526179894_li148818535531:

   Log in to the node for which the alarm is generated as the **root** user and run the following command to check whether the value in the **%ifutil** column is close to 1.00 (100%).

   **sar -n DEV 1 1**

   -  If yes, go to :ref:`4 <alm-12043__en-us_topic_0000002577507250_en-us_topic_0000002526179894_li11744101212611>`.
   -  If no, go to :ref:`6 <alm-12043__en-us_topic_0000002577507250_en-us_topic_0000002526179894_li293773011544>`.

4. .. _alm-12043__en-us_topic_0000002577507250_en-us_topic_0000002526179894_li11744101212611:

   Contact O&M engineers to check whether there is abnormal traffic. If yes, rectify the fault.

5. Wait for 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12043__en-us_topic_0000002577507250_en-us_topic_0000002526179894_li293773011544>`.

**Collect fault information.**

6. .. _alm-12043__en-us_topic_0000002577507250_en-us_topic_0000002526179894_li293773011544:

   On MRS Manager, click **O&M**. On the displayed page, choose **Log** > **Download**.

7. Select **OmmServer** and **NodeAgent** for **Service**. Select the host name recorded in the alarm location information for **Hosts**.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Send the collected fault logs to O&M engineers for help.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
