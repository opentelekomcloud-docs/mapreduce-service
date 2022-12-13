:original_name: mrs_01_0533.html

.. _mrs_01_0533:

ZooKeeper Health Check Indicators
=================================

Average ZooKeeper Request Processing Latency
--------------------------------------------

**Indicator**: Average ZooKeeper Service Request Processing Latency

**Description**: This indicator is used to check the average delay for the ZooKeeper service to process requests. If the average delay is greater than 300 ms, the ZooKeeper service is unhealthy.

**Recovery Guide**: If the indicator is abnormal, check whether the network speed of the cluster is normal and whether the memory or CPU usage is too high.

ZooKeeper Connections Usage
---------------------------

**Indicator**: ZooKeeper Connections Usage

**Description**: This indicator is used to check whether the ZooKeeper memory usage exceeds 80%. If the disk usage exceeds the threshold, the system is unhealthy.

**Recovery Guide**: If the indicator is abnormal, you are advised to increase the memory available for the ZooKeeper service. The method of increasing the memory is as follows: Increase the value of **-Xmx** in the **GC_OPTS** configuration item in the ZooKeeper service. After the modification, restart the ZooKeeper service for the configuration to take effect.

Service Health Status
---------------------

**Indicator**: Service Status

**Description**: This indicator is used to check whether ZooKeeper service status is normal. If the status is abnormal, the service is unhealthy.

**Recovery Guide**: If the indicator is abnormal, check whether the health status of the KrbServer and LdapServer services is faulty. If yes, rectify the fault. Log in to the ZooKeeper client, check whether the ZooKeeper data writing fails. If yes, find the failure cause based on the error message and handle the fault according to error message. Rectify the fault by following the procedure for handling ALM-13000.

Alarm Check
-----------

**Indicator**: Alarm Information

**Description**: This indicator is used to check whether alarms exist. If alarms exist, the service is unhealthy.

**Recovery Guide**: If this indicator is abnormal, you can rectify the fault by referring to the alarm handling guide.
