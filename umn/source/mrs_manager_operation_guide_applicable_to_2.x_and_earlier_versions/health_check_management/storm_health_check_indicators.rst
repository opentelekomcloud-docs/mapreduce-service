:original_name: mrs_01_0531.html

.. _mrs_01_0531:

Storm Health Check Indicators
=============================

Number of Working Nodes
-----------------------

**Indicator**: Number of Supervisors

**Description**: This indicator is used to check the number of available Supervisors in a cluster. If the number of available Supervisors in a cluster is less than 1, the cluster is unhealthy.

**Recovery Guide**: If the indicator is abnormal, go to the Streaming service instance page and click the host name of the unavailable Supervisor instance. View the host health status in the **Overview** area. If the host health status is **Good**, rectify the fault by referring to ALM-12007 Process Faults. If the status is not **Good**, rectify the fault by referring to the handling procedure of the ALM-12006 Node Faults.

Number of Idle Slots
--------------------

**Indicator**: Number of Idle Slots

**Description**: This indicator is used to check the number of idle slots in a cluster. If the number of idle slots in a cluster is less than 1, the cluster is unhealthy.

**Recovery Guide**: If the indicator is abnormal, go to the Storm service instance page and check the health status of the Supervisor instance. If the health status of all Supervisor instances is **Good**, you need to expand the capacity of the Core node in the cluster. If not, rectify the fault by referring to ALM-12007 Process Faults.

Service Health Status
---------------------

**Indicator**: Service Status

**Description**: This indicator is used to check whether the Storm service status is normal. If the status is abnormal, the service is unhealthy.

**Recovery Guide**: If the indicator is abnormal, rectify the fault by referring to the alarm "ALM-26051 Storm Service Unavailable".

Alarm Check
-----------

**Indicator**: Alarm Information

**Description**: This indicator is used to check whether alarms exist. If alarms exist, the service is unhealthy.

**Recovery Guide**: If this indicator is abnormal, you can rectify the fault by referring to the alarm handling guide.
