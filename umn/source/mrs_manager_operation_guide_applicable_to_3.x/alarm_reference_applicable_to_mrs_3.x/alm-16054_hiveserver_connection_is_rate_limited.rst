:original_name: ALM-16054.html

.. _ALM-16054:

ALM-16054 HiveServer Connection Is Rate Limited
===============================================

Alarm Description
-----------------

HiveServer supports configuring the maximum number of connections for a specified user or IP address. New connections are rejected when the connection count reaches the limit, triggering this alarm. If no new connections are rejected within 5 minutes, this alarm will be automatically cleared.

This section applies to MRS 3.6.0-LTS and later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
16054    Major          Yes
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
| Additional Information | Trigger condition | Specifies the threshold for triggering the alarm.        |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

The user or IP address for which the alarm is reported cannot establish new HiveServer connections, impacting related services.

Possible Causes
---------------

-  The maximum number of HiveServer connections is set improperly and needs adjustment.
-  Related services are experiencing abnormalities, either establishing a large number of HiveServer connections or keeping a number of connections open.

Handling Procedure
------------------

**Adjust the maximum number of connections limit for the user or IP address.**

#. Log in to MRS Manager, choose **Cluster** > **Services**, and click **Hive** in the service list to enter the overview page.
#. Click the **Configurations** tab, select **All Configurations**, search for **connections.per** on the right, check and modify the following configurations of the user or IP address reported in the alarm, and click **Save**.

   -  **hive.server2.limit.connections.per.ipaddress.extend** specifies the maximum number of connections that can be opened by a specified IP address for each HiveServer. Once this limit is reached, new connections will be rejected. The format is "*IP address*:*limit*". Separate multiple IP addresses by commas (,). Up to 10 IP addresses can be specified.
   -  **hive.server2.limit.connections.per.user.extend**: specifies the maximum number of connections that a specified user can open for each HiveServer. Once this limit is reached, new connections will be rejected. The format is "*user*:*limit*". Separate multiple users by commas (,). Up to 10 users can be specified.
   -  **hive.server2.limit.connections.per.user.ipaddress.extend** specifies the maximum number of connections that can be opened by a user with a specified IP address on each HiveServer. Once this limit is reached, new connections will be rejected. The format is "*IP address*:*user*:*limit*". Separate multiple IP address and user pairs by commas (,). Up to 10 IP address and user pairs can be specified.

#. Click **Instances**, select all HiveServer instances, choose **More** > **Restart Instance**. In the displayed dialog, enter the password of the current user and click **OK** to restart the HiveServer instances.

   .. important::

      During HiveServer instance restart, the instance cannot provide services for external systems. SQL tasks that are being executed on the instance may fail.

#. Choose **O&M** > **Alarm** > **Alarms**. In the alarm list, check whether the alarm "HiveServer Connection Is Rate Limited" is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li1225065671014>`.

**Check whether the connections of the user or IP address reported in the alarm are properly closed.**

5. .. _alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li1225065671014:

   In the alarm's location information, click the name of the host for which the alarm is reported and record the IP address of the corresponding HiveServer instance.

6. View the additional information about the alarm, confirm the connection type and number of connections, and go to :ref:`7 <alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li74013389203>`.

   -  The additional information includes "user: *a1* limit: *2*, ..." indicating that the number of HiveServer connections for user **a1** exceeds the limit of **2.**
   -  The additional information contains "ipaddress: *192.168.xxx.xxx* limit: *3*, ...", indicating that the number of HiveServer connections for the IP address **192.168.xxx.xxx** exceeds the limit of **3**.
   -  The additional information includes "user: *a2* ipaddress: *192.168*..\ *xxx.xxx* limit: *10, ...*", indicating that the number of HiveServer connections for user **a2** using the IP address **192.168.xxx.xxx** exceeds the limit of **10**.

7. .. _alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li74013389203:

   Log in to the HiveServer instance node you checked in :ref:`5 <alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li1225065671014>`, execute the following commands to check the number of connections opened and closed for the user or IP address reported in the alarm:

   -  Check the number of HiveServer connections opened and closed by the user.

      **grep 'OpenSession' /var/log/Bigdata/audit/hive/hiveserver/hive-audit.log \| awk '{print $9}' \| sort \| uniq -c \| sort \| grep 'UserName=**\ *user*\ **'**

      **grep 'CloseSession' /var/log/Bigdata/audit/hive/hiveserver/hive-audit.log \| awk '{print $9}' \| sort \| uniq -c \| sort \| grep 'UserName=**\ *user*\ **'**

   -  Check the number of HiveServer connections opened and closed by the IP address.

      **grep 'OpenSession' /var/log/Bigdata/audit/hive/hiveserver/hive-audit.log \| awk '{print $10}' \| sort \| uniq -c \| sort \| grep 'UserIP=**\ *IP*\ **'**

      **grep 'CloseSession' /var/log/Bigdata/audit/hive/hiveserver/hive-audit.log \| awk '{print $10}' \| sort \| uniq -c \| sort \| grep 'UserIP=**\ *IP*\ **'**

   Check if the command output still contains active HiveServer connection that was opened by the user or IP address.

   -  If yes, go to :ref:`8 <alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li159821878503>`.
   -  If no, go to :ref:`10 <alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li3391164804417>`.

8. .. _alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li159821878503:

   Contact related business personnel to investigate the corresponding service based on the user or IP address.

9. On the homepage of MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, check if the "HiveServer Connection Is Rate Limited" alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li3391164804417>`.

**Collect fault information.**

10. .. _alm-16054__en-us_topic_0000002158671658_en-us_topic_0000002193215201_li3391164804417:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, and select **Hive** > **HiveServer** for the target cluster.

12. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs and stack information.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
