:original_name: mrs_01_0288.html

.. _mrs_01_0288:

Kafka Health Check Indicators
=============================

Number of Available Broker Nodes
--------------------------------

**Indicator**: Number of Brokers

**Description**: This indicator is used to check the number of available Broker nodes in a cluster. If the number of available Broker nodes in a cluster is less than 2, the cluster is unhealthy.

**Recovery Guide**: If the indicator is abnormal, go to the Kafka service instance page and click the host name of the unavailable Broker instance. View the host health status in the **Overview** area. If the host health status is **Good**, rectify the fault by referring to the alarm handling suggestions in **Process Fault**. If the status is not **Good**, rectify the fault by referring to the handling procedure of the **Node Fault** alarm.

Service Health Status
---------------------

**Indicator**: Service Status

**Description**: This indicator is used to check whether the Kafka service status is normal. If the status is abnormal, the service is unhealthy.

**Recovery Guide**: If the indicator is abnormal, rectify the fault by referring to the alarm "Kafka Service Unavailable".

Alarm Check
-----------

**Indicator**: Alarm Information

**Description**: This indicator is used to check whether alarms exist. If alarms exist, the service is unhealthy.

**Recovery Guide**: If this indicator is abnormal, you can rectify the fault by referring to the alarm handling guide.
