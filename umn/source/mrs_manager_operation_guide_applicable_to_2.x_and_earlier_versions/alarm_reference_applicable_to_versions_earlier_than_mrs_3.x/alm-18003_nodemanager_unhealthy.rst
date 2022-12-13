:original_name: alm_18003.html

.. _alm_18003:

ALM-18003 NodeManager Unhealthy
===============================

Description
-----------

The system checks the number of abnormal NodeManager nodes every 30 seconds, and compares the number of abnormal nodes with the threshold. The **Unhealthy Nodes** indicator has a default threshold. This alarm is generated when the value of the **Unhealthy Nodes** indicator exceeds the threshold.

This alarm is cleared when the value of **Unhealthy Nodes** is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18003    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

-  The faulty NodeManager node cannot provide the Yarn service.
-  The number of containers decreases, so the cluster performance deteriorates.

Possible Causes
---------------

-  The disk space of the host where the NodeManager node resides is insufficient.
-  User **omm** does not have the permission to access a local directory on the NodeManager node.

Procedure
---------

#. Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
