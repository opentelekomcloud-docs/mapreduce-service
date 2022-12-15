:original_name: mrs_01_0284.html

.. _mrs_01_0284:

HDFS Health Check Indicators
============================

Average Packet Sending Time
---------------------------

**Indicator**: Average Packet Sending Time

**Description**: This indicator is used to collect statistics on the average time for the DataNode in the HDFS to execute SendPacket each time. If the average time is greater than 2,000,000 ns, the DataNode is unhealthy.

**Recovery Guide**: If the indicator is abnormal, check whether the network speed of the cluster is normal and whether the memory or CPU usage is too high. Check whether the HDFS load in the cluster is high.

Service Health Status
---------------------

**Indicator**: Service Status

**Description**: This indicator is used to check whether the HDFS service status is normal. If a node is faulty, the host is unhealthy.

**Recovery Guide**: If the indicator is abnormal, check whether the health status of the KrbServer, LdapServer and ZooKeeper services are faulty. If yes, rectify the fault. Then, check whether the file writing failure is caused by HDFS SafeMode ON. Use the client to check whether data cannot be written into HDFS and locate the cause of the HDFS data writing failure. Handle the alarm following instructions in the alarm processing document.

Alarm Check
-----------

**Indicator**: Alarm Information

**Description**: This indicator is used to check whether alarms exist. If alarms exist, the service is unhealthy.

**Recovery Guide**: If this indicator is abnormal, you can rectify the fault by referring to the alarm handling guide.
