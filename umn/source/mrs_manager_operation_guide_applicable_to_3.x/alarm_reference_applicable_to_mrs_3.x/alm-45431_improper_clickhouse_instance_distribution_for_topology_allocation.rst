:original_name: ALM-45431.html

.. _ALM-45431:

ALM-45431 Improper ClickHouse Instance Distribution for Topology Allocation
===========================================================================

Description
-----------

The ClickHouseServer instance distribution does not meet the topology allocation requirements.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45431    Critical       No
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Some ClickHouseServer instances are unavailable.

Possible Causes
---------------

During installation or capacity expansion, the number of instances or allocation mode does not meet the topology requirements.

Procedure
---------

#. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**, locate the row that contains the alarm, and analyze the cause based on **Location** and **Additional Information**.
#. Handle the alarm based on the additional alarm information and handling method in the following table.

   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Additional Information                                      | Remarks                                                                                                                                                                                                                                             | Handling Method                                                                                                                                                                                                                                                          |
   +=============================================================+=====================================================================================================================================================================================================================================================+==========================================================================================================================================================================================================================================================================+
   | *n* ClickHouseServer instances should be added to other AZ. | This alarm is generated when a single cluster is deployed in cross-AZ DR mode. The ClickHouseServer instance deployment does not meet the cross-AZ DR topology allocation requirements. As a result, some instances cannot work properly.           | a. On MRS Manager, choose **Cluster** > **Services** > **ClickHouse**, click the **Instance** tab, locate the row that contains the alarm, view the host name in **Location**, and find the AZ for which the alarm is generated in the AZ column based on the host name. |
   |                                                             |                                                                                                                                                                                                                                                     | b. On the **Instance** page, click **Add Instance** to add *n* ClickHouseServer instances to other AZs except the AZ where the alarm is generated.                                                                                                                       |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | *n* ClickHouseServer instances should be added.             | This alarm is generated when a non-single-cluster is deployed in the default deployment mode of cross-AZ DR. The number of ClickHouseServer instances in the cluster is less than an even number. As a result, some instances cannot work properly. | a. Determine the number (*n*) of ClickHouseServer instances to be added based on the alarm information.                                                                                                                                                                  |
   |                                                             |                                                                                                                                                                                                                                                     | b. On MRS Manager, choose **Cluster** > **Services** > **ClickHouse**, click the **Instance** tab, and add *n* ClickHouseServer instances to the cluster.                                                                                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Alarm Clearing
--------------

This alarm needs to be manually cleared after the fault is rectified.

Related Information
-------------------

None
