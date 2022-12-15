:original_name: mrs_01_0281.html

.. _mrs_01_0281:

HBase Health Check Indicators
=============================

Normal RegionServer Count
-------------------------

**Indicator**: Normal RegionServer Count

**Description**: This indicator is used to check the number of RegionServers that are running properly in an HBase cluster.

**Recovery Guide**: If the indicator is abnormal, check whether the status of RegionServer is normal. If the status is abnormal, resolve the problem and check that the network is normal.

Service Health Status
---------------------

**Indicator**: Service Status

**Description**: This indicator is used to check whether the HBase service status is normal. If the status is abnormal, the service is unhealthy.

**Recovery Guide**: If the indicator is abnormal, check whether the status of HMaster and RegionServer is normal. If the status is abnormal, resolve the problem. Then, check whether the status of the ZooKeeper service is faulty. On the HBase client, check whether the data in the HBase table can be correctly read and locate the data reading failure cause. Handle the alarm following instructions in the alarm processing document.

Alarm Check
-----------

**Indicator**: Alarm Information

**Description**: This indicator is used to check whether alarms exist. If alarms exist, the service is unhealthy.

**Recovery Guide**: If this indicator is abnormal, you can rectify the fault by referring to the alarm handling guide.
